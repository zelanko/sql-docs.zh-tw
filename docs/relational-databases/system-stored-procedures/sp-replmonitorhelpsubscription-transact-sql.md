---
title: sp_replmonitorhelpsubscription （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelpsubscription_TSQL
- sp_replmonitorhelpsubscription
helpviewer_keywords:
- sp_replmonitorhelpsubscription
ms.assetid: a681b2db-c82d-4624-a10c-396afb0ac42f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 70b85170ec4b7cf56028b2cea6d643d5e72dfd0f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760029"
---
# <a name="sp_replmonitorhelpsubscription-transact-sql"></a>sp_replmonitorhelpsubscription (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  傳回屬於發行者端一或多個發行集之訂閱的目前狀態資訊，同時為每個傳回的訂閱，各傳回一個資料列。 這個預存程序用來監視複寫，執行於散發資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replmonitorhelpsubscription [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @mode = ] mode ]  
    [ , [ @topnum = ] topnum ]   
    [ , [ @exclude_anonymous = ] exclude_anonymous ]   
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'`這是要監視之狀態的發行者名稱。 *publisher*是**sysname**，預設值是 Null。 如果是**null**，則會傳回所有使用散發者之發行者的資訊。  
  
`[ @publisher_db = ] 'publisher_db'`這是已發行之資料庫的名稱。 *publisher_db*是**sysname**，預設值是 Null。 如果是 NULL，就會傳回發行者端所有已發行資料庫的資訊。  
  
`[ @publication = ] 'publication'`這是受監視的發行集名稱。 *發行*集是**sysname**，預設值是 Null。  
  
`[ @publication_type = ] publication_type`如果發行集的類型，則為。 *publication_type*是**int**，而且可以是下列其中一個值。  
  
|值|說明|  
|-----------|-----------------|  
|**0**|交易式發行集。|  
|**1**|快照式發行集。|  
|**2**|合併式發行集。|  
|NULL (預設值)|複寫會嘗試判斷發行集的類型。|  
  
`[ @mode = ] mode`這是傳回訂閱監視資訊時使用的篩選模式。 *模式*是**int**，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**0** (預設)|傳回所有訂閱。|  
|**1**|僅傳回有錯誤的訂閱。|  
|**2**|僅傳回產生臨界值標準警告的訂閱。|  
|**3**|僅傳回有錯誤或產生臨界值標準警告的訂閱。|  
|**4**|傳回前25個最差的執行中訂閱。|  
|**5**|傳回前 50 個執行最差的訂閱。|  
|**6**|僅傳回目前同步處理中的訂閱。|  
|**7**|僅傳回目前不在同步處理中的訂閱。|  
  
`[ @topnum = ] topnum`將結果集限制為只在傳回的資料頂端指定的訂用帳戶數目。 *t*是**int**，沒有預設值。  
  
`[ @exclude_anonymous = ] exclude_anonymous`這是指是否要從結果集排除匿名提取訂閱。 *exclude_anonymous*是**bit**，預設值是**0**;值為**1**表示已排除匿名訂閱，而值為**0**則表示包含它們。  
  
