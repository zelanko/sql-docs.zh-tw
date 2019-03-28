---
title: sp_requestpeerresponse (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_requestpeerresponse_TSQL
- sp_requestpeerresponse
helpviewer_keywords:
- sp_requestpeerresponse
ms.assetid: cbe13c22-4d7d-4a36-b194-7a13ce68ef27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9b639f692da326390808376eadfd0ab74aa706ab
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526200"
---
# <a name="sprequestpeerresponse-transact-sql"></a>sp_requestpeerresponse (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  當這個程序從點對點拓撲的節點執行時，會要求該拓撲中所有其他節點做出回應。 您可以執行這個程序和檢閱相對應的回應，以確保所有先前的命令已經全數傳遞給回應節點了。 這個預存程序執行於任何資料庫的要求節點。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_requestpeerresponse [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
    [ , [ @request_id = ] request_id OUTPUT ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 是，驗證狀態的對等項目-拓撲中的發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
`[ @description = ] 'description'` 可用來識別個別狀態要求的使用者定義資訊。 *描述*已**nvarchar(4000)**，預設值是 NULL。  
  
`[ @request_id = ] request_id` 傳回新要求的識別碼。 *request_id*已**int**是 OUTPUT 參數。 執行時，就可以使用此值[sp_helppeerresponses &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)以檢視所有回應之狀態要求。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_requestpeerresponse**用於對等項目-異動複寫中。  
  
 **sp_requestpeerresponse**用來確保，所有的命令已經接收所有其他節點之前將資料庫還原至點對點拓撲中發行。 另外，在節點離線時變更複寫資料定義語言 (DDL)，以評估這些變更何時到達其他節點時，也可以使用這個項目。  
  
 **sp_requestpeerresponse**無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_requestpeerresponse**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_deletepeerrequesthistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerrequests &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
