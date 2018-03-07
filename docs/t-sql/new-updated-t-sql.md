---
title: "已更新-T-SQL 文件 |Microsoft 文件"
description: "顯示更新的內容，如需 TRANSACT-SQL 中最近變更過的文件的程式碼片段。"
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: t-sql
ms.date: 02/03/2018
ms.openlocfilehash: c1f1ce751bd4bca781644e7e2f5282320c8c88a8
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-transact-sql-docs"></a>新的與最近的更新： TRANSACT-SQL 文件



幾乎每日 Microsoft 某些現有發行項上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文件網站。 這篇文章會顯示從最近已更新的發行項的摘錄。 可能也會列出新的文章連結。

這篇文章會定期重新執行程式所產生的。 偶爾摘錄會顯示具有完美的格式，或 markdown 從來源文件。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主體：



- *日期範圍的更新：* &nbsp; **2017年-12-03** &nbsp; -到- &nbsp; **2018年-02-03**
- *主旨區域：* &nbsp; **T-SQL**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近才建立新的發行項

下列連結會跳至最近新增的新文章。


***目前無新文章列出。***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新的發行項、 只有摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄顯示分隔其適當語意的內容。 此外，有時摘錄分開四周實際文件中的重要的 markdown 語法。 因此，這些摘錄適用於一般指導方針。 摘錄只會讓您知道您的興趣是否值得花時間按一下，瀏覽實際的發行項。

如需這些和其他原因，不要複製程式碼從這些摘錄中，而且不採用確切真為任何文字摘錄。 相反地，請瀏覽實際的發行項。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact 文件最近才更新清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [CREATE STATISTICS (Transact-SQL)](#TitleNum_1)
2. [UPDATE STATISTICS (Transact-SQL)](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-create-statistics-transact-sqlstatementscreate-statistics-transact-sqlmd"></a>1.&nbsp; [CREATE STATISTICS (Transact-SQL)](statements/create-statistics-transact-sql.md)

*更新日期︰ 2018年-01-04* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 200.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 384e68493597bcc36876a3c7bada2630106256e2 c22168ea59b6020e8ebe1ccac5fa6a6049e6db4d  (PR=4460  ,  Filename=create-statistics-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=4aeedbb88c60a4b035a49754eff48128714ad290) -->



MAXDOP = *max_degree_of_parallelism*
**適用於**: SQL Server （SQL Server 2017 CU3 開頭）。

 覆寫**的最大平行處理原則程度**組態選項的統計資料作業的持續時間。 如需詳細資訊，請參閱 [設定 max degree of parallelism 伺服器組態選項](statements/../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。 請利用 MAXDOP 來限制執行平行計畫所用的處理器數目。 最大值是 64 個處理器。

 *max_degree_of_parallelism*可以是：

 1 不顯示平行計畫的產生。

 \>1 數目上限，限制在指定的數字平行的統計資料作業所用的處理器或更少根據目前的系統工作負載。

 0 （預設值） 會使用實際的處理器數目或更少根據目前的系統工作負載。

 \<update_stats_stream_option > 識別僅供參考之用。 不支援。 我們無法保證未來的相容性。




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-update-statistics-transact-sqlstatementsupdate-statistics-transact-sqlmd"></a>2.&nbsp;[UPDATE STATISTICS (TRANSACT-SQL)](statements/update-statistics-transact-sql.md)

*更新日期︰ 2018年-01-04* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_1))

<!-- Source markdown line 167.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5721e21a9f43fa784fe9357c47cb2a814385e63d 24ae47c553635f389a182e5e643bf9bd6bf59e78  (PR=4460  ,  Filename=update-statistics-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=4aeedbb88c60a4b035a49754eff48128714ad290) -->



MAXDOP = *max_degree_of_parallelism*

**適用於**: SQL Server （從 SQL Server 2017 CU3 開始）。

 覆寫**的最大平行處理原則程度**組態選項的統計資料作業的持續時間。 如需詳細資訊，請參閱 [設定 max degree of parallelism 伺服器組態選項](statements/../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。 請利用 MAXDOP 來限制執行平行計畫所用的處理器數目。 最大值是 64 個處理器。

 *max_degree_of_parallelism*可以是：

 1 不顯示平行計畫的產生。

 \>1 數目上限，限制在指定的數字平行的統計資料作業所用的處理器或更少根據目前的系統工作負載。

 0 （預設值） 會使用實際的處理器數目或更少根據目前的系統工作負載。








## <a name="similar-articles-about-new-or-updated-articles"></a>新的或更新的發行項相關的類似文件

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>主旨區域，*不要*new 或最近更新發行項


- [新 + 更新 (1 + 3):&nbsp; **Advanced Analytics sql**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新 + 更新 (0 + 1):&nbsp; **Analytics Platform System sql**文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新 + 更新 (0 + 1):&nbsp; **連接到 SQL**文件](../connect/new-updated-connect.md)
- [新 + 更新 (0 + 1):&nbsp; **sql 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (12 + 1): **sql Integration Services**文件](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (6 + 2):&nbsp; **sql Linux**文件](../linux/new-updated-linux.md)
- [新 + 更新 (15 + 0):**適用於 SQL PowerShell**文件](../powershell/new-updated-powershell.md)
- [新 + 更新 (2 + 9):&nbsp; **關聯式資料庫供 SQL**文件](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (1 + 0):&nbsp; **Reporting Services SQL**文件](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (1 + 1):&nbsp; **SQL 作業 Studio**文件](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新 + 更新 (1 + 1):&nbsp; **Microsoft SQL Server**文件](../sql-server/new-updated-sql-server.md)
- [新 + 更新 (0 + 1):&nbsp; **SQL Server Data Tools (SSDT)**文件](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (1 + 2):&nbsp; **SQL Server Management Studio (SSMS)**文件](../ssms/new-updated-ssms.md)
- [新 + 更新 (0 + 2):&nbsp; **TRANSACT-SQL**文件](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>主旨區域執行*不*有任何新的或最近的更新發行項


- [新文章 + 更新文章 (0+0)：**SQL 資料移轉小幫手 (DMA)** 文件](../dma/new-updated-dma.md)
- [新 + 更新 (0 + 0): **ActiveX Data Objects (ADO) 的 SQL**文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**SQL Analysis Services** 文件](../analysis-services/new-updated-analysis-services.md)
- [新 + 更新 (0 + 0): **SQL 的 Data Quality Services**文件](../data-quality-services/new-updated-data-quality-services.md)
- [新 + 更新 (0 + 0):**資料採礦延伸模組 (DMX)，sql**文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新 + 更新 (0 + 0):**多維度運算式 (MDX) 的 SQL**文件](../mdx/new-updated-mdx.md)
- [新 + 更新 (0 + 0): **ODBC （開放式資料庫連接） 的 SQL**文件](../odbc/new-updated-odbc.md)
- [新 + 更新 (0 + 0):**範例 sql**文件](../sample/new-updated-sample.md)
- [新 + 更新 (0 + 0): **SQL Server 移轉小幫手 (SSMA)**文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+0)：**SQL 的工具** 文件](../tools/new-updated-tools.md)
- [新 + 更新 (0 + 0): **sql XQuery**文件](../xquery/new-updated-xquery.md)


