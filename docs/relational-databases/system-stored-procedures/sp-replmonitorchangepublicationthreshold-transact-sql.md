---
title: 'sp_replmonitorchangepublicationthreshold (T-sql) '
description: 描述變更發行集的監視臨界值標準的 sp_replmonitorchangepublicationthreshold 預存程式。
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorchangepublicationthreshold_TSQL
- sp_replmonitorchangepublicationthreshold
helpviewer_keywords:
- sp_replmonitorchangepublicationthreshold
ms.assetid: 2c3615d8-4a1a-4162-b096-97aefe6ddc16
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6114d52b0db23d04c3b8cf001b0881dbc38844a6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543148"
---
# <a name="sp_replmonitorchangepublicationthreshold-transact-sql"></a>sp_replmonitorchangepublicationthreshold (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  變更發行集的監視臨界值標準。 這個預存程序用來監視複寫，執行於散發資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replmonitorchangepublicationthreshold [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @metric_id = ] metric_id ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'   
    [ , [ @value = ] value ]   
    [ , [ @shouldalert = ] shouldalert ]   
    [ , [ @mode = ] mode ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'` 這是發行者的名稱。 *publisher* 是 **sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'` 這是已發行的資料庫名稱。 *publisher_db* 是 **sysname**，沒有預設值。  
  
`[ @publication = ] 'publication'` 這是變更監視臨界值屬性的發行集名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @publication_type = ] publication_type` 如果發行集的類型。 *publication_type* 是 **int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|交易式發行集。|  
|**1**|快照式發行集。|  
|**2**|合併式發行集。|  
|NULL (預設值)|複寫試圖判斷發行集類型。|  
  
`[ @metric_id = ] metric_id` 這是要變更的發行集臨界值標準的識別碼。 *metric_id* 是 **int**，預設值是 Null，而且可以是下列值之一。  
  
|值|標準名稱|  
|-----------|-----------------|  
|**1**|**expiration** - 監視交易式發行集的訂閱是否即將到期。|  
|**2**|**latency** - 監視交易式發行集的訂閱效能。|  
|**4**|**mergeexpiration** - 監視合併式發行集的訂閱是否即將到期。|  
|**5**|**mergeslowrunduration 利用** -監視透過低頻寬 (撥號) 連接進行合併同步處理的持續時間。|  
|**6**|**mergefastrunduration 利用** -監視透過高頻寬區域網路進行合併同步處理的持續時間 (LAN) 連接。|  
|**7**|**mergefastrunspeed** - 監視透過高頻寬 (LAN) 連接進行合併同步處理的同步處理速率。|  
|**8**|**mergeslowrunspeed** -監視透過低頻寬 (撥號) 連接進行合併同步處理的同步處理速率。|  
  
 您必須指定 *metric_id* 或 *thresholdmetricname*。 如果指定 *thresholdmetricname* ，則 *METRIC_ID* 應為 Null。  
  
`[ @thresholdmetricname = ] 'thresholdmetricname'` 這是要變更的發行集臨界值標準名稱。 *thresholdmetricname* 是 **sysname**，預設值是 Null。 您必須指定 *thresholdmetricname* 或 *metric_id*。 如果指定 *metric_id* ，則 *THRESHOLDMETRICNAME* 應該是 Null。  
  
`[ @value = ] value` 這是發行集臨界值標準的新值。 *值* 是 **int**，預設值是 Null。 如果是 **null**，則不會更新度量值。  
  
`[ @shouldalert = ] shouldalert` 這是指當達到發行集臨界值標準時，是否產生警示。 *shouldalert* 是 **bit**，預設值是 Null。 **1**值表示產生警示，值為**0**表示不會產生警示。  
  
`[ @mode = ] mode` 這是指是否啟用發行集臨界值標準。 *模式* 是 **Tinyint**，預設值是 **1**。 **1**值表示啟用此計量的監視，而值為**2**表示已停用此計量的監視。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_replmonitorchangepublicationthreshold** 用於所有類型的複寫。  
  
## <a name="permissions"></a>權限  
 只有散發資料庫中的 **db_owner** 或 **replmonitor** 固定資料庫角色的成員，才能夠執行 **sp_replmonitorchangepublicationthreshold**。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式監視複寫](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
