---
title: Microsoft SQL Server 中的純量 UDF 內嵌 | Microsoft Docs
description: 純量 UDF 內嵌功能可針對在 SQL Server (從 SQL Server 2019 開始) 中叫用純量 UDF 的查詢來改善其效能。
ms.custom: ''
ms.date: 06/23/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords: ''
ms.assetid: ''
author: s-r-k
ms.author: karam
monikerRange: = azuresqldb-current || >= sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 395d639cd62894c91fbf0690467e60aaeac57bea
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727089"
---
# <a name="scalar-udf-inlining"></a>純量 UDF 內嵌

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

本文介紹純量 UDF 內嵌，這是[智慧型查詢處理](../../relational-databases/performance/intelligent-query-processing.md)功能套件下的一項功能。 此功能可針對在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (從 [!INCLUDE[ssSQLv15](../../includes/sssqlv15-md.md)] 開始) 中叫用純量 UDF 的查詢來改善其效能。

## <a name="t-sql-scalar-user-defined-functions"></a>T-SQL 純量使用者定義函式
以 [!INCLUDE[tsql](../../includes/tsql-md.md)] 實作並傳回單一資料值的使用者定義函式 (UDF)，就是所謂的 T-SQL 純量使用者定義函式。 T-SQL UDF 是一種在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢之間達成程式碼重複使用和模組化的優雅方式。 某些計算 (例如複雜的商務規則) 更容易以命令式 UDF 格式表達。 UDF 有助於建置複雜的邏輯，而不需要撰寫複雜 SQL 查詢的專業知識。

## <a name="performance-of-scalar-udfs"></a>純量 UDF 的效能
純量 UDF 最終效能不佳通常是下列原因所致：

- **反覆叫用：** UDF 會以反覆方式叫用，每個合格的元組一次。 這會因函式叫用而產生重複內容切換的額外成本。 特別是，在其定義中執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢的 UDF 會受到嚴重影響。

- **缺少成本估算：** 在最佳化期間，只會估算關係運算子的成本，而不會估算純量運算子的成本。 在引進純量 UDF 之前，其他純量運算子通常很便宜，而不需要進行成本估算。 為純量運算子新增少量 CPU 成本便已足夠。 但還是有一些實際成本很高，卻仍然未充分表示的情況。

- **解譯執行：** UDF 會評估為陳述式批次，逐一執行陳述式。 系統會編譯每個陳述式本身，並快取已編譯的計劃。 雖然此快取策略可因避免重新編譯而節省一些時間，但每個陳述式都會單獨執行。 不會執行跨陳述式的最佳化。

- **序列執行：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允許在叫用 UDF 的查詢中使用內部查詢平行處理原則。 

## <a name="automatic-inlining-of-scalar-udfs"></a>自動內嵌純量 UDF
純量 UDF 內嵌功能的目標是改善叫用 T-SQL 純量 UDF 的查詢效能，其中的 UDF 執行是主要瓶頸。

使用這項新功能，純量 UDF 會自動轉換成純量運算式或純量子查詢，以在呼叫查詢中替代 UDF 運算子。 接著，系統就會將這些運算式和子查詢最佳化。 因此，查詢計劃不再具有使用者定義函式運算子，但在計劃中將觀察到其效果，例如檢視或內嵌 TVF。

### <a name="example-1---single-statement-scalar-udf"></a>範例 1 - 單一陳述式純量 UDF
請考慮下列查詢。

```sql
SELECT L_SHIPDATE, O_SHIPPRIORITY, SUM (L_EXTENDEDPRICE *(1 - L_DISCOUNT)) 
FROM LINEITEM
INNER JOIN ORDERS
  ON O_ORDERKEY = L_ORDERKEY 
GROUP BY L_SHIPDATE, O_SHIPPRIORITY ORDER BY L_SHIPDATE;
```

此查詢會計算明細項目折扣價格的總和，並顯示依據送貨日期和送貨優先順序分組的結果。 運算式 `L_EXTENDEDPRICE *(1 - L_DISCOUNT)` 是指定明細項目折扣價格的公式。 這類公式可以擷取至函式，以方便模組化和重複使用。

