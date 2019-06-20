---
title: sp_syscollector_run_collection_set (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_run_collection_set_TSQL
- sp_syscollector_run_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_run_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 7bbaee48-dfc7-45c0-b11f-c636b6a7e720
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e2ad81b1d92bb45d9ab15ca11897804cc0d333a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63001751"
---
# <a name="spsyscollectorruncollectionset-transact-sql"></a>sp_syscollector_run_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  如果收集器已經啟用，而且已針對非快取收集模式設定收集組，就會啟動此收集組。  
  
> [!NOTE]  
>  如果它是針對快取收集模式而設定的收集組來執行，此程序就會失敗。  
  
 sp_syscollector_run_collection_set 可讓使用者取得視需要之資料的快照集。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syscollector_run_collection_set [[ @collection_set_id = ] collection_set_id ]  
          , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @collection_set_id = ] collection_set_id` 是此收集組的唯一本機識別碼。 *collection_set_id&lt*已**int**而且必須具有值，如果*名稱*是 NULL。  
  
`[ @name = ] 'name'` 是收集組的名稱。 *名稱*已**sysname**而且必須具有值，如果*collection_set_id&lt*是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 任一*collection_set_id&lt*或是*名稱*必須具有值，兩者都不能是 NULL。  
  
 此程序會開始收集和上傳作業，針對指定的集合設定，並將在此收集組是否立即啟動收集代理程式作業及其 **@collection_mode** 設為非快取 (1)。 如需詳細資訊，請參閱[sp_syscollector_create_collection_set &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)。  
  
 sp_sycollector_run_collection_set 也可以用來執行沒有排程的收集組。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**dc_operator** （具有 EXECUTE 權限） 固定的資料庫角色，才能執行此程序。  
  
## <a name="example"></a>範例  
 使用其識別碼來啟動收集組。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_run_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [[資料收集]](../../relational-databases/data-collection/data-collection.md)  
  
  
