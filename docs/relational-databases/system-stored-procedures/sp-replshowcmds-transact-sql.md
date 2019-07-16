---
title: sp_replshowcmds & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replshowcmds
- sp_replshowcmds_TSQL
helpviewer_keywords:
- sp_replshowcmds
ms.assetid: 199f5a74-e08e-4d02-a33c-b8ab0db20f44
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7769c4e648cf3ed3898409cbdc3f0787dcb6d837
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113126"
---
# <a name="spreplshowcmds-transact-sql"></a>sp_replshowcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  以可讀取格式傳回已標記為要進行複寫的交易命令。 **sp_replshowcmds**可以在只有用戶端連線 （包括並行連接） 完全不讀取複寫的交易記錄檔中執行。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replshowcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>引數  
`[ @maxtrans = ] maxtrans` 是要傳回資訊的相關的交易數目。 *maxtrans*已**int**，預設值是**1**，其中指定的暫止複寫的交易數目上限**sp_replshowcmds**傳回的資訊。  
  
## <a name="result-sets"></a>結果集  
 **sp_replshowcmds**是診斷的程序會傳回它執行時所在發行集資料庫的相關資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**binary(10)**|命令的序號。|  
|**originator_id**|**int**|命令發起者時，一律識別碼**0**。|  
|**publisher_database_id**|**int**|識別碼的 「 發行者 」 資料庫，永遠**0**。|  
|**article_id**|**int**|發行項的識別碼。|  
|**type**|**int**|命令的類型。|  
|**command**|**nvarchar(1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 命令。|  
  
## <a name="remarks"></a>備註  
 **sp_replshowcmds**用於異動複寫中。  
  
 使用**sp_replshowcmds**，您可以檢視目前的交易未散發的交易 （保留交易記錄檔中，尚未傳送給 「 散發者 」）。  
  
 執行用戶端**sp_replshowcmds**並**sp_replcmds**相同資料庫內收到錯誤 18752。  
  
 若要避免這個錯誤，第一個用戶端必須中斷連線，或必須釋放記錄讀取器，用戶端的角色，藉由執行**sp_replflush**。 所有用戶端的連線已中斷之記錄讀取器後**sp_replshowcmds**可順利執行。  
  
> [!NOTE]  
>  **sp_replshowcmds**應該執行只有為了進行複寫問題的疑難排解。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_replshowcmds**。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤訊息](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
