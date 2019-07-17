---
title: sp_addtype (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addtype
- sp_addtype_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addtype
ms.assetid: ed72cd8e-5ff7-4084-8458-2d8ed279d817
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4e52fb6700d0af133a687c8b93e28cd12f72221c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68117919"
---
# <a name="spaddtype-transact-sql"></a>sp_addtype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立別名資料型別。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[CREATE TYPE](../../t-sql/statements/create-type-transact-sql.md)改。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addtype [ @typename = ] type,   
    [ @phystype = ] system_data_type   
    [ , [ @nulltype = ] 'null_type' ] ;  
```  
  
## <a name="arguments"></a>引數  
`[ @typename = ] type` 是別名資料類型的名稱。 別名資料型別名稱必須遵循的規則[識別碼](../../relational-databases/databases/database-identifiers.md)和每個資料庫中必須是唯一。 *型別*已**sysname**，沒有預設值。  
  
`[ @phystype = ] system_data_type` 是實體、 或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供的別名資料類型所依據的資料類型。*system_data_type*已**sysname**，沒有預設值，它可以是下列值之一：  
  
||||  
|-|-|-|  
|**bigint**|**binary(n)**|**bit**|  
|**char(n)**|**datetime**|**decimal**|  
|**float**|**image**|**int**|  
|**money**|**nchar(n)**|**ntext**|  
|**numeric**|**nvarchar(n)**|**real**|  
|**smalldatetime**|**smallint**|**smallmoney**|  
|**sql_variant**|**text**|**tinyint**|  
|**uniqueidentifier**|**varbinary(n)**|**varchar(n)**|  
  
 有內嵌的空格或標點符號的所有參數，其前後需要加上引號。 如需可用的資料類型的詳細資訊，請參閱 <<c0> [ 資料類型&#40;TRANSACT-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)。</c0>  
  
 *n*  
 這是非負數整數，表示所選資料類型的長度。  
  
 *P*  
 這是一個非負數整數，它指出可儲存的最大十進位數總數，小數點左右兩側都包括在內。 如需詳細資訊，請參閱 [decimal 和 numeric &#40;TRANSACT-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)。  
  
 *s*  
 這是一個非負數整數值，它指出小數點右側所能儲存的最大十進位數，且它必須小於或等於有效位數。 如需詳細資訊，請參閱 [decimal 和 numeric &#40;TRANSACT-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)。  
  
`[ @nulltype = ] 'null_type'` 指出別名資料型別處理 null 值的方式。 *null_type*已**varchar (** 8 **)** ，預設值是 NULL，且必須括在單引號 （'NULL'、 'NOT NULL' 或 'NONULL'）。 如果*null_type*未明確定義**sp_addtype**，它會設定為目前的預設 null 屬性。 您可以利用 GETANSINULL 系統函數來決定目前的預設 Null 屬性。 您可以利用 SET 陳述式或 ALTER DATABASE來調整這項作業。 Null 屬性應明確定義。 如果 **@phystype** 是**元**，和 **@nulltype** 未指定，預設值不是 NULL。  
  
> [!NOTE]  
>  *Null_type*參數只會定義此資料類型的預設 null 屬性。 如果在使用別名資料型別時 (在資料表建立期間) 明確定義 Null 屬性，它的優先順序高於定義的 Null 屬性。 如需詳細資訊，請參閱 < [ALTER TABLE &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-table-transact-sql.md)並[CREATE TABLE &#40;-&#41;](../../t-sql/statements/create-table-transact-sql.md)。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 別名資料型別名稱在資料庫中必須是唯一的，但名稱不同的別名資料型別可以有相同的定義。  
  
 執行**sp_addtype**會建立別名資料類型，會出現在**sys.types**目錄檢視中的特定資料庫。 如果別名資料類型必須是可在所有新的使用者定義資料庫中，將它加入**模型**。 建立別名資料型別之後，您可以在 CREATE TABLE 或 ALTER TABLE 中使用它，您也可以將預設值和規則繫結到該別名資料型別。 使用所建立的所有純量別名資料類型**sp_addtype**中所包含**dbo**結構描述。  
  
 別名資料型別繼承資料庫的預設定序。 資料行的定序和別名類型的變數定義於[!INCLUDE[tsql](../../includes/tsql-md.md)]CREATE TABLE、 ALTER TABLE 及 DECLARE @*local_variable*陳述式。 資料庫的預設定序變更只會套用至該類型的新資料行和變數；它不會改變現有類型的定序。  
  
> [!IMPORTANT]  
>  基於回溯相容性**公開金鑰**資料庫角色會自動授與使用所建立的別名資料類型的 REFERENCES 權限**sp_addtype**。 請注意使用 CREATE TYPE 陳述式，而非建立別名資料型別時**sp_addtype**，就會發生任何這類自動授與。  
  
 別名資料類型無法定義利用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**時間戳記**，**表格**， **xml**， **varchar （max)** ， **nvarchar （max)** 或是**varbinary （max)** 資料型別。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**db_owner**或是**db_ddladmin**固定的資料庫角色。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-an-alias-data-type-that-does-not-allow-for-null-values"></a>A. 建立不允許 Null 值的別名資料型別  
 下列範例會建立名為別名資料類型`ssn`（身分證號碼） 為基礎[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-提供**varchar**資料型別。 `ssn` 資料類型用於保留 11 位數之社會保險號碼 (999-99-9999) 的資料行。 該資料行不能是 NULL。  
  
 請注意，`varchar(11)` 以單引號括住，因為它包含標點 (括號)。  
  
```  
USE master;  
GO  
EXEC sp_addtype ssn, 'varchar(11)', 'NOT NULL';  
GO  
```  
  
### <a name="b-creating-an-alias-data-type-that-allows-for-null-values"></a>B. 建立允許 Null 值的別名資料型別  
 下列範例建立一個名為 `datetime` 的別名資料型別 (以 `birthday` 為基礎) ，它允許 Null 值。  
  
```  
USE master;  
GO  
EXEC sp_addtype birthday, datetime, 'NULL';  
```  
  
### <a name="c-creating-additional-alias-data-types"></a>C. 建立其他別名資料型別  
 下列範例建立兩個其他的別名資料型別 `telephone` 和 `fax`，這兩個資料類型可供國內和國際電話和傳真號碼使用。  
  
```  
USE master;  
GO  
EXEC sp_addtype telephone, 'varchar(24)', 'NOT NULL';  
GO  
EXEC sp_addtype fax, 'varchar(24)', 'NULL';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [sp_bindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_bindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_droptype &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droptype-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_unbindefault &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)   
 [sp_unbindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
