---
title: sp_dropsubscription & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropsubscription
- sp_dropsubscription_TSQL
helpviewer_keywords:
- sp_dropsubscription
ms.assetid: 7551f345-5510-4684-ab53-f9057249d13a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 08e25ee6f2de589c3d7367c140bd0ea63d4cec1e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52812963"
---
# <a name="spdropsubscription-transact-sql"></a>sp_dropsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  卸除對於發行者的特定發行項、發行集或訂閱集的訂閱。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropsubscription [ [ @publication= ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
        , [ @subscriber= ] 'subscriber'  
    [ , [ @destination_db= ] 'destination_db' ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@publication=** ] **'**_發行集_**'**  
 這是關聯的發行集名稱。 *發行集*已**sysname**，預設值是 NULL。 如果**所有**，針對指定的訂閱者的所有發行集的所有訂閱都會都取消。 *發行集*是必要的參數。  
  
 [  **@article=** ] **'**_文章_**'**  
 這是發行項的名稱。 *發行項*已**sysname**，預設值是 NULL。 如果**所有**，發行集和訂閱者端卸除指定的所有發行項每個訂用帳戶。 使用**所有**針對發行集允許立即更新。  
  
 [  **@subscriber=** ] **'**_subscribe_r **'**  
 這是將卸除訂閱的訂閱者名稱。 *訂閱者*已**sysname**，沒有預設值。 如果**所有**，會卸除所有訂閱者的所有訂用帳戶。  
  
 [  **@destination_db=** ] **'**_destination_db_**'**  
 這是目的地資料庫的名稱。 *destination_db*已**sysname**，預設值是 NULL。 如果是 NULL，就會卸除這個訂閱者的所有訂閱。  
  
 [  **@ignore_distributor =** ] *ignore_distributor*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@reserved=** ] **'**_保留_**'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_dropsubscription**用於快照式和異動複寫。  
  
 如果您在立即同步發行集中卸除發行項的訂閱，則除非您卸除發行集所有發行項的訂閱，再同時將它們全部重新加入，否則便無法重新加入它們。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropsubscription-tran_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定伺服器角色**db_owner**固定的資料庫角色或建立訂用帳戶的使用者能夠執行**sp_dropsubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [刪除發送訂閱](../../relational-databases/replication/delete-a-push-subscription.md)   
 [sp_addsubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubstatus &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [sp_helpsubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
