WITH memory_data AS (
  SELECT
    (m.data #>> ARRAY['userId'])::text AS user_id,
    ((m.data #>> ARRAY['created_at'])::timestamp AT TIME ZONE 'UTC' AT TIME ZONE 'Asia/Kolkata')::date AS memory_date
  FROM public.memory m
  JOIN public.device_registry d 
    ON (m.data #>> ARRAY['userId'])::text = d.user_id
  WHERE d.type = 'CUSTOMER_DEVICE'
    AND (m.data #>> ARRAY['userId'])::text NOT IN (
      -- blacklist
      'rzrAEd2kMKh15rfG6xLgYFc0KJj2', 'uzgt4gvbdaOvHuGpMr9Bl08SWK12', 'JtpPrxS6dhUTGJAaJMQ6M8Ve7Cj2', 
      'WUlYdMz37QXqMvojDbcQRVzl4zB2', 'vapYPKIw4KWpbDBhnlf6JsmHpGy1', 'rZz9LW913mhU3NiOAHdvaffZlAu1',
      -- ...
      'XpHlrCWF0gNOwdeppbqdPosNPhD2'
    )
),

first_memory_date AS (
  SELECT user_id, MIN(memory_date) AS first_memory
  FROM memory_data
  GROUP BY user_id
),

eligible_users AS (
  SELECT md.user_id, md.memory_date
  FROM memory_data md
  JOIN first_memory_date fmd ON md.user_id = fmd.user_id
  WHERE fmd.first_memory <= '2025-05-20'
),

memory_gaps AS (
  SELECT
    user_id,
    memory_date,
    LAG(memory_date) OVER (PARTITION BY user_id ORDER BY memory_date) AS prev_date
  FROM eligible_users
),

gap_analysis AS (
  SELECT
    user_id,
    memory_date,
    prev_date,
    (memory_date - prev_date) AS gap
  FROM memory_gaps
),

gap_flags AS (
  SELECT
    user_id,
    MAX(CASE WHEN gap >= 15 THEN 1 ELSE 0 END) AS had_churn_gap,
    COUNT(DISTINCT memory_date) AS total_days,
    MAX(memory_date) AS last_seen
  FROM gap_analysis
  GROUP BY user_id
),

final_status AS (
  SELECT
    gf.user_id,
    MIN(eu.memory_date) AS first_usage,
    gf.last_seen,
    gf.total_days,
    CASE 
      WHEN gf.had_churn_gap = 1 AND gf.last_seen >= CURRENT_DATE - 15 THEN 'returned'
      WHEN gf.last_seen < CURRENT_DATE - 15 THEN 'churned'
      ELSE 'not_churned'
    END AS status
  FROM gap_flags gf
  JOIN eligible_users eu ON eu.user_id = gf.user_id
  GROUP BY gf.user_id, gf.last_seen, gf.total_days, gf.had_churn_gap
)

SELECT
  status,
  COUNT(*) AS user_count,
  ROUND(AVG(total_days)::numeric, 2) AS avg_days_used,
  PERCENTILE_CONT(0.25) WITHIN GROUP (ORDER BY total_days) AS "25th_percentile",
  PERCENTILE_CONT(0.50) WITHIN GROUP (ORDER BY total_days) AS "50th_percentile",
  PERCENTILE_CONT(0.75) WITHIN GROUP (ORDER BY total_days) AS "75th_percentile"
FROM final_status
GROUP BY status
ORDER BY status;
