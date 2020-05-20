---
title: sp_syscollector_run_collection_set （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 88b1cd8aaf95da010883faa7033c0bd6bf3cd2a5
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82809756"
---
# <a name="sp_syscollector_run_collection_set-transact-sql"></a>sp_syscollector_run_collection_set (Transact-SQL)
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
`[ @collection_set_id = ] collection_set_id`這是收集組的唯一本機識別碼。 *collection_set_id*是**int** ，而且如果*name*為 Null，則必須有值。  
  
`[ @name = ] 'name'`這是收集組的名稱。 *name*是**sysname** ，如果*collection_set_id*是 Null，則必須有值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 *Collection_set_id*或*名稱*都必須有值，兩者都不能是 Null。  
  
 這個程式會針對指定的收集組啟動收集和上傳作業，而且如果收集組的** \@ collection_mode**設定為非快取（1），就會立即啟動收集代理程式作業。 如需詳細資訊，請參閱[sp_syscollector_create_collection_set &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)。  
  
 sp_sycollector_run_collection_set 也可以用來執行沒有排程的收集組。  
  
## <a name="permissions"></a>權限  
 需要**dc_operator** （具有 EXECUTE 許可權）固定資料庫角色中的成員資格，才能執行此程式。  
  
## <a name="example"></a>範例  
 使用其識別碼來啟動收集組。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_run_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [資料收集](../../relational-databases/data-collection/data-collection.md)  
  
  
