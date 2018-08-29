---
title: sys.masked_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 02/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.masked_columns
- masked_columns_tsql
- sys.masked_columns_tsql
- masked_columns
helpviewer_keywords:
- sys.masked_columns catalog view
ms.assetid: 671577e4-d757-4b8d-9aa9-0fc8d51ea9ca
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3a4c0fec8610dbc38c039428823e35d116889843
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43110812"
---
# <a name="sysmaskedcolumns-transact-sql"></a>sys.masked_columns & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  使用**sys.masked_columns**檢視來查詢的資料表的資料行具有動態資料遮罩套用至這些函式。 此檢視繼承自 **sys.columns** 檢視。 它會傳回 **sys.columns** 檢視中的所有資料行，加上 **is_masked** 和 **masking_function** 資料行，指出資料行是否已遮罩，若已遮罩，則指出定義了哪個遮罩函數。 此檢視只會顯示已套用遮罩函數的資料行。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|object_id|**int**|這個資料行所屬的物件識別碼。|  
|NAME|**sysname**|資料行的名稱。 在物件中，這是唯一的。|  
|column_id|**int**|資料行的識別碼。 在物件中，這是唯一的。<br /><br /> 資料行識別碼不一定會循序排列。|  
|**sys.masked_columns**會傳回許多更多的資料行，繼承自**sys.columns**。|各種|請參閱[sys.columns &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)如需更多的資料行定義。|  
|is_masked|**bit**|指出資料行加上遮罩。 1 表示遮罩。|  
|masking_function|**nvarchar(4000)**|資料行的遮罩函數。|  
  
## <a name="remarks"></a>備註  
  
## <a name="permissions"></a>Permissions  
 此檢視會傳回資料表的相關資訊，而且使用者資料表都有某種形式的權限，或如果使用者有 VIEW ANY DEFINITION 權限。  
  
## <a name="example"></a>範例  
 下列查詢會聯結**sys.masked_columns**要**sys.tables**傳回有關所有加上遮罩的資料行。  
  
```  
SELECT tbl.name as table_name, c.name AS column_name, c.is_masked, c.masking_function  
FROM sys.masked_columns AS c  
JOIN sys.tables AS tbl   
    ON c.object_id = tbl.object_id  
WHERE is_masked = 1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [動態資料遮罩](../../relational-databases/security/dynamic-data-masking.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
