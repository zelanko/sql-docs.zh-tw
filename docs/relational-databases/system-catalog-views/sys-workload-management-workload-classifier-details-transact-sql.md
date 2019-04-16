---
title: sys.workload_management_workload_classifier_details (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/26/2019
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
ms.openlocfilehash: 9afd00a887244c02849d40eed635500b06533709
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582721"
---
# <a name="sysworkloadmanagementworkloadclassifierdetails-transact-sql-preview"></a>sys.workload_management_workload_classifier_details (TRANSACT-SQL) （預覽）

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

> [!Note]
> 使用 SQL 資料倉儲 Gen2 上預覽工作負載分類。 工作負載管理分類和重要性的 preview 是組建與發行日期 2019 年 4 月 9 日，或更新版本。  使用者應該避免使用組建早於這個日期的工作負載管理測試。  若要判斷您的組建是否以工作負載管理功能，執行 select @@version時連線到您的 SQL 資料倉儲執行個體。

  傳回每個分類器的詳細資料。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|分類器的識別碼。 可聯結至[sys.workload_management_workload_classifiers](sys-workload-management-workload-classifiers-transact-sql.md)。 不可為 Null。|
|classifier_type|**sysname**|分類實體。 不可為 Null。|MEMBERNAME|
|classifier_value|**sysname**|分類器的值。 不可為 Null。||

## <a name="permissions"></a>Permissions

需要 VIEW SERVER STATE 權限。

## <a name="next-steps"></a>後續步驟
  
 如需所有 SQL 資料倉儲和平行資料倉儲的目錄檢視的清單，請參閱 < [SQL 資料倉儲和平行資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)。 若要建立工作負載分類器，請參閱[建立工作負載分類](../../t-sql/statements/create-workload-classifier-transact-sql.md)。 如需有關工作負載分類的詳細資訊，請參閱 < SQL 資料倉儲[工作負載分類](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)和[工作負載的重要性](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
