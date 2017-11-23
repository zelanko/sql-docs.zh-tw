---
title: "sp_helppeerrequests (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_helppeerrequests_TSQL
- sp_helppeerrequests
helpviewer_keywords: sp_helppeerrequests
ms.assetid: 37bd503e-46c4-47c6-996e-be7ffe636fe8
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d2ea35c01385de46ded538c98faf701e34d3892
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sphelppeerrequests-transact-sql"></a>sp_helppeerrequests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回在對等複寫拓撲中，其中這些要求由執行參與者接收之所有狀態要求的相關資訊[sp_requestpeerresponse &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)拓撲中任何發行資料庫端。 這個預存程序是在參與點對點複寫拓撲之發行者的發行集資料庫執行。 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helppeerrequests [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>引數  
 [  **@publication** =] **'***發行集***'**  
 這是針對它而傳送狀態要求的點對點拓撲中的發行集名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@description** =] **'***描述***'**  
 根據呼叫時所提供的使用者定義資訊的值可以用來識別個別狀態要求，可讓您篩選傳回的回應[sp_requestpeerresponse &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md). *描述*是**nvarchar （4000)**，預設值是 **%** 。 依預設，它會傳回所有的發行集狀態要求。 這個參數用來描述比對中提供的值傳回只能狀態要求*描述*，其中使用符合字元字串[像 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)子句。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|識別要求。|  
|**發行集**|**sysname**|發行集名稱，狀態要求就是針對它而傳送。|  
|**sent_date**|**datetime**|傳送狀態要求的日期和時間。|  
|**描述**|**nvarchar(4000)**|使用者自訂的資訊，可以用來識別個別狀態要求。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helppeerrequests**用於端對端異動複寫中。  
  
 **sp_helppeerrequests**將資料庫還原至點對點拓撲中發行時使用。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_helppeerrequests**。  
  
## <a name="see-also"></a>請參閱＜  
 [sp_deletepeerrequesthistory &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerresponses &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)  
  
  
