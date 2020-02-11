---
title: 查詢 Oracle 中的外部資料
titleSuffix: SQL Server big data clusters
description: 本教學課程示範如何從 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]查詢 Oracle 資料。 您會透過 Oracle 中的資料建立外部資料表，然後執行查詢。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b880e3758481e5b061221bd2753b5a26f01ed856
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "71708360"
---
# <a name="tutorial-query-oracle-from-a-sql-server-big-data-cluster"></a>教學課程：查詢 SQL Server 巨量資料叢集中的 Oracle

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本教學課程示範如何查詢 SQL Server 2019 巨量資料叢集中的 Oracle 資料。 若要執行本教學課程，您要能夠存取 Oracle 伺服器。 如果您無法存取，本教學課程可讓您了解 SQL Server 巨量資料叢集中，外部資料來源的資料虛擬化運作方式。

在本教學課程中，您會了解如何：

> [!div class="checklist"]
> * 為外部 Oracle 資料庫中的資料建立外部資料表。
> * 將此資料與主要執行個體中的高價值資料聯結。

> [!TIP]
> 如果您想要的話，也可以下載並執行用於本教學課程中命令的指令碼。 如需指示，請參閱 GitHub 上的[資料虛擬化範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization)。

## <a id="prereqs"></a> 必要條件

- [巨量資料工具](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
- [將範例資料載入巨量資料叢集](tutorial-load-sample-data.md)

## <a name="create-an-oracle-table"></a>建立 Oracle 資料表

下列步驟會在 Oracle 中建立名為 `INVENTORY` 的範例資料表。

1. 連線到您要用於本教學課程的 Oracle 執行個體和資料庫。

1. 執行下列陳述式，建立 `INVENTORY` 資料表：

   ```sql
    CREATE TABLE "INVENTORY"
    (
        "INV_DATE" NUMBER(10,0) NOT NULL,
        "INV_ITEM" NUMBER(10,0) NOT NULL,
        "INV_WAREHOUSE" NUMBER(10,0) NOT NULL,
        "INV_QUANTITY_ON_HAND" NUMBER(10,0)
    );

    CREATE INDEX INV_ITEM ON HR.INVENTORY(INV_ITEM);
    ```

1. 將 **inventory.csv** 檔案的內容匯入此資料表。 此檔案是由[必要條件](#prereqs)一節中的範例建立指令碼所建立。

## <a name="create-an-external-data-source"></a>建立外部資料來源

第一個步驟是建立可存取 Oracle 伺服器的外部資料來源。

1. 在 Azure Data Studio 中，連線到巨量資料叢集的 SQL Server 主要執行個體。 如需詳細資訊，請參閱[連線到 SQL Server 主要執行個體](connect-to-big-data-cluster.md#master)。

1. 按兩下 [伺服器]  視窗中的連線，顯示 SQL Server 主要執行個體的伺服器儀表板。 選取 [新增查詢]  。

   ![SQL Server 主要執行個體查詢](./media/tutorial-query-oracle/sql-server-master-instance-query.png)

1. 執行下列 Transact-SQL 命令，將內容變更為主要執行個體中的 **Sales** 資料庫。

   ```sql
   USE Sales
   GO
   ```

1. 建立資料庫範圍認證以連線到 Oracle 伺服器。 在下列陳述式中，為您的 Oracle 伺服器提供適當的認證。

   ```sql
   CREATE DATABASE SCOPED CREDENTIAL [OracleCredential]
   WITH IDENTITY = '<oracle_user,nvarchar(100),SYSTEM>', SECRET = '<oracle_user_password,nvarchar(100),manager>';
   ```

1. 建立指向 Oracle 伺服器的外部資料來源。

   ```sql
   CREATE EXTERNAL DATA SOURCE [OracleSalesSrvr]
   WITH (LOCATION = 'oracle://<oracle_server,nvarchar(100)>',CREDENTIAL = [OracleCredential]);
   ```

## <a name="create-an-external-table"></a>建立外部資料表

接下來，透過 Oracle 伺服器上的 `INVENTORY` 資料表，建立名為 **iventory_ora** 的外部資料表。

```sql
CREATE EXTERNAL TABLE [inventory_ora]
    ([inv_date] DECIMAL(10,0) NOT NULL, [inv_item] DECIMAL(10,0) NOT NULL,
    [inv_warehouse] DECIMAL(10,0) NOT NULL, [inv_quantity_on_hand] DECIMAL(10,0))
WITH (DATA_SOURCE=[OracleSalesSrvr],
        LOCATION='<oracle_service_name,nvarchar(30),xe>.<oracle_schema,nvarchar(128),HR>.<oracle_table,nvarchar(128),INVENTORY>');
```

> [!NOTE]
> 查詢 Oracle 時，資料表名稱和資料行名稱會使用 ANSI SQL 引號識別項。 因此，名稱會區分大小寫。 在外部資料表定義中指定名稱時，請務必完全符合 Oracle 中繼資料中的資料表和資料行名稱大小寫。

## <a name="query-the-data"></a>查詢資料

執行下列查詢，將 `iventory_ora` 外部資料表中的資料與本機 `Sales` 資料庫中的資料表聯結。

```sql
SELECT TOP(100) w.w_warehouse_name, i.inv_item, SUM(i.inv_quantity_on_hand) as total_quantity
  FROM [inventory_ora] as i
  JOIN item as it
    ON it.i_item_sk = i.inv_item
  JOIN warehouse as w
    ON w.w_warehouse_sk = i.inv_warehouse
 WHERE it.i_category = 'Books' and i.inv_item BETWEEN 1 and 18000 --> get items within specific range
 GROUP BY w.w_warehouse_name, i.inv_item;
```

## <a name="clean-up"></a>清除

使用下列命令，移除本教學課程所建立的資料庫物件。

```sql
DROP EXTERNAL TABLE [inventory_ora];
DROP EXTERNAL DATA SOURCE [OracleSalesSrvr] ;
DROP DATABASE SCOPED CREDENTIAL [OracleCredential];
```

## <a name="next-steps"></a>後續步驟

了解如何將資料內嵌至資料集區：
> [!div class="nextstepaction"]
> [將資料載入資料集區](tutorial-data-pool-ingest-sql.md)
