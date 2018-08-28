---
title: 原生編譯的 T-SQL 模組支援的功能 | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 05515013-28b5-4ccf-9a54-ae861448945b
caps.latest.revision: 44
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1eedf5863ff9c9ad04467771264a476a56647f22
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43065024"
---
# <a name="supported-features-for-natively-compiled-t-sql-modules"></a>原生編譯的 T-SQL 模組支援的功能
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


  本主題包含原生編譯 T-SQL 模組主體的 T-SQL 介面區和支援功能的清單，如預存程序 ([CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md))、純量使用者定義函數、內嵌資料表值的函數和觸發程序。  

 如需原生模組定義支援的功能，請參閱 [原生編譯的預存程序上支援的建構](../../relational-databases/in-memory-oltp/supported-ddl-for-natively-compiled-t-sql-modules.md)。  

-   [原生模組中的查詢介面區](#qsancsp)  

-   [資料修改](#dml)  

-   [流程控制語言](#cof)  

-   [支援的運算子](#so)  

-   [原生編譯模組中的內建函數](#bfncsp)  

-   [稽核](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md#auditing)  

-   [資料表和查詢提示](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md#tqh)  

-   [排序的限制](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md#los)  

 如需有關不支援之建構的完整資訊，以及如何處理某些原生編譯模組不支援功能的相關資訊，請參閱 [Migration Issues for Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)。 如需不支援功能的詳細資訊，請參閱 [記憶體中的 OLTP 不支援 Transact-SQL 建構](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)。  

##  <a name="qsancsp"></a> 原生模組中的查詢介面區  

以下為支援的查詢結構：  

CASE 運算式：CASE 可以用在允許有效運算式的任何陳述式或子句中。
   - **適用於：** [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]。  
    從 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 開始，原生編譯 T-SQL 模組現在支援 CASE 陳述式。

SELECT 子句：  

-   資料行和名稱別名 (使用 AS 或 = 語法)。  

-   純量子查詢
    - **適用於：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]。
      從 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 開始，原生編譯模組現在支援純量子查詢。

-   回到頁首*  

-   SELECT DISTINCT  
    - **適用於：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]。
      從 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 開始，原生編譯模組支援 DISTINCT 運算子。

              DISTINCT aggregates are not supported.  

-   UNION 和 UNION ALL
    - **適用於：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]。
      從 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 開始，原生編譯模組現在支援 UNION 和 UNION ALL 運算子。

-   變數指派  

FROM 子句：  

-   FROM \<記憶體最佳化的資料表或資料表變數>  

-   FROM \<原生編譯的內嵌 TVF>  

-   LEFT OUTER JOIN、RIGHT OUTER JOIN、CROSS JOIN 和 INNER JOIN。
    - **適用於：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]。
      從 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 開始，原生編譯模組現在支援 JOINS。

-   子查詢 `[AS] table_alias`。 如需詳細資訊，請參閱 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)。 
    - **適用於：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]。
      從 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 開始，原生編譯模組現在支援子查詢。

WHERE 子句：  

-   篩選器述詞 IS [NOT] NULL  

-   AND、BETWEEN  
-   OR、NOT、IN、EXISTS
    - **適用於：** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]。
      從 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] 開始，原生編譯模組現在支援 OR/NOT/IN/EXISTS 運算子。


[GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md) 子句：

- 彙總函數 AVG、COUNT、COUNT_BIG、MIN、MAX 和 SUM。  

- nvarchar、char、varchar、varchar、varbinary 和 binary 類型不支援 MIN 和 MAX。  

[ORDER BY](../../t-sql/queries/select-order-by-clause-transact-sql.md) 子句：


- 不支援 **ORDER BY** 子句中的 **DISTINCT** 。


- 如果 ORDER BY 清單中的運算式逐字顯示在 GROUP BY 清單中，支援 [GROUP BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md)。
  - 例如，支援 GROUP BY a + b ORDER BY a + b，但不支援 GROUP BY a, b ORDER BY a + b。  


HAVING 子句：

