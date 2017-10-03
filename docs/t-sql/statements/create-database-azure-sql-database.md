---
title: "建立資料庫 (Azure SQL Database) |Microsoft 文件"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 08/28/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: e9781bd657f094c7be57ae513cc2c4a026ad4746
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="create-database-azure-sql-database"></a>CREATE DATABASE (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  建立新資料庫。  
  
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
    | ( EDITION = {  'basic' | 'standard' | 'premium' | 'premiumrs'}   
    | SERVICE_OBJECTIVE =   
          {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' | 
            | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15'  
            | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' 
            | { ELASTIC_POOL(name = <elastic_pool_name>) } }  ) 
}  

[ AS COPY OF [source_server_name.]source_database_name ]

 [;]  
  

```  

```
To copy a database:  
CREATE DATABASE database_name  
    AS COPY OF [source_server_name.] source_database_name  
    [ ( SERVICE_OBJECTIVE =   
          {  'basic' | 'S0' | 'S1' | 'S2' | 'S3' | 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |  
            | 'P1' | 'P2' | 'P4'| 'P6' | 'P11' | 'P15'  
            | 'PRS1' | 'PRS2' | 'PRS4' | 'PRS6' 
            | { ELASTIC_POOL(name = <elastic_pool_name>) } } )  
    ]  
 [;] 
 
