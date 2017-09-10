---
title: "char 和 varchar (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- varchar
- varchar_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fixed-length data types [SQL Server]
- character data type
- char data type
- varchar(max) data type
- variable-length data types [SQL Server]
- varchar data type
ms.assetid: 282cd982-f4fb-4b22-b2df-9e8478f13f6a
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7c7bcb0e8ad7f8904703bd6c979b00aa30dd5348
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="char-and-varchar-transact-sql"></a>char 和 varchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

這些資料類型是固定的長度或可變長度。  
  
## <a name="arguments"></a>引數  
**char** [(  *n*  )] 固定長度，非 Unicode 字串資料。 *n*定義字串長度，而且必須是 1 到 8,000 的值。 儲存體大小是 *n* 位元組。 ISO 同義字**char**是**字元**。
  
**varchar** [(  *n*   |  **max** )] 可變長度，非 Unicode 字串資料。 *n*定義字串長度，而且可以是 1 到 8,000 的值。 **最大**表示最大儲存體大小是 2 ^31-1 位元組 (2 GB)。 儲存體大小是輸入資料的實際長度再加上 2 位元組。 ISO 同義字**varchar**是**charvarying**或**charactervarying**。
  
## <a name="remarks"></a>備註  
當 *n* 中未指定資料定義或變數宣告陳述式中，預設長度為 1。 當 *n* 時未指定使用 CAST 和 CONVERT 函數中，預設長度為 30。
  
物件，使用**char**或**varchar**除非利用 COLLATE 子句指派特定定序會被指派資料庫的預設定序。 定序會控制用來儲存字元資料的字碼頁。
  
如果您有支援多種語言的站台時，請考慮使用 Unicode **nchar**或**nvarchar**字元轉換問題降到最低的資料類型。 如果您使用**char**或**varchar**，我們建議下列：
- 使用**char**時一致的資料行資料項目的大小。  
- 使用**varchar**當資料行資料項目的大小變化。  
- 使用**varchar （max)**當資料行資料項目的大小變化相當大，且大小可能會超過 8,000 個位元組。  
  
SET ANSI_PADDING 是 OFF，當執行 CREATE TABLE 或 ALTER TABLE 時，如果**char**定義為 NULL 做為已處理的資料行**varchar**。
  
當定序字碼頁使用雙位元組字元時，儲存體大小仍 *n* 位元組。 根據字元字串的儲存體大小 *n* 位元組有可能少於 *n* 字元。

> [!WARNING]
> 每個非 null varchar （max） 或 nvarchar （max） 資料行需要 24 個位元組的額外修正配置，而不利於排序作業期間 8,060 位元組的資料列限制。 這樣可以建立隱含非 null varchar （max） 或可由資料表中的 nvarchar （max） 資料行的數目限制。  
建立資料表時 (高於最大資料列大小超過允許上限 8060 位元組所引發的一般警告) 或插入資料時，不會提供任何特殊錯誤。 如此大型的資料列可能會在某些一般作業 (如叢集索引鍵更新) 期間造成錯誤 (如錯誤 512)，或讓使用者直到執行作業前都無法預期多種完整資料行集。
  
##  <a name="_character"></a>將字元資料轉換  
將字元運算式轉換成不同大小的字元資料類型時，對新資料類型而言太大的值會被截斷。 **Uniqueidentifier**類型轉換為字元運算式，從的用途而言都視為字元類型，因此容易將轉換為字元類型之截斷規則。 請參閱稍後的＜範例＞一節。
  
當字元運算式轉換成字元運算式的不同資料類型或大小，例如從**char(5)**至**varchar(5)**，或**char(20)**至**char(15)**，輸入值的定序指派給轉換的值。 如果將非字元運算式轉換成字元資料類型，會將目前資料庫的預設定序指派給轉換的數值。 在任一情況下，您可以指派特定定序使用[COLLATE](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)子句。
  
> [!NOTE]  
>  字碼頁翻譯支援**char**和**varchar**資料類型，但不適用於**文字**資料型別。 舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，不會報告字碼頁翻譯期間的資料遺失。  
  
字元運算式轉換成近似**數值**資料型別可以包含選擇性的指數標記法 (小寫 e 或大寫 E 後面接著選擇性的加號 （+） 或減號 （-），再接著數字)。
  
字元運算式轉換成正確**數值**資料類型必須包含數字、 小數點和選擇性的加號 （+） 或減號 （-）。 前置的空白會被忽略。 字串不能用逗號分隔符號 (如 123,456.00 中的千位分隔符號)。
  
