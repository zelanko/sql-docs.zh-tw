---
title: sp_helppeerrequests (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppeerrequests_TSQL
- sp_helppeerrequests
helpviewer_keywords:
- sp_helppeerrequests
ms.assetid: 37bd503e-46c4-47c6-996e-be7ffe636fe8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9a51015d8c1e6e6df7f23f32fc7febf7fe9e429f
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537160"
---
# <a name="sphelppeerrequests-transact-sql"></a>sp_helppeerrequests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回在對等複寫拓撲中，這些要求由執行參與者所收到的所有狀態要求的相關資訊[b &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)隨時在拓撲中的已發行的資料庫。 這個預存程序是在參與點對點複寫拓撲之發行者的發行集資料庫執行。 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helppeerrequests [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 是針對它而傳送狀態要求的對等項目-拓撲中的發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
`[ @description = ] 'description'` 值，可用來識別個別狀態要求，可讓您篩選傳回的回應以使用者定義呼叫時所提供的資訊[b &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)。 *描述*已**nvarchar(4000)**，預設值是**%**。 依預設，它會傳回所有的發行集狀態要求。 這個參數用來傳回只有狀態的要求中提供之值的描述*描述*，其中使用比對字元字串[像&#40;-&#41; ](../../t-sql/language-elements/like-transact-sql.md)子句。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|識別要求。|  
|**publication**|**sysname**|發行集名稱，狀態要求就是針對它而傳送。|  
|**sent_date**|**datetime**|傳送狀態要求的日期和時間。|  
|**description**|**nvarchar(4000)**|使用者自訂的資訊，可以用來識別個別狀態要求。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helppeerrequests**用於對等項目-異動複寫中。  
  
 **sp_helppeerrequests**將資料庫還原至點對點拓撲中發行時使用。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_helppeerrequests**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_deletepeerrequesthistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerresponses &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)  
  
  
