---
title: sp_requestpeerresponse （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: f8d75b208cc91d52d20fb4e94340809cd6857fa1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68129725"
---
# <a name="sp_requestpeerresponse-transact-sql"></a>sp_requestpeerresponse (Transact-SQL)
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
`[ @publication = ] 'publication'`這是要驗證狀態的點對點拓撲中的發行集名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @description = ] 'description'`使用者定義的資訊，可用來識別個別狀態要求。 *description*是**Nvarchar （4000）**，預設值是 Null。  
  
`[ @request_id = ] request_id`傳回新要求的識別碼。 *request_id*是**int** ，而且是 OUTPUT 參數。 執行[sp_helppeerresponses &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)來查看狀態要求的所有回應時，可以使用這個值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_requestpeerresponse**用於點對點異動複寫中。  
  
 **sp_requestpeerresponse**是用來確保在還原點對點拓撲中發行的資料庫之前，所有其他節點都已收到所有命令。 另外，在節點離線時變更複寫資料定義語言 (DDL)，以評估這些變更何時到達其他節點時，也可以使用這個項目。  
  
 **sp_requestpeerresponse**不能在使用者自訂交易內執行。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_requestpeerresponse**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_deletepeerrequesthistory &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerrequests &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
