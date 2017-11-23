---
title: "接下來的數值 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/19/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NEXT_VALUE_TSQL
- NEXT
- NEXT VALUE
- NEXT VALUE FOR
- NEXT_TSQL
- NEXT_VALUE_FOR_TSQL
dev_langs: TSQL
helpviewer_keywords:
- NEXT VALUE FOR function
- sequence number object, NEXT VALUE FOR function
ms.assetid: 92632ed5-9f32-48eb-be28-a5e477ef9076
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a4e6ca2ce4c89e1e608d9762d1562a78f7908c23
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="next-value-for-transact-sql"></a>NEXT VALUE FOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  從指定的順序物件產生序號。  
  
 如需建立和使用順序的完整討論，請參閱[序號](../../relational-databases/sequence-numbers/sequence-numbers.md)。 使用[sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md)產生序號的範圍。  
  
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
 決定將順序值指派給資料分割中之資料列的順序。 如需詳細資訊，請參閱[OVER 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>傳回類型  
 使用順序的類型傳回數字。  
  
## <a name="remarks"></a>備註  
 **NEXT VALUE FOR**函式可用於預存程序和觸發程序。  
  
 當**NEXT VALUE FOR**函式用於查詢或預設條件約束，如果一次以上，使用相同的順序物件，或在提供值的陳述式和 default 條件約束中使用相同的順序物件正在執行，則參考相同的順序，在結果集中資料列內的所有資料行傳回相同的值。  
  
 **NEXT VALUE FOR**函式不具決定性，而且只允許在產生的序列值數目是妥善定義的內容中。 以下是指定的陳述式中每個參考的順序物件將會使用多少個值的定義：  
  
-   **選取**-針對每個參考的順序物件，新值產生一次每個資料列中的陳述式的結果。  
  
-   **插入**... **值**-每個參考的順序物件，新的值，產生一次的陳述式中每個插入資料列。  
  
-   **更新**-每個參考的順序物件，每個資料列被更新陳述式產生新的值。  
  
-   程序陳述式 (例如**DECLARE**，**設定**等等)-針對每個參考的順序物件，每個陳述式產生新的值。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 **NEXT VALUE FOR**函式不能在下列情況：  
  
-   當資料庫在唯讀模式中。  
  
-   做為資料表值函式的引數。  
  
-   做為彙總函式的引數。  
  
-   在子查詢中，包括通用資料表運算式和衍生資料表。  
  
-   在檢視表、使用者定義函數或計算資料行中。  
  
-   在陳述式使用**DISTINCT**， **UNION**， **UNION ALL**， **EXCEPT**或**INTERSECT**運算子。  
  
-   在陳述式使用**ORDER BY**子句除非**NEXT VALUE FOR** ... **透過**(**ORDER BY** ...) 會使用。  
  
-   在下列子句：**提取**，**透過**，**輸出**， **ON**， **PIVOT**， **取消樞紐**，**分組**， **HAVING**，**計算**， **COMPUTE BY**，或**FOR XML**.  
  
-   使用條件式運算式中**案例**，**選擇**， **COALESCE**， **IIF**， **ISNULL**，或**NULLIF**。  
  
-   在**值**子句不屬於**插入**陳述式。  
  
-   在檢查條件約束的定義中。  
  
-   在規則或預設物件的定義中  (它可以用於預設條件約束中)。  
  
-   使用者定義資料表類型的預設值。  
  
-   在陳述式使用**頂端**，**位移**，或當**ROWCOUNT**選項設定。  
  
-   在**其中**陳述式子句。  
  
-   在**合併**陳述式。 (除非**NEXT VALUE FOR**函數用於目標資料表中的預設條件約束，而且預設會用於**建立**陳述式的**合併**陳述式。)  
  
## <a name="using-a-sequence-object-in-a-default-constraint"></a>在預設條件約束中使用順序物件  
 當使用**NEXT VALUE FOR**函式的預設條件約束，則適用下列規則：  
  
-   可從多個資料表中的預設條件約束來參考單一順序物件。  
  
-   資料表和順序物件必須位於相同的資料庫。  
  
-   加入預設條件約束的使用者必須有順序物件的 REFERENCES 權限。  
  
-   在卸除預設條件約束之前，無法卸除從預設條件約束參考的順序物件。  
  
-   如果多個預設條件約束使用相同的順序物件，或在提供值的陳述式中以及正在執行的預設條件約束中使用相同的順序物件，則會對資料列中的所有資料行傳回相同的順序物件。  
  
-   若要參考**NEXT VALUE FOR**函式的預設條件約束不能指定**透過**子句。  
  
-   可以改變預設條件約束中參考的定順序物件。  
  
-   如果是`INSERT … SELECT`或`INSERT … EXEC`正在插入的資料來自使用查詢的陳述式**ORDER BY**子句中，所傳回的值**NEXT VALUE FOR**函式將會所指定的順序產生**ORDER BY**子句。  
  
## <a name="using-a-sequence-object-with-an-over-order-by-clause"></a>搭配 OVER ORDER BY 子句使用順序物件  
 **NEXT VALUE FOR**函式支援產生排序的順序值，藉由套用**透過**子句**NEXT VALUE FOR**呼叫。 使用**透過**子句，確保傳回的值會產生的順序**透過**子句的**順序 B**Y 次子句。 使用時，適用下列其他規則**NEXT VALUE FOR**函式與**透過**子句：  
  
-   多個呼叫**NEXT VALUE FOR**函式的相同順序產生器，在單一陳述式都必須使用相同**透過**子句定義。  
  
-   多個呼叫**NEXT VALUE FOR**函式，在單一陳述式中的參考不同順序產生器可以擁有不同**透過**子句定義。  
  
-   **透過**子句套用至**NEXT VALUE FOR**函式不支援**PARTITION BY**次子句。  
  
-   如果所有呼叫**NEXT VALUE FOR**函式在**選取**陳述式指定**透過**子句， **ORDER BY**子句可用於**選取**陳述式。  
  
-   **透過**子句則允許使用**NEXT VALUE FOR**函式中使用時**選取**陳述式或`INSERT … SELECT …`陳述式。 使用**透過**子句搭配**NEXT VALUE FOR**中不允許函式**更新**或**合併**陳述式。  
  
-   如果同時有另一個處理序正在存取順序物件，傳回的數字可能會有間距。  
  
## <a name="metadata"></a>中繼資料  
 如需有關順序的詳細資訊，查詢[sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md)目錄檢視。  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要**更新**順序物件或順序的結構描述權限。 如需授與權限的範例，請參閱本主題稍後的範例 F。  
  
### <a name="ownership-chaining"></a>擁有權鏈結  
 順序物件支援擁有權鏈結。 如果順序物件與呼叫預存程序、觸發程序或資料表 (具有順序物件做為預設條件約束) 有相同的擁有者，則不需要順序物件的權限檢查。 如果順序物件與呼叫預存程序、觸發程序或資料表有不同的擁有者，則需要順序物件的權限檢查。  
  
 當**NEXT VALUE FOR**函式做為預設值資料表中，使用者需要**插入**資料表的權限和**更新**順序物件的權限將使用預設的資料。  
  
-   如果預設條件約束與順序物件有相同的擁有者，在呼叫預設條件約束時不需要順序物件的權限。  
  
-   如果預設條件約束與順序物件有不同的擁有者，即使透過預設條件約束呼叫，也需要順序物件的權限。  
  
### <a name="audit"></a>稽核  
 若要稽核**NEXT VALUE FOR**函數，請監視 SCHEMA_OBJECT_ACCESS_GROUP。  
  
## <a name="examples"></a>範例  
 如需建立順序和使用的範例**NEXT VALUE FOR**函數產生序號，請參閱[序號](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
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
 使用**NEXT VALUE FOR**支援預設條件約束的定義中的函式。 如需使用**NEXT VALUE FOR**中**CREATE TABLE**陳述式，請參閱 < 範例 C[序號](../../relational-databases/sequence-numbers/sequence-numbers.md)。 下列範例會使用 `ALTER TABLE`，將順序做為預設值加入至目前資料表。  
  
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
  
### <a name="e-using-the-next-value-for-function-with-select--into"></a>E. 搭配使用 NEXT VALUE FOR 函數與 SELECT … INTO  
 下列範例會使用`SELECT … INTO`陳述式建立資料表，名為`Production.NewLocation`並用`NEXT VALUE FOR`函式，每個資料列的編號。  
  
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
 下列範例會授與**更新**名為使用者的權限`AdventureWorks\Larry`使用權限來執行`NEXT VALUE FOR`使用`Test.CounterSeq`順序。  
  
```  
GRANT UPDATE ON OBJECT::Test.CounterSeq TO [AdventureWorks\Larry] ;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [建立順序 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [序號](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  
