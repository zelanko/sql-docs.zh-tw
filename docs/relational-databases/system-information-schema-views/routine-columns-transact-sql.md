---
description: ROUTINE_COLUMNS (Transact-SQL)
title: ROUTINE_COLUMNS (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8cda806de638edcea2c7b28cfa850414c90006a2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550121"
---
# <a name="routine_columns-transact-sql"></a>ROUTINE_COLUMNS (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  針對目前資料庫中目前使用者所能存取的資料表值函式所能傳回的每個資料行，各傳回一個資料列。  
  
 若要從此視圖取出資訊，請指定 INFORMATION_SCHEMA 的完整名稱 **。**_view_name_。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**Nvarchar (** 128 **) **|資料表值函式的目錄或資料庫名稱。|  
|**TABLE_SCHEMA**|**Nvarchar (** 128 **) **|包含資料表值函式的結構描述名稱。<br /><br /> <strong> \* \* 重要 \* 事項 \* ：</strong>請勿使用 INFORMATION_SCHEMA views 來判斷物件的架構。 INFORMATION_SCHEMA views 只代表物件的中繼資料子集。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**TABLE_NAME**|**Nvarchar (** 128 **) **|資料表值函式的名稱。|  
|**COLUMN_NAME**|**Nvarchar (** 128 **) **|資料行名稱。|  
|**ORDINAL_POSITION**|**int**|資料行識別碼。|  
|**COLUMN_DEFAULT**|**Nvarchar (** 4000 **) **|資料行的預設值。|  
|**IS_NULLABLE**|**Varchar (** 3 **) **|如果這個資料行允許 NULL，就會傳回 YES。 否則，便傳回 NO。|  
|**DATA_TYPE**|**Nvarchar (** 128 **) **|系統提供的資料類型。|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|二進位資料、字元資料，或文字和影像資料的最大長度 (以字元為單位)。<br /><br /> -1 適用于 **xml** 和大數數值型別的資料。 否則，便傳回 NULL。 如需詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)。|  
|**CHARACTER_OCTET_LENGTH**|**int**|二進位資料、字元資料，或文字和影像資料的最大長度 (以位元組為單位)。<br /><br /> -1 適用于 **xml** 和大數數值型別的資料。 否則，便傳回 NULL。|  
|**NUMERIC_PRECISION**|**tinyint**|近似數值資料、精確數值資料、整數資料或貨幣資料的有效位數。 否則，便傳回 NULL。|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|近似數值資料、精確數值資料、整數資料或貨幣資料的有效位數基數。 否則，便傳回 NULL。|  
|**NUMERIC_SCALE**|**tinyint**|近似數值資料、精確數值資料、整數資料或貨幣資料的小數位數。 否則，便傳回 NULL。|  
|**DATETIME_PRECISION**|**smallint**|**Datetime**和 ISO**整數**資料類型的子類型代碼。 如果是其他資料類型，便傳回 NULL。|  
|**CHARACTER_SET_CATALOG**|**Varchar (** 6 **) **|傳回 **master**。 這表示如果資料行是字元資料或 **文字** 資料類型，則為字元集所在的資料庫。 否則，便傳回 NULL。|  
|**CHARACTER_SET_SCHEMA**|**Varchar (** 3 **) **|一律傳回 NULL。|  
|**CHARACTER_SET_NAME**|**Nvarchar (** 128 **) **|如果此資料行是字元資料或 **文字** 資料類型，則傳回字元集的唯一名稱。 否則，便傳回 NULL。|  
|**COLLATION_CATALOG**|**Varchar (** 6 **) **|一律傳回 NULL。|  
|**COLLATION_SCHEMA**|**Varchar (** 3 **) **|一律傳回 NULL。|  
|**COLLATION_NAME**|**Nvarchar (** 128 **) **|如果資料行是字元資料或 **文字** 資料類型，則傳回排序次序的唯一名稱。 否則，便傳回 NULL。|  
|**DOMAIN_CATALOG**|**Nvarchar (** 128 **) **|如果資料行是別名資料類型，這個資料行就是建立使用者自訂資料類型的資料庫名稱。 否則，便傳回 NULL。|  
|**DOMAIN_SCHEMA**|**Nvarchar (** 128 **) **|如果資料行是一個使用者自訂資料類型，這個資料行就是包含使用者自訂資料類型之結構描述的名稱。 否則，便傳回 NULL。<br /><br /> <strong> \* \* 重要 \* 事項 \* ：</strong>請勿使用 INFORMATION_SCHEMA views 來判斷物件的架構。 INFORMATION_SCHEMA views 只代表物件的中繼資料子集。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**DOMAIN_NAME**|**Nvarchar (** 128 **) **|如果資料行是一個使用者自訂資料類型，這個資料行就是使用者自訂資料類型的名稱。 否則，便傳回 NULL。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視 ](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [&#40;Transact-sql&#41;的資訊架構視圖 ](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
