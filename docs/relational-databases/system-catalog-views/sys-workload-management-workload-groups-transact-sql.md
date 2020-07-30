---
title: sys.databases workload_management_workload_groups （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 491b4d2dcbd84bd1f53d44716f457686d277d25f
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87393926"
---
# <a name="sysworkload_management_workload_groups-transact-sql"></a>sys.databases workload_management_workload_groups （Transact-sql）

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

 傳回工作負載群組的詳細資料。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|
|group_id|**int**|工作負載群組的唯一識別碼。 不可為 Null。||
|NAME|**sysname**|工作負載群組的名稱。 對於實例而言，必須是唯一的。  不可為 Null。||
|importance|**nvarchar(128)**|這是此工作負載群組中的要求與共用資源的工作負載群組之間的相對重要性。 不可為 Null。|low、below_normal、normal （預設值）、above_normal、high||
|min_percentage_resource|**tinyint**|保證工作負載群組中要求的資源數量。 資源不會與其他工作負載群組共用。 不可為 Null。||
|cap_percentage_resource|**tinyint**|針對工作負載群組中要求的資源百分比配置固定上限。 限制配置給指定層級的資源上限。 允許的值範圍從 1 至 100。||
|request_min_resource_grant_percent|**decimal （5，2）**|指定配置給要求的最低資源數量。 允許的值範圍是從0.75 到100。||
|request_max_resource_grant_percent |**decimal （5，2）**|指定配置給要求的資源數量上限。||
|query_execution_timeout_sec|**int**|取消查詢之前允許的執行時間量（以秒為單位）。  當查詢已達到執行的傳回階段時，即無法取消。  query_execution_timeout_sec 不包含排入佇列所花費的時間。|
|query_wait_timeout_sec|**int**|INTERNAL||
|create_time|**datetime**|建立工作負載群組的時間。 不可為 Null。||
modify_time|**datetime**|上次修改工作負載群組的時間。 不可為 Null。||
|&nbsp;||||
  
## <a name="permissions"></a>權限

需要 VIEW SERVER STATE 權限。

## <a name="next-steps"></a>後續步驟

 如需 SQL 資料倉儲和平行處理資料倉儲的所有目錄檢視清單，請參閱[SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)。 若要建立工作負載群組，請參閱[建立工作負載群組](../../t-sql/statements/create-workload-group-transact-sql.md)。 如需工作負載分類的詳細資訊，請參閱[工作負載隔離](/azure/sql-data-warehouse/sql-data-warehouse-workload-isolation)
