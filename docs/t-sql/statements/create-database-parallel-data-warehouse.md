---
title: CREATE DATABASE (平行處理資料倉儲) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 40cacde4-ac72-45f7-9564-d76e2b4a741a
caps.latest.revision: 13
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 41ed767a4acd2dbe4b202e94ed054da46810e14a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="create-database-parallel-data-warehouse"></a>CREATE DATABASE (平行處理資料倉儲)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  在 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 設備上建立新資料庫。 使用此陳述式建立和設備資料庫關聯的所有檔案，以及設定資料庫表格和交易記錄的大小上限與自動成長選項。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
CREATE DATABASE database_name   
WITH (   
    [ AUTOGROW = ON | OFF , ]   
    REPLICATED_SIZE = replicated_size [ GB ] ,  
    DISTRIBUTED_SIZE = distributed_size [ GB ] ,  
    LOG_SIZE = log_size [ GB ] )  
[;]  
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 新資料庫的名稱。 如需所允許資料庫名稱的詳細資訊，請參閱 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] 中的「物件命名規則」和「保留的資料庫名稱」。  
  
 AUTOGROW = ON | **OFF**  
 指定此資料庫的 *replicated_size*、*distributed_size*和 *log_size* 參數是否將會視需要自動成長至超出其指定大小。 預設值是 **OFF**。  
  
 如果 AUTOGROW 設為 ON，在每次插入資料、更新資料或進行其他動作而導致所需儲存空間大於已配置大小時，*replicated_size*、*distributed_size*和 *log_size* 就會視需要成長 (不在初始指定大小的區塊中)。  
  
 如果 AUTOGROW 設為 OFF，大小就不會自動成長。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 在嘗試進行需要 *replicated_size*、*distributed_size* 或 *log_size* 成長至超出其指定值的動作時，將會傳回錯誤。  
  
 只能針對所有大小將 AUTOGROW 設為 ON 或 OFF。 例如，如果為 *log_size* 將 AUTOGROW 設為 ON，就不得不為 *replicated_size* 將 AUTOGROW 設為 ON。  
  
 *replicated_size* [ GB ]  
 一個正數。 設定配置給「每個計算節點上」複寫資料表和相對應資料的總空間大小 (以整數或小數 GB 為單位)。 對於最低和最高 *replicated_size* 需求，請參閱 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] 中的「最小值與最大值」。  
  
 如果 AUTOGROW 設為 ON，將允許複寫資料表成長至超出此限制。  
  
 當 AUTOGROW 設為 OFF 時，如果使用者嘗試建立新的複寫資料表、在現有的複寫資料表中插入資料，或更新現有的複寫資料表而導致大小增加至超出 *replicated_size*，便會傳回錯誤。  
  
 *distributed_size* [ GB ]  
 一個正數。 配置給「跨設備」分散式資料表 (和相對應資料) 的總空間大小 (以整數或小數 GB 為單位)。 對於最低和最高 *distributed_size* 需求，請參閱 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] 中的「最小值與最大值」。  
  
 如果 AUTOGROW 設為 ON，將允許分散式資料表成長至超出此限制。  
  
 當 AUTOGROW 設為 OFF 時，如果使用者嘗試建立新的分散式資料表、在現有的分散式資料表中插入資料，或更新現有的分散式資料表而導致大小增加至超出 *distributed_size*，便會傳回錯誤。  
  
 *log_size* [ GB ]  
 一個正數。 *跨設備*交易記錄的大小 (以整數或十進位 GB 為單位)。  
  
 對於最低和最高 *log_size* 需求，請參閱 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] 中的「最小值與最大值」。  
  
 如果 AUTOGROW 設為 ON，會允許記錄檔成長至超過此限制。 使用 [DBCC SHRINKLOG (Azure SQL 資料倉儲)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) 陳述式，將記錄檔大小縮小至其原始大小。  
  
 當 AUTOGROW 設為 OFF 時，如果出現會導致個別計算節點的記錄檔大小增加至超出 *log_size* 的任何動作，將會向使用者傳回錯誤。  
  
## <a name="permissions"></a>Permissions  
 需要 master 資料庫中的**建立任何資料庫**權限，或**系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
 下列範例會將建立資料庫的權限提供給資料庫使用者 Fay。  
  
```  
USE master;  
GO  
GRANT CREATE ANY DATABASE TO [Fay];  
GO  
```  
  
## <a name="general-remarks"></a>一般備註  
 建立資料庫時會使用資料庫相容性層級 120 建立，這是 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 的相容性層級。 這可確保資料庫將能使用 PDW 所使用的所有 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 功能。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 在明確的交易中，並不允許使用 CREATE DATABASE 陳述式。 如需詳細資訊，請參閱[陳述式](../../t-sql/statements/statements.md)。  
  
 如需資料庫最小和最大條件約束的資訊，請參閱 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)] 中的「最小值和最大值」。  
  
 建立資料庫時，「每個計算節點上」都必須有足夠的可用空間，以配置下列大小的總和：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的資料表大小為 *replicated_table_size*。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的資料表大小為 (*distributed_table_size* / 計算節點數目)。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會記錄 (*log_size* / 計算節點數目) 的大小。  
  
## <a name="locking"></a>鎖定  
 在 DATABASE 物件上採取共用鎖定。  
  
## <a name="metadata"></a>中繼資料  
 在這項作業成功之後，[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 和 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 中繼資料檢視中將會顯示此資料庫的項目。  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-basic-database-creation-examples"></a>A. 基本資料庫建立範例  
 以下範例會建立資料庫 `mytest`，其儲存區配置為每一計算節點具備 100 GB 以用於複寫資料表、每一設備 500 GB 以用於分散式資料表，以及每一設備 100 GB 以用於交易記錄。 在這個範例中，AUTOGROW 預設為關閉。  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB );  
```  
  
 以下範例會建立與上述參數相同的資料庫 `mytest`，但 AUTOGROW 已開啟。 這可以讓資料庫成長至超出指定的大小參數。  
  
```  
CREATE DATABASE mytest  
   WITH   
   (AUTOGROW = ON,  
   REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB);  
```  
  
### <a name="b-creating-a-database-with-partial-gigabyte-sizes"></a>B. 建立具備部分 GB 大小的資料庫  
 以下範例會建立 AUTOGROW 設為關閉的資料庫 `mytest`，其儲存區配置為每一計算節點具備 1.5 GB 以用於複寫資料表、每一設備 5.25 GB 以用於分散式資料表，以及每一設備 10 GB 以用於交易記錄，。  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 1.5 GB,  
   DISTRIBUTED_SIZE = 5.25 GB,  
   LOG_SIZE = 10 GB);  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;平行處理資料倉儲&#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
