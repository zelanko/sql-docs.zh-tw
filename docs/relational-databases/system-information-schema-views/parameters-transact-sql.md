---
title: 參數 (TRANSACT-SQL) |Microsoft Docs
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
- PARAMETERS_TSQL
- PARAMETERS
dev_langs:
- TSQL
helpviewer_keywords:
- PARAMETERS view
- INFORMATION_SCHEMA.PARAMETERS view
ms.assetid: 06ded0ca-7d21-4400-864a-b801e855b257
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9289f3db5d046d3922340c33e79ef02c266b39d4
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43062321"
---
# <a name="parameters-transact-sql"></a>PARAMETERS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對目前資料庫中目前的使用者所能存取之使用者自訂函數或預存程序的每個參數，各傳回一個資料列。 如果是函數，這份檢視也會傳回一個含有傳回值資訊的資料列。  
  
 若要從這些檢視擷取資訊，請指定 完整格式的名稱 **INFORMATION_SCHEMA。 * * * view_name*。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**SPECIFIC_CATALOG**|**nvarchar(** 128 **)**|以這個項目為參數的常式之目錄名稱。|  
|**SPECIFIC_SCHEMA**|**nvarchar(** 128 **)**|以這個項目為參數的常式之結構描述名稱。<br /><br /> **\*\* 重要\* \*** 請勿使用 INFORMATION_SCHEMA 檢視來判斷物件的結構描述。 尋找物件之結構描述的唯一可靠方式就是查詢 sys.objects 目錄檢視。|  
|**SPECIFIC_NAME 排列順序**|**nvarchar(** 128 **)**|以這個項目為參數的常式名稱。|  
|**ORDINAL_POSITION**|**int**|參數的序數位置從 1 開始。 若為函數的傳回值，則是 0。|  
|**PARAMETER_MODE**|**nvarchar (** 10 **)**|如果是輸入參數，便傳回 IN；如果是輸出參數，便傳回 OUT，如果是輸入/輸出參數，便傳回 INOUT。|  
|**IS_RESULT**|**nvarchar (** 10 **)**|如果指出常式的結果是函數，便傳回 YES。 否則，便傳回 NO。|  
|**AS_LOCATOR**|**nvarchar (** 10 **)**|如果宣告成定位器，便傳回 YES。 否則，便傳回 NO。|  
|**PARAMETER_NAME**|**nvarchar(** 128 **)**|參數的名稱。 如果這對應於函數的傳回值，便是 NULL。|  
|**DATA_TYPE**|**nvarchar(** 128 **)**|系統提供的資料類型。|  
|**CHARACTER_MAXIMUM_LENGTH**|**int**|二進位或字元資料類型的最大長度 (以字元為單位)。<br /><br /> 傳回-1 **xml**和大數值類型資料。 否則，便傳回 NULL。|  
|**CHARACTER_OCTET_LENGTH**|**int**|二進位或字元資料類型的最大長度 (以位元組為單位)。<br /><br /> 傳回-1 **xml**和大數值類型資料。 否則，便傳回 NULL。|  
|**COLLATION_CATALOG**|**nvarchar(** 128 **)**|一律傳回 NULL。|  
|**COLLATION_SCHEMA**|**nvarchar(** 128 **)**|一律傳回 NULL。|  
|**COLLATION_NAME**|**nvarchar(** 128 **)**|參數的定序名稱。 如果不是字元類型之一，便傳回 NULL。|  
|**CHARACTER_SET_CATALOG**|**nvarchar(** 128 **)**|參數字元集的目錄名稱。 如果不是字元類型之一，便傳回 NULL。|  
|**CHARACTER_SET_SCHEMA**|**nvarchar(** 128 **)**|一律傳回 NULL。|  
|**CHARACTER_SET_NAME**|**nvarchar(** 128 **)**|參數字元集的名稱。 如果不是字元類型之一，便傳回 NULL。|  
|**NUMERIC_PRECISION**|**tinyint**|近似數值資料、精確數值資料、整數資料或貨幣資料的有效位數。 否則，便傳回 NULL。|  
|**NUMERIC_PRECISION_RADIX**|**smallint**|近似數值資料、精確數值資料、整數資料或貨幣資料的有效位數基數。 否則，便傳回 NULL。|  
|**NUMERIC_SCALE**|**tinyint**|近似數值資料、精確數值資料、整數資料或貨幣資料的小數位數。 否則，便傳回 NULL。|  
|**DATETIME_PRECISION**|**smallint**|如果參數類型的小數秒的有效位數**datetime**或是**smalldatetime**。 否則，便傳回 NULL。|  
|**INTERVAL_TYPE**|**nvarchar (** 30 **)**|NULL。 保留供日後使用。|  
|**INTERVAL_PRECISION**|**smallint**|NULL。 保留供日後使用。|  
|**USER_DEFINED_TYPE_CATALOG**|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|**USER_DEFINED_TYPE_SCHEMA**|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|**USER_DEFINED_TYPE_NAME**|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|**SCOPE_CATALOG**|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|**SCOPE_SCHEMA**|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
|**SCOPE_NAME**|**nvarchar(** 128 **)**|NULL。 保留供日後使用。|  
  
## <a name="see-also"></a>另請參閱  
 [系統檢視表&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [資訊結構描述檢視&#40;Transact SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  
