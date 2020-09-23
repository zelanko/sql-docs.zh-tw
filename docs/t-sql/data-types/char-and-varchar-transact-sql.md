---
description: char 和 varchar (Transact-SQL)
title: char 和 varchar (Transact-SQL)
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
- utf8
ms.assetid: 282cd982-f4fb-4b22-b2df-9e8478f13f6a
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6fcc2f6593a7fc7a72c80ee3fe271cdb392ee747
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91115395"
---
# <a name="char-and-varchar-transact-sql"></a>char 和 varchar (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

固定大小 **char** 或變動大小 **varchar** 的字元資料類型。 從 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 開始，當使用支援 UTF-8 的定序時，這些資料類型會存放完整範圍的 [Unicode](../../relational-databases/collations/collation-and-unicode-support.md#Unicode_Defn) 字元並使用 [UTF-8](https://www.wikipedia.org/wiki/UTF-8) 字元編碼。 若指定非 UTF-8 定序，則這些資料類型只會存放該定序對應之字碼頁所支援的字元子集。

## <a name="arguments"></a>引數

**char** [ ( *n* ) ] 固定大小字串資料。 *n* 會定義字串大小 (單位為位元組)，且必須是 1 到 8,000 之間的值。 針對單位元組編碼字元集 (例如*拉丁字元*)，儲存大小是 *n* 位元組，而可儲存的字元數目也是 *n*。 針對多位元組編碼字元集，儲存大小仍是 *n* 位元組，但可儲存的字元數目可能小於 *n*。 **char** 的 ISO 同義字為 **character**。 如需有關字元集的詳細資訊，請參閱[單位元組和多位元組字元集](/cpp/c-runtime-library/single-byte-and-multibyte-character-sets)。

**varchar** [ ( *n* | **max** ) ] 可變大小字串資料。 您可以使用 *n* 以位元組為單位來定義字串大小，該值可以介於 1 到 8,000，或使用 **max** 來表示資料行大小限制最多為 2^31-1 個位元組 (2 GB) 的儲存體。 針對單位元組編碼字元集 (例如*拉丁字元*)，儲存大小是 *n* 位元組 + 2 位元組，而可儲存的字元數目也是 *n*。 針對多位元組編碼字元集，儲存大小仍是 *n* 位元組 + 2 位元組，但可儲存的字元數目可能小於 *n*。 **varchar** 的 ISO 同義字為 **charvarying** 或 **charactervarying**。 如需有關字元集的詳細資訊，請參閱[單位元組和多位元組字元集](/cpp/c-runtime-library/single-byte-and-multibyte-character-sets)。

## <a name="remarks"></a>備註

常見的誤解是假設 [CHAR(*n*) 和 VARCHAR(*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md)，*n* 會定義字元數。 但是在 [CHAR(*n*) 和 VARCHAR(*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md)，*n* 會定義字串長度 (以**位元組**為單位) (0-8,000)。 *n* 一律不會定義可儲存的字元數。 這類似於 [NCHAR (*n*) 和 NVARCHAR (*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) 的定義。
發生誤解的原因是，使用單一位元組編碼時，CHAR 和 VARCHAR 的儲存體大小是 *n* 位元組，而字元數目也是 *n*。 不過，針對多位元組編碼 (例如 [UTF-8](https://www.wikipedia.org/wiki/UTF-8))，較高的 Unicode 範圍 (128-1,114,111) 會使用二或多個位元組來產生單一字元。 例如，在定義為 CHAR (10) 的資料行中，[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 可以儲存 10 個使用單一位元組編碼的字元 (Unicode 範圍 0-127)，但使用多位元組編碼時，則小於 10 個字元 (Unicode 範圍 128-1,114,111)。 如需 Unicode 儲存和字元範圍的詳細資訊，請參閱 [UTF-8 和 UTF-16 之間的儲存差異](../../relational-databases/collations/collation-and-unicode-support.md#storage_differences)。

當資料定義或變數宣告陳述式中未指定 *n* 時，預設長度為 1。 若使用 CAST 和 CONVERT 函式時未指定 *n*，則預設長度為 30。

除非使用 COLLATE 子句指派特定定序；否則，使用 **char** 或 **varchar** 的物件會被指派資料庫的預設定序。 定序會控制用來儲存字元資料的字碼頁。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的多位元組編碼包括：

- 一些東亞語言的雙位元組字元集 (DBCS) 使用字碼頁 936 與 950 (中文)、932 (日文) 或 949 (韓文)。
- UTF-8 (具有字碼頁 65001)。 **適用範圍：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (從 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 開始)

若您的網站支援多種語言：

- 從 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 開始，請考慮使用支援 UTF-8 的定序來支援 Unicode 並將字元轉換問題降到最低。
- 若使用舊版 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]，請考慮使用 Unicode **nchar** 或 **nvarchar** 資料類型，將字元轉換問題降到最低。

若使用 **char** 或 **varchar**，建議您：

- 當資料行資料項目的大小一致時，請使用 **char**。
- 當資料行資料項目的大小變化相當大時，請使用 **varchar**。
- 當資料行資料項目的大小變化相當大，且字串長度可能超出 8,000 位元組時，請使用 **varchar(max)** 。

如果執行 CREATE TABLE 或 ALTER TABLE 時，SET ANSI_PADDING 是 OFF，就會將定義為 NULL 的 **char** 資料行當作 **varchar** 來處理。

> [!WARNING]
> 每個非 null 的 varchar(max) 或 nvarchar(max) 資料行都需要額外 24 位元組的固定配置，而不利於排序作業期間 8,060 位元組的資料列限制。 因此可能會對資料表中可建立的非 null varchar(max) 或 nvarchar(max) 資料行數目建立隱含限制。
建立資料表時 (高於最大資料列大小超過允許上限 8,060 位元組所引發的一般警告) 或插入資料時，不會提供任何特殊錯誤。 如此大型的資料列可能會在某些一般作業 (如叢集索引鍵更新，或排序整個資料行集) 期間造成錯誤 (如錯誤 512)。

## <a name="converting-character-data"></a><a name="_character"></a> 轉換字元資料

將字元運算式轉換成不同大小的字元資料類型時，對新資料類型而言太大的值會被截斷。 **uniqueidentifier** 類型因為轉換字元運算式之故，視為字元類型；因此會受到轉換成字元類型之截斷規則的影響。 請參閱稍後的＜範例＞一節。

當字元運算式被轉換成不同資料類型或大小的字元運算式時，例如從 **char(5)** 轉換成 **varchar(5)** ，或從 **char(20)** 轉換成 **char(15)** ，輸入數值的定序會被指派至轉換的數值。 如果將非字元運算式轉換成字元資料類型，會將目前資料庫的預設定序指派給轉換的數值。 不論哪一種狀況，都可以使用 [COLLATE](../../t-sql/statements/collations.md) 子句指派特定的定序。

> [!NOTE]
> 支援 **char** 和 **varchar** 資料類型的字碼頁轉換，但不支援 **text** 資料類型的字碼頁轉換。 舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，不會報告字碼頁翻譯期間的資料遺失。

轉換成近似**數值**資料類型的字元運算式，可包含選擇性的指數標記法。 這個標記法是小寫 e 或大寫 E 加上選擇性的加號 (+) 或減號 (-)，再接數字。

轉換成正確 **numeric** 資料類型的字元運算式必須由數字、小數點和選擇性的加號 (+) 或減號 (-) 組成。 前置的空白會被忽略。 字串不能用逗號分隔符號，如 123,456.00 中的千位分隔符號。

轉換成 **money** 或 **smallmoney** 資料類型的字元運算式也可以包含選擇性的小數點和錢幣符號 ($)。 可用逗號分隔符號 (如 $123,456.00)。

當空字串轉換為 **int** 時，其值會變成 ```0```。 當空字串轉換成日期時，它的值會變成[日期的預設值](date-transact-sql.md)，也就是 ```1900-01-01```。

## <a name="examples"></a>範例

### <a name="a-showing-the-default-value-of-n-when-used-in-variable-declaration"></a>A. 顯示在變數宣告中使用時，n 的預設值

下列範例顯示在變數宣告中使用 `char` 和 `varchar` 資料類型時，這些資料類型的 *n* 預設值是 1。

```sql
DECLARE @myVariable AS VARCHAR = 'abc';
DECLARE @myNextVariable AS CHAR = 'abc';
--The following returns 1
SELECT DATALENGTH(@myVariable), DATALENGTH(@myNextVariable);
GO
```

### <a name="b-showing-the-default-value-of-n-when-varchar-is-used-with-cast-and-convert"></a>B. 顯示搭配 CAST 和 CONVERT 使用 varchar 時，n 的預設值

下列範例顯示搭配使用 `char` 或 `varchar` 資料類型與 `CAST` 和 `CONVERT` 函式時，*n* 的預設值是 30。

```sql
DECLARE @myVariable AS VARCHAR(40);
SET @myVariable = 'This string is longer than thirty characters';
SELECT CAST(@myVariable AS VARCHAR);
SELECT DATALENGTH(CAST(@myVariable AS VARCHAR)) AS 'VarcharDefaultLength';
SELECT CONVERT(CHAR, @myVariable);
SELECT DATALENGTH(CONVERT(CHAR, @myVariable)) AS 'VarcharDefaultLength';
```

### <a name="c-converting-data-for-display-purposes"></a>C. 轉換資料以加以顯示

下列範例將兩個資料行轉換為字元類型，並套用一個會以特定格式顯示資料的樣式。 **money** 類型會轉換為字元資料，並套用樣式 1：在數值的小數點左側每三位數顯示一個逗號，並在小數點右側留下兩位數。 **datetime** 類型會轉換為字元資料，並套用樣式 3：以 dd/mm/yy 格式顯示資料。 在 WHERE 子句中，**money** 類型將轉換為字元類型，以進行字串比較作業。

```sql
USE AdventureWorks2012;
GO
SELECT BusinessEntityID,
   SalesYTD,
   CONVERT (VARCHAR(12),SalesYTD,1) AS MoneyDisplayStyle1,
   GETDATE() AS CurrentDate,
   CONVERT(VARCHAR(12), GETDATE(), 3) AS DateDisplayStyle3
FROM Sales.SalesPerson
WHERE CAST(SalesYTD AS VARCHAR(20) ) LIKE '1%';
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
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
SELECT CONVERT(CHAR(255), @myid) AS 'char';
```

下列範例會示範當值對於要轉換的目標資料類型而言太大時，資料的截斷方式。 因為 **uniqueidentifier** 類型限制為 36 個字元，所以超過該長度的字元會被截斷。

```sql
DECLARE @ID NVARCHAR(max) = N'0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong';
SELECT @ID, CONVERT(uniqueidentifier, @ID) AS TruncatedValue;
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
String                                       TruncatedValue
-------------------------------------------- ------------------------------------
0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong    0E984725-C51C-4BF4-9960-E1C80E27ABA0

(1 row(s) affected)
```

## <a name="see-also"></a>另請參閱

[nchar 和 nvarchar &#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)

[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)

[COLLATE &#40;Transact-SQL&#41;](../../t-sql/statements/collations.md)

[資料類型轉換 &#40;資料庫引擎&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)

[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)

[估計資料庫的大小](../../relational-databases/databases/estimate-the-size-of-a-database.md)

[定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)

[單位元組和多位元組字元集](/cpp/c-runtime-library/single-byte-and-multibyte-character-sets)
