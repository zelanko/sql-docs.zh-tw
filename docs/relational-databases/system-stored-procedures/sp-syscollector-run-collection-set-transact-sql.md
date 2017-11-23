---
title: "sp_syscollector_run_collection_set (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_syscollector_run_collection_set_TSQL
- sp_syscollector_run_collection_set
dev_langs: TSQL
helpviewer_keywords:
- sp_syscollector_run_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 7bbaee48-dfc7-45c0-b11f-c636b6a7e720
caps.latest.revision: "9"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ca014293d64b0782d4844794efb5528849d0ecf9
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="spsyscollectorruncollectionset-transact-sql"></a>sp_syscollector_run_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  如果收集器已經啟用，而且已針對非快取收集模式設定收集組，就會啟動此收集組。  
  
> [!NOTE]  
>  如果它是針對快取收集模式而設定的收集組來執行，此程序就會失敗。  
  
 sp_syscollector_run_collection_set 可讓使用者取得視需要之資料的快照集。  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_syscollector_run_collection_set [[ @collection_set_id = ] collection_set_id ]  
          , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>引數  
 [  **@collection_set_id =** ] *collection_set_id*  
 這是收集組的唯一本機識別碼。 *collection_set_id*是**int**而且必須具有值，如果*名稱*是 NULL。  
  
 [  **@name =** ] **'***名稱***'**  
 這是收集組的名稱。 *名稱*是**sysname**而且必須具有值，如果*collection_set_id*是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 任一*collection_set_id*或*名稱*必須有值，不能同時為 NULL。  
  
 此程序會啟動收集和上傳作業指定的集合設定，和將在收集組是否立即啟動收集代理程式作業及其 **@collection_mode** 設為 非快取 (1)。 如需詳細資訊，請參閱[sp_syscollector_create_collection_set &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md).  
  
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
  
## <a name="see-also"></a>請參閱＜  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [[資料收集]](../../relational-databases/data-collection/data-collection.md)  
  
  
