---
title: sys.databases partition_functions （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 410c52ff5a6e38e96db990713f8564c6463cfb80
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981758"
---
# <a name="syspartition_functions-transact-sql"></a>sys.partition_functions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的每個資料分割函數，各包含一個資料列。  
  
|資料行名稱|[名稱]|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|資料分割函數的名稱。 在資料庫中，這是唯一的。|  
|**function_id**|**int**|資料分割函數識別碼。 在資料庫中，這是唯一的。|  
|**型別**|**char(2)**|函數類型。<br /><br /> R = 範圍|  
|**type_desc**|**nvarchar(60)**|函數類型。<br /><br /> RANGE|  
|**扇出**|**int**|函數所建立的資料分割數目。|  
|**boundary_value_on_right**|**bit**|用於定界資料分割。<br /><br /> 1 = 界限值是包含在該界限的 RIGHT 範圍內。<br /><br /> 0 = LEFT。|  
|**is_system**||**適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本。<br /><br /> 1 = 全文檢索片段中使用了物件。<br /><br /> 0 = 全文檢索片段未使用物件。|  
|**create_date**|**datetime**|建立函數的日期。|  
|**modify_date**|**datetime**|上次利用 ALTER 陳述式修改函數的日期。|  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色中的成員資格。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 資料[分割函數目錄&#40;Views transact-sql&#41; ](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.partition_range_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [sys. partition_parameters &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)  
  
  
