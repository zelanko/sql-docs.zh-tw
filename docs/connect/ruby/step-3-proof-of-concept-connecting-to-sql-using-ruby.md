---
title: 步驟 3：使用 Ruby 連線到 SQL 的概念證明 | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cac20b18-0a6d-4243-bbda-a5d1b9476441
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9724fb48f6ae896d9026bfec63056070e2180a8e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67992495"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>步驟 3：使用 Ruby 連線到 SQL 的概念證明

這個範例只應被視為概念證明。  為了清楚起見，已將範例程式碼簡化，而其不一定代表 Microsoft 建議的最佳做法。  
  
## <a name="step-1--connect"></a>步驟 1:連線  
  
[TinyTDS::Client](https://github.com/rails-sqlserver/tiny_tds) 函式可用來連接到 SQL Database。  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>步驟 2:執行查詢  
  
複製以下程式碼並貼到空白檔案中。 稱它為 test.rb。 然後執行它，方法是從命令提示字元輸入下列命令：  
  
    ruby test.rb  
  
在程式碼範例中， [TinyTds::Result](https://github.com/rails-sqlserver/tiny_tds) 函數可用來從針對 SQL Database 的查詢擷取結果集。 此函數會接受查詢，並傳回結果集。 結果集可使用 [result.each do |row|](https://github.com/rails-sqlserver/tiny_tds)重複列舉。  
  
``` ruby 
    require 'tiny_tds'    
    print 'test'       
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
    results = client.execute("SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC")  
    results.each do |row|  
    puts row  
    end  
```  
  
## <a name="step-3--insert-a-row"></a>步驟 3：插入資料列  
  
在這個範例中，您將了解如何安全地執行 [INSERT](../../t-sql/statements/insert-transact-sql.md) 陳述式，傳遞可保護您應用程式來防禦 [SQL 插入](../../relational-databases/tables/primary-and-foreign-key-constraints.md)值的參數。    
  
若要搭配使用 TinyTDS 和 Azure，建議您執行多個 `SET` 陳述式來變更目前工作階段處理特定資訊的方式。 建議使用程式碼範例中所提供的 `SET` 陳述式。 例如，即使未明確陳述資料行的可為 null 狀態， `SET ANSI_NULL_DFLT_ON` 也可讓新建立的資料行允許 null 值。  
  
為了與 Microsoft SQL Server [日期時間](../../t-sql/data-types/datetime-transact-sql.md)格式一致，請使用 [strftime](https://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime) 函式來轉換成對應的日期時間格式。  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
    results = client.execute("SET ANSI_NULLS ON")  
    results = client.execute("SET CURSOR_CLOSE_ON_COMMIT OFF")  
    results = client.execute("SET ANSI_NULL_DFLT_ON ON")  
    results = client.execute("SET IMPLICIT_TRANSACTIONS OFF")  
    results = client.execute("SET ANSI_PADDING ON")  
    results = client.execute("SET QUOTED_IDENTIFIER ON")  
    results = client.execute("SET ANSI_WARNINGS ON")  
    results = client.execute("SET CONCAT_NULL_YIELDS_NULL ON")  
    require 'date'  
    t = Time.now  
    curr_date = t.strftime("%Y-%m-%d %H:%M:%S.%L")  
    results = client.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate)  
    OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New', 'SQLEXPRESS New', 0, 0, '#{curr_date}' )")  
    results.each do |row|  
    puts row  
    end  
```
