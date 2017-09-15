---
title: "步驟 3： 連接到使用 Ruby SQL 的概念證明 |Microsoft 文件"
ms.custom: 
ms.date: 08/08/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cac20b18-0a6d-4243-bbda-a5d1b9476441
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 91659ce1d2946923480c1fc1a0bcf9a6a15094d8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>步驟 3： 連接到使用 Ruby SQL 的概念證明

此範例中，應該考量只概念證明。  範例程式碼為了清楚起見，已簡化，並不一定代表由 Microsoft 所建議的最佳作法。  
  
## <a name="step-1--connect"></a>步驟 1： 連接  
  
[TinyTDS::Client](https://github.com/rails-sqlserver/tiny_tds)函數用來連接到 SQL Database。  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>步驟 2： 執行查詢  
  
複製並貼入下列程式碼中的空檔案。 呼叫 test.rb。 然後執行命令提示字元輸入下列命令：  
  
    ruby test.rb  
  
在程式碼範例中， [TinyTds::Result](https://github.com/rails-sqlserver/tiny_tds)函式用來擷取結果集從查詢中，針對 SQL 資料庫。 此函式接受查詢，並傳回結果集。 逐一查看結果集使用[result.each 執行 | 資料列 |](https://github.com/rails-sqlserver/tiny_tds)。  
  
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
  
在您將了解如何執行此範例[插入](https://msdn.microsoft.com/library/ms174335.aspx)陳述式，將參數可保護您的應用程式，從[SQL 資料隱碼](https://technet.microsoft.com/library/ms161953(v=sql.105).aspx)弱點和擷取自動產生的[主索引鍵](https://msdn.microsoft.com/library/ms179610.aspx)值。    
  
若要搭配 Azure 使用 TinyTDS，建議您執行多個`SET`陳述式來變更目前工作階段處理的特定資訊的方式。 建議`SET`陳述式所提供的程式碼範例。 例如，`SET ANSI_NULL_DFLT_ON`會允許新的資料行允許 null 值，即使未明確指定資料行的 null 屬性狀態建立。  
  
若要配合 Microsoft SQL Server [datetime](http://msdn.microsoft.com/library/ms187819.aspx)格式化，請使用[strftime](http://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime)轉換成對應的日期時間格式的函式。  
  
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

