---
title: 設定 PolyBase 存取 SQL Server 中的外部資料 | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
ms.reviewer: jroth
manager: craigg
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: fe5fd6f1842e02d85f6dcd9ee53884ff4cd289e2
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/28/2019
ms.locfileid: "64776082"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>設定 PolyBase 存取 SQL Server 中的外部資料

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何在 SQL Server 執行個體上使用 PolyBase 查詢位於另一個 SQL Server 執行個體中的外部資料。

## <a name="prerequisites"></a>Prerequisites

如果您尚未安裝 PolyBase，請參閱 [PolyBase 安裝](polybase-installation.md)。 安裝文章說明必要條件。

在建立資料庫範圍認證之前，必須建立[主要金鑰](../../t-sql/statements/create-master-key-transact-sql.md)。 

## <a name="configure-a-sql-server-external-data-source"></a>設定 SQL Server 外部資料來源

若要查詢來自 SQL Server 資料來源的資料，您必須建立外部資料表參考外部資料。 本節提供建立這些外部資料表的範例程式碼。 
 
如需最佳查詢效能，請在外部資料表資料行上建立統計資料 (尤其是用於聯結、篩選和彙總的資料行)。

本節中使用下列 Transact-SQL 命令：

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1.  建立資料庫範圍認證以存取 MongoDB 資料來源。

    ```sql
    /*  specify credentials to external data source
    *  IDENTITY: user name for external source.  
    *  SECRET: password for external source.
    */
    CREATE DATABASE SCOPED CREDENTIAL SqlServerCredentials   
    WITH IDENTITY = 'username', Secret = 'password';
    ```

1. 使用 [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) 建立外部資料來源。

    ```sql
    /*  LOCATION: Location string should be of format '<vendor>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *  CREDENTIAL: the database scoped credential, created above.
    */
    CREATE EXTERNAL DATA SOURCE SQLServerInstance
    WITH ( LOCATION = 'sqlserver://SqlServer',
    -- PUSHDOWN = ON | OFF,
    CREDENTIAL = SQLServerCredentials);
    ```

1. **選擇性：** 在外部資料表上建立統計資料。

    我們建議在外部資料表資料行上建立統計資料 (尤其是用於聯結、篩選和彙總的資料行)，以取得最佳查詢效能。

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN;
    ```

>[!IMPORTANT] 
>當您建立外部資料來源之後，可以使用 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 命令透過該來源建立可查詢的資料表。

## <a name="sql-server-connector-compatible-types"></a>SQL Server 連接器相容類型

您可以對可辨識 SQL Server 連線的其他資料來源建立連線。 使用 SQL Server PolyBase 連接器來建立 Azure SQL 資料倉儲和 Azure SQL Database 的外部資料表。 若要完成此工作，請遵循上述相同步驟進行。 請確定資料庫範圍認證、伺服器位址、連接埠及位置字串皆與您想要連線之相容資料來源的對應設定相互關聯。

## <a name="next-steps"></a>後續步驟

若要深入了解 PolyBase，請參閱 [SQL Server PolyBase 概觀](polybase-guide.md)。
