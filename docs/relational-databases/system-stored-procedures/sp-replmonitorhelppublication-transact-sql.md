---
title: sp_replmonitorhelppublication (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: 8dc952f03ea2538412c864e1a9e9b228bf3ca877
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771215"
---
# <a name="spreplmonitorhelppublication-transact-sql"></a>sp_replmonitorhelppublication (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
`[ @publisher = ] 'publisher'`這是要監視之狀態的發行者名稱。 *publisher*是**sysname**, 預設值是 Null。 如果是**null**, 則會傳回所有使用散發者之發行者的資訊。  
  
`[ @publisher_db = ] 'publisher_db'`這是已發行之資料庫的名稱。 *publisher_db*是**sysname**, 預設值是 Null。 如果是 NULL，就會傳回發行者端所有已發行資料庫的資訊。  
  
`[ @publication = ] 'publication'`這是受監視的發行集名稱。 *發行*集是**sysname**, 預設值是 Null。  
  
`[ @publication_type = ] publication_type`如果發行集的類型, 則為。 *publication_type*是**int**, 而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|交易式發行集。|  
|**1**|快照式發行集。|  
|**2**|合併式發行集。|  
|NULL (預設值)|複寫試圖判斷發行集類型。|  
  
`[ @refreshpolicy = ] refreshpolicy`僅供內部使用。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**publisher_db**|**sysname**|這是發行者的名稱。|  
|**publication**|**sysname**|這是發行集的名稱。|  
|**publication_type**|**int**|這是發行集的類型，可以是下列其中一個值。<br /><br /> **0** = 交易式發行集<br /><br /> **1** = 快照式發行集<br /><br /> **2** = 合併式發行集|  
|**status**|**int**|發行集所有相關聯之複寫代理程式的狀態最大值，可以是下列其中一個值。<br /><br /> **1** = 已啟動<br /><br /> **2** = 成功<br /><br /> **3** = 進行中<br /><br /> **4** = 閒置<br /><br /> **5** = 重試<br /><br /> **6** = 失敗|  
|**warning**|**int**|屬於發行集之訂閱所產生的臨界值警告最大值，可能是其中一個或多個這些值的邏輯 OR 結果。<br /><br /> **1** = 到期-交易式發行集的訂閱未在保留期限臨界值內同步處理。<br /><br /> **2** = 延遲-將交易式發行者的資料複寫到訂閱者所花費的時間超過臨界值 (以秒為單位)。<br /><br /> **4** = mergeexpiration-合併式發行集的訂閱未在保留期限臨界值內同步處理。<br /><br /> **8** = mergefastrunduration 利用-完成合併訂閱同步處理所花費的時間超過閾值 (以秒為單位), 透過快速網路連接。<br /><br /> **16** = mergeslowrunduration-完成合併訂閱同步處理所花費的時間超過慢速或撥號網路連接的閾值 (以秒為單位)。<br /><br /> **32** = mergefastrunspeed 利用-合併訂閱同步處理期間的資料列傳遞速率無法以快速網路連接維持閾值速率 (以每秒資料列數為單位)。<br /><br /> **64** = mergeslowrunspeed-合併訂閱同步處理期間的資料列傳遞速率無法以速度較慢或撥號網路連接的速率, 以每秒資料列數來維持閾值。|  
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
|**retention_period_unit**|**int**|這是用來表示*保留*的單位。|  
|**發行者**|**sysname**|發行發行集之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或**1** (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_replmonitorhelppublication**用於所有類型的複寫。  
  
## <a name="permissions"></a>Permissions  
 只有散發資料庫的**db_owner**或**replmonitor**固定資料庫角色的成員, 才能夠執行**sp_replmonitorhelppublication**。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式監視複寫](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
