---
title: "移轉後驗證和最佳化指南 |Microsoft 文件"
ms.custom: 
ms.date: 5/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- post-migration validation and optimization
- guide, post-migration validation and optimization
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
caps.latest.revision: 3
author: pelopes
ms.author: harinid
manager: 
ms.translationtype: Human Translation
ms.sourcegitcommit: 96f6a7eeb03fdc222d0e5b42bcfbf05c25d11db6
ms.openlocfilehash: d81eabfa1bdb5736bbf6f53ed34c2e1ac157e782
ms.contentlocale: zh-tw
ms.lasthandoff: 05/25/2017

---
# <a name="post-migration-validation-and-optimization-guide"></a>移轉後驗證和最佳化指南
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]post 移轉步驟是非常重要的協調任何資料精確度和完整性，以及發現與工作負載的效能問題。

# <a name="common-performance-scenarios"></a>常見的效能案例 
以下是一些常見的效能案例遇到移轉至後[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]平台和如何解決這些問題。 這些包含案例所要 specifdic[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]至[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]移轉 （至較新版本的舊版本），以及外部平台 （例如 Oracle、 DB2、 MySQL 及 Sybase）[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]移轉。

## <a name="Parameter Sniffing"></a>敏感性參數探測

**適用於：**外部平台 （例如 Oracle、 DB2、 MySQL 及 Sybase）[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]移轉。

> [!NOTE]
> 如[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]至[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]移轉，如果此問題存在於來源[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，移轉至較新版本的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]做為-是將無法解決這種情況。 

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]編譯預存程序使用探查輸入資料分佈的參數輸入的第一次編譯，產生參數化和可重複使用的計畫，針對最佳化查詢計劃。 即使不預存程序，將會進行參數化產生一般計劃的大部分陳述式。 第一次快取計劃之後，任何未來的執行會對應至先前的快取計劃。
該第一次的編譯不具有使用最常見的參數集的一般工作負載時，就會發生潛在的問題。 針對不同的參數相同的執行計畫會變成效率不佳。

### <a name="steps-to-resolve"></a>若要解決的步驟

1.    使用`RECOMPILE`提示。 計劃會計算每次調整每個參數值。
2.    請重寫預存程序，來使用 option `(OPTIMIZE FOR(<input parameter> = <value>))`。 決定使用哪個值適合大部分相關的工作負載，建立和維護計劃會變得有效率的參數化的值。
3.    請重寫預存程序中使用的程序內的區域變數。 現在，最佳化工具會使用密度向量的估計，導致相同的計劃，不論參數值。
4.    請重寫預存程序，來使用 option `(OPTIMIZE FOR UNKNOWN)`。 如同使用本機變數的技術。
5.    查詢重新撰寫成使用提示`DISABLE_PARAMETER_SNIFFING`。 相同效果做為使用本機變數技術所完全停用參數探測，除非`OPTION(RECOMPILE)`，`WITH RECOMPILE`或`OPTIMIZE FOR <value>`用。

> [!TIP] 
> 運用[!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)]計劃分析功能來快速找出這是否發生問題。 可用的詳細資訊[這裡](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-query-performance-troubleshooting-made-easier/)。

## <a name="Missing indexes"></a>遺漏索引

**適用於：**外部的平台 （例如 Oracle、 DB2、 MySQL 及 Sybase） 和[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]至[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]移轉。

不正確或遺漏的索引會造成額外的 I/O，導致額外的記憶體和 CPU 浪費掉。 這可能因為工作負載設定檔已變更例如使用不同的述詞，使失效現有索引設計。 辨識項不佳的索引策略，或工作負載設定檔中的變更包括：
-   尋找重複出現，多餘的很少使用 」 和 「 完全未使用的索引。
-   與未使用的索引，使用更新的特別注意。

### <a name="steps-to-resolve"></a>若要解決的步驟

