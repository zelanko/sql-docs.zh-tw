---
description: sp_droppullsubscription (Transact-SQL)
title: sp_droppullsubscription (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e4e7e0f9292d9ed94139b9facfe496821b91fb03
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543436"
---
# <a name="sp_droppullsubscription-transact-sql"></a>sp_droppullsubscription (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

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
`[ @publisher = ] 'publisher'` 這是遠端伺服器名稱。 *publisher* 是 **sysname**，沒有預設值。 如果是 **all**，就會卸載所有發行者的訂閱。  
  
`[ @publisher_db = ] 'publisher_db'` 這是發行者資料庫的名稱。 *publisher_db* 是 **sysname**，沒有預設值。 **all** 表示所有發行者資料庫。  
  
`[ @publication = ] 'publication'` 這是發行集名稱。 *發行* 集是 **sysname**，沒有預設值。 如果是 **all**，就會將訂用帳戶放到所有發行集。  
  
`[ @reserved = ] reserved` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_droppullsubscription** 用於快照式複寫和異動複寫中。  
  
 **sp_droppullsubscription** 會在 [MSreplication_subscriptions &#40;transact-sql&#41;](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) 資料表中刪除對應的資料列，並在訂閱者端刪除對應的散發者代理程式。 如果 [MSreplication_subscriptions &#40;transact-sql&#41;](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md)中沒有剩餘的資料列，它會卸載資料表。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-droppullsubscription-_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色的成員或建立提取訂閱的使用者，才可以執行 **sp_droppullsubscription**。 只有在建立提取訂閱的使用者屬於此角色時， **db_owner** 固定資料庫角色才能執行 **sp_droppullsubscription** 。  
  
## <a name="see-also"></a>另請參閱  
 [刪除提取訂閱](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addpullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_change_subscription_properties &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
