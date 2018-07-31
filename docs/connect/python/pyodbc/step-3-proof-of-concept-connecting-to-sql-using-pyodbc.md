---
title: 步驟 3︰使用 pyodbc 連線到 SQL 的概念證明 | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3fa70619208df8940ec10a1b5a0f46704ce9c43
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979974"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>步驟 3︰使用 pyodbc 連線到 SQL 的概念證明

此範例應該考慮只概念證明。  範例程式碼為了清楚起見，已簡化，並不一定代表 Microsoft 建議的最佳作法。  

**執行下列的範例指令碼**建立稱為 test.py，檔案，並新增您沿用的每個程式碼片段。 

```
> python test.py
```
  
## <a name="step-1--connect"></a>步驟 1： 連線  
  
```python

import pyodbc 
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'tcp:myserver.database.windows.net' 
database = 'mydb' 
username = 'myusername' 
password = 'mypassword' 
cnxn = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()

```  
  
  
## <a name="step-2--execute-query"></a>步驟 2： 執行查詢  
  
Cursor.executefunction 可用來擷取對 SQL Database 中設定 從查詢的結果。 此函式基本上會接受任何查詢，並傳回結果集，其中可以反覆使用的 cursor.fetchone （）
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print row[0] 
    row = cursor.fetchone()

```  
  
## <a name="step-3--insert-a-row"></a>步驟 3： 插入資料列  
  
在您將了解如何執行此範例[插入](../../../t-sql/statements/insert-transact-sql.md)陳述式安全地傳遞可保護您的應用程式的參數[SQL 插入式攻擊](../../../relational-databases/tables/primary-and-foreign-key-constraints.md)值。    
  
  
```python

#Sample insert query
cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP )") 
row = cursor.fetchone()

while row: 
    print 'Inserted Product key is ' + str(row[0]) 
    row = cursor.fetchone()
```  
  `      
  ## <a name="next-steps"></a>後續步驟  
  
如需詳細資訊，請參閱 < [Python 開發人員中心](https://azure.microsoft.com/develop/python/)。
