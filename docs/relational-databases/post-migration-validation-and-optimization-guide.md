---
description: 移轉後驗證和最佳化指南
title: 移轉後驗證和最佳化指南 | Microsoft Docs
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- post-migration validation and optimization
- guide, post-migration validation and optimization
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
author: pelopes
ms.author: harinid
ms.openlocfilehash: 01b629b65c7f8ab1571aa53a944a8525bd09a0b0
ms.sourcegitcommit: 442fbe1655d629ecef273b02fae1beb2455a762e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93235448"
---
# <a name="post-migration-validation-and-optimization-guide"></a>移轉後驗證和最佳化指南

[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 移轉後步驟對於協調任何資料精確度和完整性，以及發現工作負載的效能問題等方面非常重要。

## <a name="common-performance-scenarios"></a>常見的效能案例

以下是一些移轉至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 平台後常發生的效能案例以及解決方法。 這些包含 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 移轉至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的特定案例 (舊版移轉至新版)，以及外部平台 (例如 Oracle、DB2、MySQL 及 Sybase) 移轉至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。

## <a name="query-regressions-due-to-change-in-ce-version"></a><a name="CEUpgrade"></a>因為 CE 版本變更造成的查詢衰退

**適用於：** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 移轉至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。

從舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 移轉至 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 或更新版本，並升級到最新的[資料庫相容性層級](../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)時，工作負載可能會有效能衰退的風險。

這是因為從 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 開始，所有的查詢最佳化工具變更都會繫結至最新的[資料庫相容性層級](../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)；因此，計劃不會在升級時立即變更，而是在使用者將 `COMPATIBILITY_LEVEL` 資料庫選項變更為最新版本時變更。 此功能會結合查詢存放區，可讓您在升級過程中對查詢效能擁有絕佳層級的控制。 

如需 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 所導入的查詢最佳化工具變更的詳細資訊，請參閱[使用 SQL Server 2014 基數估算程式最佳化您的查詢計劃](/previous-versions/dn673537(v=msdn.10))。

### <a name="steps-to-resolve"></a>解決步驟

將[資料庫相容性層級](../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)變更成來源版本並遵循建議的升級工作流程，如下圖所示：

![顯示建議升級工作流程的圖表。](../relational-databases/performance/media/query-store-usage-5.png "query-store-usage-5")  

如需本主題的詳細資訊，請參閱[在升級到新版 SQL Server 期間保持效能穩定](../relational-databases/performance/query-store-usage-scenarios.md#CEUpgrade)。

## <a name="sensitivity-to-parameter-sniffing"></a><a name="ParameterSniffing"></a> 參數探查的敏感度

**適用於：** 外部平台 (例如 Oracle、DB2、MySQL 及 Sybase) 至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的移轉。

> [!NOTE]
> 若為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的移轉，如果此問題存在於來源 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，依現況移轉至較新版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 無法解決這種情況。 

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 透過在第一次編譯時使用探查輸入參數來編譯預存程序的查詢計劃，產生已針對該輸入資料分佈進行最佳化的參數化和可重複使用的計畫。 即使不是預存程序，也會將產生簡單計劃的大部分陳述式進行參數化。 第一次快取計劃之後，日後的每次執行都會對應至先前快取的計劃。
第一次編譯時若未對一般工作負載使用最常見的參數集，就會引發潛在問題。 對於不同的參數，使用相同的執行計畫會變成效率不佳。 如需本主題的詳細資訊，請參閱[參數探測](../relational-databases/query-processing-architecture-guide.md#ParamSniffing)。

### <a name="steps-to-resolve"></a>解決步驟

1.  使用 `RECOMPILE` 提示。 每次調整每個參數值時，計劃會計算一次。
2.  重新撰寫預存程序來使用 `(OPTIMIZE FOR(<input parameter> = <value>))` 選項。 決定要使用哪個適合大部分相關工作負載的值，建立和維護一個對於參數化值而言變得有效率的計劃。
3.  使用程序內的區域變數重新撰寫預存程序。 現在，最佳化工具會使用密度向量進行估計，導致不論參數值為何，都會產生相同的計劃。
4.  重新撰寫預存程序來使用 `(OPTIMIZE FOR UNKNOWN)` 選項。 其效果與使用區域變數技巧相同。
5.  重新撰寫查詢來使用 `DISABLE_PARAMETER_SNIFFING` 提示。 除非使用 `OPTION(RECOMPILE)`、`WITH RECOMPILE` 或 `OPTIMIZE FOR <value>`，否則完全停用參數探查，其效果與使用區域變數技巧相同。

> [!TIP] 
> 運用 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 計劃分析功能來快速確認這是否是問題。 詳細資訊可從[這裡](/archive/blogs/sql_server_team/new-in-ssms-query-performance-troubleshooting-made-easier)取得。

## <a name="missing-indexes"></a><a name="MissingIndexes"></a> 遺漏索引

**適用於：** 外部平台 (例如 Oracle、DB2、MySQL 及 Sybase) 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的移轉。

索引不正確或遺漏會造成額外的 I/O，而導致額外的記憶體和 CPU 浪費。 這可能是因為工作負載設定檔已變更，例如使用不同的述詞，而使現有索引設計失效。 索引策略不佳或工作負載設定檔變更的辨識項包括：
-   尋找重複、多餘、很少使用和完全未使用的索引。
-   特別注意未使用的索引與更新。

### <a name="steps-to-resolve"></a>解決步驟

1.  對於遺漏索引的任何參考運用圖形化執行計畫。
2.  索引建議由 [Database Engine Tuning Advisor](../tools/dta/tutorial-database-engine-tuning-advisor.md) 產生。
3.  運用[遺漏索引 DMV](../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md) 或透過 [SQL Server 效能儀表板](https://www.microsoft.com/download/details.aspx?id=29063)。
4.  利用既有的指令碼，可以使用現有的 DMV 深入了解任何遺漏、重複、多餘、很少使用和完全未使用的索引，以及是否有任何索引參考已提示/硬式編碼成資料庫中的現有程序和函數。 

> [!TIP] 
> 這類既有指令碼的範例包括 [索引建立](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Creation)和[索引資訊](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Information)。 

## <a name="inability-to-use-predicates-to-filter-data"></a><a name="InabilityPredicates"></a>無法使用述詞來篩選資料

**適用於：** 外部平台 (例如 Oracle、DB2、MySQL 及 Sybase) 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的移轉。

> [!NOTE]
> 若為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的移轉，如果此問題存在於來源 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，依現況移轉至較新版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 無法解決這種情況。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查詢最佳化工具只能負責編譯時已知的資訊。 如果工作負載依賴只有在執行時才能得知的述詞，則會提高選擇到不佳計畫的可能性。 在品質更高的計劃中，述詞必須是 **SARGable** 或 **S** earch **Arg** ument **able** 。

非 SARGable 述詞的一些範例：
-   隱含資料轉換，如 VARCHAR 至 NVARCHAR 或 INT 至 VARCHAR。 在實際執行計畫中尋找執行階段 CONVERT_IMPLICIT 警告。 從某個類型轉換成另一個類型也可能造成致遺失有效位數。
-   複雜的不明運算式，例如 `WHERE UnitPrice + 1 < 3.975`，但不是 `WHERE UnitPrice < 320 * 200 * 32`。
-   使用函數的運算式，例如 `WHERE ABS(ProductID) = 771` 或 `WHERE UPPER(LastName) = 'Smith'`
-   包含前置萬用字元的字串，例如 `WHERE LastName LIKE '%Smith'`，但不是 `WHERE LastName LIKE 'Smith%'`。

### <a name="steps-to-resolve"></a>解決步驟

1. 一律將變數/參數宣告為預期的目標[資料型別](../t-sql/data-types/data-types-transact-sql.md)。 
  -   這可能涉及將資料庫所儲存的任何使用者定義程式碼建構 (例如預存程序、使用者定義函數或檢視表)，與保存基礎表格所用資料類型相關資訊的系統資料表 (例如 [sys.columns](../relational-databases/system-catalog-views/sys-columns-transact-sql.md)) 進行比較。
2. 如果無法周遊所有程式碼到上一個點，則基於相同目的，請變更資料表的資料類型以符合任何變數/參數宣告。
3. 推斷出下列結構的效益：

  -   作為述詞使用的函數；
  -   萬用字元搜尋；
  -   根據單欄式資料的複雜運算式 - 評估是否需要改為建立可建立索引的保存計算資料行；

> [!NOTE] 
> 上述所有作業皆可以程式設計方式完成。

## <a name="use-of-table-valued-functions-multi-statement-vs-inline"></a><a name="TableValuedFunctions"></a>　使用資料表值函數 (多重陳述式與內嵌)

**適用於：** 外部平台 (例如 Oracle、DB2、MySQL 及 Sybase) 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的移轉。

> [!NOTE]
> 若為 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的移轉，如果此問題存在於來源 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，依現況移轉至較新版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 無法解決這種情況。

資料表值函數會傳回可以代替檢視的資料表資料類型。 檢視只限於單一 `SELECT` 陳述式，而使用者自訂函數可以包含其他陳述式，所允許的邏輯比在檢視中的還多。

> [!IMPORTANT] 
> 因為 MSTVF (多重陳述式資料表值函數) 的輸出資料表不會在編譯時建立，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查詢最佳化工具會依賴啟發學習法，而不是實際的統計資料，來判斷資料列的估計值。 即使將索引加入基底資料表，也沒有什麼幫助。 對於 MSTVF，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 使用固定估計值 1 作為 MSTVF 預期傳回的資料列數目 (從 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 開始，固定估計值為 100 個資料列)。

### <a name="steps-to-resolve"></a>解決步驟

1.  如果多個陳述式 TVF 只是單一陳述式，請轉換成內嵌 TVF。

    ```sql
    CREATE FUNCTION dbo.tfnGetRecentAddress(@ID int)
    RETURNS @tblAddress TABLE
    ([Address] VARCHAR(60) NOT NULL)
    AS
    BEGIN
      INSERT INTO @tblAddress ([Address])
      SELECT TOP 1 [AddressLine1]
      FROM [Person].[Address]
      WHERE  AddressID = @ID
      ORDER BY [ModifiedDate] DESC
    RETURN
    END
    ```

    內嵌格式範例會顯示在下方。

    ```sql
    CREATE FUNCTION dbo.tfnGetRecentAddress_inline(@ID int)
    RETURNS TABLE
    AS
    RETURN (
      SELECT TOP 1 [AddressLine1] AS [Address]
      FROM [Person].[Address]
      WHERE  AddressID = @ID
      ORDER BY [ModifiedDate] DESC
    )
    ```

2.  如果更加複雜，請考慮使用記憶體最佳化資料表或暫存資料表所儲存的中繼結果。

##  <a name="additional-reading"></a><a name="Additional_Reading"></a> 其他閱讀資料

 [使用查詢存放區的最佳作法](../relational-databases/performance/best-practice-with-the-query-store.md)  
[記憶體最佳化資料表](./in-memory-oltp/sample-database-for-in-memory-oltp.md)  
[使用者定義的函式](../relational-databases/user-defined-functions/user-defined-functions.md)  
[資料表變數和資料列估計 - 第 1 部分](/archive/blogs/blogdoezequiel/table-variables-and-row-estimations-part-1)  
[資料表變數和資料列估計 - 第 2 部分](/archive/blogs/blogdoezequiel/table-variables-and-row-estimations-part-2)  
[執行計畫快取與重複使用](../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)