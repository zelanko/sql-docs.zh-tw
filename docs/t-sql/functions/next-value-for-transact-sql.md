---
title: NEXT VALUE FOR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- NEXT_VALUE_TSQL
- NEXT
- NEXT VALUE
- NEXT VALUE FOR
- NEXT_TSQL
- NEXT_VALUE_FOR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- NEXT VALUE FOR function
- sequence number object, NEXT VALUE FOR function
ms.assetid: 92632ed5-9f32-48eb-be28-a5e477ef9076
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e37586d17a7b99d3dd191f63ed858805ef497a03
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68670529"
---
# <a name="next-value-for-transact-sql"></a>NEXT VALUE FOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  從指定的順序物件產生序號。  
  
 如需建立及使用順序的完整討論，請參閱[序號](../../relational-databases/sequence-numbers/sequence-numbers.md)。 您可以使用 [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) 來產生序號的範圍。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
NEXT VALUE FOR [ database_name . ] [ schema_name . ]  sequence_name  
   [ OVER (<over_order_by_clause>) ]  
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 包含順序物件的資料庫名稱。  
  
 *schema_name*  
 包含順序物件的結構描述名稱。  
  
 *sequence_name*  
 產生數字的順序物件名稱。  
  
 *over_order_by_clause*  
 決定將順序值指派給資料分割中之資料列的順序。 如需詳細資訊，請參閱 [OVER 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)。  
  
## <a name="return-types"></a>傳回型別  
 使用順序的類型傳回數字。  
  
## <a name="remarks"></a>備註  
 **NEXT VALUE FOR** 函式可用於預存程序和觸發程序中。  
  
 當 **NEXT VALUE FOR** 函式用於查詢或預設條件約束時，如果使用相同的順序物件不只一次，或在提供值的陳述式中以及正在執行的預設條件約束中使用相同的順序物件，則會對結果集中資料列內參考相同順序的所有資料行傳回相同值。  
  
 **NEXT VALUE FOR** 函式不具確定性，而且只允許用於妥善定義產生之順序值數目的內容中。 以下是指定的陳述式中每個參考的順序物件將會使用多少個值的定義：  
  
-   **SELECT** - 針對每個參考的順序物件，為陳述式結果中的每個資料列，產生一次新值。  
  
-   **INSERT** ...**VALUES** - 針對每個參考的順序物件，為陳述式中每個插入的資料列，產生一次新值。  
  
-   **UPDATE** - 針對每個參考的順序物件，為陳述式所更新的每個資料列，產生一次新值。  
  
-   程序陳述式 (例如 **DECLARE**、**SET** 等等) - 針對每個參考的順序物件，為每個陳述式產生新值。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 **NEXT VALUE FOR** 函式不適用於下列情況：  
  
-   當資料庫在唯讀模式中。  
  
-   做為資料表值函式的引數。  
  
-   做為彙總函式的引數。  
  
-   在子查詢中，包括通用資料表運算式和衍生資料表。  
  
-   在檢視表、使用者定義函數或計算資料行中。  
  
-   在使用 **DISTINCT**、**UNION**、**UNION ALL**、**EXCEPT** 或 **INTERSECT** 運算子的陳述式中。  
  
-   在使用 **ORDER BY** 子句的陳述式中 (除非使用 **NEXT VALUE FOR** ...**OVER** (**ORDER BY** ...))。  
  
-   在下列子句中：**FETCH**、**OVER**、**OUTPUT**、**ON**、**PIVOT**、**UNPIVOT**、**GROUP BY**、**HAVING**、**COMPUTE**、**COMPUTE BY** 或 **FOR XML**。  
  
-   在使用 **CASE**、**CHOOSE**、**COALESCE**、**IIF**、**ISNULL**，或 **NULLIF** 的條件運算式中。  
  
-   在不屬於 **INSERT** 陳述式的 **VALUES** 子句中。  
  
-   在檢查條件約束的定義中。  
  
-   在規則或預設物件的定義中 (它可以用於預設條件約束中)。  
  
-   使用者定義資料表類型的預設值。  
  
-   在使用 **TOP**、**OFFSET** 的陳述式中，或是已設定 **ROWCOUNT** 選項時。  
  
-   在陳述式的 **WHERE** 子句中。  
  
-   在 **MERGE** 陳述式中。 (除非 **NEXT VALUE FOR** 函式用於目標資料表的預設條件約束中，而且預設值用於 **CREATE** 陳述式的 **MERGE** 陳述式中。)  
  
## <a name="using-a-sequence-object-in-a-default-constraint"></a>在預設條件約束中使用順序物件  
 在預設條件約束中使用 **NEXT VALUE FOR** 函式時，下列為適用規則：  
  