字元運算式轉換成**money**或**smallmoney**資料類型也可以包含選擇性小數點和錢幣符號 （$）。 可用逗號分隔符號 (如 $123,456.00)。
  
## <a name="examples"></a>範例  
  
### <a name="a-showing-the-default-value-of-n-when-used-in-variable-declaration"></a>A. 顯示在變數宣告中使用時，n 的預設值。  
下列範例顯示的預設值 *n* 為 1`char`和`varchar`在變數宣告中使用時，資料類型。
  
```sql
DECLARE @myVariable AS varchar = 'abc';  
DECLARE @myNextVariable AS char = 'abc';  
--The following returns 1  
SELECT DATALENGTH(@myVariable), DATALENGTH(@myNextVariable);  
GO  
```  
  
### <a name="b-showing-the-default-value-of-n-when-varchar-is-used-with-cast-and-convert"></a>B. 顯示搭配 CAST 和 CONVERT 使用 varchar 時，n 的預設值。  
下列範例顯示的預設值 *n* 為 30 時`char`或`varchar`資料型別會搭配`CAST`和`CONVERT`函式。
  
```sql
DECLARE @myVariable AS varchar(40);  
SET @myVariable = 'This string is longer than thirty characters';  
SELECT CAST(@myVariable AS varchar);  
SELECT DATALENGTH(CAST(@myVariable AS varchar)) AS 'VarcharDefaultLength';  
SELECT CONVERT(char, @myVariable);  
SELECT DATALENGTH(CONVERT(char, @myVariable)) AS 'VarcharDefaultLength';  
```  
  
### <a name="c-converting-data-for-display-purposes"></a>C. 轉換資料以加以顯示  
下列範例將兩個資料行轉換為字元類型，並套用一個會以特定格式顯示資料的樣式。 A **money**類型會轉換成字元資料，並套用樣式 1 時，會顯示以逗號分隔值小數點左邊每隔三位數和兩個數字的小數點右邊。 A **datetime**類型會轉換成字元資料，並套用樣式 3，資料顯示格式為 dd/mm/yy。 在 WHERE 子句中， **money**類型轉換成字元類型來執行字串比較作業。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT  BusinessEntityID,   
   SalesYTD,   
   CONVERT (varchar(12),SalesYTD,1) AS MoneyDisplayStyle1,   
   GETDATE() AS CurrentDate,   
   CONVERT(varchar(12), GETDATE(), 3) AS DateDisplayStyle3  
FROM Sales.SalesPerson  
WHERE CAST(SalesYTD AS varchar(20) ) LIKE '1%';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
BusinessEntityID SalesYTD              DisplayFormat CurrentDate             DisplayDateFormat  
---------------- --------------------- ------------- ----------------------- -----------------  
278              1453719.4653          1,453,719.47  2011-05-07 14:29:01.193 07/05/11  
280              1352577.1325          1,352,577.13  2011-05-07 14:29:01.193 07/05/11  
283              1573012.9383          1,573,012.94  2011-05-07 14:29:01.193 07/05/11  
284              1576562.1966          1,576,562.20  2011-05-07 14:29:01.193 07/05/11  
285              172524.4512           172,524.45    2011-05-07 14:29:01.193 07/05/11  
286              1421810.9242          1,421,810.92  2011-05-07 14:29:01.193 07/05/11  
288              1827066.7118          1,827,066.71  2011-05-07 14:29:01.193 07/05/11  
```  
  
### <a name="d-converting-uniqueidentifer-data"></a>D. 轉換 Uniqueidentifier 資料  
下列範例會將 `uniqueidentifier` 值轉換成 `char` 資料類型。
  
```sql
DECLARE @myid uniqueidentifier = NEWID();  
SELECT CONVERT(char(255), @myid) AS 'char';  
```  
  
下列範例會示範當值對於要轉換的目標資料類型而言太大時，資料的截斷方式。 因為**uniqueidentifier**類型限制為 36 個字元，超過該長度的字元會被截斷。
  
```sql
DECLARE @ID nvarchar(max) = N'0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong';  
SELECT @ID, CONVERT(uniqueidentifier, @ID) AS TruncatedValue;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
String                                       TruncatedValue  
-------------------------------------------- ------------------------------------  
0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong    0E984725-C51C-4BF4-9960-E1C80E27ABA0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱
[nchar 和 nvarchar &#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)  
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE &#40;TRANSACT-SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[資料類型轉換 &#40; Database Engine &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[估計資料庫的大小](../../relational-databases/databases/estimate-the-size-of-a-database.md)
  
  

