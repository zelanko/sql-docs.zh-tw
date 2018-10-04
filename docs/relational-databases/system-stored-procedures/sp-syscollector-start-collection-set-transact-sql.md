---
title: sp_syscollector_start_collection_set (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: de6aff356e5de49802f0bc2813ff481bd45244c8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47803796"
---
# <a name="spsyscollectorstartcollectionset-transact-sql"></a>sp_syscollector_start_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  如果收集器已經啟用而且收集組並未執行中，就會啟動收集組。 如果未啟用收集器，收集器執行啟用[sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)然後使用這個預存程序啟動收集組。  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syscollector_start_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>引數  
 [ **@collection_set_id =** ] *collection_set_id*  
 這是收集組的唯一本機識別碼。 *collection_set_id&lt*已**int**預設值是 NULL。 *collection_set_id&lt*必須有值，如果*名稱*是 NULL。  
  
 [ **@name =** ] '*name*'  
 這是收集組的名稱。 *名稱*已**sysname**預設值是 NULL。 *名稱*必須有值，如果*collection_set_id&lt*是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 sp_syscollector_create_collection_set 必須在 msdb 系統資料庫的內容中執行，而且 SQL Server Agent 必須已啟用。  
  
 如果此程序是針對沒有排程的收集組來執行，此程序就會失敗。 如果收集組沒有排程 （因為其收集模式設定為非快取，例如），請使用[sp_syscollector_run_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql.md)預存程序啟動收集組。  
  
 這個程序會針對指定的收集組啟用收集和上傳作業，而且如果收集組將其收集模式設定為快取 (0)，此程序將立即啟動收集代理程式作業。 如需詳細資訊，請參閱 < [sp_syscollector_create_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)。  
  
 如果收集組未包含任何收集項，這項作業沒有任何作用。 就會傳回錯誤 14685 當做警告。  
  
## <a name="permissions"></a>Permissions  
 需要 dc_operator 固定資料庫角色中的成員資格，才能執行此程序。 如果收集組沒有 Proxy 帳戶，就需要系統管理員 (sysadmin) 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會開始一個收集組，其方式是使用此收集組的識別碼。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_start_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料收集器預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [資料收集](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