```sql
CREATE FUNCTION dbo.discount_price(@price DECIMAL(12,2), @discount DECIMAL(12,2)) 
RETURNS DECIMAL (12,2) AS
BEGIN
  RETURN @price * (1 - @discount);
END
```

現在，您可以修改查詢來叫用此 UDF。

```sql
SELECT L_SHIPDATE, O_SHIPPRIORITY, SUM (dbo.discount_price(L_EXTENDEDPRICE, L_DISCOUNT)) 
FROM LINEITEM
INNER JOIN ORDERS
  ON O_ORDERKEY = L_ORDERKEY 
GROUP BY L_SHIPDATE, O_SHIPPRIORITY ORDER BY L_SHIPDATE
```

根據先前所述的原因，具有 UDF 的查詢執行狀況不佳。 現在，透過純量 UDF 內嵌，您可以在查詢中直接替代為 UDF 主體中的純量運算式。 執行此查詢的結果會顯示在下表：

| 查詢： | 沒有 UDF 的查詢 | 具有 UDF 的查詢 (不使用內嵌) | 使用純量 UDF 內嵌的查詢 | 
| --- | --- | --- | --- |
| 執行時間： | 1.6 秒 | 29 分 11 秒 | 1.6 秒 |

這些數字是根據 10-GB CCI 資料庫 (使用 TPC-H 結構描述)，其在具有雙處理器 (12 個核心)、96 GB RAM 且 SSD 支援的機器上執行。 這些數字包含冷程序快取和緩衝集區的編譯及執行時間。 使用了預設設定，但未建立任何其他的索引。

### <a name="example-2---multi-statement-scalar-udf"></a>範例 2 - 多重陳述式純量 UDF
使用多個 T-SQL 陳述式 (例如變數指派和條件式分支) 實作的純量 UDF 也可以進行內嵌。 請考慮下列純量 UDF，其可根據客戶索引鍵來判斷該客戶的服務類別。 它會先使用 SQL 查詢計算客戶所下全部訂單的總價，以到達類別。 然後，使用 `IF (...) ELSE` 邏輯根據總價決定類別。

```sql
CREATE OR ALTER FUNCTION dbo.customer_category(@ckey INT) 
RETURNS CHAR(10) AS
BEGIN
  DECLARE @total_price DECIMAL(18,2);
  DECLARE @category CHAR(10);

  SELECT @total_price = SUM(O_TOTALPRICE) FROM ORDERS WHERE O_CUSTKEY = @ckey;

  IF @total_price < 500000
    SET @category = 'REGULAR';
  ELSE IF @total_price < 1000000
    SET @category = 'GOLD';
  ELSE 
    SET @category = 'PLATINUM';

  RETURN @category;
END
```

現在，請考慮叫用此 UDF 的查詢。

```sql
SELECT C_NAME, dbo.customer_category(C_CUSTKEY) FROM CUSTOMER;
```

[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] (相容性層級 140 及更早版本) 中此查詢的執行計劃如下：

![不使用內嵌的查詢計劃](./media/query-plan-without-udf-inlining.png)

如計劃所示，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在此採用一個簡單的策略：針對 `CUSTOMER` 資料表中的每個元組，叫用 UDF 並輸出結果。 此策略過於簡易且效率不彰。 透過內嵌，這類 UDF 可轉換成相等的純量子查詢，這些子查詢會在呼叫查詢中替代 UDF。

針對相同查詢，內嵌 UDF 的計劃如下所示。

![使用內嵌的查詢計劃](./media/query-plan-with-udf-inlining.png)

如先前所述，查詢計劃不再具有使用者定義函式運算子，但目前在計劃中可觀察到其效果，例如檢視或內嵌 TVF。 以下是上述計劃的一些重要觀察結果：

-  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已推斷 `CUSTOMER` 與 `ORDERS` 之間的隱含聯結，並透過聯結運算子使其變成明確聯結。
-  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 還會推斷隱含的 `GROUP BY O_CUSTKEY on ORDERS`，並使用 IndexSpool + StreamAggregate 來進行實作。
-  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 現在正在所有的運算子之間使用平行處理原則。

