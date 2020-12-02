---
description: '&#x40;&#x40;IDENTITY (Transact-SQL)'
title: '@@IDENTITY (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@IDENTITY_TSQL'
- '@@IDENTITY'
dev_langs:
- TSQL
helpviewer_keywords:
- last-inserted identity values
- identity values [SQL Server], last-inserted
- '@@IDENTITY function'
ms.assetid: 912e4485-683c-41c2-97b3-8831c0289ee4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: eff66d795dce39c21ee6a4354e8f34a62ed15d6c
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128415"
---
# <a name="x40x40identity-transact-sql"></a>&#x40;&#x40;IDENTITY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  這是傳回最後插入的識別值之系統函數。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql  
@@IDENTITY  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>傳回型別
 **numeric(38,0)**  
  
## <a name="remarks"></a>備註  
 在 INSERT、SELECT INTO 或大量複製陳述式完成之後，@@IDENTITY 會包含陳述式所產生的最後一個識別值。 如果陳述式並未影響任何含有識別欄位的資料表，@@IDENTITY 會傳回 NULL。 如果插入多個資料列，產生多個識別值，@@IDENTITY 會傳回最後一個產生的識別值。 如果陳述式引發一或多個執行插入來產生識別值的觸發程序，在陳述式之後緊接著呼叫 @@IDENTITY，會傳回觸發程序所產生的最後一個識別值。 如果在含有識別欄位之資料表的插入動作之後引發觸發程序，且觸發程序插入另一個沒有識別欄位的資料表，@@IDENTITY 會傳回第一次插入的識別值。 如果 INSERT 或 SELECT INTO 陳述式或大量複製失敗，或回復交易，@@IDENTITY 值不會還原成先前的設定。  
  
 失敗的陳述式和交易可能會變更資料表的目前識別，以及建立識別欄位值中的間距。 識別值永遠不會回復，即使試圖將值插入資料表的交易未獲認可，也是如此。 例如，如果 INSERT 陳述式因 IGNORE_DUP_KEY 違規而失敗，資料表的目前識別值仍會遞增。  
  
 @@IDENTITY、SCOPE_IDENTITY 和 IDENT_CURRENT 是類似的函式，因為它們都會傳回最後插入資料表之 IDENTITY 資料行的值。  
  
 @@IDENTITY 和 SCOPE_IDENTITY 會傳回目前工作階段任何資料表中所產生的最後一個識別值。 不過，SCOPE_IDENTITY 只會傳回目前範圍內的值；@@IDENTITY 不限於特定範圍。  
  
 IDENT_CURRENT 不受範圍和工作階段的限制；它只限於指定的資料表。 IDENT_CURRENT 會傳回在任何工作階段和任何範圍中，產生給特定資料表的識別值。 如需詳細資訊，請參閱 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)。  
  
 @@IDENTITY 函式的範圍是執行它的本機伺服器的目前工作階段。 這個函數不適用於遠端或連結伺服器。 若要取得不同伺服器的識別值，請在該遠端或連結伺服器上執行預存程序，讓這個預存程序 (在遠端或連結伺服器的內容中執行) 收集識別值，並將它傳回本機伺服器發出呼叫的連接。  
  
 複寫可能會影響 @@IDENTITY 值，因為此值會用於複寫觸發程序和預存程序中。 如果資料行屬於複寫發行項的一部分，@@IDENTITY 就不是最近使用者建立之識別的可靠指標。 您可以使用 SCOPE_IDENTITY() 函式語法來取代 @@IDENTITY。 如需詳細資訊，請參閱 [SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md)  
  
> [!NOTE]  
>  呼叫的預存程序或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式必須重寫，才能使用 `SCOPE_IDENTITY()` 函式，此函式將會傳回在該使用者陳述式之範圍內使用的最新識別，而非在巢狀觸發程序之範圍內由複寫所使用的識別。  
  
## <a name="examples"></a>範例  
 下列範例會將資料列插入含有識別欄位 (`LocationID`) 的資料表，並利用 `@@IDENTITY` 來顯示新資料列所用的識別值。  
  
```sql  
USE AdventureWorks2012;  
GO  
--Display the value of LocationID in the last row in the table.  
SELECT MAX(LocationID) FROM Production.Location;  
GO  
INSERT INTO Production.Location (Name, CostRate, Availability, ModifiedDate)  
VALUES ('Damaged Goods', 5, 2.5, GETDATE());  
GO  
SELECT @@IDENTITY AS 'Identity';  
GO  
--Display the value of LocationID of the newly inserted row.  
SELECT MAX(LocationID) FROM Production.Location;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  
