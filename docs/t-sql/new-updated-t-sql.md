---
title: 已更新 - T-SQL 文件 | Microsoft Docs
description: 針對 Transact-SQL，顯示文件最新變更之已更新內容的程式碼片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.date: 04/28/2018
ms.openlocfilehash: 294ecf21f39eda34d2fe10d6dc07b7280c6b6954
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409107"
---
# <a name="new-and-recently-updated-transact-sql-docs"></a>新的最近更新內容：Transact-SQL 文件



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *更新日期範圍：* &nbsp; **2018-02-03** &nbsp; 至 &nbsp; **2018-04-28**
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

1. [ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)](#TitleNum_1)
2. [RESTORE 陳述式 (Transact-SQL)](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-alter-database-scoped-configuration-transact-sqlstatementsalter-database-scoped-configuration-transact-sqlmd"></a>1.&nbsp; [ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)](statements/alter-database-scoped-configuration-transact-sql.md)

*更新日期：2018-04-13* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一個](#TitleNum_2))

<!-- Source markdown line 150.  ms.author= "carlrab".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f6833910b664d0059a9073589807b195052325b3 bf969f123b22e6ebc650380a6905156f26ed6ca6  (PR=0  ,  Filename=alter-database-scoped-configuration-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



XTP_PROCEDURE_EXECUTION_STATISTICS  **=** { ON | **OFF** }

**適用於**：*{Included-Content-Goes-Here}*

在目前的資料庫上啟用或停用原生編譯 T-SQL 模組的模組層級執行統計資料收集。 預設值為 OFF。 執行統計資料會反映在 [sys.dm_exec_procedure_stats]。

如果這個選項是 ON，或已透過 [sp_xtp_control_proc_exec_stats] 啟用統計資料收集，則會收集原生編譯 T-SQL 模組的模組層級執行統計資料。

XTP_QUERY_EXECUTION_STATISTICS  **=** { ON | **OFF** }

**適用於**：*{Included-Content-Goes-Here}*

在目前的資料庫上啟用或停用原生編譯 T-SQL 模組的陳述式層級執行統計資料收集。 預設值為 OFF。 執行統計資料會反映在 [sys.dm_exec_query_stats] 和 [查詢存放區]。

如果這個選項是 ON，或已透過 [sp_xtp_control_query_exec_stats] 啟用統計資料收集，則會收集原生編譯 T-SQL 模組的陳述式層級執行統計資料。

如需原生編譯 T-SQL 模組效能監控的詳細資料，請參閱 [監視原生編譯預存程序的效能]。



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-restore-statements-transact-sqlstatementsrestore-statements-transact-sqlmd"></a>2.&nbsp; [RESTORE 陳述式 (Transact-SQL)](statements/restore-statements-transact-sql.md)

*更新日期：2018-04-13* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_1))

<!-- Source markdown line 339.  ms.author= "barbkess".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2902efb58bb964d3e9a0660956690d37f0397c00 36186a7cffd26ffa54a83e383ffd752dbc568a4d  (PR=0  ,  Filename=restore-statements-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**一般備註 - SQL Database 受控執行個體**


如果是非同步的還原，即使用戶端連線中斷，還是會繼續還原。 如果您的連線中斷，可以檢查 [sys.dm_operation_status] 檢視以取得還原作業 (以及建立和卸除資料庫) 的狀態。

會設定/覆寫下列資料庫選項，且稍後無法變更：

- NEW_BROKER (如果未在 .bak 檔案中啟用訊息代理程式)
- ENABLE_BROKER (如果未在 .bak 檔案中啟用訊息代理程式)
- AUTO_CLOSE=OFF (如果 .bak 檔案中的資料庫具有 AUTO_CLOSE=ON)
- RECOVERY FULL (如果 .bak 檔案中的資料庫具有 SIMPLE 或 BULK_LOGGED 復原模式)
- 新增記憶體最佳化檔案群組，並呼叫 XTP，如果它不在原始 .bak 檔案中的話。 任何現有的記憶體最佳化檔案群組都已重新命名為 XTP
- SINGLE_USER 和 RESTRICTED_USER 選項轉換為 MULTI_USER

**限制 - SQL Database 受控執行個體**

以下是適用的限制：

- 無法還原包含多個備份組的 .BAK 檔案。
- 無法還原包含多個記錄檔的 .BAK 檔案。
- 如果 .bak 包含 FILESTREAM 資料，則還原將會失敗。
- 目前無法還原包含具有使用中記憶體內物件之資料庫的備份。
- 目前無法還原在某處有使用中記憶體內物件存在之資料庫的備份。
- 目前無法還原唯讀模式之資料庫的備份。 即將移除這項限制。

如需詳細資訊，請參閱 [受控執行個體]







## <a name="similar-articles-about-new-or-updated-articles"></a>新文章或更新文章的類似文章

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (11+6)：&nbsp; &nbsp;**Advanced Analytics for SQL** 文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (18+0)：&nbsp; &nbsp;**Analysis Services for SQL** 文件](../analysis-services/new-updated-analysis-services.md)
- [新文章 + 更新文章 (218+14)：**連線到 SQL** 文件](../connect/new-updated-connect.md)
- [新文章 + 更新文章 (14+0)：&nbsp; &nbsp;**SQL 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新文章 + 更新文章 (3+2)：&nbsp; &nbsp; **Integration Services for SQL** 文件](../integration-services/new-updated-integration-services.md)
- [新文章 + 更新文章 (3+3)：&nbsp; &nbsp; **Linux for SQL** 文件](../linux/new-updated-linux.md)
- [新文章 + 更新文章 (7+10)：&nbsp; &nbsp;**SQL 的關聯式資料庫**文件](../relational-databases/new-updated-relational-databases.md)
- [新文章 + 更新文章 (0+2)：&nbsp; &nbsp; **Reporting Services for SQL** 文件](../reporting-services/new-updated-reporting-services.md)
- [新文章 + 更新文章 (1+3)：&nbsp; &nbsp; **SQL Operations Studio** 文件](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新文章 + 更新文章 (2+3)：&nbsp; &nbsp; **Microsoft SQL Server** 文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (1+1)：&nbsp; &nbsp; **SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新文章 + 更新文章 (5+2)：&nbsp; &nbsp; **SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新文章 + 更新文章 (0+2)：&nbsp; &nbsp; **Transact-SQL** 文件](../t-sql/new-updated-t-sql.md)
- [新文章 + 更新文章 (1+1)：&nbsp; &nbsp; **SQL 工具**文件](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (0+0)：**SQL 的分析平台系統**文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 範例**文件](../samples/new-updated-samples.md)
- [新文章 + 更新文章 (0+0)：**SQL Server 移轉小幫手 (SSMA)** 文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)

