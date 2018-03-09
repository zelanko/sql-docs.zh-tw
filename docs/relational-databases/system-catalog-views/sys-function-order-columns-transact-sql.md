---
title: sys.function_order_columns (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- function_order_columns
- sys.function_order_columns_TSQL
- function_order_columns_TSQL
- sys.function_order_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.function_order_columns catalog view
ms.assetid: 29287973-3125-4d35-8ca9-92cb45828854
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 01973c84fe0e66709230c393d445465d17dd42b1
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysfunctionordercolumns-transact-sql"></a>sys.function_order_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回一個資料列，每個資料行的一部分**順序**屬於 common language runtime (CLR) 資料表值函數的運算式。  

  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|定義順序所在之物件的識別碼 (CLR 資料表值函式)。|  
|**order_column_id**|**int**|排序資料行的識別碼。 **order_column_id**只有在是唯一**object_id**。<br /><br /> **order_column_id**表示此資料行的位置依順序排列。|  
|**column_id**|**int**|中的資料行的識別碼**object_id**。<br /><br /> **column_id**只有在是唯一**object_id**。|  
|**is_descending**|**bit**|1 = 排序資料行是以遞減方式排序。<br /><br /> 0 = 排序資料行是以遞增方式排序。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [物件目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;。TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