`[ @refreshpolicy = ] refreshpolicy`僅供內部使用。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**status**|**int**|檢查與發行集相關聯之所有複寫代理程式的狀態，而且會以下列順序傳回所找到的最高狀態：<br /><br /> **6** = 失敗<br /><br /> **5** = 重試<br /><br /> **2** = 已停止<br /><br /> **4** = 閒置<br /><br /> **3** = 進行中<br /><br /> **1** = 已啟動|  
|**warning**|**int**|屬於發行集之訂閱所產生的臨界值警告最大值，可能是其中一個或多個這些值的邏輯 OR 結果。<br /><br /> **1** = 到期-交易式發行集的訂閱未在保留期限臨界值內同步處理。<br /><br /> **2** = 延遲-將交易式發行者的資料複寫到訂閱者所花費的時間超過臨界值（以秒為單位）。<br /><br /> **4** = mergeexpiration-合併式發行集的訂閱未在保留期限臨界值內同步處理。<br /><br /> **8** = mergefastrunduration 利用-完成合併訂閱同步處理所花費的時間超過閾值（以秒為單位），透過快速網路連接。<br /><br /> **16** = mergeslowrunduration-完成合併訂閱同步處理所花費的時間超過慢速或撥號網路連接的閾值（以秒為單位）。<br /><br /> **32** = mergefastrunspeed 利用-合併訂閱同步處理期間的資料列傳遞速率無法以快速網路連接維持閾值速率（以每秒資料列數為單位）。<br /><br /> **64** = mergeslowrunspeed-合併訂閱同步處理期間的資料列傳遞速率無法以速度較慢或撥號網路連接的速率，以每秒資料列數來維持閾值。|  
|**預訂**|**sysname**|這是訂閱者的名稱。|  
|**subscriber_db**|**sysname**|這是訂閱所用資料庫的名稱。|  
|**publisher_db**|**sysname**|這是發行集資料庫的名稱。|  
|**發行集**|**sysname**|這是發行集的名稱。|  
|**publication_type**|**int**|這是發行集的類型，可以是下列其中一個值：<br /><br /> **0** = 交易式發行集<br /><br /> **1** = 快照式發行集<br /><br /> **2** = 合併式發行集|  
|**subtype**|**int**|這是訂閱類型，它可以是下列其中一個值：<br /><br /> **0** = 推播<br /><br /> **1** = 提取<br /><br /> **2** = 匿名|  
|**造成**|**int**|交易式發行集的記錄讀取器或散發代理程式所傳播之資料變更的最高延遲 (以秒為單位)。|  
|**latencythreshold**|**int**|這是交易式發行集引發警告的最大延遲。|  
|**agentnotrunning**|**int**|這是代理程式未執行的時間長度 (以小時為單位)。|  
|**agentnotrunningthreshold**|**int**|這是引發警告前代理程式未執行的時間長度 (以小時為單位)。|  
|**timetoexpiration**|**int**|這是訂閱在未同步處理的情況下過期之前的時間長度 (以小時為單位)。|  
|**expirationthreshold**|**int**|這是訂閱過期引發警告之前的時間 (以小時為單位)。|  
|**last_distsync**|**datetime**|這是散發代理程式上次執行的日期時間。|  
|**distribution_agentname**|**sysname**|這是訂閱交易式發行集之散發代理程式作業的名稱。|  
|**mergeagentname**|**sysname**|這是訂閱合併式發行集之合併代理程式作業的名稱。|  
|**mergesubscriptionfriendlyname**|**sysname**|這是提供給訂閱的易記名稱。|  
|**mergeagentlocation**|**sysname**|這是執行合併代理程式所在伺服器的名稱。|  
|**mergeconnectiontype**|**int**|同步處理訂閱合併式發行集時所用的連接，可以是下列其中一個值：<br /><br /> **1** = 區域網路（LAN）<br /><br /> **2** = 撥號網路連接<br /><br /> **3** = Web 同步處理。|  
|**mergePerformance**|**int**|以上一次同步處理的傳遞速率除以先前所有傳遞速率的平均值為基礎，上一次同步處理相對於訂閱之所有同步處理的效能。|  
|**mergerunspeed**|**float**|這是訂閱上一次同步處理的傳遞速率。|  
|**mergerunduration**|**int**|這是完成上一次訂閱同步處理的時間長度。|  
|**monitorranking**|**int**|這是對結果集裡的訂閱進行排序所用的次序值，它可以是下列值之一：<br /><br /> 對於交易式發行集：<br /><br /> **60** = 錯誤<br /><br /> **56** = 警告：效能嚴重不足<br /><br /> **52** = 警告：即將過期或已過期<br /><br /> **50** = 警告：訂閱未初始化<br /><br /> **40** = 重試失敗的命令<br /><br /> **30** = 未執行（成功）<br /><br /> **20** = 正在執行（啟動中、正在執行或閒置）<br /><br /> 對於合併式發行集：<br /><br /> **60** = 錯誤<br /><br /> **56** = 警告：效能嚴重不足<br /><br /> **54** = 警告：長時間執行的合併<br /><br /> **52** = 警告：即將過期<br /><br /> **50** = 警告：訂閱未初始化<br /><br /> **40** = 重試失敗的命令<br /><br /> **30** = 正在執行（啟動中、正在執行或閒置）<br /><br /> **20** = 未執行（成功）|  
|**distributionagentjobid**|**binary(16)**|訂閱交易式發行集之散發代理程式作業的識別碼。|  
|**mergeagentjobid**|**binary(16)**|訂閱合併式發行集之合併代理程式作業的識別碼。|  
|**distributionagentid**|**int**|訂閱之散發代理程式作業的識別碼。|  
|**distributionagentprofileid**|**int**|散發代理程式所用代理程式設定檔的識別碼。|  
|**mergeagentid**|**int**|訂閱之合併代理程式作業的識別碼。|  
|**mergeagentprofileid**|**int**|合併代理程式所用代理程式設定檔的識別碼。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_replmonitorhelpsubscription**用於所有類型的複寫。  
  
 **sp_replmonitorhelpsubscription**會根據訂用帳戶狀態的嚴重性來排序結果集，這取決於*monitorranking*的值。 例如，所有錯誤狀態中的訂閱資料列會排在警告狀態中的訂閱資料列上面。  
  
## <a name="permissions"></a>權限  
 只有散發資料庫上之**db_owner**或**replmonitor**固定資料庫角色的成員，才能夠執行**sp_replmonitorhelpsubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式監視複寫](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
