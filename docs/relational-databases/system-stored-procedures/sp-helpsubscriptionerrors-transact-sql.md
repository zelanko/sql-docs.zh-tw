---
title: sp_helpsubscriptionerrors （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpsubscriptionerrors_TSQL
- sp_helpsubscriptionerrors
helpviewer_keywords:
- sp_helpsubscriptionerrors
ms.assetid: 01c8bc21-939e-490d-8cc8-219c068be31e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c41294867de508ed39815b16183d5151c55197a4
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826069"
---
# <a name="sp_helpsubscriptionerrors-transact-sql"></a>sp_helpsubscriptionerrors (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  傳回給定訂閱的所有異動複寫錯誤。 這個預存程序執行於散發資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpsubscriptionerrors [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'   
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'`這是發行者的名稱。 *publisher*是**sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'`這是發行集資料庫的名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @subscriber = ] 'subscriber'`這是訂閱者的名稱。 *訂閱者*是**sysname**，沒有預設值。  
  
`[ @subscriber_db = ] 'subscriber_db'`這是訂閱資料庫的名稱。 *subscriber_db*是**sysname**，沒有預設值。  
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|錯誤的識別碼|  
|**time**|**datetime**|發生錯誤的時間。|  
|**error_type_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id**|**int**|錯誤來源類型識別碼。|  
|**source_name**|**Nvarchar （100）**|錯誤來源的名稱。|  
|**error_code**|**sysname**|錯誤碼。|  
|**error_text**|**ntext**|錯誤訊息。|  
|**xact_seqno**|**varbinary(16)**|執行失敗之批次的起始交易記錄序號。 只供散發代理程式使用，這是在執行失敗的批次中，第一項交易的交易記錄序號。|  
|**command_id**|**int**|執行失敗之批次的命令識別碼。 只供散發代理程式使用，這是在執行失敗的批次中，第一個命令的命令識別碼。|  
|**session_id**|**int**|發生錯誤之代理程式工作階段的識別碼。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpsubscriptionerrors**用於快照式和異動複寫。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_helpsubscriptionerrors**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_helpsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
