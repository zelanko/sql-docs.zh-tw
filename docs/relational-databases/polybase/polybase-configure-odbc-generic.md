---
title: 存取外部資料：ODBC 泛型型別 - PolyBase
ms.date: 12/13/2019
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 5017dc54a1e7858786413b2fcc164e4949f77646
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "75255416"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>設定 PolyBase 存取 SQL Server 中的外部資料

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 2019 中的 PolyBase 可讓您透過 ODBC 連接器連接到 ODBC 相容的資料來源。 

## <a name="prerequisites"></a>Prerequisites

注意 = 此功能僅適合 Windows 上的 SQL Server。 

如果您尚未安裝 PolyBase，請參閱 [PolyBase 安裝](polybase-installation.md)。

 在建立資料庫範圍認證之前，必須建立[主要金鑰](../../t-sql/statements/create-master-key-transact-sql.md)。 

請先針對您要在每個 PolyBase 節點上連接的資料來源，下載並安裝其 ODBC 驅動程式。 一旦正確安裝驅動程式，您就可以從 [ODBC 資料來源管理員] 檢視及測試驅動程式。

![PolyBase 向外延展群組](../../relational-databases/polybase/media/polybase-odbc-admin.png) 

> **重要！**
> 
> 為了提高查詢效能，請確保驅動程式已啟用連線共用。 這可透過 [ODBC 資料來源管理員] 來完成。
> 
> **注意**
> 
> 建立外部資料來源時 (下方步驟 3)，必須指定驅動程式的名稱 (上圖圈選範例)。

## <a name="create-an-external-table"></a>建立外部資料表

若要查詢來自 ODBC 資料來源的資料，您必須建立外部資料表以便參考外部資料。 本節提供建立外部資料表的範例程式碼。

本節中使用下列 Transact-SQL 命令：

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. 建立資料庫範圍認證以存取 ODBC 來源。

    ```sql
    /*  specify credentials to external data source
    *  IDENTITY: user name for external source. 
    *  SECRET: password for external source.
    */
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'password';
    ```

1. 使用 [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) 建立外部資料來源。

    ```sql
    /*  LOCATION: Location string should be of format '<type>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( LOCATION = odbc://<ODBC server address>[:<port>],
    CONNECTION_OPTIONS = 'Driver={<Name of Installed Driver>};
    ServerNode = <name of server  address>:<Port>',
    -- PUSHDOWN = ON | OFF,
    CREDENTIAL = credential_nam );
    ```

1. **選擇性：** 在外部資料表上建立統計資料。

為了取得最佳查詢效能，我們建議在外部資料表資料行上建立統計資料 (尤其是用於聯結、篩選和彙總的資料行)。

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
    ```

>[!IMPORTANT] 
>當您建立外部資料來源之後，可以使用 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 命令透過該來源建立可查詢的資料表。 

## <a name="next-steps"></a>後續步驟

若要深入了解 PolyBase，請參閱 [SQL Server PolyBase 概觀](polybase-guide.md)。
