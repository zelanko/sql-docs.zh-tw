---
title: "sys.partition_range_values (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.partition_range_values
- partition_range_values_TSQL
- partition_range_values
- sys.partition_range_values_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.partition_range_values catalog view
ms.assetid: 9aee483e-61f3-4613-bec6-f084161f45ac
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0f1fd5ab82c373dbc08edf7a901ccfee4d6eed34
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="syspartitionrangevalues-transact-sql"></a>sys.partition_range_values (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  針對 R 類型資料分割函數的每個範圍界限值，各包含一個資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**function_id**|**int**|這個範圍界限值的資料分割函數識別碼。|  
|**boundary_id**|**int**|界限值 Tuple 的識別碼 (以 1 為基底的序數)，最左邊的界限是以識別碼 1 開始。|  
|**parameter_id**|**int**|這個值對應之函數的參數識別碼。 此資料行中的值對應於在**parameter_id**資料行**sys.partition_parameters**目錄檢視中的任何特定**function_id**。|  
|**值**|**sql_variant**|實際的界限值。|  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [資料分割函數目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.partition_functions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_parameters &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)  
  
  
