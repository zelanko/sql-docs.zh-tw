---
title: sp_mergesubscription_cleanup & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergesubscription_cleanup
- sp_mergesubscription_cleanup_TSQL
helpviewer_keywords:
- sp_mergesubscription_cleanup
ms.assetid: bfad414f-2bda-4bf5-9507-56a1e743dfc4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e7f08abdc4cb7dccd148a55b8d4b0d5e05f21f93
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58532290"
---
# <a name="spmergesubscriptioncleanup-transact-sql"></a>sp_mergesubscription_cleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在移除中繼資料，觸發程序和項目，例如**sysmergesubscriptions**並**sysmergearticles**在發行者端移除指定的合併發送訂閱之後。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
> [!NOTE]  
>  對於提取訂閱移除中繼資料時[sp_dropmergepullsubscription &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)執行。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_mergesubscription_cleanup [ @publisher =] 'publisher'  
        , [ @publisher_db =] 'publisher_db'  
        , [ @publication =] 'publication'  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'` 是 「 發行者 」 的名稱。 *發行者*已**sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'` 是發行者資料庫的名稱。 *publisher_db*已**sysname**，沒有預設值。  
  
`[ @publication = ] 'publication'` 是發行集名稱。 *發行集*已**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_mergesubscription_cleanup**用於合併式複寫中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_mergesubscription_cleanup**。  
  
## <a name="see-also"></a>另請參閱  
 [刪除發送訂閱](../../relational-databases/replication/delete-a-push-subscription.md)   
 [sp_expired_subscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-expired-subscription-cleanup-transact-sql.md)   
 [sp_subscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
