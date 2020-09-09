---
description: MSmerge_history (Transact-SQL)
title: MSmerge_history (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_history_TSQL
- MSmerge_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_history system table
ms.assetid: 936195ad-ca07-41a8-a1a0-6699b6e63403
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 348df963920d35aeb874a83cad83701995d563cd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540865"
---
# <a name="msmerge_history-transact-sql"></a>MSmerge_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_history**資料表包含記錄資料列，其中包含先前合併代理程式作業會話之結果的詳細描述。 這份資料表會針對每一行代理程式輸出，各包含一個資料列。 這份資料表用於散發資料庫和每個訂閱資料庫中。 在散發資料庫中，它包含使用散發者之所有合併式發行集和訂閱的記錄。 在每個訂閱資料庫中，它包含訂閱者所訂閱之發行集的記錄。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|合併代理程式作業的識別碼。|  
|**agent_id**|**int**|合併代理程式的識別碼。|  
|**評論**|**nvarchar(255)**|訊息文字。|  
|**error_id**|**int**|[MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md)系統資料表中的錯誤識別碼。|  
|**timestamp**|**timestamp**|這份資料表的時間戳記資料行。|  
|**updatable_row**|**bit**|如果可以覆寫歷程記錄資料列，請設定為 **1** 。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
