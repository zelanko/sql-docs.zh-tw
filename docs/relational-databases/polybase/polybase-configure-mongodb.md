---
title: 設定 PolyBase 存取 MongoDB 中的外部資料 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: a51842a1682b5e02db4ea216bddefbabbf0a7f56
ms.sourcegitcommit: 8dccf20d48e8db8fe136c4de6b0a0b408191586b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2018
ms.locfileid: "48874306"
---
# <a name="configure-polybase-to-access-external-data-in-mongodb"></a>設定 PolyBase 存取 MongoDB 中的外部資料

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何在 SQL Server 執行個體上使用 PolyBase 查詢位於 MongoDB 中的外部資料。

## <a name="prerequisites"></a>Prerequisites

如果您尚未安裝 PolyBase，請參閱 [PolyBase 安裝](polybase-installation.md)。 安裝文章說明必要條件。

## <a name="configure-an-external-table"></a>設定外部資料表

若要查詢來自 MongoDB 資料來源的資料，您必須建立外部資料表參考外部資料。 本節提供建立這些外部資料表的範例程式碼。

我們建議在外部資料表資料行上建立統計資料 (尤其是用於聯結、篩選和彙總的資料行)，以取得最佳查詢效能。

在本節中，會建立這些物件：

- CREATE DATABASE SCOPED CREDENTIAL (TRANSACT-SQL)
- CREATE EXTERNAL DATA SOURCE (Transact-SQL)
- CREATE EXTERNAL TABLE (Transact-SQL)
- CREATE STATISTICS (Transact-SQL)

1.    在資料庫上建立主要金鑰。 這是加密認證祕密的必要項目。

      ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
      ```

1.   建立資料庫範圍認證。

     ```sql
     /*  specify credentials to external data source
     *  IDENTITY: user name for external source.  
     *  SECRET: password for external source.
     */
     CREATE DATABASE SCOPED CREDENTIAL MongoDBCredentials 
     WITH IDENTITY = 'username', Secret = 'password';
     ```

1.  使用 [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)建立外部資料來源。 指定 MongoDB 資料來源的外部資料來源位置和認證。

     ```sql
     /*  LOCATION: Location string should be of format '<vendor>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE MongoInstance
    WITH (
    LOCATION = mongodb://MongoServer,
    -- PUSHDOWN = ON | OFF,
      CREDENTIAL = MongoDBCredentials
    );
     ```

1. 建立外部資料結構描述

     ```sql
     CREATE SCHEMA MongoDB;
     GO
     ```

1.  建立外部資料表，表示儲存在外部 MongoDB 系統的資料 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md)。

     ```sql
     /*  LOCATION: MongoDB table/view in '<database_name>.<schema_name>.<object_name>' format
     *  DATA_SOURCE: the external data source, created above.
     */
     CREATE EXTERNAL TABLE MongoDB.orders(
     [O_ORDERKEY] DECIMAL(38) NOT NULL,
     [O_CUSTKEY] DECIMAL(38) NOT NULL,
     [O_ORDERSTATUS] CHAR COLLATE Latin1_General_BIN NOT NULL,
     [O_TOTALPRICE] DECIMAL(15,2) NOT NULL,
     [O_ORDERDATE] DATETIME2(0) NOT NULL,
     [O_COMMENT] VARCHAR(79) COLLATE Latin1_General_BIN NOT NULL
     )
     WITH (
     LOCATION='TPCH..ORDERS',
     DATA_SOURCE= MongoDBInstance
     );
     ```

1. 在外部資料表上建立統計資料，以取得最佳效能。

     ```sql
      CREATE STATISTICS OrdersOrderKeyStatistics ON MongoDB.orders(O_ORDERKEY) WITH FULLSCAN;
     ```

## <a name="flattening"></a>壓平合併
 「壓平合併」用於來自 MongoDB 文件集合的巢狀及重複資料。 使用者必須啟用建立外部資料表，明確指定可能具有巢狀和/或重複資料的 MongoDB 文件集合關聯式結構描述。 我們會在未來的里程碑中針對 MongoDB 文件集合啟用自動結構描述偵測。
JSON 巢狀/重複資料類型會以下列方式壓平合併

* 物件：未排序索引鍵/值集合會包圍在大括弧中 (巢狀)

   - 我們會為每個物件機碼建立資料表資料行

     * 資料行名稱：objectname_keyname

* 陣列：排序值，以逗號分隔，並包圍在方括弧內 (重複)

   - 我們會為每個陣列項目新增新資料表資料列

   - 我們會為每個陣列建立資料行，以儲存陣列項目索引

     * 資料行名稱：arrayname_index

     * 資料類型：bigint

此技術有數個潛在問題，其中兩個是：

* 空白重複欄位會有效遮罩包含在相同記錄一般欄位中的資料

* 多個重複欄位可能會導致所產生資料列的數量暴增

例如，假設我們評估一個儲存在非關聯式 JSON 格式中的 MongoDB 範例資料集餐廳集合。 每間餐廳都有巢狀地址欄位，以及在不同天所獲指派的等級。 下圖說明具有巢狀地址和巢狀重複等級的典型餐廳。

![MongoDB 壓平合併](../../relational-databases/polybase/media/mongo-flattening.png "MongoDB 餐廳壓平合併")

物件地址會以下列順序壓平合併：

* 巢狀欄位 restaurant.address.building becomes restaurant.address_building
* 巢狀欄位 restaurant.address.coord becomes restaurant.address_coord
* 巢狀欄位 restaurant.address.street becomes restaurant.address_street
* 巢狀欄位 restaurant.address.zipcode becomes restaurant.address_zipcode

陣列等級會以下列順序壓平合併：
| grades_date | grades_grade  | games_score | 
| ------------- | ------------------------- | -------------- |
|1393804800000 |只有在次要複本設定成手動容錯移轉模式，而且至少一個次要複本目前與主要複本 SYNCHRONIZED 時， |2|
|1378857600000|只有在次要複本設定成手動容錯移轉模式，而且至少一個次要複本目前與主要複本 SYNCHRONIZED 時， |6|
|135898560000 |只有在次要複本設定成手動容錯移轉模式，而且至少一個次要複本目前與主要複本 SYNCHRONIZED 時， |10|
|1322006400000|只有在次要複本設定成手動容錯移轉模式，而且至少一個次要複本目前與主要複本 SYNCHRONIZED 時， |9|
|1299715200000 |B |14|

## <a name="next-steps"></a>後續步驟

若要深入了解 PolyBase，請參閱 [SQL Server PolyBase 概觀](polybase-guide.md)。
