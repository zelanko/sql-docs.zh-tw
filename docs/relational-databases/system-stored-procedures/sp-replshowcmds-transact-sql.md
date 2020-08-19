---
description: sp_replshowcmds (Transact-SQL)
title: sp_replshowcmds (Transact-sql) |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: beb5ba1371c3a3e8748e5a4963106d659e7dd31f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446820"
---
# <a name="sp_replshowcmds-transact-sql"></a>sp_replshowcmds (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  以可讀取格式傳回已標記為要進行複寫的交易命令。 **sp_replshowcmds** 只有在用戶端連接 (包括目前的連接) 未從記錄檔讀取複寫的交易時，才能執行。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replshowcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>引數  
`[ @maxtrans = ] maxtrans` 這是要傳回信息的交易數目。 *>maxtrans* 是 **int**，預設值是 **1**，指定 **sp_replshowcmds** 傳回信息之交易擱置複寫的最大數目。  
  
## <a name="result-sets"></a>結果集  
 **sp_replshowcmds** 是一種診斷程式，會傳回從中執行該發行集資料庫的相關資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**binary(10)**|命令的序號。|  
|**originator_id**|**int**|命令建立者的識別碼，一律為 **0**。|  
|**publisher_database_id**|**int**|發行者資料庫的識別碼，一律為 **0**。|  
|**article_id**|**int**|發行項的識別碼。|  
|**type**|**int**|命令的類型。|  
|**command**|**nvarchar(1024)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 命令。|  
  
## <a name="remarks"></a>備註  
 **sp_replshowcmds** 用於異動複寫中。  
  
 您可以使用 **sp_replshowcmds**來查看目前未散發的交易 (尚未傳送給散發者) 的交易記錄中剩餘的交易。  
  
 在相同資料庫內執行 **sp_replshowcmds** 和 **sp_replcmds** 的用戶端會收到錯誤18752。  
  
 若要避免這個錯誤，第一個用戶端必須中斷連接或用戶端的角色，因為必須藉由執行 **sp_replflush**來釋放記錄讀取器。 當所有用戶端都與記錄讀取器中斷連線之後， **sp_replshowcmds** 可以順利執行。  
  
> [!NOTE]  
>  **sp_replshowcmds** 應僅執行以針對複寫問題進行疑難排解。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_replshowcmds**。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤訊息](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
