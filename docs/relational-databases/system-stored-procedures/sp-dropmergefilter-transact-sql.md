---
title: sp_dropmergefilter (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergefilter_TSQL
- sp_dropmergefilter
helpviewer_keywords:
- sp_dropmergefilter
ms.assetid: 798586d7-05f3-4a5e-bea8-a34b7b52d0fd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 76d83e2d36307280249ccd886c464e8cd484c296
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533220"
---
# <a name="spdropmergefilter-transact-sql"></a>sp_dropmergefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  卸除合併篩選。 **sp_dropmergefilter**卸除要卸除合併篩選所定義的所有合併篩選資料行。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropmergefilter [ @publication= ] 'publication', [ @article= ] 'article'     , [ @filtername= ] 'filtername'  
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 是發行集名稱。 *發行集*已**sysname**，沒有預設值。  
  
`[ @article = ] 'article'` 是發行項的名稱。 *發行項*已**sysname**，沒有預設值。  
  
`[ @filtername = ] 'filtername'` 是要卸除的篩選器的名稱。 *filtername*已**sysname**，沒有預設值。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 啟用或停用使快照集失效的能力。 *force_invalidate_snapshot*已**位元**，預設值**0**。  
  
 **0**指定合併發行項的變更不會使快照集失效。  
  
 **1**表示合併發行項的變更可能使快照集失效。 如果這種情況下，值為**1**提供將出現新的快照集的權限。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` 啟用或停用將標示為無效的訂用帳戶的能力。 *force_reinit_subscription*已**位元**，預設值**0**。  
  
 **0**指定合併發行項篩選的變更不會使訂閱失效。  
  
 **1**表示合併發行項篩選的變更可能使訂閱失效。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_dropmergefilter**用於合併式複寫中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_dropmergefilter**。  
  
## <a name="see-also"></a>另請參閱  
 [變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_changemergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_helpmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
