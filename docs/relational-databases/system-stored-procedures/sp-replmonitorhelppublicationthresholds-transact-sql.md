---
title: sp_replmonitorhelppublicationthresholds (TRANSACT-SQL) |Microsoft 文件
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
- sp_replmonitorhelppublicationthresholds
- sp_replmonitorhelppublicationthresholds_TSQL
helpviewer_keywords:
- sp_replmonitorhelppublicationthresholds
ms.assetid: d6b1aa4b-3369-4255-a892-c0e5cc9cb693
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c77f8e36cc33dfee704ef8f5b945a58c7011a23b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spreplmonitorhelppublicationthresholds-transact-sql"></a>sp_replmonitorhelppublicationthresholds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回針對監視發行集設定的臨界值標準。 這個預存程序用來監視複寫，執行於散發資料庫的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replmonitorhelppublicationthresholds [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'  
```  
  
## <a name="arguments"></a>引數  
 [ **@publisher**=] **'***發行者***'**  
 這是發行者的名稱。 *發行者*是**sysname**，沒有預設值。  
  
 [ **@publisher_db**=] **'***publisher_db***'**  
 這是發行的資料庫名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
 [ **@publication**=] **'***發行集***'**  
 這是發行集的名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [ **@publication_type**=] *publication_type*  
 若是發行集的類型。 *publication_type*是**int**，而且可以是下列值之一。  
  
|Value|描述|  
|-----------|-----------------|  
|**0**|交易式發行集。|  
|**1**|快照式發行集。|  
|**2**|合併式發行集。|  
|NULL (預設值)|複寫會嘗試判斷發行集的類型。|  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|複寫效能標準的識別碼，它可以是下列項目之一。<br /><br /> **1expiration** -監視交易式發行集的訂閱是否即將到期。<br /><br /> **2latency** -監視交易式發行集的訂閱效能。<br /><br /> **4mergeexpiration** -監視合併式發行集的訂閱是否即將到期。<br /><br /> **5mergeslowrunduration** -監視透過低頻寬 （撥號） 連接進行合併同步處理的持續時間。<br /><br /> **6mergefastrunduration** -監視透過高頻寬 (LAN) 連接進行合併同步處理的持續時間。<br /><br /> **7mergefastrunspeed** -監視透過高頻寬 (LAN) 連接進行合併同步處理的同步處理速率。<br /><br /> **8mergeslowrunspeed** -監視透過低頻寬 （撥號） 連接進行合併同步處理的同步處理速率。|  
|**title**|**sysname**|複寫效能標準的名稱。|  
|**value**|**int**|效能標準的臨界值。|  
|**shouldalert**|**bit**|當標準超過定義的臨界值，這個發行集; 時，如果應該產生警示值為**1**表示應該引發警示。|  
|**isenabled**|**bit**|如果，啟用此發行集; 這個複寫效能標準的監視值為**1**表示已啟用監視。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_replmonitorhelppublicationthresholds**用於所有複寫類型。  
  
## <a name="permissions"></a>Permissions  
 只有成員**db_owner**或**replmonitor**散發資料庫上的固定的資料庫角色可以執行**sp_replmonitorhelppublicationthresholds**。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式監視複寫](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
