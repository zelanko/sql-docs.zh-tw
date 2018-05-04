---
title: sp_expired_subscription_cleanup (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_expired_subscription_cleanup
- SP_EXPIRED_SUBSCRIPTION_CLEANUP_TSQL
helpviewer_keywords:
- sp_expired_subscription_cleanup
ms.assetid: 6abc29fe-d77a-4673-9d99-ae31c688012c
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 817a4e98fd8e6efdbbd38020a6ce54858d6a3ac8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spexpiredsubscriptioncleanup-transact-sql"></a>sp_expired_subscription_cleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  檢查每個發行集之所有訂閱的狀態，以及卸除已過期的訂閱。 這個預存程序執行於任何資料庫的發行者上，或為非散發資料庫的散發者端[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_expired_subscription_cleanup [ [ @publisher = ] 'publisher' ]   
```  
  
## <a name="arguments"></a>引數  
 [  **@publisher=** ] **'***發行者***'**  
 這是非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者的名稱。 *發行集*是**sysname**，預設值是 NULL。 您不應該將這個參數指定給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_expired_subscription_cleanup**用於所有複寫類型。  
  
 **sp_expired_subscription_cleanup**偵測並移除逾期的訂閱發行集資料庫中每隔 24 小時到期訂閱清除作業執行。 如果有任何訂閱過期，也就是說，未在保留期限內與發行者同步處理，就會將發行集宣告為過期，且會在發行者端清除訂閱追蹤。 如需詳細資訊，請參閱 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_expired_subscription_cleanup**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_mergesubscription_cleanup &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md)   
 [sp_subscription_cleanup &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
