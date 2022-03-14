---
layout: post
title: "Create the Shopping Cart data model in Astra DB"
subtitle: "data modeling examples in Astra DB"
#date: 2022-03-11 23:45:13 -0400
# background: '/img/posts/01.jpg'
---
# Introduction
Astra DB simplifies cloud-native Cassandra application development. This blog will walk the reader through creating a shopping cart model in Astra DB. 

## Problem
As a developer, I'd like to quickly stand up a shopping cart database in the cloud that will be used as the data store for a shopping cart sample application and report. 

## Audience
This blog is targeted to database and application developers. 

## Goal
By the end of this article, the reader should be able to create a data store in the cloud using Astra DB. The data store can be used for any application development or reporting effort.

# Prerequisites
- Have created an Astra DB account and associated credentials.
- (Optional) Have installed and configured a terminal with the astra-cqlsh application

# Procedure
- Login in to Astra (https://astra.datastax.com)
<img src="/img/posts/astra-login.png" alt="Astra Login Screen" width="650"> 
- Select your database
 <img src="/img/posts/select-database-and-cql-console.png" alt="Select Database" width="650">
- Create the shopping_cart_data keyspace
 <img src="/img/posts/create-keyspace-part1.png" alt="Select Database" width="650">
  <img src="/img/posts/create-keyspace-part2.png" alt="Select Database" width="650">
- Click CQL Console
<img src="/img/posts/astra-cql-console.png" alt="Select Database" width="650">
- Create the shopping_cart_data table
~~~sql 
    CREATE TABLE shopping_cart_data.items_by_cart (
        cart_id uuid,
        timestamp timestamp,
        item_id text,
        cart_subtotal decimal static,
        item_description text,
        item_name text,
        item_price decimal,
        quantity int,
        PRIMARY KEY (cart_id, timestamp, item_id)
    );
~~~
- create the shopping_cart_data.items_by_id table
~~~
    CREATE TABLE shopping_cart_data.items_by_id (
        id text PRIMARY KEY,
        description text,
        name text,
        price decimal
    );
~~~
- create the shopping_cart_data.carts_by_user table
~~~
    CREATE TABLE shopping_cart_data.carts_by_user (
        user_id text,
        cart_name text,
        cart_id uuid,
        cart_is_active boolean,
        user_email text static,
        PRIMARY KEY (user_id, cart_name, cart_id)
    );
~~~
- create the users table
~~~
    CREATE TABLE users (
        user_id TEXT,
        first_name TEXT,
        last_name TEXT,
        user_email TEXT,
        PRIMARY KEY ((user_id))
    );
~~~
- Populate data for carts by user
~~~
    INSERT INTO carts_by_user (user_id,cart_name,cart_id,cart_is_active,user_email)
    VALUES ('jen','Gifts for Mom',19925cc1-4f8b-4a44-b893-2a49a8434fc8,false,'jen@datastax.com');
    INSERT INTO carts_by_user (user_id,cart_name,cart_id,cart_is_active,user_email)
    VALUES ('jen','Gifts for Dad',5453bd52-8366-4776-aa7c-d8d827176493,false,'jen@datastax.com');
    INSERT INTO carts_by_user (user_id,cart_name,cart_id,cart_is_active,user_email)
    VALUES ('jen','My Birthday',4e66baf8-f3ad-4c3b-9151-52be4574f2de,true,'jen@datastax.com');
    INSERT INTO carts_by_user (user_id,cart_name,cart_id,cart_is_active,user_email)
    VALUES ('joe','Things Joe Likes',2ff01a3f-0b28-4894-bb3e-989f03412b06,true,'joe@datastax.com');
    INSERT INTO carts_by_user (user_id,cart_name,cart_id,cart_is_active,user_email)
    VALUES ('jim','My Shopping List',3ff4c697-ae75-449e-ab20-aac392f0bbf0,true,'jim@datastax.com');
~~~
- Populate data for items_by_id
~~~
    INSERT INTO items_by_id (id,name,description,price)
    VALUES('Bouquet1','Red Roses','Red roses and white Calla lilies',26.50);
    INSERT INTO items_by_id (id,name,description,price)
    VALUES('Bouquet2','Red Roses','Two dozen red roses',22.50);
    INSERT INTO items_by_id (id,name,description,price)
    VALUES('Bouquet3','Pink Roses','Pink roses, carnations and daisy poms',27.50);
    INSERT INTO items_by_id (id,name,description,price)
    VALUES('Strawberries1','Strawberries','Strawberries dipped in milk chocolate',12.50);
    INSERT INTO items_by_id (id,name,description,price)
    VALUES('Strawberries2','Strawberries','Strawberries dipped in dark chocolate',12.50);
    INSERT INTO items_by_id (id,name,description,price)
    VALUES('Box1','Truffles','16 milk, dark and white chocolate truffles',40.00);
    INSERT INTO items_by_id (id,name,description,price)
    VALUES('Box2','Chocolates','25 gourmet chocolates from our collection',60.00);
    INSERT INTO items_by_id (id,name,description,price)
    VALUES('Basket1','Wine','Cheese and wine basket',100.00);
    INSERT INTO items_by_id (id,name,description,price)
    VALUES('Basket2','Cookies','24 buttercream frosted cookies',24.00);
    INSERT INTO items_by_id (id,name,description,price)
    VALUES('Cake1','Chocolate Cake','Buttercream frosted chocolate cake',80.00);
    INSERT INTO items_by_id (id,name,description,price)
    VALUES('Cake2','Chocolate Cake','Chocolate mousse cake',80.00);
    INSERT INTO items_by_id (id,name,description,price)
    VALUES('Cake3','Cheesecake','NY original cheesecake',75.00);
~~~
- Populate table items_by_cart
~~~
    INSERT INTO items_by_cart (cart_id,timestamp,item_id,item_name,item_description,item_price,quantity,cart_subtotal)
    VALUES (19925cc1-4f8b-4a44-b893-2a49a8434fc8,'2020-10-21 11:45:03','Bouquet1','Red Roses','Red roses and white Calla lilies',26.50,1,51.50);
    INSERT INTO items_by_cart (cart_id,timestamp,item_id,item_name,item_description,item_price,quantity,cart_subtotal)
    VALUES (19925cc1-4f8b-4a44-b893-2a49a8434fc8,'2020-10-21 11:48:43','Strawberries1','Strawberries','Strawberries dipped in milk chocolate',12.50,2,51.50);
    
    INSERT INTO items_by_cart (cart_id,timestamp,item_id,item_name,item_description,item_price,quantity,cart_subtotal)
    VALUES (5453bd52-8366-4776-aa7c-d8d827176493,'2020-10-21 13:00:16','Cake3','Cheesecake','NY original cheesecake',75.00,1,87.50);
    INSERT INTO items_by_cart (cart_id,timestamp,item_id,item_name,item_description,item_price,quantity,cart_subtotal)
    VALUES (5453bd52-8366-4776-aa7c-d8d827176493,'2020-10-21 13:15:51','Strawberries2','Strawberries','Strawberries dipped in dark chocolate',12.50,1,87.50);
    
    INSERT INTO items_by_cart (cart_id,timestamp,item_id,item_name,item_description,item_price,quantity,cart_subtotal)
    VALUES (4e66baf8-f3ad-4c3b-9151-52be4574f2de,TOTIMESTAMP(NOW()),'Cake1','Chocolate Cake','Buttercream frosted chocolate cake',80.00,1,80.00);
    
    INSERT INTO items_by_cart (cart_id,timestamp,item_id,item_name,item_description,item_price,quantity,cart_subtotal)
    VALUES (2ff01a3f-0b28-4894-bb3e-989f03412b06,TOTIMESTAMP(NOW()),'Basket2','Cookies','24 buttercream frosted cookies',24.00,3,112.00);
    INSERT INTO items_by_cart (cart_id,timestamp,item_id,item_name,item_description,item_price,quantity,cart_subtotal)
    VALUES (2ff01a3f-0b28-4894-bb3e-989f03412b06,TOTIMESTAMP(NOW()),'Box1','Truffles','16 milk, dark and white chocolate truffles',40.00,1,112.00);
    
    INSERT INTO items_by_cart (cart_id,timestamp,item_id,item_name,item_description,item_price,quantity,cart_subtotal)
    VALUES (3ff4c697-ae75-449e-ab20-aac392f0bbf0,TOTIMESTAMP(NOW()),'Strawberries2','Strawberries','Strawberries dipped in dark chocolate',12.50,2,25.00);
~~~

- Populate the users table
~~~
    INSERT INTO users (user_id, first_name, last_name, user_email) VALUES ('jen', 'Jennifer', 'Goodcoder', 'jen@datastax.com');
    INSERT INTO users (user_id, first_name, last_name, user_email) VALUES ('jim', 'Jim', 'Troubleshooter', 'jim@datastax.com');
    INSERT INTO users (user_id, first_name, last_name, user_email) VALUES ('joe', 'Joe', 'Operator', 'joe@datastax.com');
~~~

# Results
The reader should now have a functioning shopping cart database in the shopping_cart_data keyspace. 

# Next Steps
The following activities are designed to use the shopping cart data:
- Write a C# Shopping Cart MVC application using REST against Astra DB
- Create a PowerBI report using Shopping Cart data in Astra DB