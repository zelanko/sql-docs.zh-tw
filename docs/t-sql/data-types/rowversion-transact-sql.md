---
title: "rowversion (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- timestamp_TSQL
- timestamp
dev_langs:
- TSQL
helpviewer_keywords:
- rowversion data type
- size [SQL Server], rowversion
- row version-stamping [SQL Server]
- rowversion columns
- version-stamping table rows
- unique rowversion numbers
- unique timestamp numbers
- timestamp data type
- timestamp columns
- size [SQL Server], timestamp
ms.assetid: 65c9cf0e-3e8a-45f8-87b3-3460d96afb0b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4a8a9c6a9ea076ec1727bfa5422a3dfbda58386c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="rowversion-transact-sql"></a>rowversion (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

此資料類型會公開在資料庫中自動產生的唯一二進位數字。 **rowversion**通常用來做為版本戳記資料表資料列的機制。 儲存體大小是 8 位元組。 **Rowversion**資料類型是只會遞增的數字，而且不會保留日期或時間。 若要記錄的日期或時間，請使用**datetime2**資料型別。
  
## <a name="remarks"></a>備註  
每個資料庫已經就會遞增每個插入的計數器或執行包含在資料表的更新作業**rowversion**資料庫內的資料行。 這個計數器是資料庫資料列版本。 這會追蹤資料庫內的相對時間，而不是可關聯於時鐘的實際時間。 資料表只能有一個**rowversion**資料行。 每次所包含的資料列**rowversion** 、 修改或插入資料行中插入累加的資料庫版本值**rowversion**資料行。 這個屬性會使**rowversion**不佳的候選項目的索引鍵，尤其是主索引鍵資料行。 資料列的任何更新都會變更資料列版本值，因而會變更索引鍵值。 如果資料行在主索引鍵中，舊的索引鍵值便不再有效，參考舊值的外部索引鍵也不再有效。 如果動態資料指標參考資料表，所有更新都會變更資料列在資料指標中的位置。 如果資料行在索引鍵中，資料列的所有更新也會產生索引的更新。  **Rowversion**值會隨著任何 update 陳述式，即使沒有資料列的值已變更。 (例如，如果資料行值為 5，update 陳述式的值設定為 5，此動作視為更新即使沒有任何變更，而**rowversion**就會遞增。)
  
**時間戳記**是同義字**rowversion**資料類型，類型同義字受限於資料的行為。 在 DDL 陳述式，使用**rowversion**而不是**時間戳記**只要做得到。 如需詳細資訊，請參閱[資料類型同義字 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/data-type-synonyms-transact-sql.md).
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] **時間戳記**資料型別是從不同**時間戳記**ISO 標準中所定義的資料類型。
  
> [!NOTE]  
>  **時間戳記**語法已被取代。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
在 CREATE TABLE 或 ALTER TABLE 陳述式中，您不必指定的資料行名稱**時間戳記**資料類型，例如：
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, timestamp);  
```  
  
如果您未指定資料行名稱，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]產生**時間戳記**資料行名稱; 不過， **rowversion**同義字不會遵循這種行為。 當您使用**rowversion**，您必須指定資料行名稱，例如：
  
```sql
CREATE TABLE ExampleTable2 (PriKey int PRIMARY KEY, VerCol rowversion) ;  
```  
  
> [!NOTE]  
>  重複的**rowversion**值可以在其中使用 SELECT INTO 陳述式產生**rowversion**資料行是在選取清單中。 我們不建議使用**rowversion**以這種方式。  
  
不可為 null **rowversion**資料行，語意等於**binary （8)**資料行。 可為 null **rowversion**資料行，語意等於**varbinary （8)**資料行。
  
您可以使用**rowversion**自從上次讀取資料行的資料列來輕鬆地判斷資料列是否已在 update 陳述式執行對它。 如果針對資料列執行 update 陳述式時，會更新 rowversion 值。 如果沒有更新陳述式會執行對資料列，版本值等同於先前讀取。 若要傳回資料庫目前的版本值，請使用[@@DBTS](../../t-sql/functions/dbts-transact-sql.md)。
  
您可以加入**rowversion**至資料表，以協助維護資料庫的完整性，當多位使用者同時更新一次的資料列的資料行。 您可能也想在不必重新查詢資料表的情況下，知道更新了多少資料列以及更新了哪些資料列。
  
例如，假設您要建立名為 `MyTest` 的資料表。 執行下列填入資料表中的某些資料[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。
  
```sql
CREATE TABLE MyTest (myKey int PRIMARY KEY  
    ,myValue int, RV rowversion);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (1, 0);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (2, 0);  
GO  
```  
  
然後可以使用下列的範例 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，在更新期間將開放式並行存取控制項實作於 `MyTest` 資料表。
  
```sql
DECLARE @t TABLE (myKey int);  
UPDATE MyTest  
SET myValue = 2  
    OUTPUT inserted.myKey INTO @t(myKey)   
WHERE myKey = 1   
    AND RV = myValue;  
IF (SELECT COUNT(*) FROM @t) = 0  
    BEGIN  
        RAISERROR ('error changing row with myKey = %d'  
            ,16 -- Severity.  
            ,1 -- State   
            ,1) -- myKey that was changed   
    END;  
```  
  
`myValue`是**rowversion**表示最後一次您讀取資料列的資料列的資料行值。 此值必須由實際取代**rowversion**值。 實際範例**rowversion**值是 0x00000000000007D3。
  
您也可以將範例 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式放入交易中。 您可藉由在交易的範圍中查詢 `@t` 變數來擷取資料表已更新的 `myKey` 資料行，而不必重新查詢 `MyTes` 資料表。
  
下列是相同的範例使用**時間戳記**語法：
  
```sql
CREATE TABLE MyTest2 (myKey int PRIMARY KEY  
    ,myValue int, TS timestamp);  
GO   
INSERT INTO MyTest2 (myKey, myValue) VALUES (1, 0);  
GO   
INSERT INTO MyTest2 (myKey, myValue) VALUES (2, 0);  
GO  
DECLARE @t TABLE (myKey int);  
UPDATE MyTest2  
SET myValue = 2  
    OUTPUT inserted.myKey INTO @t(myKey)   
WHERE myKey = 1   
    AND TS = myValue;  
IF (SELECT COUNT(*) FROM @t) = 0  
    BEGIN  
        RAISERROR ('error changing row with myKey = %d'  
            ,16 -- Severity.  
            ,1 -- State   
            ,1) -- myKey that was changed   
    END;  
```  
  
## <a name="see-also"></a>另請參閱
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)  
[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION &#40;TRANSACT-SQL &#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)
  
  
