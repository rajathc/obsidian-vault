WITH memory_data AS (
  SELECT
    (m.data #>> ARRAY['userId'])::text AS user_id,
    ((m.data #>> ARRAY['created_at'])::timestamp AT TIME ZONE 'UTC' AT TIME ZONE 'Asia/Kolkata') AS created_at,
    ((m.data #>> ARRAY['created_at'])::timestamp AT TIME ZONE 'UTC' AT TIME ZONE 'Asia/Kolkata')::date AS memory_date
  FROM public.memory m
  JOIN public.device_registry d 
    ON (m.data #>> ARRAY['userId'])::text = d.user_id
  WHERE d.type = 'CUSTOMER_DEVICE'
    AND (m.data #>> ARRAY['userId'])::text NOT IN (
  'rzrAEd2kMKh15rfG6xLgYFc0KJj2', 'uzgt4gvbdaOvHuGpMr9Bl08SWK12', 'JtpPrxS6dhUTGJAaJMQ6M8Ve7Cj2', 
  'WUlYdMz37QXqMvojDbcQRVzl4zB2', 'vapYPKIw4KWpbDBhnlf6JsmHpGy1', 'rZz9LW913mhU3NiOAHdvaffZlAu1', 
  'TXOBLZdaCIdug7UdW2WaAKrvEGa2', 'V4GhRf510cduavAekly1ojPJTzP2', '7zdQE9xqIbSLIe0ZqS3ec096hGr1', 
  'YWSJ3flT7ZRQfrJHRSKy59Bdr223', 'qWywvpjmz8QJ3R7fHQHOC0R5FmI2', '1ewpixgriiRrbFiJOSoNi9QGoYY2', 
  'NMOCO9QGY0PghcsIufB26ctzjVo1', 'zvRCzUdgEmdZI6dRCZzuIzRLvF52', 'ENCy8KECnQcOcF9YNk9liAkC8zV2', 
  'ZInrGtOxEtS8tDHOC68JuEAnrGz2', 'ca113vzroxa7eFFwQlPF9ohkrwL2', 'T1QSFKoj5mNgqPRvkUfPe6PJ9Gr1', 
  'tuTVdSZeybX4uaKOiEtZHTtICNV2', 'wlmqDrvo2KStQOSm9S3544Xy64E3', 'Vstcs0Wo96TiJJxG1lkzp5wYhoC2', 
  'mru3A23CkzdyyvvdrGV3aBC5uCB2', 'uoAIwLM89gbMzh13IpHIh5w9SWd2', 'v5Q3TSKECbXXHgnhoP8UsWv8k5a2', 
  'JA4TEeFBLdW6evaOcq4Um9UopPm1', 'EqHRiGpCOqWUWCexJNE9QUrP0AM2', 'c71DRNVYaQVMRADVMW6npJN16df2', 
  'hllkDLwm4dUGhMMfxSnfO6eJ7HI2', 'LQDrL2pZBPO56ela5suGUpCESKb2', 'wrGcVkKXZwQIKayJKLR00CHkP7Y2', 
  'AYycbAlqojapT2sGLz2o6jTW4xB3', 'LKIjYVYjEfQWquGQePfCv3PKs3P2', 'DbQMviyPJEZBNsgJbl4RfBSfOTx1', 
  'pwTdXEgieZVanwfeqBvOgIA9wej2', '1gl5y5RYnNdvzDWwDbJDdX6PNwm2', '102qRl83eiQmjpUELud40H062H13', 
  'qNKfT9P71dZKDCAqRM1Sr4tTjkC3', 'tgx3Tf3MLtTU4Ss1QVMm8tVSaor2', 'DHKWCPAj45PmqI3Qv1W2HyE22SC3', 
  'sJo6fsamDhTPfEr9dnUrVcYPWV92', 'TlYDllux39hb1cCvkoO9AbCtrX63', 'xterZN4M0zaWhonZyKID7egbW5Q2', 
  'WdUhyu29KOONNzbrv2C6xzfuSji1', 'Wfn1wDtW57hNiRjLU02Z4EeWT9W2', 'Rj6mD2pMOJWA6DHdT985W3aJFq93',
  'LVCGXrSwr9SOeBg8ejHwdOQxSf02', 'wJAZ2to7qlNSXEDauAFVosYX9Jg2', 'mtu8u6SpDPQpLaxdfOHN3dyEevv2', 
  '9DyWiMEVsONrhBmiZ8GGCBWptPw2', 'QRKbVsnY9RRrcFXzGoFLGyLYxBF2', 'YTiTIMnm8aSEpA4A03KYHSEWofK2',
  'rM8xwmQ3RKMTqRF7u5OtDiVHPpF2', 'ndHlW8S3MWVp0jMTy6x9Ekcs3yQ2', 'MBhNbvWNdMUQh9sgr59x93aPHt02',
  'KRBSFfuHFGdJPYb7bU6KDVnn2xD2', 'JKj9IYRHGWMYov1qo49se5jsXgI2', '7zdz0OD7BaPlxVfvaHHB89TJbOv1', 
  'JRBYQOR4isaMCi56SMsbNKYVaD42', 'IG8N91moWidIAvYLHOjgqh6o3vh2', 'lIYC9fqUWnbOklmBiJ6lz9YEEE82', 
  '72L1toUj7bX1uVvWtxmUroCVfBR2', '3ni7az6yn7M25DwnyBjkSsEIZkT2', 'CJHm6YG6ehTywnIZCGNuCw7Q3on1', 
  'WWUoWHqvR1d4CAHXfgE0eTsHxUl2', 'XpHlrCWF0gNOwdeppbqdPosNPhD2', 'AKVoNOSYMIN6VYIhhiYuXEMCw9K2',
  'qJeN1gLmLsb2aRqBhF8seIwlLN52', 'mKg3g4co2sOv1WWZ3uHPEpIfL7u1', 'XwEGcXEwwkVwy4Vokej1pJfJWPm2',
  'qeFfhIJGvHhao9prq5k0JrFbSo52', '4kODCeGrw9aVJjfVPtUeNRH9j7P2', 'oObqxbnweFXttlSIwgvSCGxyui12', 
  'pElkACCaGwaQdxOOsq4buucGGAB3', 's1d6MBeqpFSHbvci99SUCOgp2b33', 'M9Seyd2cvVRmFPXYvCumwNhJrS42', 
  '6xDjmuwd80dcpMvQWqk4Ds2YJrh1', '5vIhfLNbnFeeY7m3nccY6NK7MLa2', 'nnUdC7NueTUQBQvnzBdFCE3Oxsg2', 
  'DhGZCJf7b6bj18nh7ckkDDEPWQ93', 'WPV8falqwTUvSWLw8rzQj4RVvCZ2', 'vbwPmOIQ4cgdEi8WWJhjCJ23ko32', 
  'XhgVIubDqoUClQ82DFTAWrP1QIB3', 'KmSwZNzpUchITjEJGkQROi4BZQU2', 'OQOgBnZ1ASgZ53YDgQz5tYRo3zG3', 
  'WvlL5KwXfKZXeT7m0MJzU0XRJfa2', 'TYQEk1nnAqcvJJiHjs8Uk6icYHJ3', 'Qo4NNzzd6mORkdG85uKBsNrA8gG3',
  'qqi7LZnKEZa1bhsXk822zbmzNJA2', 'dLciq4a5NTb8JIL4LqTc4wbxfYS2', 'TzE2vUECaEPRCGtfJUfJOVFsUC42'
    )
),

first_memory AS (
  SELECT user_id, MIN(memory_date) AS first_date
  FROM memory_data
  GROUP BY user_id
),

eligible_memories AS (
  SELECT 
    md.user_id, 
    md.memory_date, 
    md.created_at,
    fm.first_date
  FROM memory_data md
  JOIN first_memory fm ON md.user_id = fm.user_id
  WHERE fm.first_date <= '2025-05-20'
),

week1_memories AS (
  SELECT
    user_id,
    COUNT(*) FILTER (
      WHERE memory_date <= first_date + 6
    ) AS week1_memory_count
  FROM eligible_memories
  GROUP BY user_id
),

-- churn/return classification
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
    wm.user_id,
    wm.week1_memory_count,
    CASE 
      WHEN gf.had_churn_gap = 1 AND gf.last_seen >= CURRENT_DATE - 15 THEN 'returned'
      WHEN gf.last_seen < CURRENT_DATE - 15 THEN 'churned'
      ELSE 'not_churned'
    END AS status
  FROM week1_memories wm
  JOIN gap_flags gf ON wm.user_id = gf.user_id
)

SELECT
  status,
  COUNT(*) AS user_count,
  ROUND(AVG(week1_memory_count)::numeric, 2) AS avg_memories_week1,
  PERCENTILE_CONT(0.25) WITHIN GROUP (ORDER BY week1_memory_count) AS "25th_percentile",
  PERCENTILE_CONT(0.50) WITHIN GROUP (ORDER BY week1_memory_count) AS "50th_percentile",
  PERCENTILE_CONT(0.75) WITHIN GROUP (ORDER BY week1_memory_count) AS "75th_percentile"
FROM final_status
GROUP BY status
ORDER BY status;
