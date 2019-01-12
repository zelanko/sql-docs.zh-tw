---
title: 資料行 (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- COLUMNS
- COLUMNS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- COLUMNS view
- INFORMATION_SCHEMA.COLUMNS view
ms.assetid: bbf7ac4a-7444-4351-a590-a9f71e0bc495
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f6a14751ea8a0b268c846935e5058c10d79b4d60
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54131778"
---
# <a name="columns-transact-sql"></a>COLUMNS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對目前資料庫中目前使用者所能存取的每個資料行，各傳回一個資料列。  
  
 若要從這些檢視擷取資訊，請指定 完整格式的名稱**INFORMATION_SCHEMA**_.view_name_。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG 排列**|**nvarchar(** 128 **)**|資料表限定詞。|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|包含資料表的結構描述名稱。<br /><br /> **&#42;&#42;重要&#42; &#42;** 請勿使用 INFORMATION_SCHEMA 檢視來判斷物件的結構描述。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**TABLE_NAME**|**nvarchar(** 128 **)**|資料表名稱。|  
|**COLUMN_NAME**|**nvarchar(** 128 **)**|資料行名稱。|  
|**ORDINAL_POSITION**|**int**|資料行識別碼。|  
|**COLUMN_DEFAULT**|**nvarchar (** 4000 **)**|資料行的預設值。|  
|**IS_NULLABLE**|**varchar (** 3 **)**|資料行的 Null 屬性。 如果這個資料行允許 NULL，這個資料行就會傳回 YES。 否則，它就會傳回 NO。|  
|**DATA_TYPE**|**nvarchar(** 128 **)**|系統提供的資料類型。|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|二進位資料、字元資料，或文字和影像資料的最大長度 (以字元為單位)。<br /><br /> 傳回-1 **xml**和大數值類型資料。 否則，就傳回 NULL。 如需詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)。|  
|**CHARACTER_OCTET_LENGTH**|**int**|二進位資料、字元資料，或文字和影像資料的最大長度 (以位元組為單位)。<br /><br /> 傳回-1 **xml**和大數值類型資料。 否則，就傳回 NULL。|  
|**NUMERIC_PRECISION**|**tinyint**|近似數值資料、精確數值資料、整數資料或貨幣資料的有效位數。 否則，就傳回 NULL。|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|近似數值資料、精確數值資料、整數資料或貨幣資料的有效位數基數。 否則，就傳回 NULL。|  
|**NUMERIC_SCALE**|**int**|近似數值資料、精確數值資料、整數資料或貨幣資料的小數位數。 否則，就傳回 NULL。|  
|**DATETIME_PRECISION**|**smallint**|子類型代碼**datetime**和 ISO**間隔**資料型別。 如果是其他資料類型，就傳回 NULL。|  
|**CHARACTER_SET_CATALOG**|**nvarchar(** 128 **)**|傳回**主要**。 這表示如果資料行是字元資料的字元集，資料庫或**文字**資料型別。 否則，就傳回 NULL。|  
|**CHARACTER_SET_SCHEMA**|**nvarchar(** 128 **)**|一律傳回 NULL。|  
|**CHARACTER_SET_NAME**|**nvarchar(** 128 **)**|傳回這個資料行是否為字元資料的字元集的唯一名稱或**文字**資料型別。 否則，就傳回 NULL。|  
|**COLLATION_CATALOG**|**nvarchar(** 128 **)**|一律傳回 NULL。|  
|**COLLATION_SCHEMA**|**nvarchar(** 128 **)**|一律傳回 NULL。|  
|**COLLATION_NAME**|**nvarchar(** 128 **)**|傳回定序的唯一名稱，如果資料行是字元資料或**文字**資料型別。 否則，就傳回 NULL。|  
|**DOMAIN_CATALOG**|**nvarchar(** 128 **)**|如果資料行是別名資料類型，這個資料行就是建立使用者自訂資料類型的資料庫名稱。 否則，就傳回 NULL。|  
|**DOMAIN_SCHEMA**|**nvarchar(** 128 **)**|如果資料行是一個使用者自訂資料類型，這個資料行會傳回使用者自訂資料類型的結構描述名稱。 否則，就傳回 NULL。<br /><br /> **&#42;&#42;重要&#42; &#42;** 請勿使用 INFORMATION_SCHEMA 檢視來判斷資料類型的結構描述。 尋找類型之結構描述的唯一可靠方式就是使用 TYPEPROPERTY 函數。|  
|**網域名稱**|**nvarchar(** 128 **)**|如果資料行是一個使用者自訂資料類型，這個資料行就是使用者自訂資料類型的名稱。 否則，就傳回 NULL。|  
  
## <a name="remarks"></a>備註  
 **ORDINAL_POSITION**資料行**INFORMATION_SCHEMA。資料行**檢視不相容於 COLUMNS_UPDATED 函數所傳回的資料行的位元模式。 若要取得相容於 COLUMNS_UPDATED 的位元模式，您必須參考**ColumnID**查詢時，才會進行 COLUMNPROPERTY 系統函數的屬性**INFORMATION_SCHEMA。資料行**檢視。 例如：  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TABLE_NAME, COLUMN_NAME, COLUMNPROPERTY(OBJECT_ID(TABLE_SCHEMA + '.' + TABLE_NAME), COLUMN_NAME, 'ColumnID') AS COLUMN_ID  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Person';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統檢視表&#40;Transact SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [資訊結構描述檢視&#40;Transact SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.syscharsets &#40;Transact SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [COLUMNS_UPDATED &#40;Transact SQL&#41;](../../t-sql/functions/columns-updated-transact-sql.md)  
  
  
