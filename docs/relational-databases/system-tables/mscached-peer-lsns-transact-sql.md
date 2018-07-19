---
title: MScached_peer_lsns (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- MScached_peer_lsns_TSQL
- MScached_peer_lsns
dev_langs:
- TSQL
helpviewer_keywords:
- MScached_peer_lsns system table
ms.assetid: f8b6089a-0230-45f9-8c34-9fe0d2a3a74e
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c88be8f7ffd489fbc276b58f253819b2f1d9f7ce
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33004215"
---
# <a name="mscachedpeerlsns-transact-sql"></a>MScached_peer_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MScached_peer_lsns**資料表用來追蹤交易記錄的 LSN 值，這些值可用來判斷哪些命令傳給指定的訂閱者端對端複寫中。 這份資料表儲存在散發資料庫中。  
  
## <a name="definition"></a>定義  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|散發代理程式的識別碼。|  
|**建立者**|**sysname**|原始發行者名稱。|  
|**originator_db**|**sysname**|原始發行集資料庫的名稱。|  
|**originator_publication_id**|**int**|識別原始發行集。|  
|**originator_db_version**|**int**|識別來源資料庫的版本號碼。|  
|**originator_lsn**|**varbinary(16)**|原始交易的 LSN。|  
  
## <a name="remarks"></a>備註  
 LSN 值只會在插入之後立即使用，它們在系統中並沒有長久的意義。  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
