---
title: "@@IDENTITY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 88cdaa1362e5d60b0f880c66c7fb7038ddb9f126
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40identity-transact-sql"></a>（& s) #x 40; & #x 40，則身分識別 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  這是傳回最後插入的識別值之系統函數。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@IDENTITY  
```  
  
## <a name="return-types"></a>傳回類型  
 **numeric(38,0)**  
  
## <a name="remarks"></a>備註  
 之後的 INSERT、 SELECT INTO 或大量複製陳述式已完成，@@IDENTITY包含陳述式所產生的最後一個識別值。 如果陳述式不會影響任何具有識別欄位的資料表@IDENTITY傳回 NULL。 如果插入多個資料列，產生多個識別值，@IDENTITY傳回產生的最後一個識別值。 如果陳述式引發一或多個觸發程序執行插入來產生識別值，則呼叫@IDENTITY陳述式立即傳回觸發程序所產生的最後一個識別值之後。 如果在具有識別資料行的資料表上的插入動作之後引發觸發程序和觸發程序插入另一個資料表沒有識別欄位，@@IDENTITY傳回的第一次插入的識別值。 @@IDENTITY值不會還原成先前的設定有 INSERT 或 SELECT INTO 陳述式或大量複製失敗，或如果回復交易。  
  
 失敗的陳述式和交易可能會變更資料表的目前識別，以及建立識別欄位值中的間距。 識別值永遠不會回復，即使試圖將值插入資料表的交易未獲認可，也是如此。 例如，如果 INSERT 陳述式因 IGNORE_DUP_KEY 違規而失敗，資料表的目前識別值仍會遞增。  
  
 @@IDENTITY，SCOPE_IDENTITY 和 IDENT_CURRENT 是類似函數，因為它們都會傳回最後插入資料表之 IDENTITY 資料行的值。  
  
 @@IDENTITY和 SCOPE_IDENTITY 會傳回目前工作階段中產生任何資料表中的最後一個識別值。 不過，SCOPE_IDENTITY 會傳回的值只能在目前的範圍; 內@@IDENTITY不限於特定範圍。  
  
 IDENT_CURRENT 不受範圍和工作階段的限制；它只限於指定的資料表。 IDENT_CURRENT 會傳回在任何工作階段和任何範圍中，產生給特定資料表的識別值。 如需詳細資訊，請參閱[IDENT_CURRENT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/ident-current-transact-sql.md).  
  
 範圍 @@IDENTITY函式是在本機伺服器執行所在的目前工作階段。 這個函數不適用於遠端或連結伺服器。 若要取得不同伺服器的識別值，請在該遠端或連結伺服器上執行預存程序，讓這個預存程序 (在遠端或連結伺服器的內容中執行) 收集識別值，並將它傳回本機伺服器發出呼叫的連接。  
  
 複寫可能會影響 @@IDENTITY值，因為它用在複寫觸發程序和預存程序。 @@IDENTITY不是最新的使用者建立身分識別的可靠指標資料行是否為複寫發行項的一部分。 您可以使用 scope_identity （） 函式語法而不是 @@IDENTITY。 如需詳細資訊，請參閱[SCOPE_IDENTITY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/scope-identity-transact-sql.md)  
  
> [!NOTE]  
>  呼叫預存程序或[!INCLUDE[tsql](../../includes/tsql-md.md)]必須重寫陳述式，以使用`SCOPE_IDENTITY()`函式，以傳回該使用者陳述式，在範圍內使用的最新識別和巢狀觸發程序所使用的範圍內的識別複寫。  
  
## <a name="examples"></a>範例  
 下列範例會將資料列插入含有識別欄位 (`LocationID`) 的資料表，並利用 `@@IDENTITY` 來顯示新資料列所用的識別值。  
  
```  
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
 [系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SCOPE_IDENTITY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  

