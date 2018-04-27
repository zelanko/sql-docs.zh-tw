---
title: 已更新 - T-SQL 文件 | Microsoft Docs
description: 針對 Transact-SQL，顯示文件最新變更之已更新內容的程式碼片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql
ms.component: t-sql
ms.date: 02/03/2018
ms.openlocfilehash: a3a64bb1daf2dc38aabaf723bdf6794801c6218d
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="new-and-recently-updated-transact-sql-docs"></a>新的最近更新內容：Transact-SQL 文件



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- 更新日期範圍：&nbsp;**2017 年 12 月 3 日**&nbsp;-至-&nbsp;**2018 年 2 月 3 日**
- *主旨區域：* &nbsp; **T-SQL**.




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

1. [CREATE STATISTICS (Transact-SQL)](#TitleNum_1)
2. [UPDATE STATISTICS (Transact-SQL)](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-create-statistics-transact-sqlstatementscreate-statistics-transact-sqlmd"></a>1.&nbsp; [CREATE STATISTICS (Transact-SQL)](statements/create-statistics-transact-sql.md)

更新日期：2018-01-04 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一個](#TitleNum_2))

<!-- Source markdown line 200.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 384e68493597bcc36876a3c7bada2630106256e2 c22168ea59b6020e8ebe1ccac5fa6a6049e6db4d  (PR=4460  ,  Filename=create-statistics-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=4aeedbb88c60a4b035a49754eff48128714ad290) -->



MAXDOP = *max_degree_of_parallelism*
**適用於**：SQL Server (自 SQL Server 2017 CU3 起)。

 在統計作業期間，覆寫 **max degree of parallelism** 設定選項。 如需詳細資訊，請參閱 [設定 max degree of parallelism 伺服器組態選項](statements/../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。 請利用 MAXDOP 來限制執行平行計畫所用的處理器數目。 最大值是 64 個處理器。

 *max_degree_of_parallelism* 可以是：

 1 抑制平行計畫的產生。

 \>1 根據目前的系統工作負載，將平行統計作業所使用的處理器數目上限，限制為所指定的數目或更少的數目。

 0 (預設值) 根據目前的系統工作負載來使用實際數目的處理器或比實際數目更少的處理器。

 \<update_stats_stream_option> 僅供參考之用。 不支援。 我們無法保證未來的相容性。




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-update-statistics-transact-sqlstatementsupdate-statistics-transact-sqlmd"></a>2.&nbsp; [UPDATE STATISTICS (Transact-SQL)](statements/update-statistics-transact-sql.md)

更新日期：2018-01-04 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_1))

<!-- Source markdown line 167.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5721e21a9f43fa784fe9357c47cb2a814385e63d 24ae47c553635f389a182e5e643bf9bd6bf59e78  (PR=4460  ,  Filename=update-statistics-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=4aeedbb88c60a4b035a49754eff48128714ad290) -->



MAXDOP = *max_degree_of_parallelism*

**適用於**：SQL Server (自 SQL Server 2017 CU3 起)。

 在統計作業期間，覆寫 **max degree of parallelism** 設定選項。 如需詳細資訊，請參閱 [設定 max degree of parallelism 伺服器組態選項](statements/../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。 請利用 MAXDOP 來限制執行平行計畫所用的處理器數目。 最大值是 64 個處理器。

 *max_degree_of_parallelism* 可以是：

 1 抑制平行計畫的產生。

 \>1 根據目前的系統工作負載，將平行統計作業所使用的處理器數目上限，限制為所指定的數目或更少的數目。

 0 (預設值) 根據目前的系統工作負載來使用實際數目的處理器或比實際數目更少的處理器。








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


