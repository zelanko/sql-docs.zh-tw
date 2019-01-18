---
title: 設定 PolyBase 存取具有 ODBC 泛型類型的外部資料 | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 98e06e3199d4ce8750a4a5956aec6d97c141b33b
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53214253"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>設定 PolyBase 存取 SQL Server 中的外部資料

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 2019 中的 PolyBase 可讓您透過 ODBC 連接器連接到 ODBC 相容的資料來源。 

## <a name="prerequisites"></a>Prerequisites

注意 = 此功能僅適合 Windows 上的 SQL Server。 

如果您尚未安裝 PolyBase，請參閱 [PolyBase 安裝](polybase-installation.md)。

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

在本節中，會建立這些物件：

- CREATE DATABASE SCOPED CREDENTIAL (TRANSACT-SQL) 
- CREATE EXTERNAL DATA SOURCE (Transact-SQL) 
- CREATE EXTERNAL TABLE (Transact-SQL) 
- CREATE STATISTICS (Transact-SQL)

1. 在資料庫上建立主要金鑰 (如果還沒有任何主要金鑰存在)。 這是加密認證祕密的必要項目。

     ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';  
     ```
    ## <a name="arguments"></a>引數
    PASSWORD ='password'

    這是用以加密資料庫中主要金鑰的密碼。 password 必須符合裝載 SQL Server 執行個體之電腦的 Windows 密碼原則需求。

1. 建立資料庫範圍認證以存取 ODBC 資料來源。

     ```sql
     /*  specify credentials to external data source
     *  IDENTITY: user name for external source.  
     *  SECRET: password for external source.
     */
     CREATE DATABASE SCOPED CREDENTIAL credential_name
     WITH IDENTITY = 'username', Secret = 'password';
     ```

1. 使用 [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) 建立外部資料來源。

     ```sql
    /*  LOCATION: Location string should be of format '<type>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( 
    LOCATION = odbc://<ODBC server address>[:<port>],
    CONNECTION_OPTIONS = 'SSL=0;sslAllowInvalidCertificates=1;Driver={<Name of Installed Driver>};HOST=%s;AUTHMECH=0',
    -- PUSHDOWN = ON | OFF,
      CREDENTIAL = credential_name
    );

     ```


1.  使用 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 建立外部資料表，表示外部資料來源中的資料。
 
     ```sql
     /*  LOCATION: ODBC data source table/view
     *  DATA_SOURCE: the external data source, created above.
     */
     CREATE EXTERNAL TABLE customer(
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
      LOCATION='customer',
      DATA_SOURCE= external_data_source_name
     );
      ```

1. **選擇性：** 在外部資料表上建立統計資料。

    我們建議在外部資料表資料行上建立統計資料 (尤其是用於聯結、篩選和彙總的資料行)，以取得最佳查詢效能。

     ```sql
      CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
     ```

## <a name="next-steps"></a>後續步驟

若要深入了解 PolyBase，請參閱 [SQL Server PolyBase 概觀](polybase-guide.md)。
