---
title: 步驟 3︰使用 pymssql 連線到 SQL 的概念證明 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2246ddeb-7c2f-46f3-8a91-cdd718d39b40
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8ea4fa2527fa39700647832bdd1a194389cb36e4
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38982230"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>步驟 3︰使用 pymssql 連線到 SQL 的概念證明
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

此範例應該考慮只概念證明。  範例程式碼為了清楚起見，已簡化，並不一定代表 Microsoft 建議的最佳作法。  
  
## <a name="step-1--connect"></a>步驟 1： 連線  
  
[Pymssql.connect](http://pymssql.org/en/latest/ref/pymssql.html)函數用來連接到 SQL Database。  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>步驟 2： 執行查詢  
  
[Cursor.execute](http://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.execute)函式可以用來擷取結果集從查詢中，對 SQL Database。 此函式基本上會接受任何查詢，並傳回結果集，這可以藉由使用反覆[cursor.fetchone （)](http://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.fetchone)。  
  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute('SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC;')  
    row = cursor.fetchone()  
    while row:  
        print str(row[0]) + " " + str(row[1]) + " " + str(row[2])     
        row = cursor.fetchone()  
```  
  
## <a name="step-3--insert-a-row"></a>步驟 3： 插入資料列  
  
在您將了解如何執行此範例[插入](../../../t-sql/statements/insert-transact-sql.md)陳述式安全地傳遞可保護您的應用程式的參數[SQL 插入式攻擊](../../../relational-databases/tables/primary-and-foreign-key-constraints.md)值。    
  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express', 'SQLEXPRESS', 0, 0, CURRENT_TIMESTAMP)")  
    row = cursor.fetchone()  
    while row:  
        print "Inserted Product ID : " +str(row[0])  
        row = cursor.fetchone()  
    conn.commit()
    conn.close()
```  
  
## <a name="step-4--rollback-a-transaction"></a>步驟 4： 回復交易  
  
此程式碼範例示範如何使用交易，您：  
  
* 開始交易  
* 插入資料列  
* 復原您的交易以復原插入  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute("BEGIN TRANSACTION")  
    cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New', 'SQLEXPRESS New', 0, 0, CURRENT_TIMESTAMP)")  
    conn.rollback()  
    conn.close()
```  
    
  ## <a name="next-steps"></a>後續步驟  
  
如需詳細資訊，請參閱 < [Python 開發人員中心](https://azure.microsoft.com/develop/python/)。
