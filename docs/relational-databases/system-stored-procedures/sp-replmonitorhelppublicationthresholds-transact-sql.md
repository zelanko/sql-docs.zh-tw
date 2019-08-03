---
title: sp_replmonitorhelppublicationthresholds (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelppublicationthresholds
- sp_replmonitorhelppublicationthresholds_TSQL
helpviewer_keywords:
- sp_replmonitorhelppublicationthresholds
ms.assetid: d6b1aa4b-3369-4255-a892-c0e5cc9cb693
author: stevestein
ms.author: sstein
ms.openlocfilehash: ac1efa2e63bb798ce24785e4240bd756e8737e51
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771198"
---
# <a name="spreplmonitorhelppublicationthresholds-transact-sql"></a>sp_replmonitorhelppublicationthresholds (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
`[ @publisher = ] 'publisher'`這是發行者的名稱。 *publisher*是**sysname**, 沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'`這是已發行之資料庫的名稱。 *publisher_db*是**sysname**, 沒有預設值。  
  
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**, 沒有預設值。  
  
`[ @publication_type = ] publication_type`如果發行集的類型, 則為。 *publication_type*是**int**, 而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|交易式發行集。|  
|**1**|快照式發行集。|  
|**2**|合併式發行集。|  
|NULL (預設值)|複寫會嘗試判斷發行集的類型。|  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|複寫效能標準的識別碼，它可以是下列項目之一。<br /><br /> **1expiration** -監視交易式發行集的訂閱是否即將到期。<br /><br /> **2latency** -監視交易式發行集之訂閱的效能。<br /><br /> **4mergeexpiration** -監視合併式發行集的訂閱是否即將到期。<br /><br /> **5mergeslowrunduration** -監視透過低頻寬 (撥號) 連接進行合併同步處理的持續時間。<br /><br /> **6mergefastrunduration** -監視透過高頻寬 (LAN) 連接進行合併同步處理的持續時間。<br /><br /> **7mergefastrunspeed** -監視透過高頻寬 (LAN) 連接進行合併同步處理的同步處理速率。<br /><br /> **8mergeslowrunspeed** -監視透過低頻寬 (撥號) 連接進行合併同步處理的同步處理速率。|  
|**title**|**sysname**|複寫效能標準的名稱。|  
|**value**|**int**|效能標準的臨界值。|  
|**shouldalert**|**bit**|這是指當計量超出此發行集定義的臨界值時, 是否應該產生警示;值為**1**表示應該引發警示。|  
|**isenabled**|**bit**|這是指是否針對此發行集的這個複寫效能標準啟用監視;值為**1**表示已啟用監視。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或**1** (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_replmonitorhelppublicationthresholds**用於所有類型的複寫。  
  
## <a name="permissions"></a>Permissions  
 只有散發資料庫的**db_owner**或**replmonitor**固定資料庫角色的成員, 才能夠執行**sp_replmonitorhelppublicationthresholds**。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式監視複寫](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
