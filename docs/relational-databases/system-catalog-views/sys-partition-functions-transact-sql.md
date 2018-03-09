---
title: "sys.partition_functions (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.partition_functions_TSQL
- partition_functions
- sys.partition_functions
- partition_functions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partition_functions catalog view
ms.assetid: 96515727-728b-4bea-804a-36ce915b8b75
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a440995a63e75705c0a7b5d3c56e1e649c6defbe
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="syspartitionfunctions-transact-sql"></a>sys.partition_functions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的每個資料分割函數，各包含一個資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|資料分割函數的名稱。 在資料庫中，這是唯一的。|  
|**function_id**|**int**|資料分割函數識別碼。 在資料庫中，這是唯一的。|  
|**型別**|**char(2)**|函數類型。<br /><br /> R = 範圍|  
|**type_desc**|**nvarchar （60)**|函數類型。<br /><br /> RANGE|  
|**扇出**|**int**|函數所建立的資料分割數目。|  
|**boundary_value_on_right**|**bit**|用於定界資料分割。<br /><br /> 1 = 界限值是包含在該界限的 RIGHT 範圍內。<br /><br /> 0 = LEFT。|  
|**is_system**||**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 1 = 全文檢索片段中使用了物件。<br /><br /> 0 = 全文檢索片段未使用物件。|  
|**create_date**|**datetime**|建立函數的日期。|  
|**modify_date**|**datetime**|上次利用 ALTER 陳述式修改函數的日期。|  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [資料分割函數目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.partition_range_values &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [sys.partition_parameters &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)  
  
  
