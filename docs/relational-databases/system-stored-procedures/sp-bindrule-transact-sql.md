---
title: sp_bindrule (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_bindrule_TSQL
- sp_bindrule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindrule
ms.assetid: 2606073e-c52f-498d-a923-5026b9d97e67
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 76d1572e1f99162c8daebeafadb0c8d75a53a4d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046034"
---
# <a name="spbindrule-transact-sql"></a>sp_bindrule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  將規則繫結到資料行或別名資料類型。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 使用[Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)改。 檢查條件約束藉由使用的 CHECK 關鍵字[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)或是[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)陳述式。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_bindrule [ @rulename = ] 'rule' ,   
     [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @rulename = ] 'rule'` 是 CREATE RULE 陳述式所建立之規則的名稱。 *規則*已**nvarchar(776)** ，沒有預設值。  
  
`[ @objname = ] 'object_name'` 是的資料表和資料行或別名資料類型的規則是繫結。 規則無法繫結到 **text**、 **ntext** **image**、**varchar (max)** 、**nvarchar(max)** 、**varbinary(max)** 、**xml**、CLR 使用者定義型別或 **timestamp** 資料行。 規則無法繫結到計算資料行。  
  
 *object_name*已**nvarchar(776)** 沒有預設值。 如果*object_name*是單部分名稱，它會解析成別名資料類型。 如果它是兩部分或三部分的名稱，就會先將它解析成資料表和資料行；如果這項解析失敗，就會將它解析成別名資料類型。 根據預設，現有的資料行別名資料類型的繼承*規則*除非規則有直接繫結資料行。  
  
> [!NOTE]  
>  *object_name*可以包含方括號 **[** 並 **]** 為分隔的識別碼字元的字元。 如需詳細資訊，請參閱＜ [Database Identifiers](../../relational-databases/databases/database-identifiers.md)＞。  
  
> [!NOTE]  
>  雖然在使用別名資料類型的運算式上建立的規則可以繫結到資料行或別名資料類型，但在參考它們時，會無法編譯它們。 請避免使用在別名資料類型上建立的規則。  
  
`[ @futureonly = ] 'futureonly_flag'` 只有在將規則繫結到別名資料類型時，才使用。 *future_only_flag*已**varchar(15)** 預設值是 NULL。 當設定為此參數**futureonly**防止別名資料類型的現有資料行會繼承新規則。 如果*futureonly_flag*是 NULL，新規則繫結至任何資料行的別名資料類型，目前有任何規則，或使用現有的別名資料類型的規則。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 您可以將規則繫結新的資料行 （雖然使用 CHECK 條件約束是慣用作業） 或使用別名資料型別**sp_bindrule**沒有現有的規則解除繫結。 此時會覆寫舊規則。 如果規則是利用現有 CHECK 條件約束來繫結到資料行，便會評估所有限制。 您不能將規則繫結到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。  
  
 在嘗試 INSERT 陳述式時，而非在繫結時，會強制執行這個規則。 您可以將字元規則繫結的資料行**數值**資料類型，雖然這類 INSERT 作業無效。  
  
 別名資料類型的現有資料行會繼承新規則，除非*futureonly_flag*指定為**futureonly**。 以別名資料類型來定義的新資料行一律會繼承這個規則。 不過，如果 ALTER TABLE 陳述式的 ALTER COLUMN 子句將資料行的資料類型改成繫結於規則的別名資料類型，資料行不會繼承繫結於資料類型的規則。 此規則必須特別透過繫結至資料行**sp_bindrule**。  
  
 當您將規則繫結至資料行時，相關的資訊會新增至**sys.columns**資料表。 當您將規則繫結到別名資料類型時，相關的資訊會新增至**sys.types**資料表。  
  
## <a name="permissions"></a>Permissions  
 若要將規則繫結到資料表資料行，您必須具有資料表的 ALTER 權限。 將規則繫結到別名資料類型時，需要別名資料類型的 CONTROL 權限，或類型所屬之結構描述的 ALTER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-binding-a-rule-to-a-column"></a>A. 將規則繫結到資料行  
 假設已利用 CREATE RULE 陳述式，在目前資料庫中建立名稱為 `today` 的規則，下列範例會將規則繫結到 `HireDate` 資料表的 `Employee` 資料行。 當資料列加入 `Employee` 時，會針對 `HireDate` 規則來檢查 `today` 資料行。  
  
```  
USE master;  
GO  
EXEC sp_bindrule 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-rule-to-an-alias-data-type"></a>B. 將規則繫結到別名資料類型  
 假設有一個名稱為 `rule_ssn` 的規則及名稱為 `ssn` 別名資料類型存在，下列範例會將 `rule_ssn` 繫結到 `ssn`。 在 CREATE TABLE 陳述式中，`ssn` 類型的資料行會繼承 `rule_ssn` 規則。 類型的現有資料行`ssn`也會繼承`rule_ssn`規則，除非**futureonly**指定為*futureonly_flag*，或`ssn`有直接繫結的規則。 繫結到資料行的規則，一律優先於繫結到資料類型的規則。  
  
```  
USE master;  
GO  
EXEC sp_bindrule 'rule_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonlyflag"></a>C. 使用 futureonly_flag  
 下列範例將 `rule_ssn` 規則繫結到別名資料類型 `ssn`。 由於指定了 `futureonly`，不會影響任何現有 `ssn` 類型的資料行。  
  
```  
USE master;  
GO  
EXEC sp_bindrule rule_ssn, 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. 使用分隔識別碼  
 下列範例示範如何使用分隔識別碼中的*object_name*參數。  
  
```  
USE master;  
GO  
CREATE TABLE [t.2] (c1 int) ;  
-- Notice the period as part of the table name.  
EXEC sp_bindrule rule1, '[t.2].c1' ;  
-- The object contains two periods;   
-- the first is part of the table name   
-- and the second distinguishes the table name from the column name.  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [sp_unbindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