```  
  
## <a name="arguments"></a>引數  
 此語法圖表示範 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中支援的引數。  
  
 *database_name*  
 新資料庫的名稱。 此名稱必須是唯一的 SQL 伺服器上，其可裝載兩者[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]資料庫和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]資料庫，且必須符合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]識別碼規則。 如需詳細資訊，請參閱[識別碼](http://go.microsoft.com/fwlink/p/?LinkId=180386)。  
  
 *Sys.databases*  
 指定資料庫的預設定序。 定序名稱可以是 Windows 定序名稱或 SQL 定序名稱。 如果沒有指定，資料庫會擁有指派的預設定序，即 SQL_Latin1_General_CP1_CI_AS。  
  
 如需有關 Windows 和 SQL 定序名稱， [COLLATE (TRANSACT-SQL)](http://msdn.microsoft.com/library/ms184391.aspx)。  
  
 *CATALOG_COLLATION*  
指定中繼資料類別目錄的預設定序。 *DATABASE_DEFAULT*指定中繼資料目錄使用的系統檢視表和定序，以符合資料庫的預設定序的系統資料表。  這是 SQL Server 中的行為。 

*SQL_Latin1_General_CP1_CI_AS*指定中繼資料目錄使用的系統檢視和資料表定序為固定 SQL_Latin1_General_CP1_CI_AS 定序。  如果未指定，這是 Azure SQL Database 上的預設設定。

 *版本*  
 指定資料庫的服務層。 可用的值為: 'basic'、 'standard'、 'premium' 和 'premiumrs'。  
  
 當指定 EDITION 但是未指定 MAXSIZE 時，MAXSIZE 將設為版本所支援的最高限制大小。  
  
 *MAXSIZE*  
 指定資料庫的大小上限。 MAXSIZE 對於指定的 EDITION (服務層) 而言必須有效。下表列出服務層支援的 MAXSIZE 值與預設值 (D)：  
  
|**MAXSIZE**|**Basic**|**S0 S2**|**S3 S12**|**P1 P6 和 PRS1 PRS6**| **P11 P15** 
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
|從 1024 GB 高達 4096 GB 增量的 256 GB * |不適用|不適用|不適用|不適用|√|√|  
  
 \*P11 和 P15 允許 MAXSIZE 4 TB 1024 gb 預設大小。  P11 和 P15 可以使用 4 TB，包括存放裝置，不另收費。 在優質層次中，大於 1 TB 的 MAXSIZE 是目前已提供下列區域： 美國 East2、 美國西部、 美國 Gov 維吉尼亞州、 西歐、 德國中央、 南東亞、 日本東部、 澳洲東部、 加拿大中央和加拿大東部。 如需目前的限制，請參閱[單一資料庫](https://docs.microsoft.com/azure/sql-database-single-database-resources)。  
  
 以下規則會套用到 MAXSIZE 和 EDITION 引數：  
  
-   如果指定 MAXSIZE 值的話，它必須是上表所示的有效值。  
  
-   如果指定了 EDITION 但是未指定 MAXSIZE，就會使用版本的預設值。 例如，如果 EDITION 設定為標準，而且未指定 MAXSIZE，然後 MAXSIZE 會自動設定為 250 MB。  
  
-   如果 MAXSIZE 和 EDITION 都不指定，則 EDITION 會設定為標準 (S0)，和 MAXSIZE 設為 250 GB。  
  
 SERVICE_OBJECTIVE  
 指定效能等級。 服務目標描述和大小、 版本及服務目標組合的詳細資訊，請參閱[Azure SQL Database 服務層和效能層級](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)和[SQL Database 資源限制](https://azure.microsoft.com/documentation/articles/sql-database-resource-limits)。 如果 EDITION 不支援指定的 SERVICE_OBJECTIVE，將會收到錯誤。  
  
 ELASTIC_POOL (名稱 = \<elastic_pool_name >) 彈性資料庫集區中建立新的資料庫，資料庫的 SERVICE_OBJECTIVE 設 ELASTIC_POOL 和提供的集區名稱。 如需詳細資訊，請參閱[建立及管理 SQL Database 彈性資料庫集區 （預覽）](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)。  
  
 *為複製的 [source_server_name]。source_database_name*  
 用於將資料庫複製到相同或不同的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器上。  
  
 *source_server_name*  
 來源資料庫所在的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器名稱。 當來源資料庫和目的地資料庫位於相同的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器上時，這個參數是選擇性的。  
  
 注意：`AS COPY OF` 引數不支援唯一的完整網域名稱。 換句話說，如果您伺服器的完整網域名稱為 `serverName.database.windows.net`，則在資料庫複製期間僅可使用 `serverName`。  
  
 *source_database_name*  
 要複製的資料庫名稱。  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]不支援下列引數和選項使用時`CREATE DATABASE`陳述式：  
  
-   參數與相關實體位置的檔案，例如\<filespec > 和\<檔案群組 >  
  
-   外部存取選項，例如 DB_CHAINING 和 TRUSTWORTHY  
  
-   附加資料庫  
  
-   Service Broker 選項，例如 ENABLE_BROKER、NEW_BROKER 和 ERROR_BROKER_CONVERSATIONS  
  
-   資料庫快照集  
  
 如需有關引數和`CREATE DATABASE`陳述式，請參閱[CREATE DATABASE &#40;SQL Server TRANSACT-SQL &#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
## <a name="remarks"></a>備註  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中的資料庫有數個預設設定，這些設定是在建立資料庫時所設定。 如需有關這些預設設定的詳細資訊，請參閱中的值清單[DATABASEPROPERTYEX &#40;TRANSACT-SQL &#41;](../../t-sql/functions/databasepropertyex-transact-sql.md).  
  
 MAXSIZE 提供了限制資料庫大小的功能。 如果資料庫的大小達到其 MAXSIZE，您會收到錯誤碼 40544。 發生這種情況時，您就無法插入或更新資料，或是建立新物件 (例如資料表、預存程序、檢視和函數)。 不過，您仍然可以讀取和刪除資料、截斷資料表、卸除資料表和索引，以及重建索引。 然後您可以將 MAXSIZE 升級為大於目前資料庫大小的值，或是刪除某些資料以釋出儲存空間。 在您能夠插入新資料之前，最長可能會有十五分鐘的延遲。  
  
> [!IMPORTANT]  
>  `CREATE DATABASE` 陳述式必須是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次中唯一的陳述式。 
  
 若要稍後變更大小、 版本或服務目標的值，請使用[ALTER DATABASE &#40;Azure SQL Database &#41;](../../t-sql/statements/alter-database-azure-sql-database.md).  

資料庫建立期間，才可使用 CATALOG_COLLATION 引數。 
  
## <a name="database-copies"></a>資料庫複本  
 複製資料庫，使用`CREATE DATABASE`陳述式是非同步作業。 因此，整個複製程序期間都不需要連接至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器。 `CREATE DATABASE`陳述式將控制權傳回給使用者之後，sys.databases 中的項目會建立，但資料庫複製作業已完成。 換句話說，`CREATE DATABASE` 陳述式會在資料庫複製仍進行時成功傳回。  
  
-   監視複製程序上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]伺服器： 查詢`percentage_complete`或`replication_state_desc`中的資料行[dm_database_copies](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)或`state`中的資料行**sys.databases**檢視。 [Sys.dm_operation_status](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)檢視可用，以及它會傳回包含資料庫複本的資料庫作業的狀態。  
  
 當複製程序順利完成時，目的地資料庫的交易會與來源資料庫一致。  
  
 下列語法和語意規則適用於使用 `AS COPY OF` 引數的情況：  
  
-   來源伺服器名稱和複製目標的伺服器名稱可以相同，也可以不同。 當它們是相同的時這是選擇性參數，預設會使用目前的工作階段的伺服器內容。  
  
-   來源和目的地資料庫名稱必須加以指定、是唯一的，並且符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的識別碼規則。 如需詳細資訊，請參閱[識別碼](http://go.microsoft.com/fwlink/p/?LinkId=180386)。  
  
-   `CREATE DATABASE` 陳述式必須在將要建立新資料庫之 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器的 master 資料庫內容中執行。  
  
-   複製完成後，目的地資料庫必須做為獨立資料庫管理。 您可以在與來源資料庫不相關的情況下，單獨對新資料庫執行 `ALTER DATABASE` 和 `DROP DATABASE` 陳述式。 您也可以將新資料庫複製到另一個新資料庫。  
  
-   資料庫複製正在進行時，可能會繼續存取來源資料庫。  
  
 如需詳細資訊，請參閱[建立一份使用 Transact SQL Azure SQL database](https://azure.microsoft.com/documentation/articles/sql-database-copy-transact-sql/)。  
  
## <a name="permissions"></a>Permissions  
 若要建立資料庫登入必須是下列其中一項：  
  
-   伺服器層級主體登入  
  
-   Azure AD 系統管理員的本機 Azure SQL Server  
  
-   成員的登入`dbmanager`資料庫角色  
  
 **使用的其他需求`CREATE DATABASE ... AS COPY OF`語法：**的登入本機伺服器上執行陳述式也必須至少`db_owner`來源伺服器上。 如果登入根據[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證、 登入本機伺服器上執行陳述式必須有符合的登入來源[!INCLUDE[ssSDS](../../includes/sssds-md.md)]伺服器，具有相同的名稱和密碼。  
  
## <a name="examples"></a>範例  
示範如何連接到 Azure SQL 資料庫使用 SQL Server Management Studio 的快速入門教學課程，請參閱[Azure SQL Database： 使用 SQL Server Management Studio 來連接及查詢資料](/azure/sql-database/sql-database-connect-query-ssms)。  
  
### <a name="simple-example"></a>簡單範例  
 建立資料庫的簡單範例。  
  
```tsql  
CREATE DATABASE TestDB1;  
```  
  
### <a name="simple-example-with-edition"></a>簡單的範例，版本  
 建立標準資料庫的簡單範例。  
  
```tsql  
CREATE DATABASE TestDB2  
( EDITION = 'standard' );  
```  
  
### <a name="example-with-additional-options"></a>使用其他選項的範例  
 使用多個選項的範例。  
  
```tsql  
CREATE DATABASE hito   
COLLATE Japanese_Bushu_Kakusu_100_CS_AS_KS_WS   
( MAXSIZE = 500 MB, EDITION = 'standard', SERVICE_OBJECTIVE = 'S1' ) ;  
```  
  
### <a name="creating-a-copy"></a>建立複本  
 範例建立資料庫的副本。  
  
```tsql  
CREATE DATABASE escuela   
AS COPY OF school;  
```  
  
### <a name="creating-a-database-in-an-elastic-pool"></a>彈性集區中建立資料庫  
 建立新的資料庫中名為 S3M100 集區：  
  
```tsql  
CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = S3M100 ) ) ;  
```  
  
### <a name="creating-a-copy-of-a-database-on-another-server"></a>另一部伺服器上建立資料庫的副本  
 下列範例會建立名 db_copy P2 效能層級為單一資料庫的 db_original 資料庫複本。  這是不論 db_original 是彈性集區或單一資料庫的效能層級中，則為 true。  
  
```tsql  
CREATE DATABASE db_copy   
    AS COPY OF ozabzw7545.db_original ( SERVICE_OBJECTIVE = 'P2' )  ;  
