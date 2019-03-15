---
title: sys.workload_management_workload_classifier_details (TRANSACT-SQL) |Microsoft Docs
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
ms.openlocfilehash: e4b884f779de2bf535b58d88659efffbd7901627
ms.sourcegitcommit: aa8bec762be29a29aed651d98ed4d868da85ba67
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/14/2019
ms.locfileid: "57975365"
---
# <a name="sysworkloadmanagementworkloadclassifierdetails-transact-sql-preview"></a>sys.workload_management_workload_classifier_details (TRANSACT-SQL) （預覽）

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  傳回每個分類器的詳細資料。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|分類器的識別碼。 可聯結至[sys.workload_management_workload_classifiers](sys-workload-management-workload-classifiers-transact-sql.md)。 不可為 Null。|
|classifier_type|**sysname**|分類實體。 不可為 Null。|[SQL 資料倉儲工作負載分類](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)|
|classifier_value|**sysname**|分類器的值。 不可為 Null。||

## <a name="permissions"></a>Permissions

需要 VIEW SERVER STATE 權限。

## <a name="next-steps"></a>後續步驟
  
 如需所有 SQL 資料倉儲和平行資料倉儲的目錄檢視的清單，請參閱 < [SQL 資料倉儲和平行資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)。 若要建立工作負載分類器，請參閱[建立工作負載分類](../../t-sql/statements/create-workload-classifier-transact-sql.md)。 如需工作負載分類的詳細資訊請參閱[SQL 資料倉儲工作負載分類](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