-   可從多個資料表中的預設條件約束來參考單一順序物件。  
  
-   資料表和順序物件必須位於相同的資料庫。  
  
-   加入預設條件約束的使用者必須有順序物件的 REFERENCES 權限。  
  
-   在卸除預設條件約束之前，無法卸除從預設條件約束參考的順序物件。  
  
-   如果多個預設條件約束使用相同的順序物件，或在提供值的陳述式中以及正在執行的預設條件約束中使用相同的順序物件，則會對資料列中的所有資料行傳回相同的順序物件。  
  
-   預設條件約束中 **NEXT VALUE FOR** 函式的參考不能指定 **OVER** 子句。  
  
-   可以改變預設條件約束中參考的定順序物件。  
  
-   當 `INSERT ... SELECT` 或 `INSERT ... EXEC` 陳述式中正在插入的資料來自使用 **ORDER BY** 子句的查詢時，則會依 **ORDER BY** 子句所指定的順序來產生 **NEXT VALUE FOR** 函式所傳回的值。  
  
## <a name="using-a-sequence-object-with-an-over-order-by-clause"></a>搭配 OVER ORDER BY 子句使用順序物件  
 **NEXT VALUE FOR** 函式支援透過將 **OVER** 子句套用到 **NEXT VALUE FOR** 呼叫，來產生排序的順序值。 透過使用 **OVER** 子句，可確保傳回的值依據 **OVER** 子句 **ORDER BY** 次子句的順序來產生。 搭配 **OVER** 子句使用 **NEXT VALUE FOR** 函式時，下列為額外的適用規則：  
  
-   單一陳述式中為相同順序產生器的多個 **NEXT VALUE FOR** 函式呼叫必須全都使用相同的 **OVER** 子句定義。  
  
-   單一陳述式中參考不同順序產生器的多個 **NEXT VALUE FOR** 函式呼叫可以有不同的 **OVER** 子句定義。  
  
-   套用至 **NEXT VALUE FOR** 函式的 **OVER** 子句不支援 **PARTITION BY** 次子句。  
  
-   如果 **SELECT** 陳述式中所有 **NEXT VALUE FOR** 函式呼叫都指定 **OVER** 子句，**ORDER BY** 子句可用於 **SELECT** 陳述式。  
  
-   使用於 **SELECT** 陳述式或 `INSERT ... SELECT ...` 陳述式中時，允許 **OVER** 子句與 **NEXT VALUE FOR** 函式搭配使用。 在 **UPDATE** 或 **MERGE** 陳述式中，不允許 **OVER** 子句與 **NEXT VALUE FOR** 函式搭配使用。  
  
-   如果同時有另一個處理序正在存取順序物件，傳回的數字可能會有間距。  
  
## <a name="metadata"></a>中繼資料  
 如需順序的詳細資訊，請查詢 [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md) 目錄檢視。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>權限  
 需要順序物件或順序之結構描述的 **UPDATE** 權限。 如需授與權限的範例，請參閱本主題稍後的範例 F。  
  
### <a name="ownership-chaining"></a>擁有權鏈結  
 順序物件支援擁有權鏈結。 如果順序物件與呼叫預存程序、觸發程序或資料表 (具有順序物件做為預設條件約束) 有相同的擁有者，則不需要順序物件的權限檢查。 如果順序物件與呼叫預存程序、觸發程序或資料表有不同的擁有者，則需要順序物件的權限檢查。  
  
 在資料表中 **NEXT VALUE FOR** 函式作為預設值時，使用者需要資料表的 **INSERT** 權限和順序物件的 **UPDATE** 權限，才能使用預設值插入資料。  
  
-   如果預設條件約束與順序物件有相同的擁有者，在呼叫預設條件約束時不需要順序物件的權限。  
  
-   如果預設條件約束與順序物件有不同的擁有者，即使透過預設條件約束呼叫，也需要順序物件的權限。  
  
### <a name="audit"></a>稽核  
 若要稽核 **NEXT VALUE FOR** 函式，請監視 SCHEMA_OBJECT_ACCESS_GROUP。  
  
