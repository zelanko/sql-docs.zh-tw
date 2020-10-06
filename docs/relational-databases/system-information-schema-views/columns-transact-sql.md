---
description: COLUMNS (Transact-SQL)
title: " (Transact-sql) 的資料行 |Microsoft Docs"
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f4f49fe215279782a5f2e8df8fe501e0619f4bd2
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753613"
---
# <a name="columns-transact-sql"></a>COLUMNS (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  針對目前資料庫中目前使用者所能存取的每個資料行，各傳回一個資料列。  
  
 若要從這些視圖中取出資訊，請指定 **INFORMATION_SCHEMA**_.view_name_的完整名稱。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**Nvarchar (** 128 **) **|資料表限定詞。|  
|**TABLE_SCHEMA**|**Nvarchar (** 128 **) **|包含資料表的結構描述名稱。<br /><br /> **&#42;&#42; 重要 &#42;&#42;** 請勿使用 INFORMATION_SCHEMA views 來判斷物件的架構。 INFORMATION_SCHEMA views 只代表物件的中繼資料子集。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**TABLE_NAME**|**Nvarchar (** 128 **) **|資料表名稱。|  
|**COLUMN_NAME**|**Nvarchar (** 128 **) **|資料行名稱。|  
|**ORDINAL_POSITION**|**int**|資料行識別碼。|  
|**COLUMN_DEFAULT**|**Nvarchar (** 4000 **) **|資料行的預設值。|  
|**IS_NULLABLE**|**Varchar (** 3 **) **|資料行的 Null 屬性。 如果這個資料行允許 NULL，這個資料行就會傳回 YES。 否則，它就會傳回 NO。|  
|**DATA_TYPE**|**Nvarchar (** 128 **) **|系統提供的資料類型。|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|二進位資料、字元資料，或文字和影像資料的最大長度 (以字元為單位)。<br /><br /> -1 適用于 **xml** 和大數數值型別的資料。 否則，就傳回 NULL。 如需詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)。|  
|**CHARACTER_OCTET_LENGTH**|**int**|二進位資料、字元資料，或文字和影像資料的最大長度 (以位元組為單位)。<br /><br /> -1 適用于 **xml** 和大數數值型別的資料。 否則，就傳回 NULL。|  
|**NUMERIC_PRECISION**|**tinyint**|近似數值資料、精確數值資料、整數資料或貨幣資料的有效位數。 否則，就傳回 NULL。|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|近似數值資料、精確數值資料、整數資料或貨幣資料的有效位數基數。 否則，就傳回 NULL。|  
|**NUMERIC_SCALE**|**int**|近似數值資料、精確數值資料、整數資料或貨幣資料的小數位數。 否則，就傳回 NULL。|  
|**DATETIME_PRECISION**|**smallint**|**Datetime**和 ISO **interval**資料類型的子類型代碼。 如果是其他資料類型，就傳回 NULL。|  
|**CHARACTER_SET_CATALOG**|**Nvarchar (** 128 **) **|傳回 **master**。 如果資料行是字元資料或 **文字** 資料類型，這會指出字元集所在的資料庫。 否則，就傳回 NULL。|  
|**CHARACTER_SET_SCHEMA**|**Nvarchar (** 128 **) **|一律傳回 NULL。|  
|**CHARACTER_SET_NAME**|**Nvarchar (** 128 **) **|如果此資料行是字元資料或 **文字** 資料類型，則傳回字元集的唯一名稱。 否則，就傳回 NULL。|  
|**COLLATION_CATALOG**|**Nvarchar (** 128 **) **|一律傳回 NULL。|  
|**COLLATION_SCHEMA**|**Nvarchar (** 128 **) **|一律傳回 NULL。|  
|**COLLATION_NAME**|**Nvarchar (** 128 **) **|如果資料行是字元資料或 **文字** 資料類型，則會傳回定序的唯一名稱。 否則，就傳回 NULL。|  
|**DOMAIN_CATALOG**|**Nvarchar (** 128 **) **|如果資料行是別名資料類型，這個資料行就是建立使用者自訂資料類型的資料庫名稱。 否則，就傳回 NULL。|  
|**DOMAIN_SCHEMA**|**Nvarchar (** 128 **) **|如果資料行是一個使用者自訂資料類型，這個資料行會傳回使用者自訂資料類型的結構描述名稱。 否則，就傳回 NULL。<br /><br /> **&#42;&#42; 重要 &#42;&#42;** 請勿使用 INFORMATION_SCHEMA views 來判斷資料類型的架構。 尋找類型之結構描述的唯一可靠方式就是使用 TYPEPROPERTY 函數。|  
|**DOMAIN_NAME**|**Nvarchar (** 128 **) **|如果資料行是一個使用者自訂資料類型，這個資料行就是使用者自訂資料類型的名稱。 否則，就傳回 NULL。|  
  
## <a name="remarks"></a>備註  
 INFORMATION_SCHEMA 的 **ORDINAL_POSITION** 資料行 **。資料行** 視圖與 COLUMNS_UPDATED 函數所傳回之資料行的位模式不相容。 若要取得與 COLUMNS_UPDATED 相容的位模式，您必須在查詢 INFORMATION_SCHEMA 時參考 COLUMNPROPERTY 系統函數的 **ColumnID** 屬性 **。資料行** 的觀點。 例如：  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TABLE_NAME, COLUMN_NAME, COLUMNPROPERTY(OBJECT_ID(TABLE_SCHEMA + '.' + TABLE_NAME), COLUMN_NAME, 'ColumnID') AS COLUMN_ID  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Person';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視 ](../../t-sql/language-reference.md)   
 [&#40;Transact-sql&#41;的資訊架構視圖 ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sys字元集 &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [COLUMNS_UPDATED &#40;Transact-SQL&#41;](../../t-sql/functions/columns-updated-transact-sql.md)  
  
