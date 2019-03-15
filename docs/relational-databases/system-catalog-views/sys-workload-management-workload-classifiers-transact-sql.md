---
title: sys.workload_management_workload_classifiers (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 02/08/2019
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
ms.openlocfilehash: d93876db1bb31edab2ad128a0ab8af4d4a5230cd
ms.sourcegitcommit: aa8bec762be29a29aed651d98ed4d868da85ba67
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/14/2019
ms.locfileid: "57975368"
---
# <a name="sysworkloadmanagementworkloadclassifiers-transact-sql-preview"></a>sys.workload_management_workload_classifiers (TRANSACT-SQL) （預覽）

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

 傳回工作負載分類器的詳細資料。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|分類器的唯一識別碼。 不可為 Null||
group_name|**sysname**|分類指派給工作負載群組的名稱。 不可為 Null。 |靜態資源類別</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80 </br>動態資源類別</br>smallrc</br>mediumrc</br>Largerc</br>xlargerc|
NAME|**sysname**|分類器的名稱。 必須是唯一的執行個體。 不可為 Null。||
|importance|**sysname**|是在這個工作負載群組和間共用資源的工作負載群組的相對重要性。  指定分類中的重要性會覆寫工作負載群組重要性設定。|低、 below_normal、 normal、 above_normal，最高 |
|create_time|**datetime**|建立分類器的時間。 不可為 Null。||
modify_time|**datetime**|分類器上次修改時間。 不可為 Null。||
is_enabled|**bit**|顯示是否已啟用分類器。 預設會啟用。 不可為 Null。|0 = 未啟用分類器 </br> 1 = 已啟用分類器|
|&nbsp;||||
  
## <a name="permissions"></a>Permissions

需要 VIEW SERVER STATE 權限。

## <a name="next-steps"></a>後續步驟

 如需所有 SQL 資料倉儲和平行資料倉儲的目錄檢視的清單，請參閱 < [SQL 資料倉儲和平行資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)。 若要建立工作負載分類器，請參閱[建立工作負載分類](../../t-sql/statements/create-workload-classifier-transact-sql.md)。 如需工作負載分類的詳細資訊請參閱[SQL 資料倉儲工作負載分類](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
