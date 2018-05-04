---
title: MSpeer_lsns (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- MSpeer_lsns
- MSpeer_lsns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_lsns system table
ms.assetid: 0ba33907-601b-4c3d-8099-2663f680a161
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 12c449c2673d8592b5291df0335db786fcec80e1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="mspeerlsns-transact-sql"></a>MSpeer_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Mspeer_lsns**資料表用來將每個交易對應至對等複寫拓撲中的訂閱。 這份資料表儲存在點對點複寫拓撲的每個發行集資料庫中，以及點對點發行集的所有訂閱者之訂閱資料庫中。 如需這種類型的異動複寫拓撲的詳細資訊，請參閱[Peer to Peer 異動複寫](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。 這份資料表儲存在發行集資料庫中。  
  
## <a name="definition"></a>定義  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|識別點對點 LSN。|  
|**last_updated**|**datetime**|**Datetime**在進行最後一個資料列更新。|  
|**建立者**|**sysname**|交易的來源發行者名稱。|  
|**originator_db**|**sysname**|交易的來源資料庫名稱。|  
|**originator_publication**|**sysname**|交易的來源發行集名稱。|  
|**originator_publication_id**|**int**|交易的來源發行集識別碼。|  
|**originator_db_version**|**int**|識別來源資料庫的版本號碼。|  
|**originator_lsn**|**int**|識別來源發行集中的 LSN。|  
|**originator_version**|**int**|識別發行者的版本號碼。|  
|**originator_id**|**smallint**|針對衝突偵測的目的，識別拓撲中的每個節點。 如需詳細資訊，請參閱 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
