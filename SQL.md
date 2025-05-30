SELECT
  a."$part_date"
, "Project_1_DAU"
, "Project_2_DAU"
FROM
  ((
    SELECT
      "$part_date"
    , count(DISTINCT "#user_id") "Project_1_DAU"
    FROM
      ta.v_event_1
    WHERE (
        ("$part_date" BETWEEN '2023-01-01' AND '2023-01-07')
        AND ("$part_event" = 'login')
        AND ("coin_num" BETWEEN 10 AND 100)
        AND ("user_level" BETWEEN 10 AND 15)
    )
    GROUP BY "$part_date"
)  a
INNER JOIN (
    SELECT
      "$part_date"
    , count(DISTINCT "#user_id") "Project_2_DAU"
    FROM
      ta.v_event_2
    WHERE (
        ("$part_date" BETWEEN '2023-01-01' AND '2023-01-07')
        AND ("$part_event" = 'login')
        AND ("coin_num" BETWEEN 10 AND 100) 
        AND ("user_level" BETWEEN 10 AND 15)
    )
    GROUP BY "$part_date"
)  b ON (a."$part_date" = b."$part_date"))
ORDER BY a."$part_date" ASC
