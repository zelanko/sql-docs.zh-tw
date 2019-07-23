---
title: 步驟 3︰使用 Ruby 連線到 SQL 的概念證明 | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992495"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>步驟 3︰使用 Ruby 連線到 SQL 的概念證明

這個範例應該僅視為概念證明。  為了清楚起見, 範例程式碼已簡化, 不一定代表 Microsoft 建議的最佳作法。  
  
## <a name="step-1--connect"></a>步驟 1: 連接  
  
[TinyTDS:: Client](https://github.com/rails-sqlserver/tiny_tds)函式是用來連接到 SQL Database。  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>步驟 2：執行查詢  
  
複製下列程式碼並貼到空白檔案中。 將它命名為 test. rb。 然後在命令提示字元中輸入下列命令來執行它:  
  
    ruby test.rb  
  
在程式碼範例中, [TinyTds:: Result](https://github.com/rails-sqlserver/tiny_tds)函數是用來根據 SQL Database 從查詢中取出結果集。 此函式會接受查詢並傳回結果集。 結果集會藉由使用 result 逐一查看[。每個 do | row |](https://github.com/rails-sqlserver/tiny_tds)。  
  
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
  
## <a name="step-3--insert-a-row"></a>步驟 3: 插入資料列  
  
在此範例中, 您將瞭解如何安全地執行[INSERT](../../t-sql/statements/insert-transact-sql.md)語句、傳遞可保護您的應用程式免于[SQL 插入](../../relational-databases/tables/primary-and-foreign-key-constraints.md)值的參數。    
  
若要搭配使用 TinyTDS 與 Azure, 建議您執行數個`SET`語句來變更目前會話處理特定資訊的方式。 建議`SET`的語句會在程式碼範例中提供。 例如, 即使`SET ANSI_NULL_DFLT_ON`未明確陳述資料行的 null 屬性狀態, 也會允許建立新的資料行, 以允許 null 值。  
  
若要與 Microsoft SQL Server[日期時間](../../t-sql/data-types/datetime-transact-sql.md)格式保持一致, 請使用[strftime](https://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime)函數轉換成對應的日期時間格式。  
  
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
