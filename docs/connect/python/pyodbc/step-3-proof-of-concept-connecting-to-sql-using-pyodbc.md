---
title: "步驟 3： 連接到使用 pyodbc SQL 的概念證明 |Microsoft 文件"
ms.custom: 
ms.date: 08/08/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b71b6e4f40e4f1910d825071b8a0d86db4987624
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>步驟 3： 連接到使用 pyodbc SQL 的概念證明

此範例中，應該考量只概念證明。  範例程式碼為了清楚起見，已簡化，並不一定代表由 Microsoft 所建議的最佳作法。  

**執行下列的範例指令碼**建立一個叫做 test.py，檔案並加入每個程式碼片段，您隨時。 

```
> python test.py
```
  
## <a name="step-1--connect"></a>步驟 1： 連接  
  
```python

import pyodbc 
server = 'tcp:myserver.database.windows.net' 
database = 'mydb' 
username = 'myusername' 
password = 'mypassword' 
cnxn = pyodbc.connect('DRIVER={ODBC Driver 13 for SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()

```  
  
  
## <a name="step-2--execute-query"></a>步驟 2： 執行查詢  
  
Cursor.executefunction 可以用來擷取結果集的查詢，針對 SQL 資料庫。 此函式基本上會接受任何查詢，並傳回可逐一 cursor.fetchone() 使用的結果集
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print row[0] 
    row = cursor.fetchone()

```  
  
## <a name="step-3--insert-a-row"></a>步驟 3： 插入資料列  
  
在您將了解如何執行此範例[插入](https://msdn.microsoft.com/library/ms174335.aspx)陳述式，將參數可保護您的應用程式，從[SQL 資料隱碼](https://technet.microsoft.com/library/ms161953(v=sql.105).aspx)弱點和擷取自動產生的[主索引鍵](https://msdn.microsoft.com/library/ms179610.aspx)值。    
  
  
```python

#Sample insert query
cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP )") 
row = cursor.fetchone()

while row: 
    print 'Inserted Product key is ' + str(row[0]) 
    row = cursor.fetchone()
```  
  `      
  ## <a name="next-steps"></a>後續的步驟  
  
如需詳細資訊，請參閱[Python 開發人員中心](https://azure.microsoft.com/en-us/develop/python/)。
