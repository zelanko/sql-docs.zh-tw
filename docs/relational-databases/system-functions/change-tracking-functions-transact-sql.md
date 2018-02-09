---
title: "變更追蹤函數 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/08/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], change tracking
- change tracking [SQL Server], functions
ms.assetid: 04eb53c4-8b69-414e-9696-185d227fea35
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4fdcdae5c4ec0bad80a93e6ce1520357f1132af1
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="change-tracking-functions-transact-sql"></a>變更追蹤函數 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  異動追蹤會記錄套用至追蹤資料表的插入、更新和刪除活動，並以容易取用的關聯式格式提供變更的詳細資料。 下列函數會傳回變更的相關資訊。  
  
|函數|Description|  
|--------------|-----------------|  
|[CHANGETABLE (CHANGES)](../../relational-databases/system-functions/changetable-transact-sql.md)|針對資料表在指定之版本之後發生的所有變更，傳回追蹤資訊。|  
|[CHANGETABLE （版本）](../../relational-databases/system-functions/changetable-transact-sql.md)|針對指定的資料列傳回最新的變更追蹤資訊。|  
|[CHANGE_TRACKING_MIN_VALID_VERSION()](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)|傳回適用於取得變更追蹤資訊從指定的資料表，當您使用的最小版本[CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md)函式。|  
|[CHANGE_TRACKING_CURRENT_VERSION](../../relational-databases/system-functions/change-tracking-current-version-transact-sql.md)|取得與最後確認之交易相關聯的版本。 下次您使用 CHANGETABLE 列舉變更時，可以使用這個版本。|  
|[CHANGE_TRACKING_IS_COLUMN_IN_MASK](../../relational-databases/system-functions/change-tracking-is-column-in-mask-transact-sql.md)|解譯由 CHANGETABLE(CHANGES …) 函數傳回的 SYS_CHANGE_COLUMNS 值。|  
|[WITH CHANGE_TRACKING_CONTEXT](../../relational-databases/system-functions/with-change-tracking-context-transact-sql.md)|應用程式變更資料時，啟用變更內容的指定，例如，訂閱者識別碼。|  
  
## <a name="see-also"></a>另請參閱  
 [追蹤資料變更 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
