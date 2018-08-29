---
title: sp_replmonitorchangepublicationthreshold (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_replmonitorchangepublicationthreshold_TSQL
- sp_replmonitorchangepublicationthreshold
helpviewer_keywords:
- sp_replmonitorchangepublicationthreshold
ms.assetid: 2c3615d8-4a1a-4162-b096-97aefe6ddc16
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d7d8b21453e2622eb80e5eba69d3688649f0a350
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43036506"
---
# <a name="spreplmonitorchangepublicationthreshold-transact-sql"></a>sp_replmonitorchangepublicationthreshold (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [ **@publisher** = ] **'***publisher***'**  
 這是發行者的名稱。 *發行者*已**sysname**，沒有預設值。  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 這是發行的資料庫名稱。 *publisher_db*已**sysname**，沒有預設值。  
  
 [ **@publication** = ] **'***publication***'**  
 這是變更監視臨界值屬性的發行集名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [ **@publication_type** =] *publication_type*  
 若是發行集的類型。 *publication_type*已**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|交易式發行集。|  
|**1**|快照式發行集。|  
|**2**|合併式發行集。|  
|NULL (預設值)|複寫試圖判斷發行集類型。|  
  
 [ **@metric_id** =] *metric_id*  
 這是變更發行集的監視臨界值標準的識別碼。 *metric_id*已**int**，預設值是 NULL 而且可以是下列值之一。  
  
|值|標準名稱|  
|-----------|-----------------|  
|**1**|**expiration** - 監視交易式發行集的訂閱是否即將到期。|  
|**2**|**latency** - 監視交易式發行集的訂閱效能。|  
|**4**|**mergeexpiration** - 監視合併式發行集的訂閱是否即將到期。|  
|**5**|**mergeslowrunduration** -監視透過低頻寬 （撥號） 連接的進行合併同步處理的持續時間。|  
|**6**|**mergefastrunduration** -監視透過高頻寬區域網路 (LAN) 連接的進行合併同步處理的持續時間。|  
|**7**|**mergefastrunspeed** - 監視透過高頻寬 (LAN) 連接進行合併同步處理的同步處理速率。|  
|**8**|**mergeslowrunspeed** -監視透過低頻寬 （撥號） 連接進行合併同步處理的同步處理速率。|  
  
 您必須指定*metric_id*或是*thresholdmetricname*。 如果*thresholdmetricname*指定*metric_id*應該是 NULL。  
  
 [ **@thresholdmetricname** =] **'***thresholdmetricname***'**  
 這是變更發行集的監視臨界值標準的名稱。 *thresholdmetricname*已**sysname**，預設值是 NULL。 您必須指定*thresholdmetricname*或是*metric_id*。 如果*metric_id*指定*thresholdmetricname*應該是 NULL。  
  
 [ **@value** =]*值*  
 這是發行集臨界值標準的新值。 *值*已**int**，預設值是 NULL。 如果**null**，則計量的值不會更新。  
  
 [ **@shouldalert** =] *shouldalert*  
 這是指當到達發行集臨界值標準時，是否產生警示。 *shouldalert*已**元**，預設值是 NULL。 值為**1**方法，會產生警示，並針對**0**表示，不會產生警示。  
  
 [ **@mode** =]*模式*  
 指出發行集臨界值標準是否啟用。 *模式*已**tinyint**，預設值是**1**。 值為**1**方法，會啟用這個標準的監視，並針對**2**表示監視此計量已停用。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_replmonitorchangepublicationthreshold**搭配所有類型的複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**db_owner**或是**replmonitor**散發資料庫中的固定的資料庫角色可以執行**sp_replmonitorchangepublicationthreshold**。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式監視複寫](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
