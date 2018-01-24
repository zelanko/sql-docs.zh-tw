---
title: "已更新 - 資料庫引擎文件 | Microsoft Docs"
description: "顯示最近變更過的文件更新內容，資料庫引擎的程式碼片段。"
services: na
documentationcenter: 
author: MightyPen
manager: craigg
editor: barbkess
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: database-engine
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.openlocfilehash: cbf472ba2b8d2d7abad095992895b56940a82d92
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="new-and-recently-updated-database-engine-docs"></a>新的與最近的更新：資料庫引擎文件



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *更新的日期範圍：* &nbsp; **2017-09-28** &nbsp; 到 &nbsp; **2017-12-02**
- *主旨區域：* &nbsp; **資料庫引擎**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


***目前無新文章列出。***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [臨機操作工作負載的最佳化伺服器組態選項](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-optimize-for-ad-hoc-workloads-server-configuration-optionconfigure-windowsoptimize-for-ad-hoc-workloads-server-configuration-optionmd"></a>1. &nbsp;[針對特定工作負載最佳化伺服器設定選項](configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md)

*更新日期：2017-11-20* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 38.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6ca71358f13780b930e6fd10e431d4df2bb96441 221306c4554ebd383ab68ed67cdaeca390f57106  (PR=4032  ,  Filename=optimize-for-ad-hoc-workloads-server-configuration-option.md  ,  Dirpath=docs\database-engine\configure-windows\  ,  MergeCommitSha40=7f8aebc72e7d0c8cff3990865c9f1316996a67d5) -->



**建議**

如果一次性計畫的數目佔用 OLTP 伺服器中絕大部分的 ..!NCLUDE-NotShown--ssDEnoversion--../../includes/ssdenoversion-md.md)] 記憶體，且這些計畫為特定計畫，請使用此伺服器選項來降低這些物件的記憶體使用量。
若要找到一次性快取計畫的數目，請執行下列查詢：

```
SELECT objtype, cacheobjtype,
  AVG(usecounts) AS Avg_UseCount,
  SUM(refcounts) AS AllRefObjects,
  SUM(CAST(size_in_bytes AS bigint))/1024/1024 AS Size_MB
FROM sys.dm_exec_cached_plans
WHERE objtype = 'Adhoc' AND usecounts = 1
GROUP BY objtype, cacheobjtype;
```

> [!IMPORTANT]
> 將 **optimize for ad hoc workloads** 設定為 1 只會影響新的計畫。已經存在計畫快取中的計畫則不會受到影響。
> 若要立即影響已經快取的查詢計畫，計畫快取必須使用 [ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE--../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 清除，或是 ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] 必須重新啟動。







## <a name="similar-articles"></a>類似的文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (3+14)：**SQL 的進階分析**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (1+0)：**Analysis Services for SQL** 文件](../analysis-services/new-updated-analysis-services.md)
- [新文章 + 更新文章 (87+0)：**SQL 的分析平台系統**文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新文章 + 更新文章 (5+4)：**連線到 SQL** 文件](../connect/new-updated-connect.md)
- [新文章 + 更新文章 (0+1)：**SQL 的資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新文章 + 更新文章 (2+2)：**SQL 的 Integration Services** 文件](../integration-services/new-updated-integration-services.md)
- [新文章 + 更新文章 (10+9)：**SQL 適用的 Linux** 文件](../linux/new-updated-linux.md)
- [新文章 + 更新文章 (2+4)：**SQL 的關聯式資料庫**文件](../relational-databases/new-updated-relational-databases.md)
- [新文章 + 更新文章 (4+2)：**SQL 的 Reporting Services** 文件](../reporting-services/new-updated-reporting-services.md)
- [新文章 + 更新文章 (0+1)：**SQL 範例**文件](../sample/new-updated-sample.md)
- [新文章 + 更新文章 (21+0)：**SQL Operations Studio** 文件](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新文章 + 更新文章 (5+1)：**Microsoft SQL Server** 文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新文章 + 更新文章 (1+0)：**SQL Server 移轉小幫手 (SSMA)** 文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新文章 + 更新文章 (0+2)：**Transact-SQL** 文件](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (0+0)：**SQL 資料移轉小幫手 (DMA)** 文件](../dma/new-updated-dma.md)
- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 的工具** 文件](../tools/new-updated-tools.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)


