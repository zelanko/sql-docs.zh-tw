---
description: sp_deletepeerrequesthistory (Transact-SQL)
title: sp_deletepeerrequesthistory (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 606c3f362b5be303ce7c0ccbd3cd53f21fde8cd8
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548082"
---
# <a name="sp_deletepeerrequesthistory-transact-sql"></a>sp_deletepeerrequesthistory (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  刪除與發行集狀態要求相關的歷程記錄，其中包括要求歷程記錄 ([MSpeer_request &#40;transact-sql&#41;](../../relational-databases/system-tables/mspeer-request-transact-sql.md)) 以及回應歷程記錄 (MSpeer_response [transact-sql &#40;](../../relational-databases/system-tables/mspeer-response-transact-sql.md)&#41;。這個預存程式是在參與點對點複寫拓撲之發行者的發行集資料庫上執行。 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_deletepeerrequesthistory [ @publication = ] 'publication'  
    [ , [ @request_id = ] request_id ]  
    [ , [ @cutoff_date = ] cutoff_date ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 發出狀態要求的發行集名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @request_id = ] request_id` 指定個別的狀態要求，如此一來，就會刪除此要求的所有回應。 *request_id* 是 **int**，預設值是 Null。  
  
`[ @cutoff_date = ] cutoff_date` 指定截止日期，在此日期之前會刪除所有先前的回應記錄。 *cutoff_date* 為 **datetime**，預設值為 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_deletepeerrequesthistory** 用於點對點事務複寫拓撲中。 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 執行 **sp_deletepeerrequesthistory**時，必須指定 *request_id* 或 *cutoff_date* 。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_deletepeerrequesthistory**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_helppeerrequests &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)   
 [sp_helppeerresponses &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)   
 [sp_requestpeerresponse &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)  
  
  
