---
title: 步驟 3：使用 pyodbc 連線至 SQL
description: 步驟 3 是一個概念證明，說明如何使用 Python 和 pyODBC 連線至 SQL Server。 基本範例示範如何選取和插入資料。
ms.custom: ''
ms.date: 03/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26cbdea53547f30a59dc6953d7bf68bddc712164
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88807042"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>步驟 3：使用 pyodbc 連線到 SQL 的概念證明

此範例是概念證明。 為了清楚起見，已將範例程式碼簡化，而其不一定代表 Microsoft 建議的最佳做法。  

若要開始，請執行下列範例指令碼。 建立名為 test.py 的檔案，並在您進行時新增每個程式碼片段。 

```
> python test.py
```
  
## <a name="connect"></a>連線  
  
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
  
  
## <a name="run-query"></a>執行查詢  
  
cursor.executefunction 可用來擷取對 SQL Database 查詢的結果集。 此函式會接受查詢並傳回結果集，而您可以使用 cursor.fetchone() 反覆查詢結果集。
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print(row[0])
    row = cursor.fetchone()

```  
  
## <a name="insert-a-row"></a>插入資料列  
  
在此範例中，了解如何安全地執行 [INSERT](../../../t-sql/statements/insert-transact-sql.md) 陳述式，並傳遞參數。 該參數可協助應用程式防禦 [SQL 插入](../../../relational-databases/tables/primary-and-foreign-key-constraints.md)。    
  
  
```python
#Sample insert query
cursor.execute("""
INSERT INTO SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) 
VALUES (?,?,?,?,?)""",
'SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP) 
cnxn.commit()
row = cursor.fetchone()

while row: 
    print('Inserted Product key is ' + str(row[0]))
    row = cursor.fetchone()
```  

## <a name="azure-active-directory-and-the-connection-string"></a>Azure Active Directory 與連接字串

pyODBC 使用適用於 SQL Server 的 Microsoft ODBC 驅動程式。
如果您的 ODBC 驅動程式是 17.1 版或更新版本，您可以透過 pyODBC 使用 ODBC 驅動程式的 Azure Active Directory 互動式模式。
如果 Python 與 pyODBC 允許 ODBC 驅動程式顯示對話方塊，則此互動式選項適用。 只有 Windows 作業系統才提供此選項。 

### <a name="example-connection-string-for-azure-active-directory-interactive-authentication"></a>範例 Azure Active Directory 互動式驗證連接字串

下列範例提供指定 Azure Active Directory 互動式驗證的 ODBC 連接字串：

`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

如需有關 ODBC 驅動程式驗證選項的詳細資訊，請參閱[搭配 ODBC 驅動程式使用 Azure Active Directory](../../odbc/using-azure-active-directory.md#new-andor-modified-dsn-and-connection-string-keywords)。

## <a name="next-steps"></a>後續步驟
  
如需詳細資訊，請參閱 [Python 開發人員中心](https://azure.microsoft.com/develop/python/)。
