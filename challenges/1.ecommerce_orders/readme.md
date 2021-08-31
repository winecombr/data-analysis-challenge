# Ecommerce Orders Challenge

In this challenge you will be asked to create the queries that answers the questions below. 
To setup the database follow the setup guide. 
**Found any problem ? Please open an issue !**


## 1. Questions
The SQL that answers the questions should be placed in the sql folder.
The name of the file should be 1.sql for the answer of the first question and so on.
After you are done answering all the questions you can send it to us via email.

1. What was the revenue for each store in the first quarter of 2021 segregated by web and mobile app sessions? 

2. What was the average ticket for each customer in the first quarter of 2021? List the top 10 customers by average ticket.

3. For the STORE_A, compute the cohort of customers orders to see the percentage of customer that had recurring orders for each month.

4. We want to increase recurring orders in our ecommerce, from the question 3, analyze the customers that had recurring orders to see if you can find any common trait.

5. You've been asked by the marketing team to produce a list of 50k customers for a campaign where we are going to launch our newest product which will cost R$ 200,00.

## 2. Setup Guide

1. Uncompress the files in the data folder
2. Run a postgres server using docker (remember to mount the data folder into the container):

```shell
# run this command inside this folder. you maybe have to change the $PWD command depending on your OS
docker run --name=pg -d \
           -e POSTGRES_PASSWORD=secret \
	         -p 5432:5432 \
	         -v $PWD/data:/data \
	         postgres:13  
```
3. Connect to the database using your preferred tool and create the schemas for the tables and load the data into the database:

```shell
# connecting with the cli
docker exec -ti pg psql -U postgres
```

```sql
create table orders (
  id varchar(64) not null,
  customer_id varchar(64) not null,
  created_date timestamp without time zone not null,
  total decimal(20,2) not null,
  currency varchar(64) not null,
  sku_count decimal(20,0) not null,
  status varchar(64) not null,
  store varchar(64) not null,
  had_subscription boolean not null,
  primary key (id)
);

comment on column orders.id is 'The order ID';
comment on column orders.customer_id is 'ID the of the customer that put the order';
comment on column orders.created_date is 'The timestamp when the order was issued';
comment on column orders.total is 'Total paid by the customer';
comment on column orders.currency is 'Currency used to pay';
comment on column orders.sku_count is 'Number of items in the order';
comment on column orders.status is 'Current status of the order';
comment on column orders.store is 'Store where the order was made';
comment on column orders.had_subscription is 'True if the customer was a subscriber/premium user in the moment of the purchase';

COPY orders FROM '/data/ecommerce_orders_part1.csv' WITH (FORMAT csv, HEADER);
COPY orders FROM '/data/ecommerce_orders_part2.csv' WITH (FORMAT csv, HEADER);

create table orders_metadata (
  id varchar(64) not null,
  order_id varchar(64) not null,
  item_key varchar(255) not null,
  item_value varchar(1024) default null,
  primary key (id)
);

COPY orders_metadata FROM '/data/ecommerce_orders_metadata.csv' WITH (FORMAT csv, HEADER);

```

4. All set, you can start querying now :rocket: :rocket: :rocket:.
You may want to create some indexes to speed things up... that we will leave to you :juggling_person:	