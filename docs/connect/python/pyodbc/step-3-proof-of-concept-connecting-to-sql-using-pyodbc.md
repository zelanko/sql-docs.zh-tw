---
title: 步驟 3︰使用 pyodbc 連線到 SQL 的概念證明 | Microsoft Docs
ms.custom: ''
ms.date: 10/09/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0e241d84ebc60acceafe09b1a9240711a72d2067
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798324"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>步驟 3︰使用 pyodbc 連線到 SQL 的概念證明

這個範例應該僅視為概念證明。  為了清楚起見，範例程式碼已簡化，不一定代表 Microsoft 建議的最佳作法。  

**執行下列範例腳本** 建立名為 test.py 的檔案，並在您執行時新增每個程式碼片段。 

```
> python test.py
```
  
## <a name="step-1--connect"></a>步驟1：連接  
  
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
  
  
## <a name="step-2--execute-query"></a>步驟2：執行查詢  
  
Executefunction 可以用來從查詢針對 SQL Database 取出結果集。 此函式基本上會接受任何查詢並傳回結果集，而您可以使用 cursor.fetchone （）逐一查看它。
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print(row[0])
    row = cursor.fetchone()

```  
  
## <a name="step-3--insert-a-row"></a>步驟3：插入資料列  
  
在此範例中，您將瞭解如何安全地執行[INSERT](../../../t-sql/statements/insert-transact-sql.md)語句、傳遞可保護您的應用程式免于[SQL 插入](../../../relational-databases/tables/primary-and-foreign-key-constraints.md)值的參數。    
  
  
```python

#Sample insert query
cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP )") 
cnxn.commit()
row = cursor.fetchone()

while row: 
    print 'Inserted Product key is ' + str(row[0]) 
    row = cursor.fetchone()
```  

## <a name="azure-active-directory-aad-and-the-connection-string"></a>Azure Active Directory （AAD）和連接字串

pyODBC 使用適用於 SQL Server 的 Microsoft ODBC 驅動程式。
如果您的 ODBC 驅動程式版本是17.1 或更新版本，您可以透過 pyODBC 使用 ODBC 驅動程式的 AAD 互動模式。
如果 Python 和 pyODBC 允許 ODBC 驅動程式快顯對話方塊，則此 AAD 互動選項適用。
此選項僅適用于 Windows 作業系統。

### <a name="example-connection-string-for-aad-interactive-authentication"></a>AAD 互動式驗證的範例連接字串

以下是指定 AAD 互動式驗證的 ODBC 連接字串範例：

- `server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

如需 ODBC 驅動程式之 AAD 驗證選項的詳細資訊，請參閱下列文章：

- [搭配 ODBC 驅動程式使用 Azure Active Directory](../../odbc/using-azure-active-directory.md#new-andor-modified-dsn-and-connection-string-keywords)

## <a name="next-steps"></a>後續步驟
  
如需詳細資訊，請參閱[Python 開發人員中心](https://azure.microsoft.com/develop/python/)。