視 UDF 的邏輯複雜度而定，產生的查詢計劃也可能會變得更大且更複雜。 如我們所見，UDF 內的作業現在不再是黑盒子，因此查詢最佳化工具能夠估算這些作業的成本，並將其最佳化。 此外，因為計劃中不再有 UDF，所以反覆執行 UDF 叫用會取代為完全避免函式呼叫額外負荷的計劃。

## <a name="inlineable-scalar-udfs-requirements"></a>可內嵌的純量 UDF 需求
<a name="requirements"></a> 如果符合下列所有條件，則可以內嵌純量 T-SQL UDF：

- UDF 使用下列建構函式撰寫：
    - `DECLARE`、`SET`：變數宣告和指派。
    - `SELECT`:包含單一/多個變數指派的 SQL 查詢<sup>1</sup>。
    - `IF`/`ELSE`：使用任意巢狀層級的分支。
    - `RETURN`:單一或多個傳回陳述式。
    - `UDF`:巢狀/遞迴函式呼叫<sup>2</sup>。
    - 其他：`EXISTS`、`ISNULL` 等關聯式作業。
- UDF 不會叫用任何與時間相依 (例如 `GETDATE()`) 或有副作用<sup>3</sup> (例如 `NEWSEQUENTIALID()`) 的內建函式。
- UDF 會使用 `EXECUTE AS CALLER` 子句 (如果未指定 `EXECUTE AS` 子句，則為預設行為)。
- UDF 不會參考資料表變數或資料表值參數。
- 叫用純量 UDF 的查詢不會在其 `GROUP BY` 子句中參考純量 UDF 呼叫。
- 在其選取清單中搭配 `DISTINCT` 子句叫用純量 UDF 的查詢不會具備 `ORDER BY` 子句。
- UDF 不會用在 `ORDER BY` 子句中。
- 不會以原生方式編譯 UDF (支援 Interop)。
- UDF 不會用於計算資料行或檢查條件約束定義。
- UDF 不會參考使用者定義型別。
- UDF 中沒有新增任何簽章。
- UDF 不是資料分割函式。
- UDF 不包含對通用資料表運算式 (CTE) 的參考
- UDF 不包含內建函式 (例如 @@ROWCOUNT) 的參考，這些函式可能會在內嵌時改變結果 (在 Microsoft SQL Server 2019 CU2 中新增的限制)。
- UDF 不包含當作參數傳遞至純量 UDF 的彙總函式 (在 Microsoft SQL Server 2019 CU2 中新增的限制)。
- UDF 不會參考內建檢視 (例如 OBJECT_ID，Microsoft SQL Server 2019 CU2 中新增的限制)。
-   UDF 不會參考 XML 方法 (Microsoft SQL Server 2019 CU4 中新增的限制)。
-   UDF 不包含使用 ORDER BY 的 SELECT 而沒有 "TOP 1" (Microsoft SQL Server 2019 CU4 中新增的限制)。
-   UDF 不包含搭配 ORDER BY 子句執行指派的 SELECT 查詢 (例如，SELECT @x = @x +1 FROM table ORDER BY column_name，Microsoft SQL Server 2019 CU4 中新增的限制)。
- UDF 不包含多個 RETURN 陳述式 (SQL Server 2019 CU5 中新增的限制)。
- 不會從 RETURN 陳述式呼叫 UDF (在 SQL Server 2019 CU5 中新增的限制)。
- UDF 不會參考 STRING_AGG 函式 (SQL Server 2019 CU5 中新增的限制)。 

<sup>1</sup> 內嵌不支援具有變數累積/彙總的 `SELECT` (例如 `SELECT @val += col1 FROM table1`)。

<sup>2</sup> 遞迴 UDF 只能內嵌到特定深度。

<sup>3</sup> 其結果取決於目前系統時間的內建函式具有時間相依性。 可能會更新某個內部全域狀態之內建函式為具有副作用的函式範例。 這類函式會在每次呼叫時，根據內部狀態傳回不同的結果。

