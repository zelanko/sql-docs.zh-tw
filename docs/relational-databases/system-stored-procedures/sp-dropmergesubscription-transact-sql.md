---
title: sp_dropmergesubscription & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergesubscription_TSQL
- sp_dropmergesubscription
helpviewer_keywords:
- sp_dropmergesubscription
ms.assetid: 34244ae6-bd98-4a6a-bbd3-85f50edfcdc0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1b360eed1619317e7ca3092bc47da086c520bf04
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535550"
---
# <a name="spdropmergesubscription-transact-sql"></a>sp_dropmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  卸除對於合併式發行集及其相關聯合併代理程式的訂閱。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropmergesubscription [ [ @publication= ] 'publication' ]   
    [ , [ @subscriber= ] 'subscriber'    
    [ , [ @subscriber_db= ] 'subscriber_db' ]   
    [ , [ @subscription_type= ] 'subscription_type' ]   
    [ , [ @ignore_distributor = ] ignore_distributor ]   
    [ , [ @reserved = ] reserved ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是發行集名稱。 *發行集*已**sysname**，預設值是 NULL。 發行集必須已存在，且符合識別碼的規則。  
  
`[ @subscriber = ] 'subscriber'` 是訂閱者的名稱。 *訂閱者*已**sysname**，預設值是 NULL。  
  
`[ @subscriber_db = ] 'subscriber_db'` 是訂閱資料庫的名稱。 *subscription_database*已**sysname**，預設值是 NULL。  
  
`[ @subscription_type = ] 'subscription_type'` 是訂用帳戶的類型。 *subscription_type*已**nvarchar(15)**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**all**|發送、提取和匿名訂閱|  
|**匿名**|匿名訂閱。|  
|**push**|發送訂閱。|  
|**pull**|提取訂閱。|  
|**兩者**（預設值）|發送和提取訂閱。|  
  
`[ @ignore_distributor = ] ignore_distributor` 指出是否要將此預存程序執行而不需要連線到散發者。 *ignore_distributor*已**位元**，預設值是**0**。 這個參數可在不執行散發者清除工作的情況下，用來卸除訂閱。 如果您必須重新安裝散發者，它也很有用。  
  
`[ @reserved = ] reserved` 是保留供日後使用。 *保留*已**位元**，預設值是**0**。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_dropmergesubscription**用於合併式複寫中。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropmergesubscription_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_dropmergesubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [刪除發送訂閱](../../relational-databases/replication/delete-a-push-subscription.md)   
 [刪除提取訂閱](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_changemergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
