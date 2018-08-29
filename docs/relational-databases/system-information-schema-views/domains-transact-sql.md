---
title: 網域 (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8e93a4bd265782f4942034b3483f8e045790f5f0
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43063878"
---
# <a name="domains-transact-sql"></a>DOMAINS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對目前資料庫中目前使用者所能存取的每個別名資料類型，各傳回一個資料列。  
  
 若要從這些檢視擷取資訊，請指定 完整格式的名稱 **INFORMATION_SCHEMA。 * * * view_name*。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**DOMAIN_CATALOG**|**nvarchar(** 128 **)**|別名資料類型所在的資料庫。|  
|**DOMAIN_SCHEMA**|**nvarchar(** 128 **)**|包含別名資料類型之結構描述的名稱。<br /><br /> **\*\* 重要\* \*** 請勿使用 INFORMATION_SCHEMA 檢視來判斷資料類型的結構描述。 尋找類型之結構描述的唯一可靠方式就是使用 TYPEPROPERTY 函數。|  
|**網域名稱**|**sysname**|別名資料類型。|  
|**DATA_TYPE**|**sysname**|系統提供的資料類型。|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|二進位資料、字元資料，或文字和影像資料的最大長度 (以字元為單位)。<br /><br /> 傳回-1 **xml**和大數值類型資料。 否則，就傳回 NULL。 如需詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)。|  
|**CHARACTER_OCTET_LENGTH**|**int**|二進位資料、字元資料，或文字和影像資料的最大長度 (以位元組為單位)。<br /><br /> 傳回-1 **xml**和大數值類型資料。 否則，就傳回 NULL。|  
|**COLLATION_CATALOG**|**varchar (** 6 **)**|一律傳回 NULL。|  
|**COLLATION_SCHEMA**|**varchar (** 3 **)**|一律傳回 NULL。|  
|**COLLATION_NAME**|**nvarchar(** 128 **)**|傳回排序順序的唯一名稱，如果資料行是字元資料或**文字**資料型別。 否則，就傳回 NULL。|  
|**CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|傳回**主要**。 這表示如果資料行是字元資料的字元集，資料庫或**文字**資料型別。 否則，就傳回 NULL。|  
|**CHARACTER_SET_SCHEMA**|**varchar (** 3 **)**|一律傳回 NULL。|  
|**CHARACTER_SET_NAME**|**nvarchar(** 128 **)**|傳回這個資料行是否為字元資料的字元集的唯一名稱或**文字**資料型別。 否則，就傳回 NULL。|  
|**NUMERIC_PRECISION**|**tinyint**|近似數值資料、精確數值資料、整數資料或貨幣資料的有效位數。 否則，就傳回 NULL。|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|近似數值資料、精確數值資料、整數資料或貨幣資料的有效位數基數。 否則，就傳回 NULL。|  
|**NUMERIC_SCALE**|**tinyint**|近似數值資料、精確數值資料、整數資料或貨幣資料的小數位數。 否則，就傳回 NULL。|  
|**DATETIME_PRECISION**|**smallint**|子類型代碼**datetime**和 ISO**間隔**資料型別。 其他資料類型的這個資料行都會傳回 NULL。|  
|**DOMAIN_DEFAULT**|**nvarchar (** 4000 **)**|定義 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的實際文字。|  
  
## <a name="see-also"></a>另請參閱  
 [系統檢視表&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [資訊結構描述檢視&#40;Transact SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.syscharsets &#40;Transact SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  
