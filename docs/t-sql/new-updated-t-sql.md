---
title: "已更新-T-SQL 文件 |Microsoft 文件"
description: "顯示更新的內容，如需 TRANSACT-SQL 中最近變更過的文件的程式碼片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.workload: t-sql
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: fa2ad3f4bc6071c54b9996a893ee584ba215100f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-transact-sql-docs"></a>新的與最近的更新： TRANSACT-SQL 文件



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *日期範圍的更新：* &nbsp; **2017年-07-18** &nbsp; -到- &nbsp; **2017年-09-11**
- *主旨區域：* &nbsp; **T-SQL**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結跳至最近新增的新發行項。


1. [預測 (TRANSACT-SQL)](queries/predict-transact-sql.md)
2. [ALTER 外部程式庫 (TRANSACT-SQL)](statements/alter-external-library-transact-sql.md)
3. [建立外部程式庫 (TRANSACT-SQL)](statements/create-external-library-transact-sql.md)
4. [卸除的外部程式庫 (TRANSACT-SQL)](statements/drop-external-library-transact-sql.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

此區段會顯示更新所收集從最近曾發生大規模的更新發行項的摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單所提供的摘錄的一節中所列的所有更新文章連結。

1. [CAST 和 CONVERT (TRANSACT-SQL)](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-cast-and-convert-transact-sqlfunctionscast-and-convert-transact-sqlmd"></a>1.&nbsp;[CAST 和 CONVERT (TRANSACT-SQL)](functions/cast-and-convert-transact-sql.md)

*更新日期︰ 2017年-09-08* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 647.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b805ecddecda72ffc026c3866b5284a79b69fb3f f2906eaf87c7cdf1409922d4efba8cd1c5635674  (PR=0  ,  Filename=cast-and-convert-transact-sql.md  ,  Dirpath=docs\t-sql\functions\  ,  MergeCommitSha40=b97cc9723d563b19c85661f5ad7049a96fc904ff) -->



**K。算術運算子搭配使用 CAST**

下列範例會計算單一資料行計算產品單價再除以 (`UnitPrice`) 的折扣百分比 (`UnitPriceDiscountPct`)。 這個結果在進位到最近的整數之後，會轉換成 `int` 資料類型。 使用 AdventureWorksDW。

```
SELECT ProductKey, UnitPrice,UnitPriceDiscountPct,
       CAST(ROUND (UnitPrice*UnitPriceDiscountPct,0) AS int) AS DiscountPrice
FROM dbo.FactResellerSales
WHERE SalesOrderNumber = 'SO47355'
      AND UnitPriceDiscountPct > .02;
```

..!裡 NotShown-ssResult.../../includes/ssresult-md.md)]

```
ProductKey  UnitPrice  UnitPriceDiscountPct  DiscountPrice
----------  ---------  --------------------  -------------
323         430.6445   0.05                  22
213         18.5043    0.05                  1
456         37.4950    0.10                  4
456         37.4950    0.10                  4
216         18.5043    0.05                  1
```

**L。利用 CAST 來串連**

下列範例使用 CAST 來串連非字元運算式。 使用 AdventureWorksDW。

```
SELECT 'The list price is ' + CAST(ListPrice AS varchar(12)) AS ListPrice
FROM dbo.DimProduct
WHERE ListPrice BETWEEN 350.00 AND 400.00;
```

..!裡 NotShown-ssResult.../../includes/ssresult-md.md)]

```
ListPrice
------------------------
The list price is 357.06
The list price is 364.09
The list price is 364.09
The list price is 364.09
The list price is 364.09
```

**M。利用 CAST 來產生更容易閱讀的文字**

下列範例選取清單中使用 CAST 轉換`Name`欄**char （10)**資料行。 使用 AdventureWorksDW。

```
SELECT DISTINCT CAST(EnglishProductName AS char(10)) AS Name, ListPrice
FROM dbo.DimProduct
WHERE EnglishProductName LIKE 'Long-Sleeve Logo Jersey, M';
```

..!裡 NotShown-ssResult.../../includes/ssresult-md.md)]







## <a name="similar-articles"></a>類似的文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

此區段會列出最近已更新的發行項，在我們的公用 GitHub.com 儲存機制中的其他主體區域中的非常類似文件： [MicrosoftDocs/sql 的文件](https://github.com/MicrosoftDocs/sql-docs/)。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新 + 更新 (3 + 12): **Advanced Analytics sql**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新 + 更新 (5 + 0):**連接到 SQL**文件](../connect/new-updated-connect.md)
- [新 + 更新 (5 + 1): **sql 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (19 + 82): **sql Integration Services**文件](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (1 + 8): **sql Linux**文件](../linux/new-updated-linux.md)
- [新 + 更新 (12 + 1):**關聯式資料庫供 SQL**文件](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (0 + 1): **Reporting Services SQL**文件](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (7 + 1): **Microsoft SQL Server**文件](../sql-server/new-updated-sql-server.md)
- [新 + 更新 (1 + 1): **SQL Server Data Tools (SSDT)**文件](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (0 + 2): **SQL Server 移轉小幫手 (SSMA)**文件](../ssma/new-updated-ssma.md)
- [新 + 更新 (1 + 4): **SQL Server Management Studio (SSMS)**文件](../ssms/new-updated-ssms.md)
- [新 + 更新 (4 + 1): **TRANSACT-SQL**文件](../t-sql/new-updated-t-sql.md)
- [新 + 更新 (0 + 1): **Tools for SQL**文件](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新 + 更新 (0 + 0): **sql Analysis Services**文件](../analysis-services/new-updated-analysis-services.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新 + 更新 (0 + 0): **Master Data Services (MDS) sql**文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 範例**文件](../sample/new-updated-sample.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)



