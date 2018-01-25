---
title: "ALTER DATABASE (Parallel Data Warehouse) |Microsoft 文件"
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
ms.assetid: 5751656b-7aae-4152-a314-4c631bea4fc4
caps.latest.revision: "10"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7db44d9c9f02618e4d95a9d3eb9dfc581438dea5
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="alter-database-parallel-data-warehouse"></a>ALTER DATABASE (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  修改複寫的資料表、 分散式的資料表和交易記錄檔中的最大資料庫大小選項[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。 使用此陳述式來管理資料庫的磁碟空間配置，因為它放大或縮小的大小。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 要修改的資料庫名稱。 若要顯示應用裝置上的資料庫清單，請使用[sys.databases &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
 自動成長 = {ON |OFF}  
 更新的自動成長選項。 自動成長是 ON，當[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]自動視適應儲存需求成長會增加複寫的資料表、 分散式的資料表，以及交易記錄檔已配置的空間。 自動成長是 OFF，當[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]傳回錯誤，如果複寫的資料表，散發資料表，或交易記錄超過大小上限設定。  
  
 REPLICATED_SIZE = *size* [GB]  
 指定新的上限 （gb） 每個要改變的資料庫中儲存所有的複寫資料表的計算節點。 如果您計劃應用裝置儲存空間，您必須 REPLICATED_SIZE 乘以應用裝置中的運算節點數目。  
  
 DISTRIBUTED_SIZE = *size* [GB]  
 指定新的上限 （gb） 每個資料庫的更動在資料庫中儲存的所有分散式資料表。 大小會分佈在所有的應用裝置中的計算節點。  
  
 LOG_SIZE = *size* [GB]  
 指定新的上限 （gb） 每個資料庫的更動在資料庫中儲存的所有交易記錄檔。 大小會分佈在所有的應用裝置中的計算節點。  
  
 加密 {ON |OFF}  
 設定資料庫要加密 (ON) 或是不要加密 (OFF)。 加密只能設定為[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]時[sp_pdw_database_encryption](http://msdn.microsoft.com/5011bb7b-1793-4b2b-bd9c-d4a8c8626b6e)已設定為**1**。 必須先建立資料庫加密金鑰，您可以設定透明資料加密。 如需有關資料庫加密的詳細資訊，請參閱[透明資料加密 &#40;TDE &#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 ALTER 權限。  
  
## <a name="general-remarks"></a>一般備註  
 REPLICATED_SIZE、 DISTRIBUTED_SIZE 和 LOG_SIZE 的值可以是大於、 等於或小於資料庫的目前值。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 成長和壓縮作業是近似值。 產生的實際大小而異的大小參數。  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]不會執行 ALTER DATABASE 陳述式，成為不可部分完成的作業。 如果陳述式會中止執行期間，已發生的變更將會保留。  
  
## <a name="locking-behavior"></a>鎖定行為  
 資料庫物件上採用共用的鎖定。 您無法改變正在使用另一位使用者進行讀取或寫入資料庫。 這包括已發行的工作階段[使用](http://msdn.microsoft.com/158ec56b-b822-410f-a7c4-1a196d4f0e15)在資料庫上的陳述式。  
  
## <a name="performance"></a>效能  
 壓縮資料庫可能需要大量的時間與系統資源，在資料庫中的實際資料大小而定，在磁碟上片段的數量。 例如，壓縮資料庫可能需要許多小時以上。  
  
## <a name="determining-encryption-progress"></a>判斷加密進度  
 您可以使用下列查詢來判斷資料庫透明資料加密，以百分比表示進度：  
  
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
  
 如需示範中實作 TDE 的所有步驟的完整範例，請參閱[透明資料加密 &#40;TDE &#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-altering-the-autogrow-setting"></a>A. 修改自動成長設定  
 資料庫自動成長設定為 ON `CustomerSales`。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( AUTOGROW = ON );  
```  
  
### <a name="b-altering-the-maximum-storage-for-replicated-tables"></a>B. 改變複寫的資料表的最大儲存體  
 下列範例設定設為 1 GB 的資料庫複寫的資料表儲存體限制`CustomerSales`。 這是每個計算節點的儲存體限制。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( REPLICATED_SIZE = 1 GB );  
```  
  
### <a name="c-altering-the-maximum-storage-for-distributed-tables"></a>C. 改變分散式資料表最大儲存體  
 下列範例設定分散式的資料表儲存體限制為 1000 GB (1 tb) 資料庫`CustomerSales`。 這是合併的儲存體限制設備所有計算節點，不要儲存體限制每個計算節點。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( DISTRIBUTED_SIZE = 1000 GB );  
```  
  
### <a name="d-altering-the-maximum-storage-for-the-transaction-log"></a>D. 改變的交易記錄檔的最大儲存體  
 下列範例會更新資料庫`CustomerSales`最多可以擁有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]10 GB 的 」 應用裝置中的交易記錄大小。  
  
```  
ALTER DATABASE CustomerSales  
    SET ( LOG_SIZE = 10 GB );  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立資料庫 &#40;平行資料倉儲 &#41;](../../t-sql/statements/create-database-parallel-data-warehouse.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
