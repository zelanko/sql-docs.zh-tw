---
description: sp_expired_subscription_cleanup (Transact-SQL)
title: sp_expired_subscription_cleanup (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_expired_subscription_cleanup
- SP_EXPIRED_SUBSCRIPTION_CLEANUP_TSQL
helpviewer_keywords:
- sp_expired_subscription_cleanup
ms.assetid: 6abc29fe-d77a-4673-9d99-ae31c688012c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f01368f50ce4a7a6116f58bfedee187648a8302d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474239"
---
# <a name="sp_expired_subscription_cleanup-transact-sql"></a>sp_expired_subscription_cleanup (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  檢查每個發行集之所有訂閱的狀態，以及卸除已過期的訂閱。 這個預存程式會在任何資料庫的發行者上執行，或在非發行者的散發資料庫的散發者端執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_expired_subscription_cleanup [ [ @publisher = ] 'publisher' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'` 這是非發行者的名稱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 *發行* 集是 **sysname**，預設值是 Null。 您不應該將這個參數指定給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_expired_subscription_cleanup** 用於所有類型的複寫中。  
  
 過期的訂閱清除作業會執行**sp_expired_subscription_cleanup** ，以每隔24小時偵測和移除發行集資料庫中到期的訂閱。 如果有任何訂閱過期，也就是說，未在保留期限內與發行者同步處理，就會將發行集宣告為過期，且會在發行者端清除訂閱追蹤。 如需詳細資訊，請參閱 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_expired_subscription_cleanup**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_mergesubscription_cleanup &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md)   
 [sp_subscription_cleanup &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
