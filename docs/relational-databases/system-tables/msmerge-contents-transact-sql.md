---
title: MSmerge_contents (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- MSmerge_contents
- MSmerge_contents_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_contents system table
ms.assetid: 8d68a61a-683f-4b20-92f9-c0a8d9ba0ad1
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4643b0ba6bdfd9eea4405be02ca481133f0db096
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39101556"
---
# <a name="msmergecontents-transact-sql"></a>MSmerge_contents (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_contents**資料表包含每個資料列發行以來，在目前的資料庫中修改的一個資料列。 合併處理序利用這份資料表來判斷已變更的資料列。 這份資料表儲存在發行集和訂閱資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|已發行資料表的暱稱。|  
|**rowguid**|**uniqueidentifier**|給定資料列的資料列識別碼。|  
|**產生**|**bigint**|所識別的資料列產生**tablenick**並**rowguid**。|  
|**partchangegen**|**bigint**|可能變更了資料列是否屬於篩選發行集的最後一項資料變更之相關聯層代 (Generation)。|  
|**歷程**|**varbinary(501)**|用來維護這個資料列之變更記錄的訂閱者暱稱、版本號碼組。|  
|**colvl**|**varbinary(7489)**|資料行版本資訊。|  
|**標記**|**uniqueidentifier**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**logical_record_parent_rowguid**|**uniqueidentifier**|識別中的最上層父資料列**MSmerge_contents** (由**rowguid**) 的每個邏輯記錄中對應的子資料列。|  
|**logical_record_lineage**|**varbinary(501)**|用來維護邏輯記錄中最上層父資料列之變更記錄的訂閱者暱稱、版本號碼組。 邏輯記錄中所有子資料列的這個值都是 NULL。|  
|**logical_relation_change_gen**|**bigint**|造成在邏輯記錄中重新對齊的最後一項變更之相關聯層代 (Generation) 值，現有的資料列會移入或移出邏輯記錄。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
