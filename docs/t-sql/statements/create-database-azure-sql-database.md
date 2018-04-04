---
title: CREATE DATABASE (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 02/13/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SERVICE_OBJECTIVE
- SERVICE_OBJECTIVE_TSQL
- ELASTIC_POOL
- ELASTIC_POOL_TSQL
- EDITION
- EDITION_TSQL
- MAXSIZE
- MAXSIZE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SERVICE_OBJECTIVE
- ELASTIC_POOL
- EDITION SQL Database
- MAXSIZE SQL Database
ms.assetid: 22b167f7-ae86-490b-adb3-ec02ca1c1508
caps.latest.revision: 62
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: de82cfb595559b738ca8db7d72acd620101d3995
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2018
---
# <a name="create-database-azure-sql-database"></a>CREATE DATABASE (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  建立新資料庫。  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

## <a name="syntax"></a>語法  
  
``` 
  
CREATE DATABASE database_name [ COLLATE collation_name ]  
{  
   (<edition_options> [, ...n])   
}  

[ WITH CATALOG_COLLATION = { DATABASE_DEFAULT | SQL_Latin1_General_CP1_CI_AS }  ]
  
<edition_options> ::=   
{  

      MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 … 1024 … 4096 GB }    
    | ( EDITION = {  'basic' | 'standard' | 'premium' }   
    | SERVICE_OBJECTIVE =   
          {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' | 
            | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15'  
            | { ELASTIC_POOL(name = <elastic_pool_name>) } }  ) 
}  

 [;]  
  

```  

```
To copy a database:  
CREATE DATABASE database_name  
    AS COPY OF [source_server_name.] source_database_name  
    [ ( SERVICE_OBJECTIVE =   
          {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |  
            | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15'  
            | { ELASTIC_POOL(name = <elastic_pool_name>) } } )  
    ]  
 [;] 
 
```  
  
## <a name="arguments"></a>引數  
 此語法圖表示範 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中支援的引數。  
  
 *database_name*  
 新資料庫的名稱。 此名稱在 SQL Server 上必須是唯一名稱，其可同時裝載 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 資料庫和 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 資料庫，且必須符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的識別碼規則。 如需詳細資訊，請參閱[識別碼](http://go.microsoft.com/fwlink/p/?LinkId=180386)。  
  
 *Collation_name*  
 指定資料庫的預設定序。 定序名稱可以是 Windows 定序名稱或 SQL 定序名稱。 如果沒有指定，資料庫會擁有指派的預設定序，即 SQL_Latin1_General_CP1_CI_AS。  
  
 如需有關 Windows 和 SQL 定序名稱的詳細資訊，請參閱 [COLLATE (Transact-SQL)](http://msdn.microsoft.com/library/ms184391.aspx)。  
  
 *CATALOG_COLLATION*  
指定中繼資料目錄的預設定序。 *DATABASE_DEFAULT* 指定將用於系統檢視和系統資料表的中繼資料目錄加以定序，以符合資料庫的預設定序。  這是在 SQL Server 中發現的行為。 

*SQL_Latin1_General_CP1_CI_AS* 指定將用於系統檢視和資料表的中繼資料目錄定序為固定 SQL_Latin1_General_CP1_CI_AS 定序。  如果未指定，這就是 Azure SQL Database 上的預設設定。

 *EDITION*  
 指定資料庫的服務層。 可用的值為：'basic'、'standard' 和 'premium'。 已移除 'premiumrs' 的支援。 如有疑問，請使用此電子郵件別名： premium-rs@microsoft.com。
  
 若指定 EDITION 但未指定 MAXSIZE 時，MAXSIZE 會設定為版本支援的最高限制大小。  
  
 *MAXSIZE*  
 指定資料庫的大小上限。 MAXSIZE 對於指定的 EDITION (服務層) 而言必須有效。下表列出服務層支援的 MAXSIZE 值與預設值 (D)：  
  
|**MAXSIZE**|**基本**|**S0-S2**|**S3-S12**|**P1-P6**| **P11-P15** 
|-----------------|---------------|------------------|-----------------|-----------------|-----------------|-----------------|  
|100 MB|√|√|√|√|√|  
|250 MB|√|√|√|√|√|  
|500 MB|√|√|√|√|√|  
|1 GB|√|√|√|√|√|  
|2 GB|√ (D)|√|√|√|√|  
|5 GB|不適用|√|√|√|√|  
|10 GB|不適用|√|√|√|√|  
|20 GB|不適用|√|√|√|√|  
|30 GB|不適用|√|√|√|√|  
|40 GB|不適用|√|√|√|√|  
|50 GB|不適用|√|√|√|√|  
|100 GB|不適用|√|√|√|√|  
|150 GB|不適用|√|√|√|√|  
|200 GB|不適用|√|√|√|√|  
|250 GB|不適用|√ (D)|√ (D)|√|√|  
|300 GB|不適用|不適用|√|√|√|  
|400 GB|不適用|不適用|√|√|√|
|500 GB|不適用|不適用|√|√ (D)|√|
|750 GB|不適用|不適用|√|√|√|
|1024 GB|不適用|不適用|√|√|√ (D)|
|從 1024 GB 至最大 4096 GB (以每 256 GB 的大小遞增)* |不適用|不適用|不適用|不適用|√|√|  
  
 \* P11 和 P15 允許 MAXSIZE 最大至 4 TB，並以 1024 GB 作為預設大小。  P11 和 P15 最多可使用 4 TB 的隨附儲存體，且不另收費。 在進階層中，大於 1 TB 的 MAXSIZE 目前已提供下列區域使用：美國東部2、美國西部、美國維吉尼亞州政府、西歐、德國中部、東南亞、日本東部、澳洲東部、加拿大中部和加拿大東部。 如需了解目前的限制，請參閱[單一資料庫](https://docs.microsoft.com/azure/sql-database-single-database-resources)。  
<!---Loc Comment: Link [Single databases] is not working---> 
  
 以下規則會套用到 MAXSIZE 和 EDITION 引數：  
  
-   如果指定 MAXSIZE 值的話，它必須是上表所示的有效值。  
  
-   如果指定了 EDITION 但是未指定 MAXSIZE，就會使用版本的預設值。 例如，如果 EDITION 設定為 Standard，且未指定 MAXSIZE，則 MAXSIZE 會自動設定為 250 MB。  
  
-   如果 MAXSIZE 和 EDITION 皆未指定，則 EDITION 會設定為 Standard (S0) 而 MAXSIZE 則設定為 250 GB。  
  
 SERVICE_OBJECTIVE  
 指定效能等級。 如需服務目標描述和有關大小、版本及服務目標組合的詳細資訊，請參閱 [Azure SQL Database 服務層和效能層級](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)，以及 [SQL Database 資源限制](https://azure.microsoft.com/documentation/articles/sql-database-resource-limits)。 如果 EDITION 不支援指定的 SERVICE_OBJECTIVE，將會收到錯誤。  
  
 ELASTIC_POOL (name = \<elastic_pool_name >) 若要在 彈性資料庫集區中建立新的資料庫，請將資料庫的 SERVICE_OBJECTIVE 設定為 ELASTIC_POOL，並提供集區名稱。 如需詳細資訊，請參閱[建立和管理 SQL Database 彈性資料庫集區 (預覽)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)。  
  
 *AS COPY OF [source_server_name.]source_database_name*  
 用於將資料庫複製到相同或不同的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器上。  
  
 *source_server_name*  
 來源資料庫所在的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器名稱。 當來源資料庫和目的地資料庫位於相同的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器上時，這個參數是選擇性的。  
  
 注意：`AS COPY OF` 引數不支援唯一的完整網域名稱。 換句話說，如果您伺服器的完整網域名稱為 `serverName.database.windows.net`，則在資料庫複製期間僅可使用 `serverName`。  
  
 *source_database_name*  
 要複製的資料庫名稱。  
  
 使用 `CREATE DATABASE` 陳述式時，[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 不支援下列引數和選項：  
  
-   與檔案實際位置相關的參數，例如 \<filespec> 和 \<filegroup>  
  
-   外部存取選項，例如 DB_CHAINING 和 TRUSTWORTHY  
  
-   附加資料庫  
  
-   Service Broker 選項，例如 ENABLE_BROKER、NEW_BROKER 和 ERROR_BROKER_CONVERSATIONS  
  
-   資料庫快照集  
  
 如需此引數和 `CREATE DATABASE` 陳述式的詳細資訊，請參閱 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)。  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中的資料庫有數個預設設定，這些設定是在建立資料庫時所設定。 如需有關這些預設設定的詳細資訊，請參閱 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md) 中的值清單。  
  
 MAXSIZE 提供了限制資料庫大小的功能。 如果資料庫的大小達到其 MAXSIZE，您將收到錯誤碼 40544。 發生這種情況時，您就無法插入或更新資料，或是建立新物件 (例如資料表、預存程序、檢視和函數)。 不過，您仍然可以讀取和刪除資料、截斷資料表、卸除資料表和索引，以及重建索引。 然後您可以將 MAXSIZE 升級為大於目前資料庫大小的值，或是刪除某些資料以釋出儲存空間。 在您能夠插入新資料之前，最長可能會有十五分鐘的延遲。  
  
> [!IMPORTANT]  
>  `CREATE DATABASE` 陳述式必須是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次中唯一的陳述式。 
  
 若之後要變更大小、版本或服務目標值，請使用 [ALTER DATABASE &#40;Azure SQL Database&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)。  

只有在資料庫建立期間才可使用 CATALOG_COLLATION 引數。 
  
## <a name="database-copies"></a>資料庫複本  
 使用 `CREATE DATABASE` 陳述式複製資料庫是一項非同步作業。 因此，整個複製程序期間都不需要連接至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器。 `CREATE DATABASE` 陳述式會在 sys.databases 中的項目建立後，但在資料庫複製作業完成前，將控制權交還給使用者。 換句話說，`CREATE DATABASE` 陳述式會在資料庫複製仍進行時成功傳回。  
  
-   監視 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 伺服器上的複製程序：查詢 [dm_database_copies](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md) 中的 `percentage_complete` 或 `replication_state_desc` 資料行，或是 **sys.databases** 檢視中的 `state` 資料行。 [sys.dm_operation_status](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md) 檢視也可使用，因為其會傳回資料庫作業 (包括資料庫複製) 的狀態。  
  
 當複製程序順利完成時，目的地資料庫的交易會與來源資料庫一致。  
  
 下列語法和語意規則適用於使用 `AS COPY OF` 引數的情況：  
  
-   來源伺服器名稱和複製目標的伺服器名稱可以相同，也可以不同。 兩個名稱相同時，則這是是選擇性參數，而且根據預設會使用目前工作階段的伺服器內容。  
  
-   來源和目的地資料庫名稱必須加以指定、是唯一的，並且符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的識別碼規則。 如需詳細資訊，請參閱[識別碼](http://go.microsoft.com/fwlink/p/?LinkId=180386)。  
  
-   `CREATE DATABASE` 陳述式必須在將要建立新資料庫之 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器的 master 資料庫內容中執行。  
  
-   複製完成後，目的地資料庫必須做為獨立資料庫管理。 您可以在與來源資料庫不相關的情況下，單獨對新資料庫執行 `ALTER DATABASE` 和 `DROP DATABASE` 陳述式。 您也可以將新資料庫複製到另一個新資料庫。  
  
-   資料庫複製正在進行時，可能會繼續存取來源資料庫。  
  
 如需詳細資訊，請參閱[使用 Transact-SQL 建立 Azure SQL 資料庫的複本](https://azure.microsoft.com/documentation/articles/sql-database-copy-transact-sql/)。  
  
## <a name="permissions"></a>Permissions  
 若要建立資料庫，登入必須為下列其中一項：  
  
-   伺服器層級主體登入  
  
-   本機 Azure SQL Server 的 Azure AD 系統管理員  
  
-   `dbmanager` 資料庫角色成員的登入  
  
 **使用 `CREATE DATABASE ... AS COPY OF` 語法的其他要求：**在本機伺服器上執行陳述式的登入必須至少也是來源伺服器上的 `db_owner`。 如果登入依據 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行，則在本機伺服器上執行陳述式的登入必須與來源 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器上的登入相符，具有相同的名稱和密碼。  
  
## <a name="examples"></a>範例  
如需如何使用 SQL Server Management Studio 連線到 Azure SQL Database 的快速入門教學課程，請參閱 [Azure SQL Database：使用 SQL Server Management Studio 連線及查詢資料](/azure/sql-database/sql-database-connect-query-ssms)。  
  
### <a name="simple-example"></a>簡單範例  
 建立資料庫的簡單範例。  
  
```sql  
CREATE DATABASE TestDB1;  
```  
  
### <a name="simple-example-with-edition"></a>使用 Edition 的簡單範例  
 建立標準資料庫的簡單範例。  
  
```sql  
CREATE DATABASE TestDB2  
( EDITION = 'standard' );  
```  
  
### <a name="example-with-additional-options"></a>使用額外選項的範例  
 使用多個選項的範例。  
  
```sql  
CREATE DATABASE hito   
COLLATE Japanese_Bushu_Kakusu_100_CS_AS_KS_WS   
( MAXSIZE = 500 MB, EDITION = 'standard', SERVICE_OBJECTIVE = 'S1' ) ;  
```  
  
### <a name="creating-a-copy"></a>建立複本  
 建立資料庫複本的範例。  
  
```sql  
CREATE DATABASE escuela   
AS COPY OF school;  
```  
  
### <a name="creating-a-database-in-an-elastic-pool"></a>在彈性集區中建立資料庫  
 在名為 S3M100 的集區中建立新的資料庫：  
  
```sql  
CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = S3M100 ) ) ;  
```  
  
### <a name="creating-a-copy-of-a-database-on-another-server"></a>在另一個伺服器上建立資料庫的複本  
 下列範例會建立 db_original 資料庫的複本，在單一資料庫的 P2 效能層級中名為 db_copy。  不論 db_original 位於彈性集區或單一資料庫的效能層級中，皆是如此。  
  
```sql  
CREATE DATABASE db_copy   
    AS COPY OF ozabzw7545.db_original ( SERVICE_OBJECTIVE = 'P2' )  ;  
```  
  
 下列範例會建立 db_original 資料庫的複本，在名為 ep1 的彈性集區中名為 db_copy。  不論 db_original 位於彈性集區或單一資料庫的效能層級中，皆是如此。  如果 db_original 在彈性集區中，但使用不同的名稱，則 db_copy 仍會建立在 ep1 中。  
  
```sql  
CREATE DATABASE db_copy   
    AS COPY OF ozabzw7545.db_original   
    (SERVICE_OBJECTIVE = ELASTIC_POOL( name = ep1 ) ) ;  
```  

### <a name="create-database-with-specified-catalog-collation-value"></a>使用指定的目錄定序值建立資料庫

下列範例會在資料庫建立期間，將目錄定序設定為 DATABASE_DEFAULT ，其會將目錄定序設定為與資料庫定序相同。

```sql
CREATE DATABASE TestDB3 COLLATE Japanese_XJIS_140  (MAXSIZE = 100 MB, EDITION = ‘basic’)  
      WITH CATALOG_COLLATION = DATABASE_DEFAULT 
```
  
## <a name="see-also"></a>另請參閱  

-  [sys.dm_database_copies &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)

-   [ALTER DATABASE &#40;Azure SQL Database&#41;](alter-database-azure-sql-database.md)   
    
  

