---
layout: post
title: "Using Windows Terminal with Ubuntu & CQLSH against Astra"
subtitle: "Configure cqlsh for Astra"
#date: 2022-01-14 23:45:13 -0400
# background: '/img/posts/01.jpg'
---
# Introduction
Astra DB simplifies cloud-native Cassandra application development. Each DataStax Astra DB database includes an embedded CQL shell instance. In the Astra DB console, navigate to your database and click the CQL Console tab to open a CQLSH instance that is connected to your database. Issue CQL commands directly to your Astra DB database without navigating outside of your browser.

As convenient as it is to be able to access the CQL Console in the browser, a developer may want additional flexibility of connecting to Astra via a CQL Console in a desktop application. As a developer, I often like to have prefer to have multiple terminal open. For example, I might work in two keyspaces simultaneously and want a CQL session for each keyspace. I often like keeping a CQL Console to view or manage DDL while using a seperate CQL Console for DML.

## Problem
As a developer, I'd like to be to manage multiple CQL Consoles that connect to my Astra database. 

## Audience
I'm primarily a Microsoft Stack developer and I'd like the solution to be able work within my Windows environment. This article is for you if you develop in the Windows environment. There are many terminal applications to choose from; however, this article will use a simple and free terminal application named Windows Terminal.

## Goal
By the end of this article, you should be able to use a desktop terminal application to connect to your Astra database.

# Prerequistes
- Windows 10 or Windows 11
- Have created an Astra DB account and associated credentials.
- Have installed the Windows Terminal application
- Have installed the Windows Subsystem for Unix (WSL)
- Have installed a Linux instance in the WSL. This article assumes Ubuntu has been installed; however, any Linux flavor will do.

some text here
Configuring the CQL Shell to connect to Astra - https://docs.datastax.com/en/astra/docs/connecting-to-databases-using-standalone-cqlsh.html
