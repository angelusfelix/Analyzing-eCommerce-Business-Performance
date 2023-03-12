Goal = Aggregated various business csv files and simplified to track, 
monitor and assess the success or failure of various business processes

notes = "##" = dataset

## Customer_dataset
1. There is no duplicate data in customers_dataset.
2. Most customer in customer_dataset is customer from sao paulo 15540 customers.

## orders_dataset
1. Total 2980 rows null values
2. Order purchase start from 15th Sept,2016 until 29th Aug,2018
3. Join Table to customers_dataset 
	- od.order_id,
	- od.customer_id, 
	- od.order_status,
	- cd.customer_city

## products_dataset
1. Create new table product_dataset_dropnull
2. There is no duplicate data in product_dataset_dropnull dataset
3. Most product sold is bed_bath_table in product_dataset_dropnull

## order_payments_dataset
1. The most total_value is customer from sao paulo with value 1757931.790000004 using credit_card
2. Join order_dataset, order_payments_dataset, and customers_dataset
	- select cd.customer_id, 
	- tmp.order_id,
	- cd.customer_city,
	- cd.customer_zip_code_prefix,
	- tmp.order_status,
	- tmp.payment_type,
	- tmp.payment_value
3. Create table payments_new_dataset

## order_items_dataset
1. Join payment_new_dataset, order_items_dataset, product_dataset_dropnull
	   - pnd.customer_id, 
	   - tmp.order_id,
	   - tmp.product_id,
	   - tmp.seller_id,
	   - tmp.product_category_name,
	   - pnd.customer_city,
	   - pnd.customer_zip_code_prefix,
	   - pnd.order_status,
	   - pnd.payment_type,
	   - tmp.price	
2. Create table order_items_new_dataset
3. Find total price in each product

## order_reviews_dataset
1. Join order_items_new_dataset and order_reviews_dataset
	- oind.customer_id,
	- oind.order_id,
	- oind.product_id,
	- oind.seller_id,
	- oind.product_category_name,
	- oind.customer_city,
	- oind.customer_zip_code_prefix,
	- oind.order_status,
	- oind.payment_type,
	- oind.price,
	- ord.review_score
2. Create table order_reviews_new_dataset
3. Review score in each product, 
	- "security_and_services" is the lowest product's mean_score (2.50 out of 5),
	- "cds_dvds_musicals" is the highest product's mean_score (4.64 out of 5)

## sellers_dataset
1. The most seller in seller_dataset is seller from sao paulo (694 seller)
2. Join order_reviews_new_dataset, sellers_dataset
	- ornd.customer_id,
	- ornd.order_id,
	- ornd.product_id,
	- ornd.seller_id,
	- ornd.product_category_name,
	- ornd.customer_city,
	- ornd.customer_zip_code_prefix,
	- ornd.order_status,
	- ornd.payment_type,
	- ornd.price,
	- sd.seller_city
3. create table sellers_new_dataset

## geolocation_dataset
1. Join geolocation dataset, sellers_new_dataset
	- snd.customer_id,
	- snd.seller_id,
	- snd.order_id,
	- snd.product_id,
	- snd.product_category_name,
	- snd.order_status,
	- snd.payment_type,
	- snd.price,
	- snd.customer_city,
	- snd.customer_zip_code_prefix,
	- gd.geolocation_lat,
	- gd.geolocation_lng,
	- snd.seller_city
2. Create table geolocation_new_dataset. Geolocation_new_dataset is our fix_dataset

## Result from fix_dataset
1. The customer who spends the most is the customer with the id "351e40989da90e70487765f6ea15d54b" 
with a total purchase of R$ 982607.7299999467.
2. The most product sold is bed_bath_table (1893568 units sold).
3. The most status order is "delivered", "shipped", and "cancelled".
4. The most customer is customer from rio de janeiro, sao paulo, and belo horizonte.
5. The most seller is seller from sao paulo, ibitinga, and curitiba
6. Seller with id "1f50f920176fa81dab994f9023523100" is the most seller who sell his product. The products that he/she sell is garden_tools.

