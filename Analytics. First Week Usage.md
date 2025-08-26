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

first_memory AS (
  SELECT user_id, MIN(memory_date) AS first_date
  FROM memory_data
  GROUP BY user_id
),

eligible_memories AS (
  SELECT md.user_id, md.memory_date, fm.first_date
  FROM memory_data md
  JOIN first_memory fm ON md.user_id = fm.user_id
  WHERE fm.first_date <= '2025-05-20'
),

first_week_usage AS (
  SELECT
    user_id,
    COUNT(DISTINCT memory_date) FILTER (
      WHERE memory_date <= first_date + 6
    ) AS first_week_days
  FROM eligible_memories
  GROUP BY user_id
),

-- reusing churn/return logic
memory_gaps AS (
  SELECT
    em.user_id,
    em.memory_date,
    LAG(em.memory_date) OVER (PARTITION BY em.user_id ORDER BY em.memory_date) AS prev_date
  FROM eligible_memories em
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
    MAX(memory_date) AS last_seen
  FROM gap_analysis
  GROUP BY user_id
),

final_status AS (
  SELECT
    fwu.user_id,
    fwu.first_week_days,
    CASE 
      WHEN gf.had_churn_gap = 1 AND gf.last_seen >= CURRENT_DATE - 15 THEN 'returned'
      WHEN gf.last_seen < CURRENT_DATE - 15 THEN 'churned'
      ELSE 'not_churned'
    END AS status
  FROM first_week_usage fwu
  JOIN gap_flags gf ON fwu.user_id = gf.user_id
)

SELECT
  status,
  COUNT(*) AS user_count,
  ROUND(AVG(first_week_days)::numeric, 2) AS avg_first_week_days,
  PERCENTILE_CONT(0.25) WITHIN GROUP (ORDER BY first_week_days) AS "25th_percentile",
  PERCENTILE_CONT(0.50) WITHIN GROUP (ORDER BY first_week_days) AS "50th_percentile",
  PERCENTILE_CONT(0.75) WITHIN GROUP (ORDER BY first_week_days) AS "75th_percentile"
FROM final_status
GROUP BY status
ORDER BY status;