## <a name="examples"></a>範例  
 如需建立順序和使用 **NEXT VALUE FOR** 函式產生序號的範例，請參閱[序號](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
 下列範例會使用 `CountBy1` 結構描述中的 `Test` 順序。 執行下列陳述式以建立 `Test.CountBy1` 順序。 範例 C 和 E 使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫，所以 `CountBy1` 順序是在該資料庫中建立的。  
  
```  
USE AdventureWorks2012 ;  
GO  
  
CREATE SCHEMA Test;  
GO  
  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="a-using-a-sequence-in-a-select-statement"></a>A. 在 SELECT 陳述式中使用順序  
 下列範例會建立名為 `CountBy1` 的順序，此順序每次使用時遞增一。  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1 AS FirstUse;  
SELECT NEXT VALUE FOR Test.CountBy1 AS SecondUse;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
FirstUse  
1  
  
SecondUse  
2
```  
  
### <a name="b-setting-a-variable-to-the-next-sequence-value"></a>B. 將變數設定為下一個順序值  
 下列範例示範三種將變數設定為下一個序號值的方法。  
  
```  
DECLARE @myvar1 bigint = NEXT VALUE FOR Test.CountBy1  
DECLARE @myvar2 bigint ;  
DECLARE @myvar3 bigint ;  
SET @myvar2 = NEXT VALUE FOR Test.CountBy1 ;  
SELECT @myvar3 = NEXT VALUE FOR Test.CountBy1 ;  
SELECT @myvar1 AS myvar1, @myvar2 AS myvar2, @myvar3 AS myvar3 ;  
GO  
```  
  
### <a name="c-using-a-sequence-with-a-ranking-window-function"></a>C. 並用順序與次序視窗函數  
  
```  
USE AdventureWorks2012 ;  
GO  
  
SELECT NEXT VALUE FOR Test.CountBy1 OVER (ORDER BY LastName) AS ListNumber,  
    FirstName, LastName  
FROM Person.Contact ;  
GO  
```  
  
### <a name="d-using-the-next-value-for-function-in-the-definition-of-a-default-constraint"></a>D. 在預設條件約束的定義中使用 NEXT VALUE FOR 函數  
 支援在預設條件約束的定義中使用 **NEXT VALUE FOR** 函式。 如需在 **CREATE TABLE** 陳述式中使用 **NEXT VALUE FOR** 的範例，請參閱[序號](../../relational-databases/sequence-numbers/sequence-numbers.md)中的範例 C。 下列範例會使用 `ALTER TABLE`，將順序做為預設值加入至目前資料表。  
  
```  
CREATE TABLE Test.MyTable  
(  
    IDColumn nvarchar(25) PRIMARY KEY,  
    name varchar(25) NOT NULL  
) ;  
GO  
  
CREATE SEQUENCE Test.CounterSeq  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
ALTER TABLE Test.MyTable  
    ADD   
        DEFAULT N'AdvWorks_' +   
        CAST(NEXT VALUE FOR Test.CounterSeq AS NVARCHAR(20))   
        FOR IDColumn;  
GO  
  
INSERT Test.MyTable (name)  
VALUES ('Larry') ;  
GO  
  
SELECT * FROM Test.MyTable;  
GO  
```  
  
### <a name="e-using-the-next-value-for-function-in-an-insert-statement"></a>E. 在 INSERT 陳述式中使用 NEXT VALUE FOR 函數  
 下列範例會建立名為 `TestTable` 的資料表，然後使用 `NEXT VALUE FOR` 函數插入資料列。  
  
```  
CREATE TABLE Test.TestTable  
     (CounterColumn int PRIMARY KEY,  
    Name nvarchar(25) NOT NULL) ;   
GO  
  
INSERT Test.TestTable (CounterColumn,Name)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Syed') ;  
GO  
  
SELECT * FROM Test.TestTable;   
GO  
  
```  
  
### <a name="e-using-the-next-value-for-function-with-select--into"></a>E. 搭配使用 NEXT VALUE FOR 函數與 SELECT ...INTO  
 下列範例會使用 `SELECT ... INTO` 陳述式建立名為 `Production.NewLocation` 的資料表，然後使用 `NEXT VALUE FOR` 函式指定每個資料列的編號。  
  
```  
USE AdventureWorks2012 ;   
GO  
  
SELECT NEXT VALUE FOR Test.CountBy1 AS LocNumber, Name   
    INTO Production.NewLocation  
    FROM Production.Location ;  
GO  
  
SELECT * FROM Production.NewLocation ;  
GO  
```  
  
### <a name="f-granting-permission-to-execute-next-value-for"></a>F. 授與執行 NEXT VALUE FOR 的權限  
 下列範例會將 **UPDATE** 權限授與名為 `AdventureWorks\Larry` 的使用者，以使用 `Test.CounterSeq` 順序執行 `NEXT VALUE FOR`。  
  
```  
GRANT UPDATE ON OBJECT::Test.CounterSeq TO [AdventureWorks\Larry] ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [序號](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  
