---
title: MSmerge_replinfo (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_replinfo_TSQL
- MSmerge_replinfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_replinfo system table
ms.assetid: b0924094-c0cc-49c1-869a-65be0d0465a0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cae6c84d0ca85a8cb27d8310bcc3cb02dca47f8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62903305"
---
# <a name="msmergereplinfo-transact-sql"></a>MSmerge_replinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_replinfo**資料表包含每個訂用帳戶的一個資料列。 這個資料表會追蹤訂閱的資訊。 這份資料表儲存在發行集和訂閱資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**repid**|**uniqueidentifier**|複本的唯一識別碼。|  
|**use_interactive_resolver**|**bit**|指定是否在重新調整期間使用互動式解析程式。<br /><br /> **0** = 使用互動式解析程式。<br /><br /> **1** = 使用互動式解析程式。|  
|**validation_level**|**int**|在訂閱執行的類型驗證。 指定的驗證層級可以是下列值之一：<br /><br /> **0** = 沒有驗證。<br /><br /> **1** = 僅限資料列計數驗證。<br /><br /> **2** = 資料列計數與總和檢查碼驗證。<br /><br /> **3** = 資料列計數及二進位總和檢查碼驗證。|  
|**resync_gen**|**bigint**|用於重新同步訂閱的層代 (Generation) 號碼。 值為 **-1**指出訂用帳戶未標示為要重新同步處理。|  
|**login_name**|**sysname**|建立訂閱的使用者名稱。|  
|**hostname**|**sysname**|在產生訂閱用的資料分割時，參數化資料列篩選器所用的值。|  
|**merge_jobid**|**binary(16)**|這個訂閱的合併作業識別碼。|  
|**sync_info**|**int**|僅供內部使用。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
