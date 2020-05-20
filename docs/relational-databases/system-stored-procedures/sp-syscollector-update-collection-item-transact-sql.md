---
title: sp_syscollector_update_collection_item （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collection_item
- sp_syscollector_update_collection_item_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_update_collection_item
ms.assetid: 7a0d36c8-c6e9-431d-a5a4-6c1802bce846
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e14f60cb3e1a4493e58968913a3ae840625e190f
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828212"
---
# <a name="sp_syscollector_update_collection_item-transact-sql"></a>sp_syscollector_update_collection_item (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  用來修改使用者定義之收集項的屬性，或是用來重新命名使用者定義的收集項。  
  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syscollector_update_collection_item   
      [ [ @collection_item_id = ] collection_item_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @new_name = ] 'new_name' ]  
    , [ [ @frequency = ] frequency ]  
    , [ [ @parameters = ] 'parameters' ]  
```  
  
## <a name="arguments"></a>引數  
 [ @collection_item_id =] *collection_item_id*  
 這是識別收集項的唯一識別碼。 *collection_item_id*是**int** ，預設值為 Null。 如果*name*為 Null， *collection_item_id*必須有值。  
  
 [ @name =] '*name*'  
 這是收集項目的名稱。 *名稱*是**sysname** ，預設值是 Null。 如果*collection_item_id*為 Null，*名稱*就必須有值。  
  
 [ @new_name =] '*new_name*'  
 這是收集項的新名稱。 *new_name*是**sysname**，而且如果使用的話，不可以是空字串。  
  
 *new_name*必須是唯一的。 如需目前的收集項名稱清單，請查詢 syscollector_collection_items 系統檢視表。  
  
 [ @frequency =]*頻率*  
 這是此收集項收集資料的頻率 (以秒為單位)。 *frequency*是**int**，預設值是5，這是可指定的最小值。  
  
 [ @parameters =] '*parameters*'  
 收集項的輸入參數。 *參數*是**xml** ，預設值是 Null。 *參數*架構必須符合收集器型別的參數架構。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或1（失敗）  
  
## <a name="remarks"></a>備註  
 如果收集組設定為非快取模式，系統就會忽略變更此頻率，因為這個模式會導致在針對收集組指定的排程中同時發生資料收集和上傳作業。 若要檢視收集組的狀態，請執行下列查詢。 使用要更新之收集項的識別碼取代 `<collection_item_id>`。  
  
```  
USE msdb;  
GO  
SELECT cs.collection_set_id, collection_set_uid, cs.name   
    ,'is running' = CASE WHEN is_running =  0 THEN 'No' ELSE 'Yes' END  
    ,'cache mode' = CASE WHEN collection_mode = 0 THEN 'Cached mode' ELSE 'Non-cached mode' END  
FROM syscollector_collection_sets AS cs  
JOIN syscollector_collection_items AS ci   
ON ci.collection_set_id = cs.collection_set_id  
WHERE collection_item_id = <collection_item_id>;  
```  
  
## <a name="permissions"></a>權限  
 需要 dc_admin 或 dc_operator (具有 EXECUTE 權限) 固定資料庫角色中的成員資格，才能執行此程序。 雖然 dc_operator 可以執行此預存程序，但是這個角色的成員會受限於他們可以變更的屬性。 下列屬性只能由 dc_admin 變更：  
  
-   @new_name  
  
-   @parameters  
  
## <a name="examples"></a>範例  
 下列範例是根據[sp_syscollector_create_collection_item &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)中定義的範例所建立的收集項。  
  
### <a name="a-changing-the-collection-frequency"></a>A. 變更收集頻率  
 下列範例會針對指定的收集項變更收集頻率。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@name = N'My custom TSQL query collector item',  
@frequency = 3000;  
GO  
```  
  
### <a name="b-renaming-a-collection-item"></a>B. 重新命名收集項  
 下列範例會重新命名收集項。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@name = N'My custom TSQL query collector item',  
@new_name = N'My modified TSQL item';  
GO  
```  
  
### <a name="c-changing-the-parameters-of-a-collection-item"></a>C. 變更收集項的參數  
 下列範例會變更與收集項有關聯的參數。 `<Value>` 屬性內定義的陳述式會變更，而且 `UseSystemDatabases` 屬性會設定為 false。 若要檢視這個項目的目前參數，請查詢 syscollector_collection_items 系統檢視表中的參數資料行。 您可能需要修改 `@collection_item_id` 的值。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_update_collection_item   
@collection_item_id = 9,   
@parameters = '  
    \<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
        <Query>  
            <Value>SELECT * FROM sys.dm_db_index_usage_stats</Value>  
            <OutputTable>MyOutputTable</OutputTable>  
        </Query>  
        <Databases>  
            <Database> UseSystemDatabases = "false"   
                       UseUserDatabases = "true"</Database>  
        </Databases>  
    \</ns:TSQLQueryCollector>';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [資料收集](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_create_collection_item &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)   
 [syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)  
  
  
