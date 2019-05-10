---
title: sys.workload_management_workload_classifiers (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 05/01/2019
ms.prod: ''
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 43d8921f2135dbc1a343e8f3a604cc81f79b9faa
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65089540"
---
# <a name="sysworkloadmanagementworkloadclassifiers-transact-sql"></a>sys.workload_management_workload_classifiers (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

 傳回工作負載分類器的詳細資料。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|分類器的唯一識別碼。 不可為 Null||
group_name|**sysname**|分類指派給工作負載群組的名稱。 不可為 Null。 |靜態資源類別</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80 </br> </br>靜態資源類別</br>smallrc</br>mediumrc</br>largerc</br>xlargerc|
NAME|**sysname**|分類器的名稱。 必須是唯一的執行個體。 不可為 Null。||
|importance|**sysname**|是在這個工作負載群組和間共用資源的工作負載群組的相對重要性。  指定分類中的重要性會覆寫工作負載群組重要性設定。|低、 below_normal、 normal、 above_normal，最高 |
|create_time|**datetime**|建立分類器的時間。 不可為 Null。||
modify_time|**datetime**|分類器上次修改時間。 不可為 Null。||
is_enabled|**bit**|顯示是否已啟用分類器。 預設會啟用。 不可為 Null。|0 = 未啟用分類器 </br> 1 = 已啟用分類器|
|&nbsp;||||
  
## <a name="permissions"></a>Permissions

需要 VIEW SERVER STATE 權限。

## <a name="next-steps"></a>後續步驟

 如需所有 SQL 資料倉儲和平行資料倉儲的目錄檢視的清單，請參閱 < [SQL 資料倉儲和平行資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)。 若要建立工作負載分類器，請參閱[建立工作負載分類](../../t-sql/statements/create-workload-classifier-transact-sql.md)。 如需有關工作負載分類的詳細資訊，請參閱[SQL 資料倉儲工作負載分類](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
