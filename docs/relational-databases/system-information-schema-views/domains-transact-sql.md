---
description: DOMAINS (Transact-SQL)
title: 網域 (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DOMAINS_TSQL
- DOMAINS
dev_langs:
- TSQL
helpviewer_keywords:
- DOMAINS view
- INFORMATION_SCHEMA.DOMAINS view
ms.assetid: f0b734d5-816f-4b10-a60c-615931b515c2
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c7933697f38ea9404d2c3dd469d450a68126575b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543762"
---
# <a name="domains-transact-sql"></a>DOMAINS (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  針對目前資料庫中目前使用者所能存取的每個別名資料類型，各傳回一個資料列。  
  
 若要從這些視圖中取出資訊，請指定 INFORMATION_SCHEMA 的完整名稱 **。**_view_name_。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**DOMAIN_CATALOG**|**Nvarchar (** 128 **) **|別名資料類型所在的資料庫。|  
|**DOMAIN_SCHEMA**|**Nvarchar (** 128 **) **|包含別名資料類型之結構描述的名稱。<br /><br /> **&#42;&#42; 重要 &#42;&#42;** 請勿使用 INFORMATION_SCHEMA views 來判斷資料類型的架構。 尋找類型之結構描述的唯一可靠方式就是使用 TYPEPROPERTY 函數。|  
|**DOMAIN_NAME**|**sysname**|別名資料類型。|  
|**DATA_TYPE**|**sysname**|系統提供的資料類型。|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|二進位資料、字元資料，或文字和影像資料的最大長度 (以字元為單位)。<br /><br /> -1 適用于 **xml** 和大數數值型別的資料。 否則，就傳回 NULL。 如需詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)。|  
|**CHARACTER_OCTET_LENGTH**|**int**|二進位資料、字元資料，或文字和影像資料的最大長度 (以位元組為單位)。<br /><br /> -1 適用于 **xml** 和大數數值型別的資料。 否則，就傳回 NULL。|  
|**COLLATION_CATALOG**|**Varchar (** 6 **) **|一律傳回 NULL。|  
|**COLLATION_SCHEMA**|**Varchar (** 3 **) **|一律傳回 NULL。|  
|**COLLATION_NAME**|**Nvarchar (** 128 **) **|如果資料行是字元資料或 **文字** 資料類型，則傳回排序次序的唯一名稱。 否則，就傳回 NULL。|  
|**CHARACTER_SET_CATALOG**|**Varchar (** 6 **) **|傳回 **master**。 如果資料行是字元資料或 **文字** 資料類型，這會指出字元集所在的資料庫。 否則，就傳回 NULL。|  
|**CHARACTER_SET_SCHEMA**|**Varchar (** 3 **) **|一律傳回 NULL。|  
|**CHARACTER_SET_NAME**|**Nvarchar (** 128 **) **|如果此資料行是字元資料或 **文字** 資料類型，則傳回字元集的唯一名稱。 否則，就傳回 NULL。|  
|**NUMERIC_PRECISION**|**tinyint**|近似數值資料、精確數值資料、整數資料或貨幣資料的有效位數。 否則，就傳回 NULL。|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|近似數值資料、精確數值資料、整數資料或貨幣資料的有效位數基數。 否則，就傳回 NULL。|  
|**NUMERIC_SCALE**|**tinyint**|近似數值資料、精確數值資料、整數資料或貨幣資料的小數位數。 否則，就傳回 NULL。|  
|**DATETIME_PRECISION**|**smallint**|**Datetime**和 ISO **interval**資料類型的子類型代碼。 其他資料類型的這個資料行都會傳回 NULL。|  
|**DOMAIN_DEFAULT**|**Nvarchar (** 4000 **) **|定義 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的實際文字。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視 ](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [&#40;Transact-sql&#41;的資訊架構視圖 ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sys字元集 &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  
