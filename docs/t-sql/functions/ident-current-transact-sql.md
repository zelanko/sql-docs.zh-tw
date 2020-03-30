---
title: IDENT_CURRENT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IDENT_CURRENT
- IDENT_CURRENT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- last identity value generated for table
- identity values [SQL Server], last generated
- identity columns, current value
- IDENT_CURRENT function
ms.assetid: 21517ced-39f5-4cd8-8d9c-0a0b8aff554a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2271bbdd9a5b61fdfbf4985ca68acbffbc0b0b9d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "73843697"
---
# <a name="ident_current-transact-sql"></a>IDENT_CURRENT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回針對指定之資料表或檢視表所產生的最後一個識別值。 最後一個識別值可能是針對任何工作階段和任何範圍所產生的。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
IDENT_CURRENT( 'table_or_view' )  
```  
  
## <a name="arguments"></a>引數  
*table_or_view*  
這是傳回之識別值所屬的資料表或檢視名稱。 *table_or_view* 是沒有預設值的 **varchar**。  
  
## <a name="return-types"></a>傳回型別  
**numeric**([@@MAXPRECISION](../../t-sql/functions/max-precision-transact-sql.md),0))  
  
## <a name="exceptions"></a>例外狀況  
當發生錯誤，或呼叫端沒有檢視物件的權限時，便會傳回 NULL。  
  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，使用者只能檢視使用者擁有或被授與某些權限之安全性實體的中繼資料。 這表示發出中繼資料的內建函數 (例如，IDENT_CURRENT) 會在使用者不具有該物件任何權限時傳回 NULL。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="remarks"></a>備註  
IDENT_CURRENT 與 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 識別函式 SCOPE_IDENTITY 和 @@IDENTITY 相似。 三個函數都會傳回最後產生的識別值。 不過，各函式定義 *last* 的範圍和工作階段各不相同：  

-   IDENT_CURRENT 會傳回在任何工作階段和任何範圍中，產生給特定資料表的最後一個識別值。  
-   @@IDENTITY 會傳回所有範圍的目前工作階段中，任何資料表所產生的最後一個識別值。  
-   SCOPE_IDENTITY 會傳回在目前工作階段以及目前範圍中，任何資料表產生的最後一個識別值。  
  
當 IDENT_CURRENT 值為 NULL (因為資料表從未包含過資料列或是已遭到截斷) 時，IDENT_CURRENT 函數會傳回初始值。  
  
失敗的陳述式和交易可能會變更資料表的目前識別，以及建立識別欄位值中的間距。 識別值永遠不會回復，即使試圖將值插入資料表的交易未獲認可，也是如此。 例如，如果 INSERT 陳述式因 IGNORE_DUP_KEY 違規而失敗，資料表的目前識別值仍會遞增。  

在包含聯結的檢視上使用 IDENT_CURRENT 時，會傳回 NULL。 這是因為只有一或多個聯結資料表具有識別欄位。 
  
> [!IMPORTANT]
> 使用 IDENT_CURRENT 預測下一個產生的識別值時請小心。 因為有其他工作階段所執行的插入，所以實際產生的值可能與 IDENT_CURRENT 加 IDENT_INCR 不同。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-the-last-identity-value-generated-for-a-specified-table"></a>A. 傳回為指定資料表產生的最後一個識別值  
 下列範例會傳回為 `Person.Address` 資料庫中 `AdventureWorks2012` 資料表產生的最後識別值。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT IDENT_CURRENT ('Person.Address') AS Current_Identity;  
GO  
```  
  
### <a name="b-comparing-identity-values-returned-by-ident_current-identity-and-scope_identity"></a>B. 比較由 IDENT_CURRENT、@@IDENTITY 和 SCOPE_IDENTITY 傳回的識別值  
 下列範例會顯示 `IDENT_CURRENT`、`@@IDENTITY` 和 `SCOPE_IDENTITY` 傳回的不同識別值。  
  
```sql 
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N't6', N'U') IS NOT NULL   
    DROP TABLE t6;  
GO  
IF OBJECT_ID(N't7', N'U') IS NOT NULL   
    DROP TABLE t7;  
GO  
CREATE TABLE t6(id int IDENTITY);  
CREATE TABLE t7(id int IDENTITY(100,1));  
GO  
CREATE TRIGGER t6ins ON t6 FOR INSERT   
AS  
BEGIN  
   INSERT t7 DEFAULT VALUES  
END;  
GO  
--End of trigger definition  
  
SELECT id FROM t6;  
--IDs empty.  
  
SELECT id FROM t7;  
--ID is empty.  
  
--Do the following in Session 1  
INSERT t6 DEFAULT VALUES;  
SELECT @@IDENTITY;  
/*Returns the value 100. This was inserted by the trigger.*/  
  
SELECT SCOPE_IDENTITY();  
/* Returns the value 1. This was inserted by the   
INSERT statement two statements before this query.*/  
  
SELECT IDENT_CURRENT('t7');  
/* Returns value inserted into t7, that is in the trigger.*/  
  
SELECT IDENT_CURRENT('t6');  
/* Returns value inserted into t6. This was the INSERT statement four statements before this query.*/  
  
-- Do the following in Session 2.  
SELECT @@IDENTITY;  
/* Returns NULL because there has been no INSERT action   
up to this point in this session.*/  
  
SELECT SCOPE_IDENTITY();  
/* Returns NULL because there has been no INSERT action   
up to this point in this scope in this session.*/  
  
SELECT IDENT_CURRENT('t7');  
/* Returns the last value inserted into t7.*/  
```  
  
## <a name="see-also"></a>另請參閱  
 [@@IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)   
 [SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [IDENT_INCR &#40;Transact-SQL&#41;](../../t-sql/functions/ident-incr-transact-sql.md)   
 [IDENT_SEED &#40;Transact-SQL&#41;](../../t-sql/functions/ident-seed-transact-sql.md)   
 [運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  