1.    利用遺漏索引的任何參考的圖形化執行計畫。
2.    索引所產生的建議[Database Engine Tuning Advisor](../tools/dta/tutorial-database-engine-tuning-advisor.md)。
3.    運用[遺漏索引 DMV](../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)或透過[SQL Server 效能儀表板](https://www.microsoft.com/en-us/download/details.aspx?id=29063)。
4.    利用既有可以使用現有的 Dmv，同時也提供深入了解任何遺漏、 重複、 備援、 很少使用和完全未使用的索引，如果任何索引參考有所提示/硬式編碼成現有的程序和函式在資料庫中的指令碼。 

> [!TIP] 
> 這類預先存在的指令碼的範例包括[索引建立](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Creation)和[索引資訊](https://github.com/Microsoft/tigertoolbox/tree/master/Index-Information)。 

## <a name="Inability to use predicates"></a>無法使用述詞來篩選資料

**適用於：**外部的平台 （例如 Oracle、 DB2、 MySQL 及 Sybase） 和[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]至[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]移轉。

> [!NOTE]
> 如[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]至[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]移轉，如果此問題存在於來源[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，移轉至較新版本的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]做為-是將無法解決這種情況。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]查詢最佳化工具可以只負責在編譯時期已知的資訊。 如果工作負載依賴只可以在執行時期已知的述詞，如不佳的計畫選擇可能會提高。 對於更高品質計劃中，必須是述詞**SARGable**，或**S**earch **Arg**文**無法**。

非 SARGable 述詞的一些範例：
-   隱含資料轉換，例如 VARCHAR 為 NVARCHAR 或 VARCHAR 的 INT。 尋找在實際執行計畫的執行階段 CONVERT_IMPLICIT 警告。 從一個類型轉換成另一個也可能導致遺失有效位數。
-   不明的複雜運算式，例如`WHERE UnitPrice + 1 < 3.975`，但不是`WHERE UnitPrice < 320 * 200 * 32`。
-   運算式使用函式，例如`WHERE ABS(ProductID) = 771`或`WHERE UPPER(LastName) = 'Smith'`
-   字串包含前置的萬用字元，例如`WHERE LastName LIKE '%Smith'`，但不是`WHERE LastName LIKE 'Smith%'`。

### <a name="steps-to-resolve"></a>若要解決的步驟

1. 一律將變數/參數宣告為預期的目標[資料型別](../t-sql/data-types/data-types-transact-sql.md)。 
  -   這可能會比較儲存在保存基礎資料表中所使用的資料類型的詳細資訊的系統資料表 （例如預存程序、 使用者定義函數或檢視表） 的資料庫中任何使用者定義的程式碼建構 (例如[sys.columns](../relational-databases/system-catalog-views/sys-columns-transact-sql.md))。
2. 如果無法周遊至上一個點的所有程式碼，然後針對相同目的，變更資料表上的資料類型，比對任何變數/參數宣告。
3. 原因出下列結構的效益：
  -   做為述詞; 正在使用的函式
  -   萬用字元搜尋。
  -   根據單欄式資料的複雜運算式會評估需要改為建立保存的計算資料行，可以建立索引。

> [!NOTE] 
> 上述所有可以透過 programmaticaly。

## <a name="Table Valued Functions"></a>資料表值函式 （多重陳述式與內嵌） 的使用

**適用於：**外部的平台 （例如 Oracle、 DB2、 MySQL 及 Sybase） 和[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]至[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]移轉。

> [!NOTE]
> 如[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]至[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]移轉，如果此問題存在於來源[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，移轉至較新版本的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]做為-是將無法解決這種情況。

資料表值函式傳回資料表的資料類型，可以是檢視的替代方式。 雖然檢視僅限於單一`SELECT`陳述式中，使用者定義函數可以包含允許更多邏輯，而不是在檢視中的其他陳述式。

> [!IMPORTANT] 
> 因為輸出資料表的 MSTVF （多重陳述式資料表值函式） 不會建立在編譯時期[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]查詢最佳化工具會依賴啟發學習法，並不是實際的統計資料，以判斷資料列數量的估計值。 即使索引加入至基底資料表時，這並非要幫助。 MSTVFs，如[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 1 的固定的估計的資料列數目必須是要傳回之 MSTVF (開頭為[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]修正估計是 100 個資料列)。

### <a name="steps-to-resolve"></a>若要解決的步驟
1.    如果多重陳述式 TVF 單一陳述式，將轉換成內嵌 TVF。

    ```tsql
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
    若要 

    ```tsql
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

2.    如果是更複雜，請考慮使用儲存在記憶體最佳化的資料表或暫存資料表的中繼結果。

##  <a name="Additional_Reading"></a> 其他閱讀資料  
 [使用查詢存放區的最佳作法](../relational-databases/performance/best-practice-with-the-query-store.md)  
[Memory-Optimized Tables](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
[使用者定義的函式](../relational-databases/user-defined-functions/user-defined-functions.md)  
[資料表變數和資料列估計為第 1 部分](https://blogs.msdn.microsoft.com/blogdoezequiel/2012/11/30/table-variables-and-row-estimations-part-1/)  
[資料表變數和資料列估計為第 2 部分](https://blogs.msdn.microsoft.com/blogdoezequiel/2012/12/09/table-variables-and-row-estimations-part-2/)  
[執行計畫快取和重複使用](../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)

