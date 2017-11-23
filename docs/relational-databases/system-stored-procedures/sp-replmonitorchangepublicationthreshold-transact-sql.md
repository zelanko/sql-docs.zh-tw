---
title: "sp_replmonitorchangepublicationthreshold (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_replmonitorchangepublicationthreshold_TSQL
- sp_replmonitorchangepublicationthreshold
helpviewer_keywords: sp_replmonitorchangepublicationthreshold
ms.assetid: 2c3615d8-4a1a-4162-b096-97aefe6ddc16
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e24fd4746ee5a93489e55b6cf16edc0150c647b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
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
 [  **@publisher**  =] **'***發行者***'**  
 這是發行者的名稱。 *發行者*是**sysname**，沒有預設值。  
  
 [  **@publisher_db**  =] **'***publisher_db***'**  
 這是發行的資料庫名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
 [  **@publication**  =] **'***發行集***'**  
 這是變更監視臨界值屬性的發行集名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@publication_type**  =] *publication_type*  
 若是發行集的類型。 *publication_type*是**int**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|交易式發行集。|  
|**1**|快照式發行集。|  
|**2**|合併式發行集。|  
|NULL (預設值)|複寫試圖判斷發行集類型。|  
  
 [  **@metric_id**  =] *metric_id*  
 這是變更發行集的監視臨界值標準的識別碼。 *metric_id*是**int**，預設值是 NULL，而且可以是下列值之一。  
  
|值|標準名稱|  
|-----------|-----------------|  
|**1**|**expiration** - 監視交易式發行集的訂閱是否即將到期。|  
|**2**|**latency** - 監視交易式發行集的訂閱效能。|  
|**4**|**mergeexpiration** - 監視合併式發行集的訂閱是否即將到期。|  
|**5**|**mergeslowrunduration** -監視透過低頻寬 （撥號） 連接進行合併同步處理的持續時間。|  
|**6**|**mergefastrunduration** -監視透過高頻寬區域網路 (LAN) 連接進行合併同步處理的持續時間。|  
|**7**|**mergefastrunspeed** - 監視透過高頻寬 (LAN) 連接進行合併同步處理的同步處理速率。|  
|**8**|**mergeslowrunspeed** -監視透過低頻寬 （撥號） 連接進行合併同步處理的同步處理速率。|  
  
 您必須指定*metric_id*或*thresholdmetricname*。 如果*thresholdmetricname*不指定，則*metric_id*應該是 NULL。  
  
 [  **@thresholdmetricname**  =] **'***thresholdmetricname***'**  
 這是變更發行集的監視臨界值標準的名稱。 *thresholdmetricname*是**sysname**，預設值是 NULL。 您必須指定*thresholdmetricname*或*metric_id*。 如果*metric_id*不指定，則*thresholdmetricname*應該是 NULL。  
  
 [  **@value**  =]*值*  
 這是發行集臨界值標準的新值。 *值*是**int**，預設值是 NULL。 如果**null**，則不會更新公制值。  
  
 [  **@shouldalert**  =] *shouldalert*  
 這是指當到達發行集臨界值標準時，是否產生警示。 *shouldalert*是**元**，預設值是 NULL。 值為**1**方法，會產生警示，而值為**0**表示，不會產生警示。  
  
 [  **@mode**  =]*模式*  
 指出發行集臨界值標準是否啟用。 *模式*是**tinyint**，預設值是**1**。 值為**1**方法，這個標準的監視已啟用，而值為**2**表示這個標準的監視已停用。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_replmonitorchangepublicationthreshold**用於所有複寫類型。  
  
## <a name="permissions"></a>Permissions  
 只有成員**db_owner**或**replmonitor**散發資料庫中的固定的資料庫角色可以執行**sp_replmonitorchangepublicationthreshold**。  
  
## <a name="see-also"></a>請參閱＜  
 [以程式設計方式監視複寫](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
