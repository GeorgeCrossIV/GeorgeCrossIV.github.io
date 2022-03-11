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

# Prerequistes
- Have created an Astra DB account and associated credentials.
- (Optional) Have installed and configured a terminal with the astra-cqlsh application

# Steps
## Open the Astra DB Console
- Login in to Astra (https://astra.datastax.com)
<img src="/img/posts/astra-login.png" alt="Astra Login Screen" width="350"> 
- Select your database
<img src="/img/posts/select-database-and-cql-console.png>" alt="Select Database" width="350">
- Click CQL Console
<img src="/img/posts/astra-cql-console.png>" alt="Select Database" width="350">
~~~ 
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


