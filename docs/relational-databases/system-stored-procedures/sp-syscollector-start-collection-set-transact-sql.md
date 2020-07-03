---
title: sp_syscollector_start_collection_set （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_start_collection_set_TSQL
- sp_syscollector_start_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_start_collection_set
ms.assetid: d8357180-f51e-4681-99f9-0596fe2d2b53
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 56fa6b114d58512f9cdec9c3da2575539af0d03b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892844"
---
# <a name="sp_syscollector_start_collection_set-transact-sql"></a>sp_syscollector_start_collection_set (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  如果收集器已經啟用而且收集組並未執行中，就會啟動收集組。 如果收集器未啟用，請執行[sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)來啟用收集器，然後使用這個預存程式來啟動收集組。  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syscollector_start_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @collection_set_id = ] collection_set_id`這是收集組的唯一本機識別碼。 *collection_set_id*是**int** ，預設值為 Null。 如果*name*為 Null， *collection_set_id*必須有值。  
  
`[ @name = ] 'name'`這是收集組的名稱。 *名稱*是**sysname** ，預設值是 Null。 如果*collection_set_id*為 Null，*名稱*就必須有值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 sp_syscollector_create_collection_set 必須在 msdb 系統資料庫的內容中執行，而且 SQL Server Agent 必須已啟用。  
  
 如果此程序是針對沒有排程的收集組來執行，此程序就會失敗。 如果收集組沒有排程（例如，其收集模式設定為非快取），請使用[sp_syscollector_run_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql.md)預存程式來啟動收集組。  
  
 這個程序會針對指定的收集組啟用收集和上傳作業，而且如果收集組將其收集模式設定為快取 (0)，此程序將立即啟動收集代理程式作業。 如需詳細資訊，請參閱[sp_syscollector_create_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)。  
  
 如果收集組未包含任何收集項，這項作業沒有任何作用。 就會傳回錯誤 14685 當做警告。  
  
## <a name="permissions"></a>權限  
 需要 dc_operator 固定資料庫角色中的成員資格，才能執行此程序。 如果收集組沒有 Proxy 帳戶，就需要系統管理員 (sysadmin) 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會開始一個收集組，其方式是使用此收集組的識別碼。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_start_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的資料收集器預存程式](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [資料收集](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
