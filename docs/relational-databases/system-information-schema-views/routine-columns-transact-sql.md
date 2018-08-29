---
title: ROUTINE_COLUMNS (TRANSACT-SQL) |Microsoft Docs
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
- ROUTINE_COLUMNS_TSQL
- ROUTINE_COLUMNS
dev_langs:
- TSQL
helpviewer_keywords:
- ROUTINE_COLUMNS view
- INFORMATION_SCHEMA.ROUTINE_COLUMNS view
ms.assetid: 91dbc61b-e4c0-4826-976c-b2fce88b7793
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e976804e34e7074b23f89ba8c61eeb46a7d3d9e7
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43110461"
---
# <a name="routinecolumns-transact-sql"></a>ROUTINE_COLUMNS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對目前資料庫中目前使用者所能存取的資料表值函式所能傳回的每個資料行，各傳回一個資料列。  
  
 若要從這個檢視中擷取資訊，請指定 完整格式的名稱 **INFORMATION_SCHEMA。 * * * view_name*。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG 排列**|**nvarchar(** 128 **)**|資料表值函式的目錄或資料庫名稱。|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|包含資料表值函式的結構描述名稱。<br /><br /> **\*\* 重要\* \*** 請勿使用 INFORMATION_SCHEMA 檢視來判斷物件的結構描述。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**TABLE_NAME**|**nvarchar(** 128 **)**|資料表值函式的名稱。|  
|**COLUMN_NAME**|**nvarchar(** 128 **)**|資料行名稱。|  
|**ORDINAL_POSITION**|**int**|資料行識別碼。|  
|**COLUMN_DEFAULT**|**nvarchar (** 4000 **)**|資料行的預設值。|  
|**IS_NULLABLE**|**varchar (** 3 **)**|如果這個資料行允許 NULL，就會傳回 YES。 否則，便傳回 NO。|  
|**DATA_TYPE**|**nvarchar(** 128 **)**|系統提供的資料類型。|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|二進位資料、字元資料，或文字和影像資料的最大長度 (以字元為單位)。<br /><br /> 傳回-1 **xml**和大數值類型資料。 否則，便傳回 NULL。 如需詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)。|  
|**CHARACTER_OCTET_LENGTH**|**int**|二進位資料、字元資料，或文字和影像資料的最大長度 (以位元組為單位)。<br /><br /> 傳回-1 **xml**和大數值類型資料。 否則，便傳回 NULL。|  
|**NUMERIC_PRECISION**|**tinyint**|近似數值資料、精確數值資料、整數資料或貨幣資料的有效位數。 否則，便傳回 NULL。|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|近似數值資料、精確數值資料、整數資料或貨幣資料的有效位數基數。 否則，便傳回 NULL。|  
|**NUMERIC_SCALE**|**tinyint**|近似數值資料、精確數值資料、整數資料或貨幣資料的小數位數。 否則，便傳回 NULL。|  
|**DATETIME_PRECISION**|**smallint**|子類型代碼**datetime**和 ISO**整數**資料型別。 如果是其他資料類型，便傳回 NULL。|  
|**CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|傳回**主要**。 指出字元集所在如果資料行是字元資料的資料庫或**文字**資料型別。 否則，便傳回 NULL。|  
|**CHARACTER_SET_SCHEMA**|**varchar (** 3 **)**|一律傳回 NULL。|  
|**CHARACTER_SET_NAME**|**nvarchar(** 128 **)**|傳回這個資料行是否為字元資料的字元集的唯一名稱或**文字**資料型別。 否則，便傳回 NULL。|  
|**COLLATION_CATALOG**|**varchar (** 6 **)**|一律傳回 NULL。|  
|**COLLATION_SCHEMA**|**varchar (** 3 **)**|一律傳回 NULL。|  
|**COLLATION_NAME**|**nvarchar(** 128 **)**|傳回排序順序的唯一名稱，如果資料行是字元資料或**文字**資料型別。 否則，便傳回 NULL。|  
|**DOMAIN_CATALOG**|**nvarchar(** 128 **)**|如果資料行是別名資料類型，這個資料行就是建立使用者自訂資料類型的資料庫名稱。 否則，便傳回 NULL。|  
|**DOMAIN_SCHEMA**|**nvarchar(** 128 **)**|如果資料行是一個使用者自訂資料類型，這個資料行就是包含使用者自訂資料類型之結構描述的名稱。 否則，便傳回 NULL。<br /><br /> **\*\* 重要\* \*** 請勿使用 INFORMATION_SCHEMA 檢視來判斷物件的結構描述。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**網域名稱**|**nvarchar(** 128 **)**|如果資料行是一個使用者自訂資料類型，這個資料行就是使用者自訂資料類型的名稱。 否則，便傳回 NULL。|  
  
## <a name="see-also"></a>另請參閱  
 [系統檢視表&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [資訊結構描述檢視&#40;Transact SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
