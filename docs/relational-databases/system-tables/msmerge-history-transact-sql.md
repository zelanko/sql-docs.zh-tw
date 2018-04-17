---
title: Y (TRANSACT-SQL) |Microsoft 文件
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
- MSmerge_history_TSQL
- MSmerge_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_history system table
ms.assetid: 936195ad-ca07-41a8-a1a0-6699b6e63403
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3bfcd14e9d597a5bb557569ba94c6625579dec94
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="msmergehistory-transact-sql"></a>MSmerge_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_history**資料表包含記錄資料列詳細描述了先前合併代理程式作業工作階段的結果。 這份資料表會針對每一行代理程式輸出，各包含一個資料列。 這份資料表用於散發資料庫和每個訂閱資料庫中。 在散發資料庫中，它包含使用散發者之所有合併式發行集和訂閱的記錄。 在每個訂閱資料庫中，它包含訂閱者所訂閱之發行集的記錄。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|合併代理程式作業的識別碼。|  
|**agent_id**|**int**|合併代理程式的識別碼。|  
|**註解**|**nvarchar(255)**|訊息文字。|  
|**error_id**|**int**|中的錯誤識別碼[MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md)系統資料表。|  
|**timestamp**|**timestamp**|這份資料表的時間戳記資料行。|  
|**updatable_row**|**bit**|設定為**1**如果可以覆寫記錄資料列。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
