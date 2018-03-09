---
title: "MSmerge_tombstone (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSmerge_tombstone_TSQL
- MSmerge_tombstone
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_tombstone system table
ms.assetid: 8b3fc7bf-729b-40f2-8a26-e7dfbe8ddb38
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 55644aa0543de70ca4ec11ee65a446d073ce3556
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="msmergetombstone-transact-sql"></a>MSmerge_tombstone (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_tombstone**資料表包含已刪除資料列的相關資訊，可讓刪除動作傳播到其他訂閱者。 這份資料表儲存在發行集和訂閱資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**rowguid**|**uniqueidentifier**|資料列識別碼。|  
|**tablenick**|**int**|資料表的暱稱。|  
|**型別**|**tinyint**|刪除動作的類型：<br /><br /> 1 = 使用者刪除。<br /><br /> 5 = 資料列不再屬於已篩選的資料分割。<br /><br /> 6 = 系統刪除。|  
|**歷程**|**varbinary(249)**|指出已刪除的記錄版本，以及刪除時有哪些已知的更新。 當訂閱者更新另一個訂閱者正在刪除的資料列時，允許一致的衝突解決規則。|  
|**產生**|**int**|在刪除資料列時，指派這個項目。 如果訂閱者要求 N 層代 (Generation)，就只會傳送層代 (Generation) >= N 的 Tombstone。|  
|**logical_record_parent_rowguid**|**uniqueidentifier**|識別刪除的資料列所屬的邏輯記錄。|  
|**logical_record_lineage**|**Varbinary(501)**|用來維護這個資料列所屬邏輯記錄之刪除記錄的訂閱者暱稱與版本號碼組。|  
  
## <a name="see-also"></a>請參閱＜  
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
