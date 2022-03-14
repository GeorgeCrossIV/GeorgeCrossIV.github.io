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
- Downloaded the connection bundle to the Windows client

# Procedure
- Configure the Apache Cassandra ODBC Driver
    - Download the ODBC Driver <a href="https://downloads.datastax.com/#odbc-jdbc-drivers" target="_blank">download here</a>
    <img src="/img/posts/downloads-datastax-odbc.png" alt="ODBC Download" width="650">
        - Change the package to "Windows (64-bit)"
        - Click the agreement box and then the download button
    - Install the ODBC drivers. 
        - review the <a href="https://www.datastax.com/blog/how-use-datastax-odbc-drivers" target="_blank">How to Use DataStax ODBC Drivers blog</a>
        - Start the ODBC Data Sources (64-bit) application
        <img src="/img/posts/start-odbc-data-sources.png" alt="Start ODBC data sources" width="650">
        - Create new ODBC Entry
        <img src="/img/posts/odbc-data-source-administrator.png" alt="ODBC Data Source Administrator" width="650">
        - Create a new DataStax Cassandra ODBC Data Source
        <img src="/img/posts/create-new-data-source.png" alt="Create new data source" width="650">
        - Configure the Cassandra ODBC Driver
        <img src="/img/posts/configure-cassandra-odbc-driver.png" alt="Configure Cassandra ODBC Driver" width="650">
            - Data Source Name: "Astra Shopping Cart"
            - Descripton: "Astra Shopping Cart Demo"
            - Default keyspace: "shopping_cart_data"
            - Mechanism: "Cloud Secure Connection Bundle"
            - User name: client id goes here
            - Password: client secret goes here
            - Connection Bundle: path to the connection bundle
        - Test the client. Click the Test button
        <img src="/img/posts/odbc-driver-test-results.png" alt="Test ODBC Driver" width="650">
            - should show that test test was successful
- Create the Power BI Report
    - Start Power BI in Administrator mode
    <img src="/img/posts/start-power-bi-desktop.png" alt="Start Power BI Desktop" width="650">
    - Click Get Data
    <img src="/img/posts/power-bi-desktop-get-data.png" alt="Power BI Get Data" width="650">
    - Configure ODBC Connection
    <img src="/img/posts/power-bi-desktop-configure-odbc-part1.png" alt="Configure ODBC Connections" width="650">
        - Select "Other"
        - Select "ODBC"
        - Click "Connect"
    - Select the ODBC Data Source
    <img src="/img/posts/power-bi-desktop-select-odbc-source.png" alt="Select ODBC Data Source" width="650">
        - Change drop down to "Astra Shopping Cart"
        - Click OK
    - Authenticate the ODBC Connection
    <img src="/img/posts/power-bi-desktop-authenticate-odbc.png" alt="Authenticate the ODBC Connection" width="650">
        - user name: use the client id from Astra DB
        - password: use the client secret from Astra DB
    - Load the Shopping Cart data
    <img src="/img/posts/power-bi-desktop-load-data.png" alt="Load the Shopping Cart Data" width="650">
        - Expand "Cassandra"
        - Expand "shopping_cart_data" keyspace
        - check the following:
            - carts_by_user
            - items_by_cart
            - users
        - Click the "Load" button
    - Configure Page Visuals
        - Add user slicer
        <img src="/img/posts/power-bi-desktop-add-user-slicer.png" alt="Add User slicer" width="650">
            - Click Users table
            - click "last_name" field checkbox
            - Click the slicer visualization
        - Change the Slicer text size
             - <img src="/img/posts/power-bi-desktop-change-user-slicer-text-size.png" alt="Change user slicer text size" width="350">
            - Click the format icon
            - change the Text size to 16 pt
        - Change the Slicer title
             - <img src="/img/posts/power-bi-desktop-change-user-slicer-title.png" alt="Change the user slicer title" width="350">
            - Click the format icon
            - change the Title Text to "Select User"
        - Add the Selected Cart widget
        <img src="/img/posts/power-bi-desktop-add-cart-slicer.png" alt="Add Cart Slicer" width="650">
            - Click an empty portion of the report. No widget should be selected.
            - Expand the "carts_by_user" table and check the cart_name field
            - Click the Slicer Visualization
            - Change Slicer Heading --> Title Text to "Select Cart"
            - Change Items --> Text Size to 16 pt
        - Add the Item Quantity Column Chart
        <img src="/img/posts/power-bi-desktop-add-item-quantity-column-chart.png" alt="Add item quantity column chart" width="650">
            - Click an empty portion of the report. No widget should be selected
            - Expand the items_by_cart table and click the following fields:
                - item_name
                - quantity
            - click the stacked column chart visulization
            - Change the Title Text to "Item Quantities"
            - move the widget to the right of the User slicer
        - Add the Item Quantity Pie Chart
        <img src="/img/posts/power-bi-desktop-add-item-quantity-pie-chart.png" alt="Add item quantity pie chart" width="650">
            - Click an empty portion of the report. No widget should be selected
            - Expand the items_by_cart table and click the following fields:
                - item_name
                - quantity
            - click the pie chart visulization
            - Change the Title Text to "Item Qty"
            - move the widget to the right of the Cart slicer
        - Add the Item Quantity table
        <img src="/img/posts/power-bi-desktop-add-item-table.png" alt="Add item quantity table" width="650">
            - Click an empty portion of the report. No widget should be selected
            - Expand the users table and check the following:
                - first_name
                - last_name
            - Expand the items_by_cart table and check the following:
                - item_name
                - Item_price
                - quantity
                - item_description
            - Move the widget to the right of the Item quantity column chart

# Results
The reader should now have a functioning Power BI report that uses the shopping cart database in Astra DB. 
<img src="/img/posts/power-bi-desktop-final-results.png" alt="Power BI - final results" width="650">

# Next Steps
The following activities are designed to use the shopping cart data:
- Write a C# Shopping Cart MVC application using REST against Astra DB