- 和 WHERE 子句一樣的運算式限制。


#### <a name="order-by-and-top-are-supported-in-natively-compiled-modules-with-some-restrictions"></a>原生編譯模組支援 ORDER BY 和 TOP，但有一些限制：


- 不支援 **WITH TIES** 子句中的 **PERCENT** 或 **TOP** 。


- 不支援 **ORDER BY** 子句中的 **DISTINCT** 。  


- 在**TOP** 子句中使用常數時， **ORDER BY** 與 **TOP** 結合不可大於 8,192。
  - 如果查詢包含聯結或彙總函數，這個限制可能會降低。 (例如，如果有一個聯結 (兩個資料表)，限制為 4,096 個資料列。 如果使用兩個聯結 (三個資料表)，限制為 2,730 個資料列)。  
  - 您可以在變數中儲存資料列數，以取得大於 8,192 的結果。  

```sql
DECLARE @v INT = 9000;
SELECT TOP (@v) … FROM … ORDER BY …
```

不過，與使用變數相較， **TOP** 子句中的常數會產生較好的效能。  

這些原生編譯限制 [!INCLUDE[tsql](../../includes/tsql-md.md)] 不適用於記憶體最佳化資料表上解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存取。  


##  <a name="dml"></a> 資料修改  

以下為支援的 DML 陳述式。  

-   INSERT VALUES (每個陳述式一個資料列) 和 INSERTSELECT  

-   UPDATE  

-   Delete  

-   UPDATE 和 DELETE 陳述式支援 WHERE。  

##  <a name="cof"></a> 流程控制語言  
 支援下列的流程控制語言建構。  

-   [IF...ELSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)  

