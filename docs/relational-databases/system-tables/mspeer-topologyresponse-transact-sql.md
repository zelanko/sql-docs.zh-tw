---
title: "M (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSpeer_topologyresponse
- MSpeer_topologyresponse_TSQL
dev_langs: TSQL
helpviewer_keywords: MSpeer_topologyresponse
ms.assetid: 1bc5c0c6-c432-405c-89fd-e953d173a247
caps.latest.revision: "10"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 059fa8cb441bde356e2020a7bf6ffa11e3417ad3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mspeertopologyresponse-transact-sql"></a>MSpeer_topologyresponse (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  用於點對點複寫中，以儲存每一個節點對於拓撲狀態要求的回應。 這份資料表儲存在發行集資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|request_id|**int**|識別拓撲狀態要求項目中的[MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md)資料表。|  
|peer|**sysname**|產生回應的伺服器執行個體名稱。|  
|peer_version|**int**|識別發行者的版本號碼。|  
|peer_db|**sysname**|產生回應之對等的訂閱資料庫。|  
|originator_id|**int**|針對衝突偵測的目的，識別拓撲中的每個節點。 如需詳細資訊，請參閱 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。|  
|peer_conflict_retention|**int**|該中繼資料儲存在衝突資料表內的期間 (天數)。|  
|received_date|**datetime**|收到拓撲要求的時間。|  
|connection_info|**xml**|有關回應要求之節點的資訊。|  
  
## <a name="see-also"></a>請參閱＜  
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
