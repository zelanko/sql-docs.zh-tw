---
title: sys.databases dm_xe_map_values （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_xe_map_values
- dm_xe_map_values
- dm_xe_map_values_TSQL
- sys.dm_xe_map_values_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_map_values dynamic management view
- xe
ms.assetid: c0c5dd7e-9cee-47e2-b65a-88194c00aa1f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 79d26f8ff6a04953f6312ba8749371f6d269b912
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826657"
---
# <a name="sysdm_xe_map_values-transact-sql"></a>sys.dm_xe_map_values (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回內部數值索引鍵與人們可讀取之文字的對應。  
 
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|NAME|**nvarchar(256)**|對應的名稱。 名稱在本機系統中是唯一的。 不可為 Null。|  
|object_package_guid|**uniqueidentifier**|包含對應之封裝的 GUID。 不可為 Null。|  
|map_key|**int**|內部索引鍵值。 不可為 Null。|  
|map_value|**Nvarchar （3072）**|索引鍵值的描述。 不可為 Null。|  
  
## <a name="permissions"></a>權限  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
### <a name="relationship-cardinalities"></a>關聯性基數  
  
|從|至|關聯性|  
|----------|--------|------------------|  
|dm_xe_map_values.object_package_guid<br /><br /> dm_xe_map_values.name|sys.dm_xe_objects.package_guid<br /><br /> sys.dm_xe_objects.name|多對一| 
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

