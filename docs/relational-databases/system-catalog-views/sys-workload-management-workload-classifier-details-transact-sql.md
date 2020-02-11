---
title: sys.databases workload_management_workload_classifier_details （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 58b3f3315309a734a22e2732af5207b64e2f0a9d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73632921"
---
# <a name="sysworkload_management_workload_classifier_details-transact-sql"></a>sys.databases workload_management_workload_classifier_details （Transact-sql）

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  傳回每個分類器的詳細資料。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|分類器的識別碼。  不可為 Null。|
|classifier_type|**sysname**|Joinable 至[sys. workload_management_workload_classifiers](sys-workload-management-workload-classifiers-transact-sql.md)。|`membername`</br>`wlm_label`</br>`wlm_context`</br>`start_time`</br>`end_time`|
|classifier_value|**sysname**|分類器的值。 不可為 Null。||

## <a name="permissions"></a>權限

需要 VIEW SERVER STATE 權限。

## <a name="next-steps"></a>後續步驟
  
如需 SQL 資料倉儲和平行處理資料倉儲的所有目錄檢視清單，請參閱[SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)。 若要建立工作負載分類器，請參閱[建立工作負載分類器](../../t-sql/statements/create-workload-classifier-transact-sql.md)。 如需工作負載分類的詳細資訊，請參閱 SQL 資料倉儲[工作負載分類](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)和[工作負載重要性](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
