---
title: 存取外部資料：SQL Server - PolyBase
ms.date: 12/13/2019
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: fa0a133e7a2c966798c168a74841350702b54295
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "75252320"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>設定 PolyBase 存取 SQL Server 中的外部資料

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何在 SQL Server 執行個體上使用 PolyBase 查詢位於另一個 SQL Server 執行個體中的外部資料。

## <a name="prerequisites"></a>Prerequisites

如果您尚未安裝 PolyBase，請參閱 [PolyBase 安裝](polybase-installation.md)。 安裝文章說明必要條件。 安裝後，也請務必[啟用 PolyBase](polybase-installation.md#enable)。

在建立資料庫範圍認證之前，必須建立[主要金鑰](../../t-sql/statements/create-master-key-transact-sql.md)。 

## <a name="configure-a-sql-server-external-data-source"></a>設定 SQL Server 外部資料來源

若要查詢來自 SQL Server 資料來源的資料，您必須建立外部資料表參考外部資料。 本節提供建立這些外部資料表的範例程式碼。 
 
如需最佳查詢效能，請在外部資料表資料行上建立統計資料 (尤其是用於聯結、篩選和彙總的資料行)。

本節中使用下列 Transact-SQL 命令：

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. 建立資料庫範圍認證以存取 SQL Server 來源。 下列範例使用 `IDENTITY = 'username'` 和 `SECRET = 'password'` 來建立外部資料來源認證。

    ```sql
    CREATE DATABASE SCOPED CREDENTIAL SqlServerCredentials
    WITH IDENTITY = 'username', SECRET = 'password';
    ```

1. 使用 [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) 建立外部資料來源。 下列範例將：

   - 建立名為 `SQLServerInstance` 的外部資料來源。
   - 指定外部資料來源 (`LOCATION = '<vendor>://<server>[:<port>]'`)。 在範例中，它會指向 SQL Server 的預設執行個體。
   - 識別是否應將計算推送至來源 (`PUSHDOWN`)。 `PUSHDOWN` 預設為 `ON`。

   最後，範例會使用先前建立的認證。

    ```sql
    CREATE EXTERNAL DATA SOURCE SQLServerInstance
        WITH ( LOCATION = 'sqlserver://SqlServer',
        PUSHDOWN = ON,
        CREDENTIAL = SQLServerCredentials);
    ```

1. (選擇性) 在外部資料表上建立統計資料。

  如需最佳查詢效能，請在外部資料表資料行上建立統計資料 (尤其是用於聯結、篩選和彙總的資料行)。

  ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY)
    WITH FULLSCAN;
  ```

>[!IMPORTANT] 
>當您建立外部資料來源之後，可以使用 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 命令透過該來源建立可查詢的資料表。

## <a name="sql-server-connector-compatible-types"></a>SQL Server 連接器相容類型

您可以對可辨識 SQL Server 連線的其他資料來源建立連線。 使用 SQL Server PolyBase 連接器來建立 Azure SQL 資料倉儲和 Azure SQL Database 的外部資料表。 若要完成此工作，請遵循上述相同步驟進行。 請確定資料庫範圍認證、伺服器位址、連接埠及位置字串皆與您想要連線之相容資料來源的對應設定相互關聯。

## <a name="next-steps"></a>後續步驟

若要深入了解 PolyBase，請參閱 [SQL Server PolyBase 概觀](polybase-guide.md)。
