---
title: MSreplication_monitordata (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSreplication_monitordata_TSQL
- MSreplication_monitordata
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_monitordata system table
ms.assetid: 843d3ffd-a1ef-4fd5-a744-c2252199793e
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cc66db7f28a55eddb403fbe9b0cc48df5398d820
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39103696"
---
# <a name="msreplicationmonitordata-transact-sql"></a>MSreplication_monitordata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSreplication_monitordata**資料表包含複寫監視器所使用的每個受監視的訂用帳戶的其中一個資料列的快取的資料。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**lastrefresh**|**datetime**|重新整理監視資料的日期和時間。|  
|**computetime**|**int**|這是計算監視資料所花的時間 (以秒為單位)。|  
|**publication_id**|**int**|發行集識別碼。|  
|**發行者**|**sysname**|發行者的名稱。|  
|**publisher_srvid**|**int**|發行者的伺服器識別碼。|  
|**publisher_db**|**sysname**|發行集資料庫的名稱。|  
|**發行集**|**sysname**|發行集的名稱。|  
|**publication_type**|**int**|發行集的類型，它可以是下列值之一：<br /><br /> **0** = 交易式發行集<br /><br /> **1** = 快照式發行集<br /><br /> **2** = 合併式發行集|  
|**agent_type**|**int**|複寫代理程式的類型，它可以是下列值之一：<br /><br /> **1** = 快照集代理程式<br /><br /> **2** = 記錄讀取器代理程式<br /><br /> **3** = 散發代理程式<br /><br /> **4** = 合併代理程式<br /><br /> **9** = 佇列讀取器代理程式|  
|**agent_id**|**int**|複寫代理程式的識別碼。|  
|**agent_name**|**sysname**|複寫代理程式作業的名稱。|  
|**job_id**|**uniqueidentifier**|複寫代理程式作業的 GUID。|  
|**status**|**int**|複寫代理程式的狀態，它可以是下列其中一個值：<br /><br /> **1** = 啟動<br /><br /> **2** = 成功<br /><br /> **3** = 進行中<br /><br /> **4** = 閒置<br /><br /> **5** = 正在重試<br /><br /> **6** = 失敗|  
|**isagentrunningnow**|**bit**|指出如果代理程式作業目前正在，值的旗標**1**作業正在執行的方法。|  
|**警告**|**int**|訂閱所產生的臨界值警告，它可能是一或多個這些值的邏輯 OR 結果。<br /><br /> **1** = expiration – 交易式發行集的訂閱已超出保留期限的超過允許的臨界值，保留期限的百分比。<br /><br /> **2** = latency-將交易式發行者資料複寫到訂閱者所花的時間超出臨界值，以秒為單位。<br /><br /> **4** = mergeexpiration-合併式發行集的訂閱已超出保留期限的超過允許的臨界值，保留期限的百分比。 8 = mergefastrunduration - 利用快速網路連接來完成合併訂閱的同步處理所花的時間超出臨界值 (以秒為單位)。<br /><br /> **16** = mergeslowrunduration-完成合併訂閱的同步處理所花費的時間超出臨界值，以秒為單位，慢速或撥號網路連線。<br /><br /> **32** = mergefastrunspeed – 傳遞速率無法維持臨界速率，以每秒的資料列快速網路連接合併訂閱同步處理期間，資料列。<br /><br /> **64** = mergeslowrunspeed – 傳遞速率的合併訂閱同步處理期間，資料列無法維持臨界速率，以每秒的資料列，透過慢速或撥號網路連線。|  
|**last_distsync**|**datetime**|上次執行散發代理程式的日期和時間。|  
|**agentstoptime**|**datetime**|停止代理程式的日期和時間。|  
|**distdb**|**sysname**|訂閱的散發資料庫名稱。|  
|**保留期**|**int**|發行集的保留期限。|  
|**time_stamp**|**datetime**|僅供內部使用。|  
|**worst_latency**|**int**|交易式發行集的記錄讀取器或散發代理程式所傳播之資料變更的最高延遲 (以秒為單位)。|  
|**best_latency**|**int**|交易式發行集的記錄讀取器或散發代理程式所傳播之資料變更的最低延遲 (以秒為單位)。|  
|**avg_latency**|**int**|交易式發行集的記錄讀取器或散發代理程式所傳播之資料變更的平均延遲 (以秒為單位)。|  
|**cur_latency**|**int**|在目前的執行期間，記錄讀取器或散發代理程式所傳播之資料變更的延遲 (以秒為單位)。|  
|**worst_runspeedPerf**|**int**|合併式發行集的最長同步處理時間|  
|**best_runspeedPerf**|**int**|合併式發行集的最短同步處理時間|  
|**average_runspeedPerf**|**int**|合併式發行集的平均同步處理時間|  
|**mergePerformance**|**int**|以上一次同步處理的傳遞速率除以先前所有傳遞速率的平均值為基礎，上一次同步處理相對於訂閱之所有同步處理的效能。|  
|**mergelatestsessionrunduration**|**int**|最近合併代理程式執行的持續時間。|  
|**mergelatestsessionrunspeed**|**float(53)**|最近合併代理程式執行的傳遞速率。|  
|**mergelatestsessionconnectiontype**|**int**|最近的合併代理程式工作階段所用的連接，它可以是下列其中一個值：<br /><br /> **1** = 區域網路 (LAN)<br /><br /> **2** = 撥號網路連接|  
|**retention_period_unit**|**tinyint**|定義用來定義保留的單位，它可以是下列值之一：<br /><br /> **1** = 週<br /><br /> **2** = 月<br /><br /> **3** = 年|  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式監視複寫](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)   
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_replmonitorhelpsubscription &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md)   
 [sp_replmonitorhelppublication &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md)   
 [sp_replmonitorhelppublisher &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md)   
 [sp_replmonitorhelpmergesession &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)   
 [sp_replmonitorhelppublicationthresholds &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md)   
 [sp_replmonitorhelpmergesessiondetail &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)  
  
  
