---
title: ALTER DATABASE (平行處理資料倉儲) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5751656b-7aae-4152-a314-4c631bea4fc4
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3d199b9822d591c10f1f4d9af232b9f74d7e8a81
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
---
# <a name="alter-database-parallel-data-warehouse"></a>ALTER DATABASE (平行處理資料倉儲)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  修改適用於[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]中的複寫資料表、分散式資料表和交易記錄的資料庫大小上限選項。 在資料庫的大小成長或壓縮時，使用此陳述式來管理它的磁碟空間配置。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Parallel Data Warehouse  
ALTER DATABASE database_name    
    SET ( <set_database_options>   | <db_encryption_option> )  
[;]  
  
<set_database_options> ::=   
{  
    AUTOGROW = { ON | OFF }  
    | REPLICATED_SIZE = size [GB]  
    | DISTRIBUTED_SIZE = size [GB]  
    | LOG_SIZE = size [GB]  
}  
  
<db_encryption_option> ::=  
    ENCRYPTION { ON | OFF }  
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 要修改之資料庫的名稱。 若要顯示設備上之資料庫的清單，請使用 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。  
  
 AUTOGROW = { ON | OFF }  
 更新 AUTOGROW 選項。 當 AUTOGROW 為 ON 時，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]會視需要針對複寫資料表、分散式資料表及交易記錄自動提高配置的空間，以適應儲存空間需求的增長。 當 AUTOGROW 為 OFF 時，如果複寫資料表、分散式資料表或交易記錄超過大小上限設定，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]就會傳回錯誤。  
  
 REPLICATED_SIZE = *size* [GB]  
 指定每個計算節點的新 GB 上限，以用來儲存要改變之資料庫中的所有複寫資料表。 如果您正在規劃設備儲存空間，就必須將 REPLICATED_SIZE 乘以設備中計算節點的數目。  
  
 DISTRIBUTED_SIZE = *size* [GB]  
 指定每個資料庫的新 GB 上限，以用來儲存要改變之資料庫中的所有分散式資料表。 此大小會分佈於設備中的所有計算節點上。  
  
 LOG_SIZE = *size* [GB]  
 指定每個資料庫的新 GB 上限，以用來儲存要改變之資料庫中的所有交易記錄。 此大小會分佈於設備中的所有計算節點上。  
  
 ENCRYPTION { ON | OFF }  
 設定資料庫要加密 (ON) 或是不要加密 (OFF)。 只有在將 [sp_pdw_database_encryption](http://msdn.microsoft.com/5011bb7b-1793-4b2b-bd9c-d4a8c8626b6e) \(英文\) 設為 **1** 時，才能針對[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]設定加密。 您必須先建立資料庫加密金鑰，才能設定透明資料加密。 如需資料庫加密的詳細資訊，請參閱[透明資料加密 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)。  
  
## <a name="permissions"></a>Permissions  
 需要資料庫上的 ALTER 權限。  
  
## <a name="general-remarks"></a>一般備註  
 REPLICATED_SIZE、DISTRIBUTED_SIZE 和 LOG_SIZE 的值可以大於、等於或小於資料庫的目前值。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 成長和壓縮作業很近似。 產生的實際大小會因大小參數而異。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]不會以不可部分完成之作業的形式來執行 ALTER DATABASE 陳述式。 如果陳述式在執行期間中止，系統將會保留已發生的變更。  
  
## <a name="locking-behavior"></a>鎖定行為  
 在 DATABASE 物件上採取共用鎖定。 您無法改變有另一個使用者正在讀取或寫入的資料庫。 這包括已在資料庫上發出 [USE](http://msdn.microsoft.com/158ec56b-b822-410f-a7c4-1a196d4f0e15) \(英文\) 陳述式的工作階段。  
  
## <a name="performance"></a>效能  
 根據資料庫內實際資料的大小及磁碟上的片段程度而定，壓縮資料庫可能需要大量的時間與系統資源。 例如，壓縮資料庫可能需要數小時以上的時間。  
  
## <a name="determining-encryption-progress"></a>判斷加密進度  
 使用下列查詢來判斷資料庫透明資料加密的進度 (以百分比表示)：  
  
```  
WITH  
database_dek AS (  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id,  
        dek.encryption_state, dek.percent_complete,  
        dek.key_algorithm, dek.key_length, dek.encryptor_thumbprint,  
        type  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
    INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
        ON dek.database_id = node_db_map.database_id   
        AND dek.pdw_node_id = node_db_map.pdw_node_id  
    LEFT JOIN sys.pdw_database_mappings AS db_map  
        ON node_db_map .physical_name = db_map.physical_name  
    INNER JOIN sys.dm_pdw_nodes nodes  
        ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
),  
dek_percent_complete AS (  
    SELECT database_dek.database_id, AVG(database_dek.percent_complete) AS percent_complete  
    FROM database_dek  
    WHERE type = 'COMPUTE'  
    GROUP BY database_dek.database_id  
)  
SELECT DB_NAME( database_dek.database_id ) AS name,  
    database_dek.database_id,  
    ISNULL(  
       (SELECT TOP 1 dek_encryption_state.encryption_state  
        FROM database_dek AS dek_encryption_state  
        WHERE dek_encryption_state.database_id = database_dek.database_id  
        ORDER BY (CASE encryption_state  
            WHEN 3 THEN -1  
            ELSE encryption_state  
            END) DESC), 0)  
        AS encryption_state,  
dek_percent_complete.percent_complete,  
database_dek.key_algorithm, database_dek.key_length, database_dek.encryptor_thumbprint  
FROM database_dek  
INNER JOIN dek_percent_complete   
    ON dek_percent_complete.database_id = database_dek.database_id  
WHERE type = 'CONTROL';  
```  
  
 如需示範實作 TDE 之所有步驟的完整範例，請參閱[透明資料加密 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)。  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-altering-the-autogrow-setting"></a>A. 改變 AUTOGROW 設定  
 針對 `CustomerSales` 資料庫，將 AUTOGROW 設為 ON。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( AUTOGROW = ON );  
```  
  
### <a name="b-altering-the-maximum-storage-for-replicated-tables"></a>B. 改變複寫資料表的儲存空間上限  
 下列範例會針對 `CustomerSales` 資料庫，將複寫資料表儲存空間限制設為 1 GB。 這是每個計算節點的儲存空間限制。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( REPLICATED_SIZE = 1 GB );  
```  
  
### <a name="c-altering-the-maximum-storage-for-distributed-tables"></a>C. 改變分散式資料表的儲存空間上限  
 下列範例會針對 `CustomerSales` 資料庫，將分散式資料表儲存空間限制設為 1000 GB (1 TB)。 這是設備上所有計算節點的組合儲存空間限制，而非每個計算節點的儲存空間限制。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( DISTRIBUTED_SIZE = 1000 GB );  
```  
  
### <a name="d-altering-the-maximum-storage-for-the-transaction-log"></a>D. 改變交易記錄的儲存空間上限  
 下列範例會更新 `CustomerSales` 資料庫，使其可在設備上擁有最多 10 GB 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 交易記錄大小。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( LOG_SIZE = 10 GB );  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE DATABASE &#40;平行處理資料倉儲&#41;](../../t-sql/statements/create-database-parallel-data-warehouse.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
