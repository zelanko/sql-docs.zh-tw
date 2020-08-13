---
title: 將 SQL 資料表的資料插入 Python pandas 資料框架
titleSuffix: SQL machine learning
description: 了解如何從 SQL 資料表讀取資料，並使用 Python 將資料插入 pandas 資料框架。
author: cawrites
ms.author: chadam
ms.date: 07/23/2020
ms.topic: how-to
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=azuresqldb-current||=sqlallproducts-allversions'
ms.openlocfilehash: a4f2c9c30c1655df531ca9b455ecfad3d9c75c7e
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247997"
---
# <a name="insert-data-from-a-sql-table-into-a-python-pandas-dataframe"></a>將 SQL 資料表的資料插入 Python pandas 資料框架
[!INCLUDE[sql-asdb-asdbmi-asa](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

本文描述如何使用 Python 中的 [pyodbc](../../connect/python/pyodbc/python-sql-driver-pyodbc.md) 套件，將 SQL 資料插入 [pandas](https://pandas.pydata.org/) 資料框架。 資料框架內所含資料列和資料行可用於進一步的資料探索。

## <a name="prerequisites"></a>必要條件

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
* SQL Server。 如需了解如何安裝，請參閱 [SQL Server for Windows](../../database-engine/install-windows/install-sql-server.md) 或 [SQL Server for Linux](../../linux/sql-server-linux-overview.md)。
::: moniker-end

::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"
* Azure SQL Database。 如需了解如何註冊，請參閱 [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
::: moniker-end

::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
* Azure SQL 受控執行個體。 如需了解如何註冊，請參閱 [Azure SQL 受控執行個體](https://docs.microsoft.com/azure/azure-sql/managed-instance/instance-create-quickstart)。

* 請參閱 [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md)，以了解如何將範例資料庫還原到 Azure SQL 受控執行個體。
::: moniker-end

* Azure Data Studio。 如需了解如何安裝，請參閱 [Azure Data Studio](../../azure-data-studio/what-is.md)。

* [還原範例資料庫](../../samples/adventureworks-install-configure.md)以取得本文中所使用的範例資料。

## <a name="verify-restored-database"></a>驗證還原的資料庫

您可透過查詢 **Person.CountryRegion** 資料表驗證還原的資料庫是否存在：

```sql
USE AdventureWorks;
SELECT * FROM Person.CountryRegion;
```

## <a name="install-python-packages"></a>安裝 Python 套件

[下載及安裝 Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md)。

安裝下列 Python 套件：
  * pyodbc
  * pandas

  若要安裝這些套件：

  1. 在 Azure Data Studio 筆記本中，選取 [管理套件]。
  2. 在 [管理套件] 窗格中，選取 [新增] 索引標籤。
  3. 針對每個下列套件，輸入套件名稱，按一下 [搜尋]，然後按一下 [安裝]。

## <a name="insert-data"></a>插入資料

使用下列指令碼來從 Person.CountryRegion 資料表選取資料，並插入資料框架。 編輯連接字串變數 'server'、'database'、'username' 和 'password' 以連線到 SQL。

建立新的筆記本：

1. 在 Azure Data Studio 中，選取 [檔案]，選取 [新增 Notebook]。
2. 在筆記本中，選取核心程序 [Python3]，選取 [+code]。
3. 將程式碼貼到筆記本中，選取 [全部執行]。

```python
import pyodbc
import pandas as pd
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'servername' 
database = 'AdventureWorks' 
username = 'yourusername' 
password = 'databasename'  
cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
# select 26 rows from SQL table to insert in dataframe.
query = "SELECT [CountryRegionCode], [Name] FROM Person.CountryRegion;"
df = pd.read_sql(query, cnxn)
print(df.head(26))
```

**輸出**

以上指令碼中 `print` 命令會顯示 `pandas` 資料框架 `df` 的資料列。

```text
CountryRegionCode                 Name
0                 AF          Afghanistan
1                 AL              Albania
2                 DZ              Algeria
3                 AS       American Samoa
4                 AD              Andorra
5                 AO               Angola
6                 AI             Anguilla
7                 AQ           Antarctica
8                 AG  Antigua and Barbuda
9                 AR            Argentina
10                AM              Armenia
11                AW                Aruba
12                AU            Australia
13                AT              Austria
14                AZ           Azerbaijan
15                BS         Bahamas, The
16                BH              Bahrain
17                BD           Bangladesh
18                BB             Barbados
19                BY              Belarus
20                BE              Belgium
21                BZ               Belize
22                BJ                Benin
23                BM              Bermuda
24                BT               Bhutan
25                BO              Bolivia
```

## <a name="next-steps"></a>後續步驟

+ [將 Python 資料框架插入 SQL](../data-exploration/python-dataframe-sql-server.md)
