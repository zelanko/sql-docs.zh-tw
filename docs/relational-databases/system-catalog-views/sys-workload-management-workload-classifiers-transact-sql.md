---
title: sys.databases workload_management_workload_classifiers （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 585eb4551fb688f4f6a620729310b0245462cbff
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632968"
---
# <a name="sysworkload_management_workload_classifiers-transact-sql"></a>sys.databases workload_management_workload_classifiers （Transact-sql）

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

 傳回工作負載分類器的詳細資料。  
  
|資料行名稱|資料類型|說明|範圍|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|分類器的唯一識別碼。 不可為 Null||
group_name|**sysname**|分類器指派的工作負載組名。 不可為 Null。 Joinable 至 sys. workload_management_workload_groups ||
name|**sysname**|分類器的名稱。 對於實例而言，必須是唯一的。 不可為 Null。||
|importance|**sysname**|這是此工作負載群組中的要求與共用資源的工作負載群組之間的相對重要性。  分類器中指定的重要性會覆寫工作負載群組的重要性設定。 可為 Null。  若為 null，則會使用工作負載群組重要性設定。|low、below_normal、normal （預設值）、above_normal、high |
|create_time|**datetime**|建立分類器的時間。 不可為 Null。||
modify_time|**datetime**|分類器上次修改的時間。 不可為 Null。||
is_enabled|**bit**|內部||
|&nbsp;||||
  
## <a name="permissions"></a>Permissions

需要 VIEW SERVER STATE 權限。

## <a name="next-steps"></a>後續的步驟

 如需 SQL 資料倉儲和平行處理資料倉儲的所有目錄檢視清單，請參閱[SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)。 若要建立工作負載分類器，請參閱[建立工作負載分類器](../../t-sql/statements/create-workload-classifier-transact-sql.md)。 如需工作負載分類的詳細資訊，請參閱[工作負載分類](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
