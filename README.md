# sql-solves

--1

SELECT user_id, spend, transaction_date
FROM
  (SELECT 
    user_id, 
    ROW_NUMBER() OVER (PARTITION BY user_id 
                      ORDER BY transaction_date ASC) as transaction_number,
    spend, 
    transaction_date
  FROM transactions
  order by user_id, transaction_date ASC) t
where transaction_number = 3
ORDER BY user_id ASC
