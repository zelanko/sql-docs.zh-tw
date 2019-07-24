---
title: 步驟 3︰使用 pymssql 連線到 SQL 的概念證明 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2246ddeb-7c2f-46f3-8a91-cdd718d39b40
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27b56a20a0456bef04553c614432bde270d8e98d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935778"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>步驟 3︰使用 pymssql 連線到 SQL 的概念證明
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

這個範例應該僅視為概念證明。  為了清楚起見, 範例程式碼已簡化, 不一定代表 Microsoft 建議的最佳作法。  
  
## <a name="step-1--connect"></a>步驟 1: 連接  
  
[Pymssql](https://pymssql.org/en/latest/ref/pymssql.html)函數是用來連接到 SQL Database。  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>步驟 2: 執行查詢  
  
您可以使用[cursor. execute](https://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.execute)函數, 從查詢針對 SQL Database 取出結果集。 此函式基本上會接受任何查詢並傳回結果集, 而您可以使用[cursor.fetchone ()](https://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.fetchone)來反復查看它。  
  
  
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
  
## <a name="step-3--insert-a-row"></a>步驟 3: 插入資料列  
  
在此範例中, 您將瞭解如何安全地執行[INSERT](../../../t-sql/statements/insert-transact-sql.md)語句、傳遞可保護您的應用程式免于[SQL 插入](../../../relational-databases/tables/primary-and-foreign-key-constraints.md)值的參數。    
  
  
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
  
## <a name="step-4--rollback-a-transaction"></a>步驟 4: 復原交易  
  
這個程式碼範例會示範交易的使用方式, 您可以在其中:  
  
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
  
如需詳細資訊, 請參閱[Python 開發人員中心](https://azure.microsoft.com/develop/python/)。
