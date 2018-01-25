---
title: "建立資料庫 (Parallel Data Warehouse) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 40cacde4-ac72-45f7-9564-d76e2b4a741a
caps.latest.revision: "13"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4e9ff76a4d260604a93f59baa3b61f5c37b4952f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="create-database-parallel-data-warehouse"></a>建立資料庫 (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  建立新的資料庫上[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]應用裝置。 若要建立的應用裝置資料庫相關聯的所有檔案，並設定最大的大小和資料庫資料表和交易記錄檔自動成長選項，請使用此陳述式。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 新資料庫的名稱。 如需允許的資料庫名稱的詳細資訊，請參閱 「 物件命名規則 」 和 「 保留的資料庫名稱 」 中[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 自動成長 = ON |**OFF**  
 指定是否*replicated_size*， *distributed_size*，和*log_size*參數，此資料庫會自動擴大超過其指定所需大小。 預設值是**OFF**。  
  
 如果自動成長是 ON， *replicated_size*， *distributed_size*，和*log_size*會成長為所需要的 （不在指定的初始大小的區塊） 的每個資料插入，已配置更新或需要更多的儲存空間，比其他動作。  
  
 如果自動成長是 OFF，大小不會自動成長。 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]嘗試的動作需要時，會傳回錯誤*replicated_size*， *distributed_size*，或*log_size*成長超過指定的值。  
  
 自動成長為各種規模的 ON 或 OFF，所有大小的。 例如，不可能設為自動成長 ON *log_size*，但未設定為*replicated_size*。  
  
 *replicated_size* [ GB ]  
 正數。 設定複寫的資料表和對應的資料配置的總空間的大小 （以整數或十進位 gb 為單位）*每個計算節點上*。 最小值和最大值為*replicated_size*需求，請參閱中的 「 最小和最大值 」 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 如果自動成長是 ON，將允許複寫的資料表成長超過這個限制。  
  
 如果自動成長是 OFF，將會的插入到現有的複寫資料的資料表，或更新現有使用者嘗試建立新的複寫的資料表時，如果複寫資料表的方式，將會增加的大小超過傳回錯誤*replicated_size*.  
  
 *distributed_size* [ GB ]  
 正數。 大小，以整數或十進位 （gb），配置給分散式的資料表 （和對應的資料） 的總空間*跨設備*。 最小值和最大值為*distributed_size*需求，請參閱中的 「 最小和最大值 」 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 如果自動成長是 ON，將允許分散式的資料表成長超過這個限制。  
  
 如果使用者嘗試建立新的分散式的資料表，將資料插入現有的分散式資料表，或更新現有的分散式的資料表將會增加的大小超過的方式，如果自動成長是 OFF 時，會傳回錯誤*distributed_size*.  
  
 *log_size* [ GB ]  
 正數。 交易記錄檔的大小 （以整數或十進位 gb 為單位）*跨設備*。  
  
 最小值和最大值為*log_size*需求，請參閱中的 「 最小和最大值 」 [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 如果自動成長為 ON 時，記錄檔可以成長超過這個限制。 使用[DBCC SHRINKLOG （Azure SQL 資料倉儲）](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)陳述式的記錄檔的大小減少回其原始大小。  
  
 如果自動成長是 OFF，將會傳回錯誤，會增加記錄大小超出個別計算節點上的任何動作的使用者*log_size*。  
  
## <a name="permissions"></a>Permissions  
 需要**CREATE ANY DATABASE**中 master 資料庫或成員資格的權限**sysadmin**固定的伺服器角色。  
  
 下列範例會將建立資料庫的權限提供給資料庫使用者 Fay。  
  
```  
USE master;  
GO  
GRANT CREATE ANY DATABASE TO [Fay];  
GO  
```  
  
## <a name="general-remarks"></a>一般備註  
 建立資料庫時資料庫相容性層級 120 的相容性層級[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。 這可確保資料庫將無法使用的所有[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]PDW 使用的功能。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 CREATE DATABASE 陳述式不允許在明確的交易。 如需詳細資訊，請參閱[陳述式](../../t-sql/statements/statements.md)。  
  
 最小和最大資料庫上的條件約束上的資訊，請參閱 「 最小和最大值 」，在[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
 建立資料庫時，必須有足夠的空間*每個計算節點上*配置以下幾種大小的總和：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫與資料表的大小*replicated_table_size*。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫與資料表的大小 (*distributed_table_size* / 計算節點的數字)。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]記錄檔的大小 (*log_size* / 計算節點的數字)。  
  
## <a name="locking"></a>鎖定  
 資料庫物件上採用共用的鎖定。  
  
## <a name="metadata"></a>中繼資料  
 這項作業成功，項目會顯示此資料庫之後[sys.databases &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)和[sys.objects &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)中繼資料檢視。  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-basic-database-creation-examples"></a>A. 基本資料庫建立範例  
 下列範例會建立資料庫`mytest`100 GB 的儲存體配置每個複寫的資料表、 500 GB，每個應用裝置分散式的資料表，和 100 GB，每個交易記錄檔的應用裝置的運算節點。 在此範例中，自動成長預設為關閉。  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB );  
```  
  
 下列範例會建立資料庫`mytest`與上述相同的參數，除了自動成長已開啟。 這可讓資料庫成長超出指定的大小參數。  
  
```  
CREATE DATABASE mytest  
   WITH   
   (AUTOGROW = ON,  
   REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB);  
```  
  
### <a name="b-creating-a-database-with-partial-gigabyte-sizes"></a>B. 建立部分 gb 大小的資料庫  
 下列範例會建立資料庫`mytest`，關閉自動成長，每個複寫資料表的計算節點的 1.5 GB、 5.25 GB，每個應用裝置分散式的資料表和每個交易記錄檔的應用裝置的 10 GB 的儲存體配置。  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 1.5 GB,  
   DISTRIBUTED_SIZE = 5.25 GB,  
   LOG_SIZE = 10 GB);  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;平行資料倉儲 &#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
