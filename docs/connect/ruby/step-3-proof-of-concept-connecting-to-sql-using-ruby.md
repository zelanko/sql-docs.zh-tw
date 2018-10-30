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
manager: craigg
ms.openlocfilehash: 9eed37349152b48ab49859b44cc23cb463d8541b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47801376"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>步驟 3︰使用 Ruby 連線到 SQL 的概念證明

此範例應該考慮只概念證明。  範例程式碼為了清楚起見，已簡化，並不一定代表 Microsoft 建議的最佳作法。  
  
## <a name="step-1--connect"></a>步驟 1： 連線  
  
[Tinytds:: Client](https://github.com/rails-sqlserver/tiny_tds)函數用來連接到 SQL Database。  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>步驟 2：執行查詢  
  
複製並貼上下列程式碼中的空白檔案。 稱它為 test.rb。 然後執行方法是從命令提示字元中輸入下列命令：  
  
    ruby test.rb  
  
在程式碼範例中， [tinytds:: Result](https://github.com/rails-sqlserver/tiny_tds)函式用來擷取結果集從查詢中，對 SQL Database。 此函數會接受查詢，並傳回結果集。 結果集會使用在逐一查看[result.each 執行 | 資料列 |](https://github.com/rails-sqlserver/tiny_tds)。  
  
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
  
## <a name="step-3--insert-a-row"></a>步驟 3： 插入資料列  
  
在您將了解如何執行此範例[插入](../../t-sql/statements/insert-transact-sql.md)陳述式安全地傳遞可保護您的應用程式的參數[SQL 插入式攻擊](../../relational-databases/tables/primary-and-foreign-key-constraints.md)值。    
  
若要搭配使用 TinyTDS 和 Azure，建議您執行多個`SET`陳述式來變更目前工作階段處理的特定資訊的方式。 建議`SET`陳述式所提供的程式碼範例。 比方說，`SET ANSI_NULL_DFLT_ON`可建立允許 null 值，即使未明確指定資料行的 null 屬性狀態的新資料行。  
  
Microsoft SQL Server 與對齊[datetime](../../t-sql/data-types/datetime-transact-sql.md)格式，請使用[strftime](http://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime)函式來轉換成對應的日期時間格式。  
  
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
