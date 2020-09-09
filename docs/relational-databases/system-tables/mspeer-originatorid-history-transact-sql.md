---
description: MSpeer_originatorid_history (Transact-SQL)
title: MSpeer_originatorid_history (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_originatorid_history_TSQL
- MSpeer_originatorid_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_originatorid_history
ms.assetid: c1f53d0f-4080-43ff-be38-2b10395c68c9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 05ba5720a45bc8d448fe1ed24d6bdc950dcf290d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545518"
---
# <a name="mspeer_originatorid_history-transact-sql"></a>MSpeer_originatorid_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對拓撲中已定義的每一個訂閱者識別碼，各包含一個資料列。 這包括不再使用中之節點的識別碼。 當您正在設定新的節點進行衝突偵測，以確保指定的訂閱者識別碼尚未使用時，就會使用此資料表。 這份資料表儲存在發行集資料庫中。 如需有關衝突偵測的詳細資訊，請參閱對等複寫 [中的衝突偵測](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|originator_publication|**sysname**|指定訂閱者識別碼所針對的發行集。|  
|originator_id|**int**|針對衝突偵測的目的，識別拓撲中每個節點的數字。|  
|originator_node|**sysname**|指定訂閱者識別碼所針對的伺服器執行個體。|  
|originator_db|**sysname**|指定訂閱者識別碼所針對的發行集資料庫。|  
|originator_db_version|**int**|識別來源資料庫的版本號碼。|  
|originator_version|**int**|識別發行者的版本號碼。|  
|inserted_date|**datetime**|訂閱者識別碼插入此資料表的日期和時間。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
