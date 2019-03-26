---
layout: post
title: Automate DB (Database) testing with Pester and dbatools
description: 
headline: 
modified: 2018-05-26
category: Automation
tags: [automation, testing, database, pester, dbatools]
imagefeature: 
mathjax: 
chart: 
comments: true
featured: true
---

Typically when writing and testing applications people will often not write tests directly at the database level, often because developers or testers are unsure how to tackle this problem or are simply not aware that they can. I've seen many people write unit, integration/service or UI tests but never tests which test just the database.

Last week I was very fortunate to pair on a piece of work with an exceptional DBA - Michal Poreba. He showed me some things around testing at the database level using Pester and dbatools and so I thought I would note it down in a blog post not only as a point of reference for myself but to hopefully help others.

## Prerequisites

In order to follow along with this blog post you will need to ensure you have the following installed:

* [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)
* [Visual Studio Code](https://code.visualstudio.com/download)
* [Visual Studio Code Powershell Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell) - the easiest way to  install the Powershell extension is within Visual Studio Code. Within extensions search for and install the Powershell extension.

## What is Pester?

> "Pester is the ubiquitous test and mock framework for PowerShell."

Pester is a flexible testing framework for PowerShell. Pester tests are written as PowerShell scripts. In basic terms, if you can retrieve information with PowerShell, you can verify it with Pester. 

### Install Pester

In order to install Pester firstly open powershell as an administrator and then run the following: 
```
Install-Module -Name Pester -Force -SkipPublisherCheck
```

You may get prompted to install NuGet provider. If you do type 'y' and press enter to continue.

You may be prompted that this is a untusted repository. If you do type 'y' and press enter to continue.

## What is dbatools?

> "dbatools is a free PowerShell module with over 300 SQL Server administration, best practice and migration commands included."

dbatools when paired with Pester enables you to verify various things about your database - for example, you can verify that a stored procedure exist, a column is of the correct type and size, and so this when paired with Pester is a powerful combination.

### Install dbatools

In order to install dbatools firstly open powershell as an administrator and then run the following: 
```
Install-Module dbatools
```
You may get prompted to install NuGet provider. If you do type 'y' and press enter to continue.

You may be prompted that this is a untusted repository. If you do type 'y' and press enter to continue.

## Getting started with our first test

For our first test we will create a test to check the given stored procedure exists in the database.

Within VSCode create a new [yourfilename].ps1 file. We are going to write a test which checks that a stored procedure exits for a database. If you have a database setup locally already with some tables and stored procedures then great, if not create a new database, i.e. named 'Sample' and create a new table called 'Users' which has the following columns: Id (int), Firstname varchar(50), Surname varchar(50). Next create a stored procedure called GetAllUsers which gets all users from the 'Users' table.

Next copy the below in to the [yourfilename].ps1 file you created

```
$testInstance = "localhost\sql2017" <- replace with your local instance info!!
$testDatabase = "Sample"

function CheckProcedureExists{
    param([string]$ProcedureName) 
    process {
        
        $result = (Invoke-DbaSqlQuery -SqlInstance $testInstance -Database $testDatabase -Query "select count(*) from sys.procedures where name = '$ProcedureName'")[0]
            $result | Should -Be 1
    }
}

Describe "Testing Sample stored procedures" {
    Context "GetAllUsers" {
        It "GetAllUsers stored procedure exists" {
            CheckProcedureExists("GetAllUsers")
        }
    }
}
```

![_config.yml]({{ site.baseurl }}/images/dba-testing.png)

In the above test we've created a function called CheckProcedureExists which takes one parameter, a string. The function queries the database to see if a row is returned for the stored procedure name (string) we passed to the function which would indicate the expected stored procedure indeed exists. In the test we simply call the function and give the name of the stored procedure we want to check exists.

### Running the first test

Next press 'F5' and the above .ps1 file will now run within PowerShell. If all goes well your test will run and assert that the stored procedure exists in your database and you should get no errors. 

It's worth noting the first time you run the test it may take a little while but each time thereafter the test will run considerably faster.

### Problem running the first test?

When I first tried to run the above on my local machine at home having be shown how to write these tests at work, I kept getting the following error:

> "Arithmetic overflow exception when opening SQL connection"

After trying many things to ensure I had everything setup correctly I was unable to get dbatools to query my local database via PowerShell. After a day or two of searching I finally found [this post which resolved this issue](https://stackoverflow.com/questions/32609088/arithmetic-overflow-exception-when-opening-sql-connection/#answer-38451174). It turns out Lavasoft was causing some issues which once uninstalled and restarting my computer, enabled me to successfully run the above test.

The above is a very basic example of the awesomeness of Pester and dbatools and can be taken so much further, hopefully it's wet your appetite.