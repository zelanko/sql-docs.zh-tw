---
title: CREATE DEFAULT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_DEFAULT_TSQL
- CREATE DEFAULT
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], default
- default objects
- CREATE DEFAULT statement
- objects [SQL Server], creating
- DEFAULT definition
ms.assetid: 08475db4-7d90-486a-814c-01a99d783d41
caps.latest.revision: 47
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f4022c33a87178fd7efde1974491f69da24309dc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="create-default-transact-sql"></a>CREATE DEFAULT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  建立一個稱為預設值的物件。 當繫結到某個資料行或別名資料型別，且在插入作業期間未明確提供任何值時，預設值會指定要插入物件所繫結之資料行 (如果是別名資料型別，則是所有資料行) 的值。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改為使用透過 ALTER TABLE 或 CREATE TABLE 的 DEFAULT 關鍵字所建立的預設定義。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE DEFAULT [ schema_name . ] default_name   
AS constant_expression [ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *schema_name*  
 這是預設值所屬的結構描述名稱。  
  
 *default_name*  
 這是預設值的名稱。 預設名稱必須符合[識別碼](../../relational-databases/databases/database-identifiers.md)的規則。 您可以選擇性地指定預設擁有者名稱。  
  
 *constant_expression*  
 這是一個只包含常數值的[運算式](../../t-sql/language-elements/expressions-transact-sql.md) (其中不能有任何資料行或其他資料庫物件的名稱)。 除了包含別名資料類型者之外，任何常數、內建函數或數學運算式都可以使用。 不能使用使用者自訂函數。 請用單引號 (**'**) 括住字元和日期常數；貨幣、整數和浮點數常數不需要引號。 二進位資料的前面必須是 0x，貨幣資料的前面必須是錢幣符號 ($)。 預設值必須相容於資料行資料類型。  
  
## <a name="remarks"></a>Remarks  
 預設名稱只能建立在目前資料庫中。 在資料庫內，必須藉由結構描述，使預設名稱成為唯一。 當建立預設值時，請使用 **sp_bindefault**，將它繫結到資料行或別名資料類型。  
  
 如果預設值與所繫結的資料行不相容，當嘗試插入預設值時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會產生一則錯誤訊息。 例如，N/A 不能用來作為 **numeric** 資料行的預設值。  
  
 如果預設值對它所繫結的資料行而言太長，就會截斷這個值。  
  
 CREATE DEFAULT 陳述式無法在單一批次中，與其他 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式結合起來。  
  
 您必須先卸除預設值，才能建立同名的新預設值，在卸除預設值之前，您必須先執行 **sp_unbindefault** 來解除預設值的繫結。  
  
 如果資料行有預設值和相關聯的規則，預設值便不能違反規則。 永遠不會插入與規則衝突的預設值，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 每次嘗試插入預設值時，都會產生一則錯誤訊息。  
  
 當繫結到資料行時，在下列情況下，會插入預設值：  
  
-   未明確插入值。  
  
-   搭配 INSERT 使用 DEFAULT VALUES 或 DEFAULT 關鍵字來插入預設值。  
  
 如果建立資料行時指定了 NOT NULL，且並未建立其預設值，當使用者無法在這個資料行中建立項目時，便會產生錯誤訊息。 下表說明預設值的存在與資料行定義為 NULL 或 NOT NULL 之間的關聯性。 資料表中各項目顯示其結果。  
  
|資料行定義|無項目，無預設值|無項目，有預設值|輸入 NULL，無預設值|輸入 NULL，有預設值|  
|-----------------------|--------------------------|-----------------------|----------------------------|-------------------------|  
|**NULL**|NULL|預設|NULL|NULL|  
|**NOT NULL**|錯誤|預設|error|error|  
  
 若要重新命名預設值，請使用 **sp_rename**。 如需預設值的報表，請使用 **sp_help**。  
  
## <a name="permissions"></a>Permissions  
 若要執行 CREATE DEFAULT，使用者至少必須有目前資料庫中的 CREATE DEFAULT 權限，以及正在建立的預設值之結構描述的 ALTER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-simple-character-default"></a>A. 建立簡單字元預設值  
 下列範例會建立一個稱為 `unknown` 的字元預設值。  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE DEFAULT phonedflt AS 'unknown';  
```  
  
### <a name="b-binding-a-default"></a>B. 繫結預設值  
 下列範例會繫結 A 範例中所建立的預設值。只有在 `Phone` 資料表的 `Contact` 資料行中沒有指定任何項目時，預設值才會生效。 請注意，省略任何項目與在 INSERT 陳述式中明確地陳述 NULL 並不相同。  
  
 由於名稱為 `phonedflt` 的預設值不存在，因此，下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式會失敗。 這個範例只供說明。  
  
```sql  
USE AdventureWorks2012;  
GO  
sp_bindefault 'phonedflt', 'Person.PersonPhone.PhoneNumber';  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [sp_bindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_unbindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)  
  
  
