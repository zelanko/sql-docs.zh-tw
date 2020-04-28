---
title: sp_helppeerrequests （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 5b9e2a370c9acc9c22dac7e5e60ceb10e08e46ba
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68137616"
---
# <a name="sp_helppeerrequests-transact-sql"></a>sp_helppeerrequests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回參與者在點對點複寫拓撲中收到之所有狀態要求的資訊，這些要求是藉由在拓撲中任何已發行的資料庫上執行[sp_requestpeerresponse &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)來起始。 這個預存程序是在參與點對點複寫拓撲之發行者的發行集資料庫執行。 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helppeerrequests [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'`這是傳送狀態要求的點對點拓撲中的發行集名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @description = ] 'description'`可以用來識別個別狀態要求的值，這可讓您根據在呼叫[sp_requestpeerresponse &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)時所提供的使用者定義資訊，篩選傳回的回應。 *描述*是**Nvarchar （4000）**，預設值是**%**。 依預設，它會傳回所有的發行集狀態要求。 這個參數是用來傳回狀態要求，其描述項合*描述*中提供的值，其中的字元字串會使用[LIKE &#40;transact-sql&#41;](../../t-sql/language-elements/like-transact-sql.md)子句進行比對。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|識別要求。|  
|**發行集**|**sysname**|發行集名稱，狀態要求就是針對它而傳送。|  
|**sent_date**|**datetime**|傳送狀態要求的日期和時間。|  
|**描述**|**nvarchar(4000)**|使用者自訂的資訊，可以用來識別個別狀態要求。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helppeerrequests**用於點對點異動複寫中。  
  
 還原點對點拓撲中發行的資料庫時，會使用**sp_helppeerrequests** 。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_helppeerrequests**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_deletepeerrequesthistory &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerresponses &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)  
  
  
