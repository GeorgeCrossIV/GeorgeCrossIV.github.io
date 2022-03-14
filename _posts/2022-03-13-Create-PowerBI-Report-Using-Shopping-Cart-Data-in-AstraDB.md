---
layout: post
title: "Create a PowerBI report using Shopping Cart data in Astra DB"
subtitle: "data modeling examples in Astra DB"
#date: 2022-03-11 23:45:13 -0400
# background: '/img/posts/01.jpg'
---
# Introduction
Astra DB simplifies cloud-native Cassandra application development. This blog will walk the reader through creating a PowerBI report against shopping cart data in Astra DB. 

## Problem
As a report developer, I'd like to create a Power BI report using shopping cart data stored in Astra DB. 

## Audience
This blog is targeted to Power BI developers who use the Microsoft development stack. It is assumed that the developer will use a 64-bit Windows environment.

## Goal
By the end of this article, the reader should be able to create a Power BI report using data stored in the cloud using Astra DB. 

# Prerequisites
- Have created an Astra DB account and associated credentials.
- Have created the Shopping Cart data in Astra DB. [Using this blog to complete](/2022/03/11/Create-shopping-cart-model-in-AstraDB.html)
- Installed Power BI Desktop. <a href="https://powerbi.microsoft.com/en-us/downloads/" target="_blank">Download here </a> 

# Procedure
- Configure the Apache Cassandra ODBC Driver
    - Download the ODBC Driver <a href="https://downloads.datastax.com/#odbc-jdbc-drivers" target="_blank">download here</a>
    <img src="img/posts/downloads-datastax-odbc.png" alt="ODBC Download" size="650">
        - Change the package to "Windows (64-bit)"
        - Click the agreement box and then the download button
- Create the Power BI Report


# Results
The reader should now have a functioning Power BI report that uses the shopping cart database in Astra DB. 

# Next Steps
The following activities are designed to use the shopping cart data:
- Write a C# Shopping Cart MVC application using REST against Astra DB