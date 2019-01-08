---
title: sp_droppullsubscription & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_droppullsubscription
- sp_droppullsubscription_TSQL
helpviewer_keywords:
- sp_droppullsubscription
ms.assetid: 7352d94a-f8f2-42ea-aaf1-d08c3b5a0e76
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d8d796c5e7b309ef33bf30eba851b3aedb6c1e6b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52823932"
---
# <a name="spdroppullsubscription-transact-sql"></a>sp_droppullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在訂閱者的目前資料庫卸除訂閱。 這個預存程序執行於提取訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_droppullsubscription [ @publisher= ] 'publisher'  
        , [ @publisher_db= ] 'publisher_db'  
        , [ @publication= ] 'publication'  
    [ , [ @reserved= ] reserved ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@publisher=** ] **'***發行者***'**  
 這是遠端伺服器的名稱。 *發行者*已**sysname**，沒有預設值。 如果**所有**，訂用帳戶會卸除所有的發行者。  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 這是發行者資料庫的名稱。 *publisher_db*已**sysname**，沒有預設值。 **所有**表示所有發行者資料庫。  
  
 [  **@publication=** ] **'***發行集***'**  
 這是發行集名稱。 *發行集*已**sysname**，沒有預設值。 如果**所有**，所有發行集卸除訂閱。  
  
 [  **@reserved=** ]*保留*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_droppullsubscription**用於快照式複寫和異動複寫。  
  
 **sp_droppullsubscription**刪除中對應的資料列[MSreplication_subscriptions &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md)資料表和對應的散發者代理程式在訂閱者。 如果沒有任何資料列會處於[MSreplication_subscriptions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md)，就會卸除資料表。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-droppullsubscription-_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或建立提取訂閱的使用者能夠執行**sp_droppullsubscription**。 **Db_owner**固定的資料庫角色，才能夠執行**sp_droppullsubscription**如果建立提取訂閱的使用者屬於此角色。  
  
## <a name="see-also"></a>另請參閱  
 [刪除提取訂閱](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addpullsubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_change_subscription_properties &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_helppullsubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
