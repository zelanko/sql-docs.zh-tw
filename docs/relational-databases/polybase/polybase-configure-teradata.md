---
title: 存取外部資料：Teradata - PolyBase
description: 了解如何在 SQL Server 執行個體上使用 PolyBase 查詢位於 Teradata 中的外部資料。 建立外部資料表以參考外部資料。
ms.date: 12/13/2019
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 31ce6dbde09a9be1a69e6f024dc885f5cd38dfc8
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/08/2020
ms.locfileid: "91833798"
---
# <a name="configure-polybase-to-access-external-data-in-teradata"></a>設定 PolyBase 存取 Teradata 中的外部資料

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

本文說明如何在 SQL Server 執行個體上使用 PolyBase 查詢位於 Teradata 中的外部資料。

## <a name="prerequisites"></a>Prerequisites

如果您尚未安裝 PolyBase，請參閱 [PolyBase 安裝](polybase-installation.md)。 安裝文章說明必要條件。

在建立資料庫範圍認證之前，必須建立[主要金鑰](../../t-sql/statements/create-master-key-transact-sql.md)。 

若要在 Teradata 上使用 PolyBase，需具備 VC++ 可轉散發套件。
 
## <a name="configure-a-teradata-external-data-source"></a>設定 Teradata 外部資料來源

若要查詢來自 Teradata 資料來源的資料，您必須建立外部資料表參考外部資料。 本節提供建立這些外部資料表的範例程式碼。 



本節中使用下列 Transact-SQL 命令：

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. 建立資料庫範圍認證以存取 MongoDB 資料來源。

    ```sql
    /*  specify credentials to external data source
    *  IDENTITY: user name for external source. 
    *  SECRET: password for external source.
    */
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'password';
    ```

   > [!IMPORTANT] 
   > 適用於 PolyBase 的 Teradata ODBC 連接器僅支援基本驗證，不支援 Kerberos 驗證。

1. 使用 [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) 建立外部資料來源。

    ```sql
    /*  LOCATION: Location string should be of format '<vendor>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    * CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH (LOCATION = teradata://<server address>[:<port>],
    -- PUSHDOWN = ON | OFF,
    CREDENTIAL =credential_name);
    ```

1. **選擇性：** 在外部資料表上建立統計資料。

    我們建議在外部資料表資料行上建立統計資料 (尤其是用於聯結、篩選和彙總的資料行)，以取得最佳查詢效能。

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
    ```

>[!IMPORTANT] 
>當您建立外部資料來源之後，可以使用 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 命令透過該來源建立可查詢的資料表。

## <a name="next-steps"></a>後續步驟

若要深入了解 PolyBase，請參閱 [SQL Server PolyBase 概觀](polybase-guide.md)。
