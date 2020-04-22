---
title: 步驟 3：使用 Node.js 連線到 SQL
description: 這個範例應該被視為一個概念證明，說明如何使用 Node.js 連線到 SQL，而且為了清楚起見，已將其簡化。
ms.custom: ''
ms.date: 07/23/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5d5b41b6-129a-40b1-af8b-7e8fbd4a84bb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e7bc243bbcfe0f132cebe73df18d52ee769ec77e
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528912"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-nodejs"></a>步驟 3：使用 Node.js 連線到 SQL 的概念證明

![Download-DownArrow-Circled](../../ssms/media/download-icon.png)[下載 Node.js SQL 驅動程式](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

這個範例只應被視為一個概念證明。  為了清楚起見，已將範例程式碼簡化，而其不一定代表 Microsoft 建議的最佳做法。 GitHub 上提供使用相同重要功能的其他範例：

- [https://github.com/tediousjs/tedious/blob/master/examples/](https://github.com/tediousjs/tedious/blob/master/examples/)
  
## <a name="step-1-connect"></a>步驟 1:連線  
  
**new Connection** 函式可用來連接到 SQL Database。  
  
```javascript  
    var Connection = require('tedious').Connection;  
    var config = {  
        server: 'your_server.database.windows.net',  //update me
        authentication: {
            type: 'default',
            options: {
                userName: 'your_username', //update me
                password: 'your_password'  //update me
            }
        },
        options: {
            // If you are on Microsoft Azure, you need encryption:
            encrypt: true,
            database: 'your_database'  //update me
        }
    };  
    var connection = new Connection(config);  
    connection.on('connect', function(err) {  
        // If no error, then good to proceed.
        console.log("Connected");  
    });  
```  
  
## <a name="step-2--execute-a-query"></a>步驟 2:執行查詢  
  
  
所有 SQL 陳述式都會使用 **new Request()** 函式來執行。 如果陳述式傳回資料列 (例如 SELECT 陳述式)，您可以使用 **request.on()** 函式擷取這些資料列。 如果沒有資料列，request.on() 函式會傳回空白清單。  
  
  
```javascript  
    var Connection = require('tedious').Connection;  
    var config = {  
        server: 'your_server.database.windows.net',  //update me
        authentication: {
            type: 'default',
            options: {
                userName: 'your_username', //update me
                password: 'your_password'  //update me
            }
        },
        options: {
            // If you are on Microsoft Azure, you need encryption:
            encrypt: true,
            database: 'your_database'  //update me
        }
    }; 
    var connection = new Connection(config);  
    connection.on('connect', function(err) {  
        // If no error, then good to proceed.  
        console.log("Connected");  
        executeStatement();  
    });  
  
    var Request = require('tedious').Request;  
    var TYPES = require('tedious').TYPES;  
  
    function executeStatement() {  
        request = new Request("SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC;", function(err) {  
        if (err) {  
            console.log(err);}  
        });  
        var result = "";  
        request.on('row', function(columns) {  
            columns.forEach(function(column) {  
              if (column.value === null) {  
                console.log('NULL');  
              } else {  
                result+= column.value + " ";  
              }  
            });  
            console.log(result);  
            result ="";  
        });  
  
        request.on('done', function(rowCount, more) {  
        console.log(rowCount + ' rows returned');  
        });  
        connection.execSql(request);  
    }  
```  
  
## <a name="step-3-insert-a-row"></a>步驟 3：插入資料列  
  
在此範例中，您將了解如何安全地執行 [INSERT](../../t-sql/statements/insert-transact-sql.md) 陳述式，傳遞可協助您應用程式防禦 [SQL 插入](../../relational-databases/security/sql-injection.md)值的參數。    
  
  
```javascript  
    var Connection = require('tedious').Connection;  
    var config = {  
        server: 'your_server.database.windows.net',  //update me
        authentication: {
            type: 'default',
            options: {
                userName: 'your_username', //update me
                password: 'your_password'  //update me
            }
        },
        options: {
            // If you are on Microsoft Azure, you need encryption:
            encrypt: true,
            database: 'your_database'  //update me
        }
    };  
    var connection = new Connection(config);  
    connection.on('connect', function(err) {  
        // If no error, then good to proceed.  
        console.log("Connected");  
        executeStatement1();  
    });  
  
    var Request = require('tedious').Request  
    var TYPES = require('tedious').TYPES;  
  
    function executeStatement1() {  
        request = new Request("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES (@Name, @Number, @Cost, @Price, CURRENT_TIMESTAMP);", function(err) {  
         if (err) {  
            console.log(err);}  
        });  
        request.addParameter('Name', TYPES.NVarChar,'SQL Server Express 2014');  
        request.addParameter('Number', TYPES.NVarChar , 'SQLEXPRESS2014');  
        request.addParameter('Cost', TYPES.Int, 11);  
        request.addParameter('Price', TYPES.Int,11);  
        request.on('row', function(columns) {  
            columns.forEach(function(column) {  
              if (column.value === null) {  
                console.log('NULL');  
              } else {  
                console.log("Product id of inserted item is " + column.value);  
              }  
            });  
        });       
        connection.execSql(request);  
    }  
```  
