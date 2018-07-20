---
title: MSpublications (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- MSpublications
- MSpublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublications system table
ms.assetid: 7a0b3457-7265-4f24-a255-7f055d908f20
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fefc80e4a9d3ea5d18d9621b21a4ebf6d9432777
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39102336"
---
# <a name="mspublications-transact-sql"></a>MSpublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSpublications**資料表包含每個發行者所複寫的發行集的一個資料列。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|發行者的識別碼。|  
|**publisher_db**|**sysname**|發行者資料庫的名稱。|  
|**發行集**|**sysname**|發行集的名稱。|  
|**publication_id**|**int**|發行集的識別碼。|  
|**publication_type**|**int**|發行集類型：<br /><br /> **0** = 交易式。<br /><br /> **1** = 快照集。<br /><br /> **2** = 合併式。|  
|**thirdparty_flag**|**bit**|指出發行集是否[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫：<br /><br /> **0** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **1** = 資料來源以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**independent_agent**|**bit**|指出這個發行集是否有獨立的散發代理程式。|  
|**immediate_sync**|**bit**|指出每次執行快照集代理程式時，是否要建立或重新建立同步處理檔案。|  
|**allow_push**|**bit**|指出是否能夠建立給定發行集的發送訂閱。|  
|**allow_pull**|**bit**|指出是否能夠建立給定發行集的提取訂閱。|  
|**allow_anonymous**|**bit**|指出是否能夠建立給定發行集的匿名訂閱。|  
|**description**|**nvarchar(255)**|發行集的描述。|  
|**vendor_name**|**nvarchar(100)**|如果發行者不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，這便是供應商的名稱。|  
|**保留期**|**int**|發行集的保留期限 (以小時為單位)。|  
|**sync_method**|**int**|同步處理方法：<br /><br /> **0** = 的 native （產生所有資料表的原生模式大量複製輸出）。<br /><br /> **1** = 的 character （產生所有資料表的字元模式大量複製輸出）。<br /><br /> **3** = concurrent （產生的所有原生模式大量複製輸出資料表，但快照集期間，不鎖定資料表）。<br /><br /> **4** = Concurrent_c （產生所有的字元模式大量複製輸出資料表，但快照集期間，不鎖定資料表）<br /><br /> 值**3**並**4**可用於異動複寫和合併式複寫，但不適用於快照式複寫。|  
|**allow_subscription_copy**|**bit**|啟用或停用複製訂閱這個發行集之訂閱資料庫的能力。 **0**表示，已停用複製，並**1**表示它啟用。|  
|**thirdparty_options**|**int**|指定是否顯示在 [複寫] 資料夾中的發行集的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]隱藏：<br /><br /> **0** = 複寫資料夾中，顯示異質性發行集[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。<br /><br /> **1** = 隱藏顯示異質性發行集的複寫資料夾中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。|  
|**allow_queued_tran**|**bit**|指定發行集是否允許佇列更新：<br /><br /> **0 =** 發行集是非排入佇列。<br /><br /> **1** = 發行集已排入佇列。|  
|**options**|**int**|這個版本沒有可用的資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
