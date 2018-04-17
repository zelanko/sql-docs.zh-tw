---
title: 已更新 - SSMS for SQL Server 文件 | Microsoft Docs
description: 顯示最近變更過的文件更新內容，SQL Server Management Studio (SSMS) for Microsoft SQL Server 的程式碼片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: ssms
ms.date: 02/03/2018
ms.openlocfilehash: f282e36152697b906b2d4e115be26943ae014fd9
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2018
---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>新文章和最近更新的文章：SQL Server Management Studio (SSMS) for SQL Server



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- 更新日期範圍：&nbsp;**2017 年 12 月 3 日**&nbsp;-至-&nbsp;**2018 年 2 月 3 日**
- *主題區：*&nbsp; **SQL Server Management Studio (SSMS)**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [安裝非英文版本的 SQL Server Management Studio (SSMS)](install-other-languages.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [下載 SQL Server Management Studio (SSMS)](#TitleNum_1)
2. [SQL Server Management Studio - 變更記錄 (SSMS)](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-sql-server-management-studio-ssmsdownload-sql-server-management-studio-ssmsmd"></a>1.&nbsp; [下載 SQL Server Management Studio (SSMS)](download-sql-server-management-studio-ssms.md)

更新日期：2018 年 1 月 18 日 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一個](#TitleNum_2))

<!-- Source markdown line 83.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0e123e7bdf04f02fcd26ac31fa30ed5f31b19c7d 924246b55d3cad6a5d068da8a41f4be23dcfeb2b  (PR=4652  ,  Filename=download-sql-server-management-studio-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=6b4aae3706247ce9b311682774b13ac067f60a79) -->



SSMS 17.4 是 SQL Server Management Studio 的最新版本。 17.x 世代的 SSMS 幾乎支援 SQL Server 2008 到 SQL Server 2017 的所有功能領域。 17.x 版也支援 SQL Analysis Service PaaS。

17.4 版包括：

弱點評定：
- 已加入新的 SQL 弱點評定服務，可在您的資料庫中掃描潛在的弱點和偏離最佳做法的項目，例如錯誤的設定、過多的權限和公開的機密資料。
- 評定結果包含可以解決個別問題的可操作步驟，以及合適情況下的自訂補救指令碼。 您可以針對每個環境和特定需求來自訂評定報告。 於 [SQL 弱點評定](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment)深入了解。

SMO：
- 已修正 *HasMemoryOptimizedObjects* 在 Azure 上擲回例外狀況的問題。
- 已加入新 CATALOG_COLLATION 功能的支援。

Always On 儀表板：
- 改進了可用性群組中延遲分析。
- 已加入兩個新的報告：*AlwaysOn\_Latency\_Primary* 和 *AlwaysOn\_Latency\_Secondary*。

執行程序表：
- 已更新連結，以指向正確的文件。
- 允許直接從產生的實際計劃進行單一計劃分析。
- 新的圖示集。
- 已加入辨識 GbApply、InnerApply 等「套用邏輯運算子」的支援。

XE 分析工具：
- 已重新命名為 XEvent 分析工具。
- 停止/啟動功能表命令現在預設會停止/啟動工作階段。
- 已啟用鍵盤快速鍵 (例如，CTRL-F 可進行搜尋)。
- 已加入 database\_name 與 client\_hostname 動作至 XEvent 分析工具工作階段中適當的事件。 若要讓變更生效，您可能需要刪除伺服器上現有的 QuickSessionStandard 或 QuickSessionTSQL 工作階段執行個體 - [Connect 3142981](https://connect.microsoft.com/SQLServer/feedback/details/3142981)



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-server-management-studio---changelog-ssmssql-server-management-studio-changelog-ssmsmd"></a>2.&nbsp; [SQL Server Management Studio - 變更記錄 (SSMS)](sql-server-management-studio-changelog-ssms.md)

更新日期：2018 年 1 月 29 日 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_1))

<!-- Source markdown line 27.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b5096fa8f1ae3f2e4bc040f43cb8810d96f2c69c eb641ac39386a26a76dc303f5bd55eb3f9f4c78d  (PR=0  ,  Filename=sql-server-management-studio-changelog-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=ba4b1c2e5200f2f78786b710da18fd38fedde6c9) -->



**[SSMS 17.4](download-sql-server-management-studio-ssms.md)**

正式運作 | 組建編號：14.0.17213.0

**新功能**


**一般 SSMS**

弱點評定：
- 已加入新的 SQL 弱點評定服務，可在您的資料庫中掃描潛在的弱點和偏離最佳做法的項目，例如錯誤的設定、過多的權限和公開的機密資料。
- 評定結果包含可以解決個別問題的可操作步驟，以及合適情況下的自訂補救指令碼。 您可以針對每個環境和特定需求來自訂評定報告。 於 [SQL 弱點評定](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment)深入了解。

SMO：
- 已修正 *HasMemoryOptimizedObjects* 在 Azure 上擲回例外狀況的問題。
- 已加入新 CATALOG_COLLATION 功能的支援。

Always On 儀表板：
- 改進了可用性群組中延遲分析。
- 已加入兩個新的報告：*AlwaysOn\_Latency\_Primary* 和 *AlwaysOn\_Latency\_Secondary*。

執行程序表：
- 已更新連結，以指向正確的文件。
- 允許直接從產生的實際計劃進行單一計劃分析。
- 新的圖示集。
- 已加入辨識 GbApply、InnerApply 等「套用邏輯運算子」的支援。

XE 分析工具：
- 已重新命名為 XEvent 分析工具。
- 停止/啟動功能表命令現在預設會停止/啟動工作階段。
- 已啟用鍵盤快速鍵 (例如，CTRL-F 可進行搜尋)。
- 已加入 database\_name 與 client\_hostname 動作至 XEvent 分析工具工作階段中適當的事件。 若要讓變更生效，您可能需要刪除伺服器上現有的 QuickSessionStandard 或 QuickSessionTSQL 工作階段執行個體 - [Connect 3142981](https://connect.microsoft.com/SQLServer/feedback/details/3142981)

命令列：
- 已加入新的命令列選項 ("-G")，可用來讓 SSMS 使用 Active Directory 驗證 (「整合式」或「密碼」)，自動連線至伺服器/資料庫。 如需詳細資訊，請參閱 [Ssms 公用程式](ssms-utility.md)。







## <a name="similar-articles-about-new-or-updated-articles"></a>新文章或更新文章的類似文章

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區


- [新文章 + 更新文章 (1+3)：&nbsp;**Advanced Analytics for SQL** 文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (0+1)：&nbsp;**Analytics Platform System for SQL** 文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新文章 + 更新文章 (0+1)：&nbsp;**連線到 SQL** 文件](../connect/new-updated-connect.md)
- [新文章 + 更新文章 (0+1)：&nbsp;**Database Engine for SQL** 文件](../database-engine/new-updated-database-engine.md)
- [新文章 + 更新文章 (12+1)：**Integration Services for SQL**  文件](../integration-services/new-updated-integration-services.md)
- [新文章 + 更新文章 (6+2)：&nbsp;**Linux for SQL** 文件](../linux/new-updated-linux.md)
- [新文章 + 更新文章 (15+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (2+9)：&nbsp;**Relational Databases for SQL** 文件](../relational-databases/new-updated-relational-databases.md)
- [新文章 + 更新文章 (1+0)：&nbsp;**Reporting Services for SQL** 文件](../reporting-services/new-updated-reporting-services.md)
- [新文章 + 更新文章 (1+1)：&nbsp;**SQL Operations Studio** 文件](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新文章 + 更新文章 (1+1)：&nbsp;**Microsoft SQL Server** 文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (0+1)：&nbsp;**SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新文章 + 更新文章 (1+2)：&nbsp;**SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新文章 + 更新文章 (0+2)：&nbsp;**Transact-SQL** 文件](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區


- [新文章 + 更新文章 (0+0)：**SQL 資料移轉小幫手 (DMA)** 文件](../dma/new-updated-dma.md)
- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**SQL Analysis Services** 文件](../analysis-services/new-updated-analysis-services.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**SQL 範例**文件](../samples/new-updated-samples.md)
- [新文章 + 更新文章 (0+0)：**SQL Server 移轉小幫手 (SSMA)** 文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+0)：**SQL 的工具** 文件](../tools/new-updated-tools.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)


