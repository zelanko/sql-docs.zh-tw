---
title: sp_deletepeerrequesthistory (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletepeerrequesthistory
- sp_deletepeerrequesthistory_TSQL
helpviewer_keywords:
- sp_deletepeerrequesthistory
ms.assetid: 63a4ec6e-ce79-4bf1-9d37-5ac88f8d6beb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e3c4797478b114918ce2bd79abb9e4671a0dd022
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529930"
---
# <a name="spdeletepeerrequesthistory-transact-sql"></a>sp_deletepeerrequesthistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  刪除發行集狀態要求，其中包含要求歷程記錄與相關的記錄 ([MSpeer_request &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mspeer-request-transact-sql.md)) 以及回應記錄 ([MSpeer_response &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mspeer-response-transact-sql.md))。在參與對等複寫拓撲之發行者的發行集資料庫上執行這個預存程序。 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_deletepeerrequesthistory [ @publication = ] 'publication'  
    [ , [ @request_id = ] request_id ]  
    [ , [ @cutoff_date = ] cutoff_date ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 為其產生狀態要求的發行集名稱。 *發行集*已**sysname**，沒有預設值。  
  
`[ @request_id = ] request_id` 指定的個別狀態要求，如此將會刪除所有與此要求的回應。 *request_id*已**int**，預設值是 NULL。  
  
`[ @cutoff_date = ] cutoff_date` 指定截止日期，也會刪除所有先前的回應記錄之前。 *cutoff_date*已**datetime**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_deletepeerrequesthistory**用於對等項目-異動複寫拓撲中。 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 執行時**sp_deletepeerrequesthistory**，可以是*request_id*或是*cutoff_date*必須指定。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_deletepeerrequesthistory**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_helppeerrequests &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)   
 [sp_helppeerresponses &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)   
 [sp_requestpeerresponse &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)  
  
  
