---
title: 針對 MSSQL JDBC Driver 使用大量複製 API 進行批次插入作業 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3050cdf87775a67618902dfbb88b656003020769
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027099"
---
# <a name="using-bulk-copy-api-for-batch-insert-operation"></a>使用大量複製 API 執行批次插入作業

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

適用于 SQL Server 的 Microsoft JDBC Driver 7.0 支援使用大量複製 API 來進行 Azure 資料倉儲的批次插入作業。 這項功能可讓使用者在執行批次插入作業時, 啟用驅動程式來執行大量複製操作。 此驅動程式的目的是要改善效能, 同時插入與驅動程式定期執行批次插入作業相同的資料。 驅動程式會剖析使用者的 SQL 查詢, 利用大量複製 API 代替一般的批次插入作業。 以下是啟用批次插入功能的大量複製 API, 以及其限制清單的各種方式。 此頁面也包含一個小範例程式碼, 示範用法和效能增加。

這項功能僅適用于 java.sql.preparedstatement 和 java.sql.callablestatement 的`executeBatch()`  &  `executeLargeBatch()` api。

## <a name="prerequisites"></a>Prerequisites

有兩個必要條件可啟用大量複製 API 以進行批次插入。

* 伺服器必須是 Azure 資料倉儲。
* 查詢必須是插入查詢 (查詢可能包含批註, 但查詢必須以 INSERT 關鍵字開頭, 此功能才會生效)。

## <a name="enabling-bulk-copy-api-for-batch-insert"></a>啟用大量複製 API 以進行批次插入

有三種方式可啟用大量複製 API 以進行批次插入。

### <a name="1-enabling-with-connection-property"></a>1.使用連接屬性啟用

將**useBulkCopyForBatchInsert = true;** 加入至連接字串會啟用這項功能。

```java
Connection connection = DriverManager.getConnection("jdbc:sqlserver://<server>:<port>;userName=<user>;password=<password>;database=<database>;useBulkCopyForBatchInsert=true;");
```

### <a name="2-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverconnection-object"></a>2.使用 SQLServerConnection 物件的 setUseBulkCopyForBatchInsert () 方法啟用

呼叫**SQLServerConnection. setUseBulkCopyForBatchInsert (true)** 可啟用這項功能。

**SQLServerConnection. getUseBulkCopyForBatchInsert ()** 會抓取**useBulkCopyForBatchInsert**連接屬性的目前值。

**UseBulkCopyForBatchInsert**的值在其初始化期間會針對每個 java.sql.preparedstatement 保持不變。 任何後續對 SQLServerConnection 的呼叫**setUseBulkCopyForBatchInsert ()** 都不會影響已建立的 java.sql.preparedstatement 與其值有關。

### <a name="3-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverdatasource-object"></a>3.使用 SQLServerDataSource 物件的 setUseBulkCopyForBatchInsert () 方法啟用

與上述類似, 但使用 SQLServerDataSource 來建立 SQLServerConnection 物件。 這兩種方法皆會獲得相同的結果。

## <a name="known-limitations"></a>已知限制

目前有適用于這項功能的限制。

* 不支援包含非參數化值的插入查詢 (例如`INSERT INTO TABLE VALUES (?, 2`,))。 萬用字元 (？) 是這個函數唯一支援的參數。
* 不支援包含插入選取運算式 (例如, `INSERT INTO TABLE SELECT * FROM TABLE2`) 的插入查詢。
* 不支援包含多個值運算式 (例如, `INSERT INTO TABLE VALUES (1, 2) (3, 4)`) 的插入查詢。
* 不支援將後面接著 OPTION 子句、與多個資料表聯結, 或後面接著另一個查詢的插入查詢。
* 由於大量複製`MONEY`API、 、`TIME`、 `DATE` `SMALLMONEY` `DATETIME`、 `DATETIMEOFFSET` 、、`GEOGRAPHY` 、、和資料類型的限制, 目前不支援此項`SMALLDATETIME` `GEOMETRY`特徵.

如果查詢因為非「SQL server」相關錯誤而失敗, 驅動程式將會記錄錯誤訊息, 並回溯至批次插入的原始邏輯。

## <a name="example"></a>範例

以下範例程式碼示範適用于數千個數據列之 Azure DW 的批次插入作業使用案例, 適用于 (一般 vs 大量複製 API) 案例。

```java
    public static void main(String[] args) throws Exception
    {
        String tableName = "batchTest";
        String tableNameBulkCopyAPI = "batchTestBulk";

        String azureDWconnectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(azureDWconnectionUrl); // connects to an Azure Data Warehouse.
                Statement stmt = con.createStatement();
                PreparedStatement pstmt = con.prepareStatement("insert into " + tableName + " values (?, ?)");) {

            String dropSql = "if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[" + tableName + "]') and OBJECTPROPERTY(id, N'IsUserTable') = 1) DROP TABLE [" + tableName + "]";
            stmt.execute(dropSql);

            String createSql = "create table " + tableName + " (c1 int, c2 varchar(20))";
            stmt.execute(createSql);

            System.out.println("Starting batch operation using regular batch insert operation.");
            long start = System.currentTimeMillis();
            for (int i = 0; i < 1000; i++) {
                pstmt.setInt(1, i);
                pstmt.setString(2, "test" + i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

            long end = System.currentTimeMillis();

            System.out.println("Finished. Time taken : " + (end - start) + " milliseconds.");
        }

        try (Connection con = DriverManager.getConnection(azureDWconnectionUrl + ";useBulkCopyForBatchInsert=true"); // connects to an Azure Data Warehouse, with useBulkCopyForBatchInsert connection property set to true.
                Statement stmt = con.createStatement();
                PreparedStatement pstmt = con.prepareStatement("insert into " + tableNameBulkCopyAPI + " values (?, ?)");) {

            String dropSql = "if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[" + tableNameBulkCopyAPI + "]') and OBJECTPROPERTY(id, N'IsUserTable') = 1) DROP TABLE [" + tableNameBulkCopyAPI + "]";
            stmt.execute(dropSql);

            String createSql = "create table " + tableNameBulkCopyAPI + " (c1 int, c2 varchar(20))";
            stmt.execute(createSql);

            System.out.println("Starting batch operation using Bulk Copy API.");
            long start = System.currentTimeMillis();
            for (int i = 0; i < 1000; i++) {
                pstmt.setInt(1, i);
                pstmt.setString(2, "test" + i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

            long end = System.currentTimeMillis();

            System.out.println("Finished. Time taken : " + (end - start) + " milliseconds.");
        }
    }
```

結果：

```bash
Starting batch operation using regular batch insert operation.
Finished. Time taken : 104132 milliseconds.
Starting batch operation using Bulk Copy API.
Finished. Time taken : 1058 milliseconds.
```

## <a name="see-also"></a>另請參閱

[改善JDBC 驅動程式的效能與可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
