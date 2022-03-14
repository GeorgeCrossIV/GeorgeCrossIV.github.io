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

# Procedure
- Download the Windows Terminal app from the Microsoft Store. Note - the Terminal app is already installed if using Windows 11. 
    - Open Microsoft Store
    - Search for "Windows Terminal"
    <img src="/img/posts/microsoft-store-windows-terminal.png" alt="Microsoft Store - Windows Terminal" width="650">
    - Install
- Install Ubuntu (if necessary)
- Configure Windows Terminal app with shortcuts
    - Start Windows Terminal. PowerShell should be the default Window
        <img src="/img/posts/windows-terminal-powershell.png" alt="Windows Terminal - PowerShell" width="650">

    - Create a new Terminal entry (if necessary)
        - Find list of Linux distributions
            ~~~
            wsl.exe -l --all
            ~~~
            <img src="/img/posts/powershell-display-linux-distributions.png" alt="PowerShell - Display Linux Distributions" width="650">
        - Open the Settings screen
            <img src="/img/posts/windows-terminal-open-settings-part1.png" alt="Windows Terminal - Open Settings" width="650">        
            <img src="/img/posts/windows-terminal-open-settings-part2.png" alt="Windows Terminal - Open Settings" width="650">   
        - Edit the settings file
        <img src="/img/posts/windows-terminal-add-terminal-tab-part1.png" alt="Windows Terminal - Add terminal tab" width="650"> 
            - Find the "list" section in the JSON
            - Add an entry for the Linux Distribution
            ~~~json
            {
                "guid": "{6f9994f0-4403-5e85-9cce-98e5da3839bb}",
                "hidden": false,
                "name": "Ubuntu-16.04",
                "source": "Windows.Terminal.Wsl"
            }
            ~~~   
                - use a GUID generator to provide a unique GUID for the guid key
                - use the name of the Linux distribution name from the previous step from executing the wsl -l --all step.
                - Save the file   
        - Restart Windows Terminal
- Open a new terminal tab for a Linux distribution
    <img src="/img/posts/windows-terminal-open-new-terminal-tab.png" alt="Windows Terminal - Open new terminal tab" width="650">  
    - Click the down arrow to display the list of available terminal types
    - Click the Ubuntu distribution, which should open a new terminal tab
    - Note - If there are no Linux distributions, use the steps above to add a new entry  
    <img src="/img/posts/windows-terminal-open-new-linux-distribution-tab.png" alt="Windows Terminal - Open new terminal tab" width="650"> 
- Install Standalone CQL Shell
    - use the [Standalone CQL Shell article](https://docs.datastax.com/en/astra/docs/connecting-to-databases-using-standalone-cqlsh.html) to install and configure
        - I recommend that you configure the cqlshrc file in the ~/.cassandra folder to prevent typing the client id and client secret each time you want to start the CQL shell.
    - Notes: You must have Python installed to run the cqlsh-astra standalone client. A version of Python with SSL support is also required. I've had issues running Python 2.7 in Ubuntu versions earlier than 20.06. 
        - There is a method for compiling an older version of Python 2.7 with SSL support. I'll update this blog with the information once I find it. In the meantime, I recommend using Ubuntu 20.06 or installing Python 3.x. Be aware that you need Python 2.7 if you are also running DSE in the Linux distribution.
- Update your .bashrc file with the cqlsh-astra folder
    - Assuming the installation folder for cqlsh-astra is ~/cqlsh-astra.
    - add the following to the .bashrc file
    ~~~
    export PATH=$PATH:~/cqlsh-astra/bin
    ~~~ 
    - source your .bashrc file
    ~~~
    $ source .bashrc
    ~~~
- Start the cqlsh
~~~
$ cqlsh
~~~
<img src="/img/posts/windows-terminal-start-astra-cqlsh.png" alt="Windows Terminal - Start Astra CQLSH" width="650"> 
- Display the keyspaces
~~~
cqlsh> desc keyspaces;
~~~
<img src="/img/posts/astra-cqlsh-display-keyspaces.png" alt="Astra CQLSH - Display keyspaces" width="650"> 

# Results
The reader should now have a stand-alone console that can be used to connect to and manage Astra DB. 

# Next Steps
- [Create the shopping cart data in Astra DB](/2022/03/11/Create-shopping-cart-model-in-AstraDB.html)

# References
- <a href="https://docs.datastax.com/en/astra/docs/connecting-to-databases-using-standalone-cqlsh.html" target="_blank">Configuring the CQL Shell to connect to Astra</a>