-   [WHILE &#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)  

-   [RETURN &#40;Transact-SQL&#41;](../../t-sql/language-elements/return-transact-sql.md)  

-   [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md) 可以使用所有[支援的資料類型 (記憶體內部 OLTP)](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md)，以及記憶體最佳化的資料表類型。 變數可以宣告為 NULL 或 NOT NULL。  

-   [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  

-   [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  

               To achieve optimal performance, use a single TRY/CATCH block for an entire natively compiled T-SQL module.  

-   [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)  

-   BEGIN ATOMIC (在預存程序的外部等級)。 如需詳細資訊，請參閱 [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)。  

##  <a name="so"></a> 支援的運算子  
 下列為支援的運算子。  

-   [比較運算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md) (例如，>、\<、>= 和 <=)  

-   一元運算子 (+、-)。  

-   二元運算子 (*、/、+、-、% (模數) )。  

               The plus operator (+) is supported on both numbers and strings.  

-   邏輯運算子 (AND、OR、NOT)。  

-   位元運算子 ~、&、| 和 ^  

-   APPLY 運算子
    - **適用於：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]。  
      從 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 開始，原生編譯模組支援 APPLY 運算子。

##  <a name="bfncsp"></a> 原生編譯模組中的內建函數  
 記憶體最佳化資料表條件約束和原生編譯 T-SQL 模組支援下列函數。  

-   所有[數學函數 &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  

-   日期函數：CURRENT_TIMESTAMP、DATEADD、DATEDIFF、DATEFROMPARTS、DATEPART、DATETIME2FROMPARTS、DATETIMEFROMPARTS、DAY、EOMONTH、GETDATE、GETUTCDATE、MONTH、SMALLDATETIMEFROMPARTS、SYSDATETIME、SYSUTCDATETIME 和 YEAR。  

-   字串函數：LEN、LTRIM、RTRIM 和 SUBSTRING。  
    - **適用於：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]。  
      從 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 開始，也支援下列內建函式︰TRIM、TRANSLATE 及 CONCAT_WS。  

-   Identity 函數：SCOPE_IDENTITY  

-   NULL 函數：ISNULL  

-   Uniqueidentifier 函數：NEWID 和 NEWSEQUENTIALID  

-   JSON 函數  
    - **適用於：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]。  
      從 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 開始，原生編譯模組支援 JSON 函式。

-   錯誤函數：ERROR_LINE、ERROR_MESSAGE、ERROR_NUMBER、ERROR_PROCEDURE、ERROR_SEVERITY 和 ERROR_STATE  

-   系統函式：@@rowcount。 原生編譯預存程序內的陳述式會更新 @@rowcount，您可以在原生編譯預存程序中使用 @@rowcount，來判斷該原生編譯預存程序內最後執行之陳述式所影響的資料列數。 不過，@@rowcount 會在原生編譯預存程序開始及結束執行時重設為 0。  

-   安全性函數：IS_MEMBER({'group' | 'role'})、IS_ROLEMEMBER ('role' [, 'database_principal'])、IS_SRVROLEMEMBER ('role' [, 'login'])、ORIGINAL_LOGIN()、SESSION_USER、CURRENT_USER、SUSER_ID(['login'])、SUSER_SID(['login'] [, Param2])、SUSER_SNAME([server_user_sid])、SYSTEM_USER、SUSER_NAME、USER、USER_ID(['user'])、USER_NAME([id])、CONTEXT_INFO()。

-   原生模組可以巢狀方式執行。

##  <a name="auditing"></a> 稽核  
 原生編譯預存程序中支援程序層級稽核。  

 如需有關稽核的詳細資訊，請參閱＜ [Create a Server Audit and Database Audit Specification](../../relational-databases/security/auditing/create-a-server-audit-and-database-audit-specification.md)＞。  

##  <a name="tqh"></a> 資料表和查詢提示  
 支援下列功能：  

-   在資料表提示語法或查詢的 [OPTION 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md) 中的 INDEX、FORCESCAN 和 FORCESEEK 提示。 如需詳細資訊，請參閱[資料表提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)。  

-   FORCE ORDER  

-   LOOP 聯結提示  

-   OPTIMIZE FOR  

 如需詳細資訊，請參閱[查詢提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)。  

##  <a name="los"></a> 排序的限制  
 在使用 [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md) 和一個 [ORDER BY 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md) 的查詢中，您可以排序 8000 多個資料列。 但是沒有 [ORDER BY 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md)，[TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md) 最多只能排序 8000 個資料列 (如果有聯結則資料列更少)。  

 如果查詢同時使用 [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md) 運算子和一個 [ORDER BY 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md)，TOP 運算子最多可以指定 8192 個資料列。 如果您指定超過 8192 個資料列，則會收到錯誤訊息：**Msg 41398，層級 16，狀態 1、程序 *\<程序名稱>*、行 *\<行號>*。TOP 運算子最多可以傳回 8192 個資料列；要求 *\<數字>*。**  

 如果您沒有 TOP 子句，則可以使用 ORDER BY 排序任意數目的資料列。  

 如果您未使用 ORDER BY 子句，則可以使用任何整數值搭配 TOP 運算子。  

 TOP N = 8192 的範例：編譯  

```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    SELECT TOP 8192 ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```

 TOP N > 8192 的範例：編譯失敗。  

```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    SELECT TOP 8193 ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```

 8192 資料列限制只適用於 `TOP N` ，其中 `N` 是常數，如前面的範例中所示。  如果您需要讓 `N` 大於 8192，可以將值指派給變數，並使用該變數搭配 `TOP`。  

 使用變數的範例：編譯  

```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    DECLARE @v int = 8193   
    SELECT TOP (@v) ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```

 **傳回資料列的限制：** 有兩種情況可能會減少 TOP 運算子能夠傳回的資料列數目：  

-   在查詢中使用 JOIN。  JOIN 對限制的影響取決於查詢計劃。  

-   使用彙總函式或參考彙總 ORDER BY 子句中的函式。  

 計算 TOP N 中最差情況下支援之最大值 N 的公式是： `N = floor ( 65536 / number_of_tables * 8 + total_size+of+aggs )`。  

## <a name="see-also"></a>另請參閱  
 [原生編譯的預存程序](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)   
 [原生編譯預存程序的移轉問題](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)  


