---
title: sp_syscollector_create_collection_item （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_create_collection_item
- sp_syscollector_create_collection_item_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_create_collection_item
- data collector [SQL Server], stored procedures
ms.assetid: 60dacf13-ca12-4844-b417-0bc0a8bf0ddb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: dc35ba06f17b3b067e3b7ba9059c27e1f6db2d18
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892971"
---
# <a name="sp_syscollector_create_collection_item-transact-sql"></a>sp_syscollector_create_collection_item (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  建立使用者定義之收集組內的收集項。 收集項會定義要收集的資料以及資料收集的頻率。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syscollector_create_collection_item   
      [ @collection_set_id = ] collection_set_id   
    , [ @collector_type_uid = ] 'collector_type_uid'  
    , [ @name = ] 'name'   
    , [ [ @frequency = ] frequency ]  
    , [ @parameters = ] 'parameters'  
    , [ @collection_item_id = ] collection_item_id OUTPUT  
```  
  
## <a name="arguments"></a>引數  
 [ @collection_set_id =] *collection_set_id*  
 這是收集組的唯一本機識別碼。 *collection_set_id*為**int**。  
  
 [ @collector_type_uid =] '*collector_type_uid*'  
 是識別要用於此專案之收集器型別的 GUID *collector_type_uid*是不含預設值的**uniqueidentifier** 。 如需收集器型別的清單，請查詢 syscollector_collector_types 系統檢視表。  
  
 [ @name =] '*name*'  
 這是收集項目的名稱。 *名稱*是**sysname** ，不能是空字串或 Null。  
  
 *名稱*必須是唯一的。 如需目前的收集項名稱清單，請查詢 syscollector_collection_items 系統檢視表。  
  
 [ @frequency =]*頻率*  
 這可用來指定此收集項收集資料的頻率 (以秒為單位)。 *frequency*是**int**，預設值是5。 可指定的最小值是 5 秒。  
  
 如果收集組設定為非快取模式，系統就會忽略此頻率，因為這個模式會導致在針對收集組指定的排程中同時發生資料收集和上傳作業。 若要查看收集組的收集模式，請查詢[syscollector_collection_sets](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)系統檢視。  
  
 [ @parameters =] '*parameters*'  
 收集器類型的輸入參數。 *參數*是**xml** ，預設值是 Null。 *參數*架構必須符合收集器型別的參數架構。  
  
 [ @collection_item_id =] *collection_item_id*  
 這是可識別收集組項目的唯一識別碼。 *collection_item_id*為**int** ，且具有輸出。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 sp_syscollector_create_collection_item 必須在 msdb 系統資料庫的內容中執行。  
  
 加入收集項的目標收集組必須先停止後，才能建立收集項。 收集項不能加入至系統收集組中。  
  
## <a name="permissions"></a>權限  
 需要 dc_admin (具有 EXECUTE 權限) 固定資料庫角色中的成員資格，才能執行此程序。  
  
## <a name="examples"></a>範例  
 下列範例會根據 `Generic T-SQL Query Collector Type` 收集類型來建立收集項，然後將它加入至名為 `Simple collection set test 2` 的收集組。 若要建立指定的收集組，請在[sp_syscollector_create_collection_set &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)中執行範例 B。  
  
```  
USE msdb;  
GO  
DECLARE @collection_item_id int;  
DECLARE @collection_set_id int = (SELECT collection_set_id   
                                  FROM syscollector_collection_sets  
                                  WHERE name = N'Simple collection set test 2');  
DECLARE @collector_type_uid uniqueidentifier =   
    (SELECT collector_type_uid  
     FROM syscollector_collector_types  
     WHERE name = N'Generic T-SQL Query Collector Type');  
DECLARE @params xml =   
    CONVERT(xml, N'\<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
            <Query>  
                <Value>SELECT * FROM sys.objects</Value>  
                <OutputTable>MyOutputTable</OutputTable>  
            </Query>  
            <Databases>   
                <Database> UseSystemDatabases = "true"   
                           UseUserDatabases = "true"  
                </Database>  
            </Databases>  
         \</ns:TSQLQueryCollector>');  
  
EXEC sp_syscollector_create_collection_item  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = @collector_type_uid,  
    @name = 'My custom TSQL query collector item',  
    @frequency = 6000,  
    @parameters = @params,  
    @collection_item_id = @collection_item_id OUTPUT;  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [資料收集](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_update_collection_item &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql.md)   
 [sp_syscollector_delete_collection_item &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql.md)   
 [syscollector_collector_types &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)   
 [sp_syscollector_create_collection_set &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)   
 [syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)  
  
  
