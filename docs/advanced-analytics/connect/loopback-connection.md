---
title: 從 Python 或 R 腳本對 SQL Server 的回送連接
description: 瞭解如何使用回送連接, 透過 ODBC 連接回到 SQL Server, 以從 sp_execute_external_script 執行的 Python 或 R 腳本讀取或寫入資料。 當您無法使用 sp_execute_external_script 的 InputDataSet 和 OutputDataSet 引數時, 可以使用此參數。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/21/2019
ms.topic: conceptual
author: Aniruddh25
ms.author: anmunde
ms.reviewer: dphansen
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 62b4ce483df2d38e5e2549d054c02b6c797837f3
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69657485"
---
# <a name="loopback-connection-to-sql-server-from-a-python-or-r-script"></a>從 Python 或 R 腳本對 SQL Server 的回送連接
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

瞭解如何使用回送連接, 透過[ODBC](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)連接回 SQL Server, 以從執行`sp_execute_external_script`的 Python 或 R 腳本讀取或寫入資料。 當您不能使用的**InputDataSet**和**OutputDataSet**引數時`sp_execute_external_script` , 可以使用此參數。

## <a name="connection-string"></a>連接字串

若要建立回送連接, 您必須使用正確的連接字串。 一般的強制引數是[ODBC 驅動程式](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)的名稱、伺服器位址, 以及資料庫的名稱。

### <a name="connection-string-on-windows"></a>Windows 上的連接字串

若要在 Windows 上 SQL Server 上進行驗證, Python 或 R 腳本可以使用**Trusted_Connection**連接字串屬性, 以執行 sp_execute_external_script 的相同使用者身分進行驗證。

以下是 Windows 上的回送連接字串範例:

``` 
"Driver=SQL Server;Server=.;Database=nameOfDatabase;Trusted_Connection=Yes;"
```

### <a name="connection-string-on-linux"></a>Linux 上的連接字串

若要在 Linux 上的 SQL Server 上進行驗證, Python 或 R 腳本必須使用 ODBC 驅動程式的**ClientCertificate**和**ClientKey**屬性, 以執行`sp_execute_external_script`的相同使用者身分進行驗證。 這需要使用[最新的 ODBC 驅動程式](../../connect/odbc/download-odbc-driver-for-sql-server.md)版本17.4.1.1。

以下是 Linux 上的回送連接字串範例:

```
"Driver=ODBC Driver 17 for SQL Server;Server=fe80::8012:3df5:0:5db1%eth0;Database=nameOfDatabase;ClientCertificate=file:/var/opt/mssql-extensibility/data/baeaac72-60b3-4fae-acfd-c50eff5d34a2/sqlsatellitecert.pem;ClientKey=file:/var/opt/mssql-extensibility/data/baeaac72-60b3-4fae-acfd-c50eff5d34a2/sqlsatellitekey.pem;TrustServerCertificate=Yes;Trusted_Connection=no;Encrypt=Yes"
```

伺服器位址、用戶端憑證檔案位置和用戶端金鑰檔案位置對每個`sp_execute_external_script`都是唯一的, 而且可以透過使用適用于 Python 的 API **rx_get_sql_loopback_connection_string ()** 取得, 或適用于 R 的 rxGetSqlLoopbackConnectionString ()。

如需連接字串屬性的詳細資訊, 請參閱 Microsoft ODBC Driver for SQL Server 的[DSN 和連接字串關鍵字和屬性](https://docs.microsoft.com/sql/connect/odbc/dsn-connection-string-attribute?view=sql-server-linux-ver15#new-connection-string-keywords-and-connection-attributes)。

## <a name="generate-connection-string-with-revoscalepy-for-python"></a>使用適用于 Python 的 revoscalepy 產生連接字串

您可以使用[revoscalepy](../python/ref-py-revoscalepy.md)中的 API **rx_get_sql_loopback_connection_string ()** , 為 Python 腳本中的回送連接產生正確的連接字串。

它接受下列引數:

| 引數 | 描述 |
|-|-|
| name_of_database | 要建立連接的資料庫名稱 |
| odbc_driver | Odbc 驅動程式的名稱 |

### <a name="examples"></a>範例

Windows 上 SQL Server 的範例:

```sql
EXECUTE sp_execute_external_script
@language = N'Python',
@script = N'
from revoscalepy import rx_get_sql_loopback_connection_string, RxSqlServerData, rx_data_step
loopback_connection_string = rx_get_sql_loopback_connection_string(odbc_driver="SQL Server", name_of_database="DBName")
print("Connection String:{0}".format(loopback_connection_string))
data_set = RxSqlServerData(sql_query = "select col1, col2 from tableName",
                           connection_string = loopback_connection_string)
OutputDataSet = rx_data_step(data_set)
'
WITH RESULT SETS ((col1 int, col2 int))
GO
```

Linux 上的 SQL Server 的範例:

```sql
EXECUTE sp_execute_external_script
@language = N'Python',
@script = N'
from revoscalepy import rx_get_sql_loopback_connection_string, RxSqlServerData, rx_data_step
loopback_connection_string = rx_get_sql_loopback_connection_string(odbc_driver="ODBC Driver 17 for SQL Server",
                                                                   name_of_database="DBName")
print("Loopback Connection String:{0}".format(loopback_connection_string))
data_set = RxSqlServerData(sql_query = "select col1, col2 from tableName",
                           connection_string = loopback_connection_string)
OutputDataSet = rx_data_step(data_set)
'
WITH RESULT SETS ((col1 int, col2 int))
GO
```

## <a name="generate-connection-string-with-revoscaler-for-r"></a>使用適用于 R 的 RevoScaleR 產生連接字串

您可以使用[RevoScaleR](../r/ref-r-revoscaler.md)中的 API **rxGetSqlLoopbackConnectionString ()** , 針對 R 腳本中的回送連接產生正確的連接字串。

它接受下列引數:

| 引數 | 描述 |
|-|-|
| nameOfDatabase | 要建立連接的資料庫名稱 |
| odbcDriver | Odbc 驅動程式的名稱 |

### <a name="examples"></a>範例

Windows 上 SQL Server 的範例:

```sql
EXECUTE sp_execute_external_script
@language = N'R',
@script = N'
    loopbackConnectionString <- rxGetSqlLoopbackConnectionString(nameOfDatabase="DBName", odbcDriver ="SQL Server")
    print(paste("Connection String:", loopbackConnectionString))
    dataSet <- RxSqlServerData(sqlQuery = "select col1, col2 from tableName",
                               connectionString = loopbackConnectionString)
    OutputDataSet <- rxDataStep(dataSet)
'
WITH RESULT SETS ((col1 int, col2 int))
GO
```

Linux 上的 SQL Server 的範例:

```sql
EXECUTE sp_execute_external_script
@language = N'R',
@script = N'
    loopbackConnectionString <-  rxGetSqlLoopbackConnectionString(nameOfDatabase="DBName", 
                                                                  odbcDriver ="ODBC Driver 17 for SQL Server")
    print(paste("Connection String:", loopbackConnectionString))
    dataSet <- RxSqlServerData(sqlQuery = "select col1, col2 from tableName", 
                               connectionString = loopbackConnectionString)
    OutputDataSet <- rxDataStep(dataSet)
'
WITH RESULT SETS ((col1 int, col2 int))
GO
```

## <a name="next-steps"></a>後續步驟

+ [適用于 SQL Server 的 Microsoft ODBC 驅動程式](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)
+ [revoscalepy](../python/ref-py-revoscalepy.md)
+ [RevoScaleR](../r/ref-r-revoscaler.md)