> [!NOTE]
> 如需最新的 T-SQL 純量 UDF 內嵌修正和內嵌資格案例變更的資訊，請參閱知識庫文章：[修正：SQL Server 2019 中的純量 UDF 內嵌問題](https://support.microsoft.com/en-us/help/4538581/fix-scalar-udf-inlining-issues-in-sql-server-2019) \(機器翻譯\)。

### <a name="checking-whether-or-not-a-udf-can-be-inlined"></a>檢查是否可以內嵌 UDF
針對每個 T-SQL 純量 UDF，[sys.sql_modules](../system-catalog-views/sys-sql-modules-transact-sql.md) 目錄檢視包含一個稱為 `is_inlineable` 的屬性，其表示是否可內嵌 UDF。 

> [!NOTE]
> `is_inlineable` 屬性衍生自 UDF 定義內找到的建構。 它不會在編譯時間檢查 UDF 是否可實際內嵌。 如需詳細資訊，請參閱[內嵌條件](#requirements)。

值 1 表示可內嵌，而 0 表示不可以。 對於所有內嵌 TVF，此屬性的值均為 1。 對於其他所有模組，值會是 0。

如果純量 UDF 可內嵌，並不表示它一律都會內嵌。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將決定 (在每個查詢上，根據每個 UDF) 是否要內嵌 UDF。 在 UDF 可能無法內嵌時的一些範例包括：

-  如果 UDF 定義達到數千行程式碼，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會選擇不要加以內嵌。 
-  系統將不會內嵌 `GROUP BY` 子句中的 UDF 引動過程。 這項決定會在編譯參考純量 UDF 的查詢時進行。
-  如果 UDF 是以憑證簽署。 因為可以在建立 UDF 之後加入並置放簽章，所以在編譯參考純量 UDF 的查詢時，會決定是否要內嵌。 例如，系統函式通常會以憑證簽署。 您可以使用 [sys. crypt_properties](../../relational-databases/system-catalog-views/sys-crypt-properties-transact-sql.md) 尋找已簽署的物件。 

   ```sql
   SELECT * 
   FROM sys.crypt_properties AS cp
   INNER JOIN sys.objects AS o ON cp.major_id = o.object_id;
   ```

### <a name="checking-whether-inlining-has-happened-or-not"></a>檢查是否已進行內嵌
如果符合所有先決條件，且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 決定執行內嵌，則它會將 UDF 轉換成關聯運算式。 您可以從查詢計劃輕鬆地看出是否已進行內嵌：

- 針對已成功內嵌的 UDF，計劃 XML不會有 `<UserDefinedFunction>` XML 節點。 
- 會發出特定 XEvent。

## <a name="enabling-scalar-udf-inlining"></a>啟用純量 UDF 內嵌
您可以啟用資料庫的相容性層級 150，讓工作負載自動符合純量 UDF 內嵌的資格。 您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 設定此項目。 例如：  

```sql
ALTER DATABASE [WideWorldImportersDW] SET COMPATIBILITY_LEVEL = 150;
```

除此之外，不需要對 UDF 或查詢進行任何其他變更，就能夠利用這項功能。

## <a name="disabling-scalar-udf-inlining-without-changing-the-compatibility-level"></a>停用純量 UDF 內嵌而不變更相容性層級
您可以在資料庫、陳述式或 UDF 的範圍停用純量 UDF 內嵌，同時仍將資料庫相容性層級維持在 150 以上。 若要在資料庫範圍停用純量 UDF 內嵌，請在適用資料庫的內容中執行下列陳述式： 

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = OFF;
```

若要為資料庫重新啟用純量 UDF 內嵌，請在適用資料庫的內容中執行下列陳述式：

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = ON;
```

當設為 ON 時，此設定會在 [`sys.database_scoped_configurations`](../system-catalog-views/sys-database-scoped-configurations-transact-sql.md) 中顯示為已啟用。 您也可以將 `DISABLE_TSQL_SCALAR_UDF_INLINING` 指定為 `USE HINT` 查詢提示，以停用特定查詢的純量 UDF 內嵌。 例如：

```sql
SELECT L_SHIPDATE, O_SHIPPRIORITY, SUM (dbo.discount_price(L_EXTENDEDPRICE, L_DISCOUNT)) 
FROM LINEITEM
INNER JOIN ORDERS
  ON O_ORDERKEY = L_ORDERKEY 
GROUP BY L_SHIPDATE, O_SHIPPRIORITY ORDER BY L_SHIPDATE
OPTION (USE HINT('DISABLE_TSQL_SCALAR_UDF_INLINING'));
```

`USE HINT` 查詢提示的優先順序高於資料庫範圍設定或相容性層級設定。

您也可以使用 `CREATE FUNCTION` 或 `ALTER FUNCTION` 陳述式中的 INLINE 子句來停用特定 UDF 的純量 UDF 內嵌。
例如：

```sql
CREATE OR ALTER FUNCTION dbo.discount_price(@price DECIMAL(12,2), @discount DECIMAL(12,2))
RETURNS DECIMAL (12,2)
WITH INLINE = OFF
AS
BEGIN
    RETURN @price * (1 - @discount);
END;
```

一旦執行上述陳述式，絕對不會將此 UDF 內嵌至叫用它的任何查詢中。 若要重新啟用內嵌此 UDF 的功能，請執行下列陳述式：

```sql
CREATE OR ALTER FUNCTION dbo.discount_price(@price DECIMAL(12,2), @discount DECIMAL(12,2))
RETURNS DECIMAL (12,2)
WITH INLINE = ON
AS
BEGIN
    RETURN @price * (1 - @discount);
END
```

> [!NOTE]
> `INLINE` 子句非為強制。 如果未指定 `INLINE` 子句，它會根據是否可以內嵌 UDF 自動設為 `ON`/`OFF`。 如果指定了 `INLINE = ON`，但發現 UDF 不適合進行內嵌，則會擲回錯誤。

## <a name="important-notes"></a>重要事項
如本文所述，純量 UDF 內嵌會將具有純量 UDF 的查詢轉換成具有對等純量子查詢的查詢。 由於此轉換之故，使用者可能會注意到下列案例中的一些行為差異：

1. 內嵌會導致相同的查詢文字產生不同查詢雜湊。
1. UDF 內先前可能已隱藏的陳述式特定警告 (例如除以零等等)，可能會因內嵌而顯示出來。
1. 查詢層級的聯結提示可能不再有效，因為內嵌可能會引進新的聯結。 必須改為使用本機聯結提示。
1. 參考內嵌純量 UDF 的檢視無法編製索引。 如果您需要在這類檢視上建立索引，請停用所參考 UDF 的內嵌功能。
1. [動態資料遮罩](../security/dynamic-data-masking.md)與內嵌 UDF 的行為可能有一些差異。 在某些情況下 (視 UDF 中的邏輯而定)，對於遮罩輸出資料行，內嵌可能更為保守。 在 UDF 中所參考資料行不是輸出資料行的情況下，它們不會被遮罩。 
1. 如果 UDF 參考內建函式 (例如 `SCOPE_IDENTITY()`、`@@ROWCOUNT` 或 `@@ERROR`)，則內建函式所傳回的值會隨著內嵌而變更。 此行為變更是因為內嵌變更了陳述式在 UDF 內的範圍。 從 Microsoft SQL Server 2019 CU2 開始，如果 UDF 參考特定內建函式 (例如，@@ROWCOUNT)，我們就會封鎖內嵌。

## <a name="see-also"></a>另請參閱
[SQL Server 資料庫引擎和 Azure SQL Database 的效能中心](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[查詢處理架構指南](../../relational-databases/query-processing-architecture-guide.md)     
[執行程序邏輯和實體運算子參考](../../relational-databases/showplan-logical-and-physical-operators-reference.md)     
[聯結](../../relational-databases/performance/joins.md)     
[示範智慧查詢處理](https://aka.ms/IQPDemos)    \(英文\)  
[修正：SQL Server 2019 中的純量 UDF 內嵌問題](https://support.microsoft.com/en-us/help/4538581/fix-scalar-udf-inlining-issues-in-sql-server-2019) \(機器翻譯\)     

