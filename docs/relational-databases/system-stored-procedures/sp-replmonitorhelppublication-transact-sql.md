---
title: sp_replmonitorhelppublication (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelppublication_TSQL
- sp_replmonitorhelppublication
helpviewer_keywords:
- sp_replmonitorhelppublication
ms.assetid: 7928c50c-617f-41c5-9e0f-4e42e8be55dc
author: stevestein
ms.author: sstein
ms.openlocfilehash: dd0c5b02603afce65b084eac76701d4685ea2504
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950588"
---
# <a name="spreplmonitorhelppublication-transact-sql"></a>sp_replmonitorhelppublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回在發行者端一或多個發行集的目前狀態資訊。 這個預存程序用來監視複寫，執行於散發資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replmonitorhelppublication [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db'   
    [ , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'` 是受監視的狀態 「 發行者 」 的名稱。 *發行者*已**sysname**，預設值是 NULL。 如果**null**，會傳回所有使用散發者之發行者的資訊。  
  
`[ @publisher_db = ] 'publisher_db'` 是已發行名稱。 *publisher_db*已**sysname**，預設值是 NULL。 如果是 NULL，就會傳回發行者端所有已發行資料庫的資訊。  
  
`[ @publication = ] 'publication'` 受監視發行集名稱。 *發行集*已**sysname**，預設值是 NULL。  
  
`[ @publication_type = ] publication_type` 如果發行集的類型。 *publication_type*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|交易式發行集。|  
|**1**|快照式發行集。|  
|**2**|合併式發行集。|  
|NULL (預設值)|複寫試圖判斷發行集類型。|  
  
`[ @refreshpolicy = ] refreshpolicy` 僅供內部使用。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**publisher_db**|**sysname**|這是發行者的名稱。|  
|**publication**|**sysname**|這是發行集的名稱。|  
|**publication_type**|**int**|這是發行集的類型，可以是下列其中一個值。<br /><br /> **0** = 交易式發行集<br /><br /> **1** = 快照式發行集<br /><br /> **2** = 合併式發行集|  
|**status**|**int**|發行集所有相關聯之複寫代理程式的狀態最大值，可以是下列其中一個值。<br /><br /> **1** = 啟動<br /><br /> **2** = 成功<br /><br /> **3** = 進行中<br /><br /> **4** = 閒置<br /><br /> **5** = 正在重試<br /><br /> **6** = 失敗|  
|**警告**|**int**|屬於發行集之訂閱所產生的臨界值警告最大值，可能是其中一個或多個這些值的邏輯 OR 結果。<br /><br /> **1** = 到期-交易式發行集的訂閱尚未同步保留期限臨界值內。<br /><br /> **2** = latency-將交易式發行者資料複寫到訂閱者所花的時間超出臨界值，以秒為單位。<br /><br /> **4** = mergeexpiration-合併式發行集的訂閱尚未同步保留期限臨界值內。<br /><br /> **8** = mergefastrunduration-完成合併訂閱的同步處理所花費的時間超出臨界值，以秒為單位，快速網路連接。<br /><br /> **16** = mergeslowrunduration-完成合併訂閱的同步處理所花費的時間超出臨界值，以秒為單位，慢速或撥號網路連線。<br /><br /> **32** = mergefastrunspeed-傳遞速率無法維持臨界速率，以每秒的資料列快速網路連接合併訂閱同步處理期間，資料列。<br /><br /> **64** = mergeslowrunspeed-傳遞速率的合併訂閱同步處理期間，資料列無法維持臨界速率，以每秒的資料列，透過慢速或撥號網路連線。|  
|**worst_latency**|**int**|交易式發行集的記錄讀取器或散發代理程式所傳播之資料變更的最高延遲 (以秒為單位)。|  
|**best_latency**|**int**|交易式發行集的記錄讀取器或散發代理程式所傳播之資料變更的最低延遲 (以秒為單位)。|  
|**average_latency**|**int**|交易式發行集的記錄讀取器或散發代理程式所傳播之資料變更的平均延遲 (以秒為單位)。|  
|**last_distsync**|**datetime**|這是上次執行散發代理程式的日期時間。|  
|**retention**|**int**|這是發行集的保留期限。|  
|**latencythreshold**|**int**|這是交易式發行集所設定的延遲臨界值。|  
|**expirationthreshold**|**int**|當發行集是合併式發行集時，所設定的期限臨界值。|  
|**agentnotrunningthreshold**|**int**|這是代理程式尚未執行的最長時間所設定的臨界值。|  
|**subscriptioncount**|**int**|這是發行集的訂閱數目。|  
|**runningdistagentcount**|**int**|這是針對發行集而執行的散發代理程式數目。|  
|**snapshot_agentname**|**sysname**|發行集的快照集代理程式作業名稱。|  
|**logreader_agentname**|**sysname**|交易式發行集的記錄讀取器代理程式作業名稱。|  
|**qreader_agentname**|**sysname**|支援佇列更新的交易式發行集之佇列讀取器代理程式作業名稱。|  
|**worst_runspeedPerf**|**int**|這是合併式發行集的最長同步處理時間。|  
|**best_runspeedPerf**|**int**|這是合併式發行集的最短同步處理時間。|  
|**average_runspeedPerf**|**int**|這是合併式發行集的平均同步處理時間。|  
|**retention_period_unit**|**int**|是用來表示的單位*保留*。|  
|**發行者**|**sysname**|發行發行集之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_replmonitorhelppublication**搭配所有類型的複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**db_owner**或是**replmonitor**散發資料庫的固定的資料庫角色可以執行**sp_replmonitorhelppublication**。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式監視複寫](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
