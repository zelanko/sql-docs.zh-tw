---
title: "sp_subscription_cleanup (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_subscription_cleanup_TSQL
- sp_subscription_cleanup
helpviewer_keywords: sp_subscription_cleanup
ms.assetid: bdc8aaa0-ff2d-40c2-84b2-4ba513ced279
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4867466ac5c45411851f601349454733697abf25
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spsubscriptioncleanup-transact-sql"></a>sp_subscription_cleanup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在訂閱者端卸除訂閱時，移除中繼資料。 如果是同步處理中的交易訂閱，它也會包括立即更新觸發程序。 這個預存程序執行於訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_subscription_cleanup [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
    [ , [ @publication = ] 'publication']  
    [ , [ @reserved = ] 'reserved']  
```  
  
## <a name="arguments"></a>引數  
 [  **@publisher=**] **'***發行者***'**  
 這是發行者的名稱。 *發行者*是**sysname**，沒有預設值。  
  
 [  **@publisher_db=**] **'***publisher_db***'**  
 這是發行者資料庫的名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
 [  **@publication=**] **'***發行集***'**  
 這是發行集的名稱。 *發行集*是**sysname**，預設值是 NULL。 如果是 NULL，就會刪除使用發行資料庫中之共用代理程式發行集的訂閱。  
  
 [  **@reserved=**] **'***保留***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_subscription_cleanup**用於交易式和快照式複寫中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_subscription_cleanup**。  
  
## <a name="see-also"></a>請參閱＜  
 [sp_expired_subscription_cleanup &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-expired-subscription-cleanup-transact-sql.md)   
 [sp_mergesubscription_cleanup &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
