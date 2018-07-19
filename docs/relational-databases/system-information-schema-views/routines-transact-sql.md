---
title: 常式 (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ROUTINES_TSQL
- ROUTINES
dev_langs:
- TSQL
helpviewer_keywords:
- ROUTINES view
- INFORMATION_SCHEMA.ROUTINES view
ms.assetid: c75561b2-c9a1-48a1-9afa-a5896b6454cf
caps.latest.revision: 50
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 00ec03e10cd41e964c9687f04478e05871de5b68
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33240598"
---
# <a name="routines-transact-sql"></a>ROUTINES (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對目前資料庫中目前使用者所能存取的每個預存程序和函數，各傳回一個資料列。 描述傳回值的資料行只適用於函數。 如果是預存程序，這些資料行就是 NULL。  
  
 若要從這些檢視中擷取資訊，請指定 INFORMATION_SCHEMA 的完整限定的名稱。*view_name*。  
  
> [!NOTE]  
>  ROUTINE_DEFINITION 資料行包含建立函數或預存程序的來源陳述式。 這些來源陳述式可能包含內嵌歸位字元。 如果您將這個資料行傳回用文字格式來顯示結果的應用程式，ROUTINE_DEFINITION 結果中的內嵌歸位字元可能會影響整體結果集的格式。 如果您選取 ROUTINE_DEFINITION 資料行，您必須針對內嵌歸位字元來進行調整；例如，將結果集傳回方格，或將 ROUTINE_DEFINITION 傳回它自己的文字框。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|SPECIFIC_CATALOG|**nvarchar(** 128 **)**|目錄的特定名稱。 這個名稱與 ROUTINE_CATALOG 相同。|  
|SPECIFIC_SCHEMA|**nvarchar(** 128 **)**|結構描述的特定名稱。<br /><br /> **\*\* 重要\* \*** 請勿使用 INFORMATION_SCHEMA 檢視來判斷物件的結構描述。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|SPECIFIC_NAME|**nvarchar(** 128 **)**|目錄的特定名稱。 這個名稱與 ROUTINE_NAME 相同。|  
|ROUTINE_CATALOG|**nvarchar(** 128 **)**|函數的目錄名稱。|  
|ROUTINE_SCHEMA|**nvarchar(** 128 **)**|包含這個函數的結構描述名稱。<br /><br /> **\*\* 重要\* \*** 請勿使用 INFORMATION_SCHEMA 檢視來判斷物件的結構描述。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|ROUTINE_NAME|**nvarchar(** 128 **)**|函數的名稱。|  
|ROUTINE_TYPE|**nvarchar (** 20 **)**|傳回 PROCEDURE (預存程序) 和 FUNCTION (函數)。|  
|MODULE_CATALOG|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|MODULE_SCHEMA|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|MODULE_NAME|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|UDT_CATALOG|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|UDT_SCHEMA|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|UDT_NAME|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|DATA_TYPE|**nvarchar(** 128 **)**|函數傳回值的資料類型。 傳回**資料表**如果資料表值函式。|  
|CHARACTER_MAXIMUM_LENGTH|**int**|傳回類型是字元類型時的最大長度 (以字元為單位)。<br /><br /> -1 代表**xml**和大數值類型資料。|  
|CHARACTER_OCTET_LENGTH|**int**|傳回類型是字元類型時的最大長度 (以位元組為單位)。<br /><br /> -1 代表**xml**和大數值類型資料。|  
|COLLATION_CATALOG|**nvarchar(** 128 **)**|一律傳回 NULL。|  
|COLLATION_SCHEMA|**nvarchar(** 128 **)**|一律傳回 NULL。|  
|COLLATION_NAME|**nvarchar(** 128 **)**|傳回值的定序名稱。 如果是非字元類型，則傳回 NULL。|  
|CHARACTER_SET_CATALOG|**nvarchar(** 128 **)**|一律傳回 NULL。|  
|CHARACTER_SET_SCHEMA|**nvarchar(** 128 **)**|一律傳回 NULL。|  
|CHARACTER_SET_NAME|**nvarchar(** 128 **)**|傳回值字元集的名稱。 如果是非字元類型，則傳回 NULL。|  
|NUMERIC_PRECISION|**smallint**|傳回值的數值有效位數。 如果是非數值類型，則傳回 NULL。|  
|NUMERIC_PRECISION_RADIX|**smallint**|傳回值的數值有效位數基數。 如果是非數值類型，則傳回 NULL。|  
|NUMERIC_SCALE|**smallint**|傳回值的小數位數。 如果是非數值類型，則傳回 NULL。|  
|DATETIME_PRECISION|**smallint**|如果傳回值的類型，第二個小數有效位數**datetime**。 否則，便傳回 NULL。|  
|INTERVAL_TYPE|**nvarchar (** 30 **)**|NULL。 保留供日後使用。|  
|INTERVAL_PRECISION|**smallint**|NULL。 保留供日後使用。|  
|TYPE_UDT_CATALOG|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|TYPE_UDT_SCHEMA|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|TYPE_UDT_NAME|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|SCOPE_CATALOG|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|SCOPE_SCHEMA|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|SCOPE_NAME|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|MAXIMUM_CARDINALITY|**bigint**|NULL。 保留供日後使用。|  
|DTD_IDENTIFIER|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|ROUTINE_BODY|**nvarchar (** 30 **)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 函數傳回 SQL，外部寫入的函數傳回 EXTERNAL。<br /><br /> 函數一律是 SQL。|  
|ROUTINE_DEFINITION|**nvarchar (** 4000 **)**|如果函數或預存程序未加密，則傳回函數或預存程序之定義文字的前 4000 個字元。 否則，便傳回 NULL。<br /><br /> 若要確保您取得完整定義，請查詢[OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)函式定義中或資料行[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)目錄檢視。|  
|EXTERNAL_NAME|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|EXTERNAL_LANGUAGE|**nvarchar (** 30 **)**|NULL。 保留供日後使用。|  
|PARAMETER_STYLE|**nvarchar (** 30 **)**|NULL。 保留供日後使用。|  
|IS_DETERMINISTIC|**nvarchar (** 10 **)**|如果常式具決定性，便傳回 YES。<br /><br /> 如果常式不具決定性，便傳回 NO。<br /><br /> 預存程序一律傳回 NO。|  
|SQL_DATA_ACCESS|**nvarchar (** 30 **)**|傳回下列其中一值：<br /><br /> NONE = 函數不包含 SQL。<br /><br /> CONTAINS = 函數可能包含 SQL。<br /><br /> READS = 函數可能讀取 SQL 資料。<br /><br /> MODIFIES = 函數可能修改 SQL 資料。<br /><br /> 所有函數都傳回 READS，所有預存程序都傳回 MODIFIES。|  
|IS_NULL_CALL|**nvarchar (** 10 **)**|指出如果常式的任何引數是 NULL，是否要呼叫常式。|  
|SQL_PATH|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|SCHEMA_LEVEL_ROUTINE|**nvarchar (** 10 **)**|如果是結構描述層級函數，便傳回 YES；如果不是結構描述層級函數，便傳回 NO。<br /><br /> 一律傳回 YES。|  
|MAX_DYNAMIC_RESULT_SETS|**smallint**|常式傳回的最大動態結果集數目。<br /><br /> 如果是函數，便傳回 0。|  
|IS_USER_DEFINED_CAST|**nvarchar (** 10 **)**|如果是使用者自訂轉換函數，便傳回 YES；如果不是使用者自訂轉換函數，便傳回 NO。<br /><br /> 一律傳回 NO。|  
|IS_IMPLICITLY_INVOCABLE|**nvarchar (** 10 **)**|如果可以隱含地叫用常式，便傳回 YES；如果不能隱含地叫用常式，便傳回 NO。<br /><br /> 一律傳回 NO。|  
|CREATED|**datetime**|建立常式的時間。|  
|LAST_ALTERED|**datetime**|上次修改函數的時間。|  
  
## <a name="see-also"></a>另請參閱  
 [系統檢視表&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [資訊結構描述檢視&#40;Transact SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.procedures &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)  
  
  
