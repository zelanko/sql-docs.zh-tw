---
title: "CREATE DATABASE (Azure SQL 資料倉儲) | Microsoft Docs"
ms.custom: 
ms.date: 02/14/20178
ms.prod: 
ms.prod_service: sql-data-warehouse
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|statements
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
author: barbkess
ms.author: barbkess
manager: craigg
ms.openlocfilehash: 3a802dc74793ef79ca35b177b4416d9464a8c34f
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="create-database-azure-sql-data-warehouse"></a>CREATE DATABASE (Azure SQL 資料倉儲)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

建立新資料庫。  
  
## <a name="syntax"></a>語法  
  
```  
CREATE DATABASE database_name [ COLLATE collation_name ]  
(  
    [ MAXSIZE = { 
          250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 | 30720 
        | 40960 | 51200 | 61440 | 71680 | 81920 | 92160 | 102400 
        | 153600 | 204800 | 245760 
      } GB ,
    ]  
    EDITION = 'datawarehouse',  
    SERVICE_OBJECTIVE = { 
         'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' | 'DW600' 
        | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' | 'DW3000' | 'DW6000' 
        | 'DW1000c' | 'DW1500c' | 'DW2000c' | 'DW2500c' | 'DW3000c' | 'DW5000c' 
        | 'DW6000c' | 'DW7500c' | 'DW10000c' | 'DW15000c' | 'DW30000c'
    }  
)  
[;]  
```  
  
## <a name="arguments"></a>引數  
*database_name*  
新資料庫的名稱。 此名稱在 SQL Server 上必須是唯一名稱，其可同時裝載 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 資料庫和 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 資料庫，且必須符合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的識別碼規則。 如需詳細資訊，請參閱[識別碼](http://go.microsoft.com/fwlink/p/?LinkId=180386)。  
  
*collation_name*  
指定資料庫的預設定序。 定序名稱可以是 Windows 定序名稱或 SQL 定序名稱。 如果未指定，則會將資料庫指派預設定序，即 SQL_Latin1_General_CP1_CI_AS。  
  
如需有關 Windows 和 SQL 定序名稱的詳細資訊，請參閱 [COLLATE (Transact-SQL)](http://msdn.microsoft.com/library/ms184391.aspx)。  
  
*EDITION*  
指定資料庫的服務層。 若是 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，請使用 'datawarehouse'。  
  
*MAXSIZE*  
預設為 245,760 GB (240 TB)。  

**適用於：**最佳化彈性效能層級

資料庫的允許大小上限。 資料庫不可增大超過 MAXSIZE。 

**適用於：**最佳化計算效能層級

資料庫中資料列存放區資料的允許大小上限。 儲存在資料列存放區資料表的資料、資料行存放區索引的差異存放區、或叢集資料行存放區索引的非叢集索引，不可增大超過 MAXSIZE。  壓縮成資料行存放區格式的資料大小沒有大小限制，所以不受 MAXSIZE 限制。
  
SERVICE_OBJECTIVE  
指定效能等級。 如需 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 的服務目標相關資訊，請參閱[效能層級](https://azure.microsoft.com/documentation/articles/performance-tiers/)。  
  
## <a name="general-remarks"></a>一般備註  
使用 [DATABASEPROPERTYEX &#40;TRANSACT-SQL &#41;](../../t-sql/functions/databasepropertyex-transact-sql.md) 以查看資料庫屬性。  
  
使用 [ALTER DATABASE &#40;Azure SQL Database&#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md) 在之後變更大小上限或服務目標值。   

SQL 資料倉儲設定為 COMPATIBILITY_LEVEL 130，而且不可變更。 如需詳細資訊，請參閱[Azure SQL Database 中改善的查詢效能與相容性層級 130](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/)。
  
## <a name="permissions"></a>Permissions  
必要權限：  
  
-   由佈建程序建立的伺服器層級主體登入，或  
  
-   `dbmanager` 資料庫角色的成員。  
  
## <a name="error-handling"></a>錯誤處理  
如果資料庫的大小達到 MAXSIZE，您將收到錯誤碼 40544。 若發生這種情況，您就無法插入和更新資料，或是建立新物件 (例如資料表、預存程序、檢視和函式)。 您仍然可以讀取和刪除資料、截斷資料表、卸除資料表和索引，以及重建索引。 然後您可以將 MAXSIZE 升級為大於目前資料庫大小的值，或是刪除某些資料以釋出儲存空間。 在您能夠插入新資料之前，最長可能會有十五分鐘的延遲。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
您必須連接到 master 資料庫才能建立新的資料庫。  
  
`CREATE DATABASE` 陳述式必須是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次中唯一的陳述式。

在資料庫建立後，您就無法變更資料庫定序。   
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]  
  
### <a name="a-simple-example"></a>A. 簡單範例  
建立資料倉儲資料庫的簡單範例。 這所建立出的資料庫，其大小上限最小為 10240 GB、預設定序為 SQL_Latin1_General_CP1_CI_AS，且最小運算能力為 DW100。  
  
```  
CREATE DATABASE TestDW  
(EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');  
```  
  
### <a name="b-create-a-data-warehouse-database-with-all-the-options"></a>B. 以所有選項建立資料倉儲資料庫  
使用所有選項建立 10 TB 資料倉儲的範例。  
  
```  
CREATE DATABASE TestDW COLLATE Latin1_General_100_CI_AS_KS_WS  
(MAXSIZE = 10240 GB, EDITION = 'datawarehouse', SERVICE_OBJECTIVE = 'DW1000');  
```  
  
## <a name="see-also"></a>另請參閱  
[ALTER DATABASE &#40;Azure SQL Data Warehouse&#40;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)
[CREATE TABLE &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-table-azure-sql-data-warehouse.md) 
[DROP DATABASE &#40;Transact-SQL&#40;](../../t-sql/statements/drop-database-transact-sql.md) 
  

