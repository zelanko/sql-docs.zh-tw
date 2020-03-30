---
title: rowversion (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6c79f2e87ccb6706eab6621cc72bb2fa45b7e9e6
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "77179279"
---
# <a name="rowversion-transact-sql"></a>rowversion (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

此資料類型會公開在資料庫中自動產生的唯一二進位數字。 **rowversion** 通常用來作為版本戳記資料表資料列的機制。 儲存體大小是 8 位元組。 **rowversion** 資料類型只是會遞增的數字，因此不會保留日期或時間。 若要記錄日期或時間，請使用 **datetime2** 資料類型。
  
## <a name="remarks"></a>備註  
每個資料庫都有一個計數器，會針對在資料庫內包含 **rowversion** 資料行的資料表所執行的每個插入或更新作業而遞增。 這個計數器是資料庫資料列版本。 這會追蹤資料庫內的相對時間，而不是可關聯於時鐘的實際時間。 資料表只能有一個 **rowversion** 資料行。 每次修改或插入含 **rowversion** 資料行的資料列時，都會在 **rowversion** 資料行中插入遞增的資料庫資料列版本值。 這個屬性會使 **rowversion** 資料行不適合作為索引鍵 (尤其是主索引鍵) 的候選項。 資料列的任何更新都會變更資料列版本值，因而會變更索引鍵值。 如果資料行在主索引鍵中，舊的索引鍵值便不再有效，參考舊值的外部索引鍵也不再有效。 如果動態資料指標參考資料表，所有更新都會變更資料列在資料指標中的位置。 如果資料行在索引鍵中，資料列的所有更新也會產生索引的更新。  **rowversion** 值會隨著任何 update 陳述式而遞增，即使沒有變更任何資料列值。 (例如，若資料行值為 5，而 update 陳述式將該值設為 5，即使沒有任何變更，此動作仍然會被視為更新；因此 **rowversion** 便會遞增。)
  
**timestamp** 是 **rowversion** 資料類型的同義字，遵照資料類型同義字的行為。 在 DDL 陳述式中，請盡可能的使用 **rowversion** 而非 **timestamp**。 如需詳細資訊，請參閱[資料類型同義字 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-synonyms-transact-sql.md)。
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] **timestamp** 資料類型不同於 ISO 標準中所定義的 **timestamp** 資料類型。
  
> [!NOTE]  
>  **timestamp** 語法已淘汰。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
在 CREATE TABLE 或 ALTER TABLE 陳述式中，您不需要指定 **timestamp** 資料類型的資料行名稱，例如：
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, timestamp);  
```  
  
如果您沒有指定資料行名稱，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會產生 **timestamp** 資料行名稱；不過，**rowversion** 同義字不會遵循這個行為。 當您使用 **rowversion** 時，您必須指定一個資料行名稱，例如：
  
```sql
CREATE TABLE ExampleTable2 (PriKey int PRIMARY KEY, VerCol rowversion) ;  
```  
  
> [!NOTE]  
>  您可以使用 SELECT INTO 陳述式來產生重複的 **rowversion** 值，**rowversion** 資料行在 SELECT 清單中。 我們不建議您以這個方式來使用 **rowversion**。  
  
不可為 Null 的**rowversion** 資料行，語意等於 **binary(8)** 資料行。 可為 Null 的 **rowversion** 資料行，語意等於 **varbinary(8)** 資料行。
  
您可以使用資料列的 **rowversion** 資料行來輕鬆地判斷自上一次讀取以來，是否已對該資料列執行過 update 陳述式。 若已針對該資料列執行 update 陳述式，則 rowversion 值便會更新。 若沒有針對該資料列執行 update 陳述式，則 rowversion 值便會與先前讀取時相同。 若要傳回資料庫目前的 rowversion 值，請使用 [@@DBTS](../../t-sql/functions/dbts-transact-sql.md)。
  
您可以將 **rowversion** 資料行新增至資料表，以確保能在多個使用者同時更新資料列時維護資料庫的完整性。 您可能也想在不必重新查詢資料表的情況下，知道更新了多少資料列以及更新了哪些資料列。
  
例如，假設您要建立名為 `MyTest` 的資料表。 您可透過執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，在資料表中填入一些資料。
  
```sql
CREATE TABLE MyTest (myKey int PRIMARY KEY  
    ,myValue int, RV rowversion);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (1, 0);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (2, 0);  
GO  
```  
  
然後可以使用下列的範例 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，在更新期間將開放式並行存取控制項實作於 `MyTest` 資料表。 指令碼會使用 `<myRv>` 代表上次讀取資料列時的 **rowversion** 值。 請以實際的 **rowversion** 值取代此值。 **是實際**rowversion`0x00000000000007D3` 值的範例。
  
```sql
DECLARE @t TABLE (myKey int);  
UPDATE MyTest  
SET myValue = 2  
    OUTPUT inserted.myKey INTO @t(myKey)   
WHERE myKey = 1   
    AND RV = <myRv>;  
IF (SELECT COUNT(*) FROM @t) = 0  
    BEGIN  
        RAISERROR ('error changing row with myKey = %d'  
            ,16 -- Severity.  
            ,1 -- State   
            ,1) -- myKey that was changed   
    END;  
```  
  


您也可以將範例 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式放入交易中。 您可以透過在交易的範圍中查詢 `@t` 變數來擷取資料表已更新的 `myKey` 資料行，而不必重新查詢 `MyTest` 資料表。

下列為使用**時間戳記**語法的相同範例。 以實際的`<myTS>`時間戳記**取代** 。

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
    AND TS = <myTS>;  
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
[MIN_ACTIVE_ROWVERSION &#40;Transact-SQL&#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)
  
  
