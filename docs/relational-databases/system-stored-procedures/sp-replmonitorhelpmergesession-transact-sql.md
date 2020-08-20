---
description: sp_replmonitorhelpmergesession (Transact-SQL)
title: sp_replmonitorhelpmergesession (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelpmergesession_TSQL
- sp_replmonitorhelpmergesession
helpviewer_keywords:
- sp_replmonitorhelpmergesession
ms.assetid: a0400ba8-9609-4901-917e-925e119103a1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5fe48c8ed194434fa71ce3fd01f2a8db93ecac74
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485694"
---
# <a name="sp_replmonitorhelpmergesession-transact-sql"></a>sp_replmonitorhelpmergesession (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  傳回有關某個給定複寫合併代理程式過去的工作階段，只要符合篩選準則的每個工作階段，都會傳回一個資料列。 這個預存程序用來監視合併式複寫，它執行於散發資料庫的散發者端，或是訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replmonitorhelpmergesession [ [ @agent_name = ] 'agent_name' ]  
    [ , [ @hours = ] hours ]  
    [ , [ @session_type = ] session_type ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @agent_name = ] 'agent_name'` 這是代理程式的名稱。 *agent_name* 是 **Nvarchar (100) ** 沒有預設值。  
  
`[ @hours = ] hours` 這是傳回曆程記錄代理程式會話資訊的時間範圍（以小時為單位）。 *hours* 是 **int**，它可以是下列其中一個範圍。  
  
|值|描述|  
|-----------|-----------------|  
|< **0**|傳回有關過去代理程式的執行資訊，最多可傳回 100 筆的執行資訊。|  
|**0** (預設)|傳回所有過去代理程式的執行資訊。|  
|> **0**|傳回在過去 *小時* 數內發生的代理程式執行的資訊。|  
  
`[ @session_type = ] session_type` 根據會話的 end 結果來篩選結果集。 *session_type* 是 **int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**1** (預設值)|結果為重試或成功的代理程式工作階段。|  
|**0**|結果為失敗的代理程式工作階段。|  
  
`[ @publisher = ] 'publisher'` 這是發行者的名稱。 *publisher* 是 **sysname**，預設值是 Null。 在「訂閱者」端執行 **sp_replmonitorhelpmergesession** 時，會使用這個參數。  
  
`[ @publisher_db = ] 'publisher_db'` 這是發行集資料庫的名稱。 *publisher_db* 是 **sysname**，預設值是 Null。 在「訂閱者」端執行 **sp_replmonitorhelpmergesession** 時，會使用這個參數。  
  
`[ @publication = ] 'publication'` 這是發行集的名稱。 *發行* 集是 **sysname**，預設值是 Null。 在「訂閱者」端執行 **sp_replmonitorhelpmergesession** 時，會使用這個參數。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**Session_id**|**int**|代理程式作業工作階段的識別碼。|  
|**狀態**|**int**|代理程式執行狀態：<br /><br /> **1** = 開始<br /><br /> **2** = 成功<br /><br /> **3** = 進行中<br /><br /> **4** = 閒置<br /><br /> **5** = 重試<br /><br /> **6** = 失敗|  
|**StartTime**|**datetime**|時間代理程式作業工作階段已開始。|  
|**EndTime**|**datetime**|時間代理程式作業工作階段已完成。|  
|**有效期間**|**int**|這個作業工作階段的累加持續時間 (以秒為單位)。|  
|**UploadedCommands**|**int**|代理程式工作階段期間所上傳的命令數。|  
|**DownloadedCommands**|**int**|代理程式工作階段期間所下載的命令數。|  
|**ErrorMessages**|**int**|代理程式工作階段期間所產生的錯誤訊息數。|  
|**錯誤識別碼**|**int**|所發生之錯誤的識別碼|  
|**PercentageDone**|**decimal**|使用中的工作階段已傳遞的總變更估計百分比。|  
|**TimeRemaining**|**int**|使用中的工作階段其餘的估計秒數。|  
|**CurrentPhase**|**int**|這是使用中工作階段的目前階段，它可以是下列項目之一。<br /><br /> **1** = 上傳<br /><br /> **2** = 下載|  
|**LastMessage**|**Nvarchar (500) **|這是在工作階段期間，由合併代理程式所記錄的最後一則訊息。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_replmonitorhelpmergesession** 用來監視合併式複寫。  
  
 在訂閱者上執行時， **sp_replmonitorhelpmergesession** 只會傳回最後五個合併代理程式會話的資訊。  
  
## <a name="permissions"></a>權限  
 只有散發者端或訂閱者端之訂閱資料庫上的 **db_owner** 或 **replmonitor** 固定資料庫角色的成員，才能夠執行 **sp_replmonitorhelpmergesession**。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式監視複寫](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
