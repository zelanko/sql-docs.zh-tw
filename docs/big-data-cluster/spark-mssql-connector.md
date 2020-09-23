---
title: 使用適用於 SQL Server 和 Azure SQL 的 Apache Spark 連接器
titleSuffix: SQL Server big data clusters
description: 了解如何使用適用於 SQL Server 和 Azure SQL 的 Apache Spark 連接器來讀取和寫入 SQL Server。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning-bdc
ms.openlocfilehash: 454d5fadaa88d645e9d1c2feec2c9d87c2af29c9
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645499"
---
# <a name="use-the-apache-spark-connector-for-sql-server-and-azure-sql"></a>使用適用於 SQL Server 和 Azure SQL 的 Apache Spark 連接器

[適用於 SQL Server 和 Azure SQL 的 Apache Spark 連接器](https://github.com/microsoft/sql-spark-connector) \(英文\) 是一種高效能連接器，可讓您在巨量資料分析中使用交易資料，並且保存結果以供臨機操作查詢或報告使用。 此連接器可讓您使用內部部署或雲端中的任何 SQL 資料庫，作為 Spark 作業的輸入資料來源或輸出資料接收器。 此連接器使用 SQL Server 大量寫入 API。 使用者可以以選擇性參數傳遞任何大量寫入參數，再由連接器依現狀將其傳遞至基礎 API。 如需有關大量寫入作業的詳細資訊，請參閱[搭配 JDBC 驅動程式使用大量複製]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions)。

此連接器預設包含在 SQL Server 巨量資料叢集中。

請在[開放原始碼存放庫](https://github.com/microsoft/sql-spark-connector) \(英文\) 中深入了解此連接器。 如需範例，請參閱[範例](https://github.com/microsoft/sql-spark-connector/tree/master/samples) \(英文\)。

## <a name="write-to-a-new-sql-table"></a>寫入新的 SQL 資料表

>[!CAUTION]
> 在 `overwrite` 模式下，如果資料表預設已存在於資料庫中，連接器會先加以卸除。 請謹慎使用此選項，以免發生非預期的資料遺失。
> 
> 使用 `overwrite` 模式時，如果您未使用 `truncate` 選項，在重新建立資料表時將會遺失索引。 例如，資料行存放區資料表會變成堆積。 如果您想要維護現有的索引，請同時指定 `truncate` 選項並將其值設定為 `true`。 例如 `.option("truncate",true)`

```python
server_name = "jdbc:sqlserver://{SERVER_ADDR}"
database_name = "database_name"
url = server_name + ";" + "databaseName=" + database_name + ";"

table_name = "table_name"
username = "username"
password = "password123!#" # Please specify password here

try:
  df.write \
    .format("com.microsoft.sqlserver.jdbc.spark") \
    .mode("overwrite") \
    .option("url", url) \
    .option("dbtable", table_name) \
    .option("user", username) \
    .option("password", password) \
    .save()
except ValueError as error :
    print("Connector write failed", error)
```

## <a name="append-to-sql-table"></a>附加至 SQL 資料表
```python
try:
  df.write \
    .format("com.microsoft.sqlserver.jdbc.spark") \
    .mode("append") \
    .option("url", url) \
    .option("dbtable", table_name) \
    .option("user", username) \
    .option("password", password) \
    .save()
except ValueError as error :
    print("Connector write failed", error)
```

## <a name="specify-the-isolation-level"></a>指定隔離等級

此連接器在對資料庫執行大量插入時，依預設會使用 READ_COMMITTED 隔離等級。 如果您想要將此設定覆寫為另一個隔離等級，請使用 `mssqlIsolationLevel` 選項，如下所示。
```python
    .option("mssqlIsolationLevel", "READ_UNCOMMITTED") \
```

## <a name="read-from-sql-table"></a>從 SQL 資料表讀取

```python
jdbcDF = spark.read \
        .format("com.microsoft.sqlserver.jdbc.spark") \
        .option("url", url) \
        .option("dbtable", table_name) \
        .option("user", username) \
        .option("password", password).load()
```

## <a name="non-active-directory-mode"></a>非 Active Directory 模式

在非 Active Directory 模式安全性中，每個使用者都有使用者名稱與密碼，在連接器具現化期間必須將這些使用者名稱和密碼提供為參數，以執行讀取和/或寫入。

非 Active Directory 模式的範例連接器具現化如下。 執行指令碼之前，請將 `?` 取代為您帳戶的值。

```python
# Note: '?' is a placeholder for a necessary user-specified value
connector_type = "com.microsoft.sqlserver.jdbc.spark" 

url = "jdbc:sqlserver://master-p-svc;databaseName=?;"
writer = df.write \ 
   .format(connector_type)\ 
   .mode("overwrite") 
   .option("url", url) \ 
   .option("user", ?) \ 
   .option("password",?) 
writer.save() 
```

## <a name="active-directory-mode"></a>Active Directory 模式

在 Active Directory 模式安全性中，使用者在產生金鑰表檔案之後，必須在連接器具現化期間提供 `principal` 和 `keytab` 作為參數。

在此模式中，驅動程式會將金鑰表檔案載入至個別的執行程式容器。 然後，執行程式會使用主體名稱和金鑰表來產生權杖，以用來建立用於讀取/寫入的 JDBC 連接器。

Active Directory 模式的連接器具現化範例如下。 執行指令碼之前，請將 `?` 取代為您帳戶的值。

```python
# Note: '?' is a placeholder for a necessary user-specified value
connector_type = "com.microsoft.sqlserver.jdbc.spark"

url = "jdbc:sqlserver://master-p-svc;databaseName=?;integratedSecurity=true;authenticationScheme=JavaKerberos;" 
writer = df.write \ 
   .format(connector_type)\ 
   .mode("overwrite") 
   .option("url", url) \ 
   .option("principal", ?) \ 
   .option("keytab", ?)   

writer.save() 
```

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[如何在 Kubernetes 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-guidance.md)

有 SQL Server 巨量資料叢集的意見反應或功能建議嗎？ [請在 SQL Server 巨量資料叢集意見反應中留言](https://aka.ms/sql-server-bdc-feedback)。
