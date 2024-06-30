CREATE TABLE kimia_farma.kf_analysis AS
with gross_laba AS
  (SELECT distinct
  price, product_id,
  CASE
    when price <= 50000 then 0.1
    when price between 50000 and 100000 then 0.15
    when price between 100000 and 300000 then 0.20
    when price between 300000 and 500000 then 0.25
    when price > 500000 then 0.3
  END AS percentage_gross_laba
  from `kimia_farma.kf_final_transaction`)

  SELECT DISTINCT
  trc.transaction_id,
  trc.date,
  trc.branch_id,
  brc.branch_name,
  brc.kota as city,
  brc.provinsi as province,
  brc.rating as branch_rating,
  trc.customer_name,
  trc.product_id,
  prd.product_name,
  trc.price as actual_price,
  trc.discount_percentage,
  pgl.percentage_gross_laba,
  (trc.price - (trc.price * trc.discount_percentage)) as nett_sales,
  (trc.price - (trc.price * trc.discount_percentage)) * pgl.percentage_gross_laba as nett_profit,
  trc.rating as transaction_rating
  FROM gross_laba as pgl
  inner join `kimia_farma.kf_final_transaction` as trc on pgl.product_id = trc.product_id
  inner join `kimia_farma.kf_kantor_cabang` as brc on trc.branch_id = brc.branch_id
  inner join `kimia_farma.kf_product` as prd on trc.product_id = prd.product_id
  ORDER BY date ASC
