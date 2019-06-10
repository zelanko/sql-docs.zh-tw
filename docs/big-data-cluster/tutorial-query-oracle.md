---
title: 在 Oracle 中的查詢外部資料
titleSuffix: SQL Server big data clusters
description: 本教學課程會示範如何查詢 SQL Server 2019 巨量資料叢集 （預覽） 中的 Oracle 資料。 您會在 Oracle 中的資料建立外部資料表，然後再執行查詢。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 12/12/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 036118c3c5620b9685a9971b1aa8c22bdb2b6b9b
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66770788"
---
# <a name="tutorial-query-oracle-from-a-sql-server-big-data-cluster"></a>教學課程：從 SQL Server 的巨量資料叢集查詢 Oracle

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本教學課程會示範如何查詢 SQL Server 2019 巨量資料叢集從 Oracle 資料。 若要執行本教學課程中，您必須擁有 Oracle 伺服器的存取權。 如果您無法存取，本教學課程可讓您了解在 SQL Server 的巨量資料叢集的外部資料來源的資料虛擬化的運作方式。

在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 外部的 Oracle 資料庫中建立外部資料表的資料。
> * 在主要執行個體中加入此資料與高價值的資料。

> [!TIP]
> 如果您想，您可以下載並執行命令的指令碼，在本教學課程。 如需相關指示，請參閱 <<c0> [ 資料虛擬化範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization)GitHub 上。

## <a id="prereqs"></a> 必要條件

- [巨量資料工具](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
- [將範例資料載入您的巨量資料叢集](tutorial-load-sample-data.md)

## <a name="create-an-oracle-table"></a>建立 Oracle 資料表

下列步驟會建立名為的範例資料表`INVENTORY`在 Oracle 中。

1. 連接到 Oracle 執行個體和您想要用於本教學課程中的資料庫。

1. 執行下列陳述式來建立`INVENTORY`資料表：

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

1. 匯入的內容**inventory.csv**插入此資料表的檔案。 建立此檔案中的範例建立指令碼[必要條件](#prereqs)一節。

## <a name="create-an-external-data-source"></a>建立外部資料來源

第一個步驟是建立可存取您的 Oracle 伺服器的外部資料來源。

1. 在 Azure Data Studio，連接到您的巨量資料叢集的 SQL Server 主要執行個體。 如需詳細資訊，請參閱 <<c0> [ 連接到 SQL Server 的主要執行個體](connect-to-big-data-cluster.md#master)。

1. 在連線 中按兩下**伺服器**視窗以顯示 SQL Server 的主要執行個體的伺服器儀表板。 選取 **新的查詢**。

   ![SQL Server 的主要執行個體查詢](./media/tutorial-query-oracle/sql-server-master-instance-query.png)

1. 執行下列 TRANSACT-SQL 命令，以將內容變更為**銷售**主要執行個體中的資料庫。

   ```sql
   USE Sales
   GO
   ```

1. 建立資料庫範圍認證以連接到 Oracle 伺服器。 提供適當的認證，以您在下列陳述式中的 Oracle 伺服器。

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

接下來，建立名為外部資料表**iventory_ora**透過`INVENTORY`Oracle 伺服器上的資料表。

```sql
CREATE EXTERNAL TABLE [inventory_ora]
    ([inv_date] DECIMAL(10,0) NOT NULL, [inv_item] DECIMAL(10,0) NOT NULL,
    [inv_warehouse] DECIMAL(10,0) NOT NULL, [inv_quantity_on_hand] DECIMAL(10,0))
WITH (DATA_SOURCE=[OracleSalesSrvr],
        LOCATION='<oracle_service_name,nvarchar(30),xe>.<oracle_schema,nvarchar(128),HR>.<oracle_table,nvarchar(128),INVENTORY>');
```

> [!NOTE]
> 資料表名稱和資料行名稱會使用引號識別項，針對 Oracle 查詢時的 ANSI SQL。 如此一來，名稱會區分大小寫。 請務必符合中 Oracle 中繼資料的資料表和資料行名稱的大小寫完全相符的外部資料表定義中指定的名稱。

## <a name="query-the-data"></a>查詢資料

執行下列查詢來加入資料`iventory_ora`本機資料表的外部資料表`Sales`資料庫。

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

您可以使用下列命令，移除在本教學課程中建立的資料庫物件。

```sql
DROP EXTERNAL TABLE [inventory_ora];
DROP EXTERNAL DATA SOURCE [OracleSalesSrvr] ;
DROP DATABASE SCOPED CREDENTIAL [OracleCredential];
```

## <a name="next-steps"></a>後續步驟

了解如何將資料內嵌到資料集區：
> [!div class="nextstepaction"]
> [將資料載入資料集區](tutorial-data-pool-ingest-sql.md)
