---
title: sp_addtype （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c876b024b0e8dd218064999adde4a43a18404829
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833584"
---
# <a name="sp_addtype-transact-sql"></a>sp_addtype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立別名資料型別。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用[CREATE TYPE](../../t-sql/statements/create-type-transact-sql.md) 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addtype [ @typename = ] type,   
    [ @phystype = ] system_data_type   
    [ , [ @nulltype = ] 'null_type' ] ;  
```  
  
## <a name="arguments"></a>引數  
`[ @typename = ] type`這是別名資料類型的名稱。 別名資料類型名稱必須遵循[識別碼](../../relational-databases/databases/database-identifiers.md)的規則，而且在每個資料庫中都必須是唯一的。 *類型*為**sysname**，沒有預設值。  
  
`[ @phystype = ] system_data_type`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]這是別名資料類型所依據的實體或提供的資料類型。*system_data_type*是**sysname**，沒有預設值，而且可以是下列其中一個值：  
  
||||  
|-|-|-|  
|**bigint**|**binary(n)**|**bit**|  
|**char(n)**|**datetime**|**decimal**|  
|**float**|**image**|**int**|  
|**money**|**Nchar （n）**|**ntext**|  
|**numeric**|**Nvarchar （n）**|**real**|  
|**smalldatetime**|**smallint**|**smallmoney**|  
|**sql_variant**|**text**|**tinyint**|  
|**uniqueidentifier**|**varbinary(n)**|**varchar(n)**|  
  
 有內嵌的空格或標點符號的所有參數，其前後需要加上引號。 如需可用資料類型的詳細資訊，請參閱[&#40;transact-sql&#41;的資料類型](../../t-sql/data-types/data-types-transact-sql.md)。  
  
 *n*  
 這是非負數整數，表示所選資料類型的長度。  
  
 *P*  
 這是一個非負數整數，它指出可儲存的最大十進位數總數，小數點左右兩側都包括在內。 如需詳細資訊，請參閱 [decimal 和 numeric &#40;TRANSACT-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)。  
  
 *今日*  
 這是一個非負數整數值，它指出小數點右側所能儲存的最大十進位數，且它必須小於或等於有效位數。 如需詳細資訊，請參閱 [decimal 和 numeric &#40;TRANSACT-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)。  
  
`[ @nulltype = ] 'null_type'`指出別名資料類型處理 null 值的方式。 *null_type*是**Varchar （** 8 **）**，預設值是 null，而且必須以單引號括住（' null '、' NOT null ' 或 ' NONull '）。 如果*null_type*未由**sp_addtype**明確定義，則會設定為目前的預設 null 屬性。 您可以利用 GETANSINULL 系統函數來決定目前的預設 Null 屬性。 您可以利用 SET 陳述式或 ALTER DATABASE來調整這項作業。 Null 屬性應明確定義。 如果** \@ phystype**為**bit**，而且未指定** \@ NullTYPE** ，則預設值為 not Null。  
  
> [!NOTE]  
>  *Null_type*參數只會定義此資料類型的預設 null 屬性。 如果在使用別名資料型別時 (在資料表建立期間) 明確定義 Null 屬性，它的優先順序高於定義的 Null 屬性。 如需詳細資訊，請參閱[ALTER TABLE &#40;transact-sql&#41;](../../t-sql/statements/alter-table-transact-sql.md)和[CREATE TABLE &#40;transact-sql&#41;](../../t-sql/statements/create-table-transact-sql.md)。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 別名資料型別名稱在資料庫中必須是唯一的，但名稱不同的別名資料型別可以有相同的定義。  
  
 執行**sp_addtype**會建立一個別名資料類型，它會出現在特定資料庫的**sys.databases**目錄檢視中。 如果別名資料類型在所有新的使用者自訂資料庫中都必須可用，請將它加入至**模型**。 建立別名資料型別之後，您可以在 CREATE TABLE 或 ALTER TABLE 中使用它，您也可以將預設值和規則繫結到該別名資料型別。 使用**sp_addtype**建立的所有純量別名資料類型都會包含在**dbo**架構中。  
  
 別名資料型別繼承資料庫的預設定序。 別名類型之資料行和變數的定序是在 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TABLE、ALTER TABLE 和 DECLARE @*local_variable*語句中定義。 資料庫的預設定序變更只會套用至該類型的新資料行和變數；它不會改變現有類型的定序。  
  
> [!IMPORTANT]  
>  為了回溯相容性目的，**公用**資料庫角色會自動授與使用**sp_addtype**所建立之別名資料類型的 REFERENCES 許可權。 請注意，使用 CREATE TYPE 語句（而不是**sp_addtype**）建立別名資料類型時，不會發生這類自動授與。  
  
 無法使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp**、 **table**、 **xml**、 **Varchar （max）**、 **Nvarchar （max）** 或**Varbinary （max）** 資料類型來定義別名資料類型。  
  
## <a name="permissions"></a>權限  
 需要**db_owner**或**db_ddladmin**固定資料庫角色中的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-an-alias-data-type-that-does-not-allow-for-null-values"></a>A. 建立不允許 Null 值的別名資料型別  
 下列範例 `ssn` 會根據 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供的**Varchar**資料類型，建立名為（社會保險號碼）的別名資料類型。 `ssn` 資料類型用於保留 11 位數之社會保險號碼 (999-99-9999) 的資料行。 該資料行不能是 NULL。  
  
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
 [資料庫引擎預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE TYPE &#40;Transact-sql&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [sp_bindefault &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_bindrule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_droptype &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droptype-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_unbindefault &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)   
 [sp_unbindrule &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
