---
description: sp_dropmergefilter (Transact-SQL)
title: sp_dropmergefilter (Transact-sql) |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5eb42c423d562ad251dc55ce015fdd111fa7d6fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464333"
---
# <a name="sp_dropmergefilter-transact-sql"></a>sp_dropmergefilter (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  卸除合併篩選。 **sp_dropmergefilter** 會卸載要卸載的合併篩選所定義的所有合併篩選資料行。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropmergefilter [ @publication= ] 'publication', [ @article= ] 'article'     , [ @filtername= ] 'filtername'  
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是發行集的名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @article = ] 'article'` 這是發行項的名稱。 *文章* 是 **sysname**，沒有預設值。  
  
`[ @filtername = ] 'filtername'` 這是要卸載的篩選名稱。 *filtername* 是 **sysname**，沒有預設值。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 啟用或停用使快照集失效的能力。 *force_invalidate_snapshot* 是 **bit**，預設值是 **0**。  
  
 **0** 指定合併發行項的變更不會使快照集失效。  
  
 **1** 表示合併發行項的變更可能會導致快照集無效。 如果是這種情況，值 **1** 就會提供要發生之新快照集的許可權。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` 啟用或停用將訂用帳戶標示為不正確能力。 *force_reinit_subscription* 是 **bit**，預設值是 **0**。  
  
 **0** 指定合併發行項篩選的變更不會使訂閱失效。  
  
 **1** 表示合併發行項篩選的變更會導致訂閱無效。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_dropmergefilter** 用於合併式複寫中。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_dropmergefilter**。  
  
## <a name="see-also"></a>另請參閱  
 [變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergefilter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_changemergefilter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_helpmergefilter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
