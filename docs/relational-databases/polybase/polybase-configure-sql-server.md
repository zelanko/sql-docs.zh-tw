---
title: 設定 PolyBase 存取 SQL Server 中的外部資料 | Microsoft Docs
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
ms.openlocfilehash: d2b4bb2249f0c4a6ec57c037db54c490f3066e2b
ms.sourcegitcommit: 41979c9d511b3eeb45134d30ccb0dbc6bba70f1a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/01/2018
ms.locfileid: "50757943"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>設定 PolyBase 存取 SQL Server 中的外部資料

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何在 SQL Server 執行個體上使用 PolyBase 查詢位於另一個 SQL Server 執行個體中的外部資料。

## <a name="prerequisites"></a>Prerequisites

如果您尚未安裝 PolyBase，請參閱 [PolyBase 安裝](polybase-installation.md)。 安裝文章說明必要條件。

## <a name="configure-an-external-table"></a>設定外部資料表

若要查詢來自 SQL Server 資料來源的資料，您必須建立外部資料表參考外部資料。 本節提供建立這些外部資料表的範例程式碼。 
 
如需最佳查詢效能，請在外部資料表資料行上建立統計資料 (尤其是用於聯結、篩選和彙總的資料行)。

在本節中，會建立這些物件：

- CREATE DATABASE SCOPED CREDENTIAL (TRANSACT-SQL) 
- CREATE EXTERNAL DATA SOURCE (Transact-SQL) 
- CREATE EXTERNAL TABLE (Transact-SQL) 
- CREATE STATISTICS (Transact-SQL)

1. 在資料庫上建立主要金鑰。 加密認證祕密時需要主要金鑰。

     ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
     ```

1. 建立資料庫範圍認證。

     ```sql
     /*  specify credentials to external data source
     *  IDENTITY: user name for external source.  
     *  SECRET: password for external source.
     */
     CREATE DATABASE SCOPED CREDENTIAL SqlServerCredentials   
     WITH IDENTITY = 'username', Secret = 'password';
     ```

1. 使用 [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) 建立外部資料來源。 指定 SQL Server 的外部資料來源位置和認證。

     ```sql
    /*  LOCATION: Location string should be of format '<vendor>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE SQLServerInstance
    WITH ( 
    LOCATION = sqlserver://SqlServer,
    -- PUSHDOWN = ON | OFF,
      CREDENTIAL = SQLServerCredentials
    );

     ```

1. 建立外部資料結構描述。

     ```sql
     CREATE SCHEMA sqlserver;
     GO
     ```

1.  使用 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 來建立代表外部 SQL Server 執行個體中所儲存資料的外部資料表。
 
     ```sql
     /*  LOCATION: sql server table/view in 'database_name.schema_name.object_name' format
     *  DATA_SOURCE: the external data source, created above.
     */
     CREATE EXTERNAL TABLE sqlserver.customer(
     C_CUSTKEY INT NOT NULL,
     C_NAME VARCHAR(25) NOT NULL,
     C_ADDRESS VARCHAR(40) NOT NULL,
     C_NATIONKEY INT NOT NULL,
     C_PHONE CHAR(15) NOT NULL,
     C_ACCTBAL DECIMAL(15,2) NOT NULL,
     C_MKTSEGMENT CHAR(10) NOT NULL,
     C_COMMENT VARCHAR(117) NOT NULL
      )
      WITH (
      LOCATION='tpch_10.dbo.customer',
      DATA_SOURCE=SqlServerInstance
     );
      ```

1. 在外部資料表上建立統計資料。

     ```sql
      CREATE STATISTICS CustomerCustKeyStatistics ON sqlserver.customer (C_CUSTKEY) WITH FULLSCAN; 
     ```

## <a name="sql-server-connector-compatible-types"></a>SQL Server 連接器相容類型

您可以對可辨識 SQL Server 連線的其他資料來源建立連線。 使用 SQL Server PolyBase 連接器來建立 Azure SQL 資料倉儲和 Azure SQL Database 的外部資料表。 若要完成此工作，請遵循上述相同步驟進行。 請確定資料庫範圍認證、伺服器位址、連接埠及位置字串皆與您想要連線之相容資料來源的對應設定相互關聯。

## <a name="next-steps"></a>後續步驟

若要深入了解 PolyBase，請參閱 [SQL Server PolyBase 概觀](polybase-guide.md)。
