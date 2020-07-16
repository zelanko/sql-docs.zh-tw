---
title: 存取外部資料：ODBC 泛型型別 - PolyBase
description: SQL Server 中的 PolyBase 可供透過 ODBC 連接器連接到相容的資料來源。 安裝 ODBC 驅動程式並建立外部資料表。
ms.date: 02/19/2020
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: ab118c18b2656701470a22b6987a659b45f2fdc7
ms.sourcegitcommit: d1535944bff3f2580070cc036ece30f1d43ee2ce
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2020
ms.locfileid: "86406111"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>設定 PolyBase 存取 SQL Server 中的外部資料

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

SQL Server 2019 中的 PolyBase 可讓您透過 ODBC 連接器連接到 ODBC 相容的資料來源。

本文提供一些使用 ODBC 驅動程式的範例。 如需特定範例，請洽詢您的 ODBC 提供者。 參考資料來源的 ODBC 驅動程式文件，以判斷適當的連接字串選項。 本文中的範例可能不適用於任何特定 ODBC 驅動程式。

## <a name="prerequisites"></a>Prerequisites

>[!NOTE]
>這項功能需要 Windows 上的 SQL Server。

* [安裝 PolyBase](polybase-installation.md)。

* 在建立資料庫範圍認證之前，必須建立[主要金鑰](../../t-sql/statements/create-master-key-transact-sql.md)。

## <a name="install-the-odbc-driver"></a>安裝 ODBC 驅動程式

首先，請下載並安裝您在每個 PolyBase 節點所要連接資料來源的 ODBC 驅動程式。 正確安裝好驅動程式之後，您就可以從 **ODBC 資料來源管理員**檢視及測試驅動程式。

![PolyBase 向外延展群組](../../relational-databases/polybase/media/polybase-odbc-admin.png) 

上例中的驅動程式名稱會以紅圈圈起。 當您建立外部資料來源時，請使用此名稱。

> [!IMPORTANT]
> 為改善查詢效能，請啟用連接共用。 這可在 **ODBC 資料來源管理員**中完成。

## <a name="create-an-external-table"></a>建立外部資料表

若要查詢來自 ODBC 資料來源的資料，您必須建立外部資料表以便參考外部資料。 本節提供建立外部資料表的範例程式碼。

本節中使用下列 Transact-SQL 命令：

* [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
* [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
* [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. 建立資料庫範圍認證以存取 ODBC 來源。

    ```sql
    CREATE DATABASE SCOPED CREDENTIAL <credential_name> WITH IDENTITY = '<username>', Secret = '<password>';
    ```

    例如，下列範例會建立名為 `credential_name` 的認證，其具有 `username` 身分識別和複雜密碼。

    ```sql
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'BycA4ZjrE#*2W%!';
    ```

1. 使用 [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) 建立外部資料來源。

    ```sql
    CREATE EXTERNAL DATA SOURCE <external_data_source_name>
    WITH ( LOCATION = 'odbc://<ODBC server address>[:<port>]',
    CONNECTION_OPTIONS = 'Driver={<Name of Installed Driver>};
    ServerNode = <name of server  address>:<Port>',
    -- PUSHDOWN = [ON] | OFF,
    CREDENTIAL = <credential_name> );
    ```

    下列範例會建立外部資料來源：
    * 名為 `external_data_source_name`
    * 位於 ODBC `SERVERNAME` 和連接埠 `4444`
    * 使用 `CData ODBC Driver For SAP 2015` 連線 - 這是建立在[安裝 ODBC 驅動程式](#install-the-odbc-driver)下的驅動程式
    * 位於 `ServerNode` `sap_server_node` 連接埠 `5555`
    * 設定處理向下推送至伺服器 (`PUSHDOWN = ON`)
    * 使用 `credential_name` 認證

    ```sql
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( LOCATION = 'odbc://SERVERNAME:4444',
    CONNECTION_OPTIONS = 'Driver={CData ODBC Driver For SAP 2015};
    ServerNode = sap_server_node:5555',
    PUSHDOWN = ON,
    CREDENTIAL = credential_name );
    ```

1. **選擇性：** 在外部資料表上建立統計資料。

    為了取得最佳查詢效能，我們建議在外部資料表資料行上建立統計資料 (尤其是用於聯結、篩選和彙總的資料行)。

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
    ```

>[!IMPORTANT]
>在您建立外部資料來源之後，請使用 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 命令對該來源建立可查詢的資料表。

## <a name="next-steps"></a>後續步驟

若要深入了解 PolyBase，請參閱 [SQL Server PolyBase 概觀](polybase-guide.md)。
