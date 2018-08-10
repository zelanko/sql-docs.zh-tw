---
title: MSSQL JDBC 驅動程式的批次插入作業中使用大量複製 API |Microsoft Docs
ms.custom: ''
ms.date: 07/27/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a62845e404024ae6d4d2aa8d30acef3f7ce233dd
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/02/2018
ms.locfileid: "39467766"
---
# <a name="using-bulk-copy-api-for-batch-insert-operation"></a>使用大量複製 API 執行批次插入作業

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

使用大量複製 API 的批次插入作業，Azure 資料倉儲的 SQL Server 支援的 Microsoft JDBC 驅動程式 7.0。 這項功能可讓使用者啟用驅動程式執行時執行的批次插入作業下的大量複製作業。 驅動程式目的是，為了改進效能，同時插入相同的資料，因為驅動程式會使用一般的批次插入作業。 驅動程式會剖析使用者的 SQL 查詢，利用大量複製 API 取代一般的批次插入作業。 以下是各種啟用批次的大量複製 API 插入功能，以及其限制的清單。 此頁面也包含小型示範程式碼範例使用方式和效能提升。

這項功能僅適用於 PreparedStatement 和 CallableStatement 的`executeBatch()`  &  `executeLargeBatch()` Api。

## <a name="pre-requisites"></a>必要條件

有兩個批次插入為啟用大量複製 API 的必要條件。

* 伺服器必須是 Azure 資料倉儲。
* 查詢必須是 insert 查詢 （查詢可能會包含註解，但是查詢必須以開始生效的這項功能的插入關鍵字開頭）。

## <a name="enabling-bulk-copy-api-for-batch-insert"></a>啟用批次插入大量複製 API

有三種方式可啟用大量複製 API 的批次插入。

### <a name="1-enabling-with-connection-property"></a>1.啟用搭配連接屬性

新增**useBulkCopyForBatchInsert = true;** 連接字串可讓這項功能。

```java
Connection connection = DriverManager.getConnection("jdbc:sqlserver://<server>:<port>;userName=<user>;password=<password>;database=<database>;useBulkCopyForBatchInsert=true;");
```

### <a name="2-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverconnection-object"></a>2.啟用搭配 SQLServerConnection 物件 setUseBulkCopyForBatchInsert() 方法

呼叫**SQLServerConnection.setUseBulkCopyForBatchInsert(true)** 啟用這項功能。

**SQLServerConnection.getUseBulkCopyForBatchInsert()** 擷取目前的值，如**useBulkCopyForBatchInsert**連接屬性。

值**useBulkCopyForBatchInsert**維持不變的每個 PreparedStatement 在其初始化階段。 任何後續呼叫**SQLServerConnection.setUseBulkCopyForBatchInsert()** 就不會影響已建立的 PreparedStatement 有關它的值。

### <a name="3-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverdatasource-object"></a>3.啟用使用 SQLServerDataSource 物件從 setUseBulkCopyForBatchInsert() 方法

與上述類似，但是使用 SQLServerDataSource 建立 SQLServerConnection 物件。 這兩種方法皆會獲得相同的結果。

## <a name="known-limitations"></a>已知限制

目前沒有這項功能適用於這些限制。

* 插入包含非參數化值的查詢 (例如`INSERT INTO TABLE VALUES (?, 2`))，不支援。 萬用字元 （？） 是唯一支援的參數，此函式。
* 插入包含 INSERT SELECT 運算式的查詢 (例如`INSERT INTO TABLE SELECT * FROM TABLE2`)，不支援。
* 插入包含多個值運算式的查詢 (例如`INSERT INTO TABLE VALUES (1, 2) (3, 4)`)，不支援。
* 插入查詢後面的 OPTION 子句中，加入多個資料表，或後面接著另一個查詢，不支援。
* 由於大量複製 API 的限制`DATETIME`， `SMALLDATETIME`，`GEOMETRY`，和`GEOGRAPHY`資料型別，不支援這項功能。

如果查詢失敗，因為非 「 SQL server 」 相關的錯誤，此驅動程式會以批次插入的原始邏輯記錄的錯誤訊息和後援。

## <a name="example"></a>範例

以下是示範批次插入作業針對 Azure DW 的一千個資料列，這兩個 （標準與大量複製 API） 案例的使用案例的範例程式碼。

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

[善 JDBC Driver 的效能與可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
