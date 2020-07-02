---
title: MSmerge_tombstone （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_tombstone_TSQL
- MSmerge_tombstone
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_tombstone system table
ms.assetid: 8b3fc7bf-729b-40f2-8a26-e7dfbe8ddb38
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 10e32b235a431d7d5a9d19b82a2a55af6e41f3ec
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85639325"
---
# <a name="msmerge_tombstone-transact-sql"></a>MSmerge_tombstone (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_tombstone**資料表包含已刪除資料列的資訊，並允許將刪除傳播到其他訂閱者。 這份資料表儲存在發行集和訂閱資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**rowguid**|**uniqueidentifier**|資料列識別碼。|  
|**tablenick**|**int**|資料表的暱稱。|  
|**type**|**tinyint**|刪除動作的類型：<br /><br /> 1 = 使用者刪除。<br /><br /> 5 = 資料列不再屬於已篩選的資料分割。<br /><br /> 6 = 系統刪除。|  
|**衍生**|**Varbinary （249）**|指出已刪除的記錄版本，以及刪除時有哪些已知的更新。 當訂閱者更新另一個訂閱者正在刪除的資料列時，允許一致的衝突解決規則。|  
|**代數**|**int**|在刪除資料列時，指派這個項目。 如果訂閱者要求產生 N，則只會傳送具有層代 >= N 的標記。|  
|**logical_record_parent_rowguid**|**uniqueidentifier**|識別刪除的資料列所屬的邏輯記錄。|  
|**logical_record_lineage**|**Varbinary （501）**|用來維護這個資料列所屬邏輯記錄之刪除記錄的訂閱者暱稱與版本號碼組。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
