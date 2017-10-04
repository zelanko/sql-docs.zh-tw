---
title: "建立資料庫 （Azure SQL 資料倉儲） |Microsoft 文件"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 03/14/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 42819b93-b757-4b2c-8179-d4be3c512c19
caps.latest.revision: 20
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a178756610f0d0e463c21a2a62a287ada6c863a1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-database-azure-sql-data-warehouse"></a>建立資料庫 （Azure SQL 資料倉儲）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

建立新資料庫。  
  
## <a name="syntax"></a>語法  
  
```  
CREATE DATABASE database_name [ COLLATE collation_name ]  
(  
    [ MAXSIZE = { 250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 | 30720 | 40960 | 51200 | 61440 | 71680 | 81920 | 92160 | 102400 | 153600 | 204800 | 245760 } GB ,]  
    EDITION = 'datawarehouse',  
    SERVICE_OBJECTIVE = { 'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' | 'DW600' | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' | 'DW3000' | 'DW6000' }  
)  
[;]  
```  
  
## <a name="arguments"></a>引數  
*database_name*  
新資料庫的名稱。 此名稱必須是唯一的 SQL 伺服器上，其可裝載兩者[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]資料庫和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]資料庫，且必須符合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]識別碼規則。 如需詳細資訊，請參閱[識別碼](http://go.microsoft.com/fwlink/p/?LinkId=180386)。  
  
*sys.databases*  
指定資料庫的預設定序。 定序名稱可以是 Windows 定序名稱或 SQL 定序名稱。 如果未指定，資料庫就會指派預設定序為 SQL_Latin1_General_CP1_CI_AS。  
  
如需有關 Windows 和 SQL 定序名稱的詳細資訊，請參閱[COLLATE (TRANSACT-SQL)](http://msdn.microsoft.com/library/ms184391.aspx)。  
  
*版本*  
指定資料庫的服務層。 如[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]使用 'datawarehouse'。  
  
*MAXSIZE*  
資料庫的最大可以增長至。 設定此值可防止大小設定超過資料庫大小的成長。 預設值*MAXSIZE*時未指定為 10240 GB (10 TB)。  其他可能的值範圍從 250 GB 最多 240 TB。  
  
SERVICE_OBJECTIVE  
指定效能等級。 如需服務目標[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，請參閱[SQL 資料倉儲上的小數位數效能](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-performance-scale/)。  
  
## <a name="general-remarks"></a>一般備註  
使用[DATABASEPROPERTYEX &#40;TRANSACT-SQL &#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)以查看資料庫屬性。  
  
使用[ALTER DATABASE &#40;Azure SQL 資料倉儲 &#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)變更大小上限，或更新版本的服務目標的值。   

SQL 資料倉儲設定為 COMPATIBILITY_LEVEL 130，而且無法變更。 如需詳細資訊，請參閱[改善查詢效能與 Azure SQL Database 中的相容性層級 130](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/)。
  
## <a name="permissions"></a>Permissions  
必要的權限：  
  
-   伺服器層級主體登入，由佈建程序，或  
  
-   成員的`dbmanager`資料庫角色。  
  
## <a name="error-handling"></a>錯誤處理  
如果資料庫的大小達到的 MAXSIZE，您將收到錯誤碼 40544。 當發生這種情況時，您就無法插入和更新資料，或建立新物件 （例如資料表、 預存程序、 檢視和函數）。 您仍可以讀取和刪除資料、 截斷資料表、 卸除資料表和索引，及重建索引。 然後您可以將 MAXSIZE 升級為大於目前資料庫大小的值，或是刪除某些資料以釋出儲存空間。 在您能夠插入新資料之前，最長可能會有十五分鐘的延遲。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
您必須連接到 master 資料庫才能建立新的資料庫。  
  
`CREATE DATABASE` 陳述式必須是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次中唯一的陳述式。

在建立資料庫之後，您無法變更資料庫定序。   
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]  
  
### <a name="a-simple-example"></a>A. 簡單範例  
建立資料倉儲資料庫的簡單範例。 這會建立資料庫的最小的最大大小為 10240 GB 的預設定序為 SQL_Latin1_General_CP1_CI_AS，其中最小的運算能力即 DW100。  
  
```  
CREATE DATABASE TestDW  
(EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');  
```  
  
### <a name="b-create-a-data-warehouse-database-with-all-the-options"></a>B. 建立資料倉儲資料庫的所有選項  
建立的範例使用所有選項的 10 tb 的資料倉儲。  
  
```  
CREATE DATABASE TestDW COLLATE Latin1_General_100_CI_AS_KS_WS  
(MAXSIZE = 10240 GB, EDITION = 'datawarehouse', SERVICE_OBJECTIVE = 'DW1000');  
```  
  
## <a name="see-also"></a>另請參閱  
[ALTER DATABASE &#40;Azure SQL 資料倉儲 &#40;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md) 
[建立資料表 &#40;Azure SQL 資料倉儲 &#41;](../../t-sql/statements/create-table-azure-sql-data-warehouse.md)  
[卸除資料庫 &#40;TRANSACT-SQL &#40;](../../t-sql/statements/drop-database-transact-sql.md) 
  


