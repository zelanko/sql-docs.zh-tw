---
title: DOMAIN_CONSTRAINTS （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DOMAIN_CONSTRAINTS
- DOMAIN_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.DOMAIN_CONSTRAINTS view
- DOMAIN_CONSTRAINTS view
ms.assetid: 436c4480-f1e3-403f-b2bd-de04539afe3c
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7392edabcef2b1ff8348bab641380b6ab64cea0f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67950760"
---
# <a name="domain_constraints-transact-sql"></a>DOMAIN_CONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對目前資料庫中，每個具有其繫結規則，並且可由目前使用者存取的別名資料類型，各傳回一個資料列。  
  
 若要從這些視圖中取出資訊，請指定 INFORMATION_SCHEMA 的完整名稱 **。**_view_name_。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**Nvarchar （** 128 **）**|規則所在的資料庫。|  
|**CONSTRAINT_SCHEMA**|**Nvarchar （** 128 **）**|包含條件約束之結構描述的名稱。<br /><br /> <strong> \* \*重要\*事項</strong>請勿使用 INFORMATION_SCHEMA views 來判斷物件的架構。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**CONSTRAINT_NAME**|**sysname**|規則名稱。|  
|**DOMAIN_CATALOG**|**Nvarchar （** 128 **）**|別名資料類型所在的資料庫。|  
|**DOMAIN_SCHEMA**|**Nvarchar （** 128 **）**|包含別名資料類型之結構描述的名稱。<br /><br /> <strong> \* \*重要\*事項</strong>請勿使用 INFORMATION_SCHEMA views 來判斷資料類型的架構。 尋找類型之結構描述的唯一可靠方式就是使用 TYPEPROPERTY 函數。|  
|**DOMAIN_NAME**|**sysname**|別名資料類型。|  
|**IS_DEFERRABLE**|**Varchar （** 2 **）**|指定條件約束檢查是否可以延後。 一律傳回 NO。|  
|**INITIALLY_DEFERRED**|**Varchar （** 2 **）**|指定一開始時是否延遲條件約束檢查。 一律傳回 NO。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [資訊架構視圖 &#40;Transact-sql&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  