```  
  
 下列範例會建立一份 db_original 資料庫中，名為 db_copy 名為 ep1 彈性集區中。  這是不論 db_original 是彈性集區或單一資料庫的效能層級中，則為 true。  如果 db_original 在彈性集區使用不同的名稱，然後 db_copy 仍會建立在 ep1。  
  
```tsql  
CREATE DATABASE db_copy   
    AS COPY OF ozabzw7545.db_original   
    (SERVICE_OBJECTIVE = ELASTIC_POOL( name = ep1 ) ) ;  
```  

### <a name="create-database-with-specified-catalog-collation-value"></a>使用指定的目錄定序值建立資料庫

下列範例將 DATABASE_DEFAULT 目錄定序設定在資料庫建立時，設定，使資料庫定序與相同的目錄定序。

```tsql
CREATE DATABASE TestDB3 COLLATE Japanese_XJIS_140  (MAXSIZE = 100 MB, EDITION = ‘basic’)  
      WITH CATALOG_COLLATION = DATABASE_DEFAULT 
```
  
## <a name="see-also"></a>另請參閱  

-  [sys.dm_database_copies &#40;Azure SQL Database &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)

-   [ALTER DATABASE &#40;Azure SQL Database &#41;](alter-database-azure-sql-database.md)   
    
  


