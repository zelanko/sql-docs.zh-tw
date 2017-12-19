---
title: "已更新 - SQL Server 文件 | Microsoft Docs"
description: "針對 SQL Server，顯示文件最新變更之已更新內容的程式碼片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: 
ms.component: sql-non-specified
ms.suite: sql
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: sql-server
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.author: genemi
ms.openlocfilehash: 77a97d94d005b43bf4c1a313a15a501cbe74a216
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="new-and-recently-updated-sql-server-docs"></a>新文章和最近更新的文章：SQL Server 文件



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *更新的日期範圍：* &nbsp; **2017-09-28** &nbsp; 到 &nbsp; **2017-12-02**
- *主旨區域：*&nbsp;**SQL Server**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [SQL Server 開發夥伴](partner-dev-sql-server.md)
2. [SQL Server 高可用性和災害復原夥伴](partner-hadr-sql-server.md)
3. [SQL Server 管理夥伴](partner-management-sql-server.md)
4. [SQL Server 監視夥伴](partner-monitor-sql-server.md)
5. [SQL Server 2012 SP4 版本資訊](sql-server-2012-sp4-release-notes.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [SQL Server 2017 版本資訊](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-2017-release-notessql-server-2017-release-notesmd"></a>1.&nbsp;[SQL Server 2017 版本資訊](sql-server-2017-release-notes.md)

*更新日期︰2017-11-20* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 37.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c9ac7e027e32b17bb9b54a4a878f70a70404f1cb 5b1aa8dc715fbb08d82b241f1e47f6e443b3e2fc  (PR=4032  ,  Filename=sql-server-2017-release-notes.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=7f8aebc72e7d0c8cff3990865c9f1316996a67d5) -->



- **因應措施：**首先請重新啟動電腦，並檢查 FILESTREAM 網路共用是否可用。 如果仍無法使用此共用，請完成下列步驟：

    1. 在 SQL Server 設定管理員中，以滑鼠右鍵按一下 SQL Server 執行個體，然後按一下 [屬性]。
    2. 在 [FILESTREAM] 索引標籤上，清除 [啟用 FILESTREAM 的檔案 I/O 資料流存取]，然後按一下 [套用]。
    3. 使用原始共用名稱再次選取 [啟用 FILESTREAM 的檔案 I/O 資料流存取]，然後按一下 [套用]。

**Master Data Services (MDS)**

- **問題和客戶的影響：**在使用者權限頁面上，當您將權限授予實體樹狀檢視中的根層級時，會看到下列錯誤：`"The model permission cannot be saved. The object guid is not valid"`

- **因應措施：**
  - 將權限授予樹狀檢視中的子節點而不是根層級。
  - 或
  - 執行「[在實體層級上套用權限時發生錯誤](http://sqlblog.com/blogs/mds_team/archive/2017/09/05/sql-server-2016-sp1-cu4-regression-error-while-applying-permission-on-entity-level-quick-workaround.aspx)」這個 MDS 小組部落格中說明的指令碼

**Analysis Services (英文)**

- **問題和客戶的影響：**1400 相容性層級的表格式模型目前無法使用下列來源的資料連接器。
  - Amazon Redshift
  - IBM Netezza
  - Impala
- **因應措施** ：無。

- **問題和客戶的影響：**具有檢視方塊且相容性層級為 1400 的直接查詢模型可能會在查詢或探索中繼資料時失敗。
- **因應措施：**移除檢視方塊，然後重新部署。







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
- [新文章 + 更新文章 (87 + 0)：**SQL 的分析平台系統**文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新文章 + 更新文章 (5+4)：**連線到 SQL** 文件](../connect/new-updated-connect.md)
- [新文章 + 更新文章 (0+1)：**SQL 的資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新文章 + 更新文章 (2+2)：**SQL 的 Integration Services** 文件](../integration-services/new-updated-integration-services.md)
- [新文章 + 更新文章 (10+9)：**SQL 適用的 Linux** 文件](../linux/new-updated-linux.md)
- [新文章 + 更新文章 (2+4)：**SQL 的關聯式資料庫**文件](../relational-databases/new-updated-relational-databases.md)
- [新文章 + 更新文章 (4+2)：**SQL 的 Reporting Services** 文件](../reporting-services/new-updated-reporting-services.md)
- [新文章 + 更新文章 (0+1)：**SQL 範例**文件](../sample/new-updated-sample.md)
- [新文章 + 更新文章 (21 + 0)：**SQL Operations Studio** 文件](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新文章 + 更新文章 (5+1)：**Microsoft SQL Server** 文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新文章 + 更新文章 (1+0)：**SQL Server 移轉小幫手 (SSMA)** 文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新文章 + 更新文章 (0+2)：**Transact-SQL** 文件](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (0 + 0)：**SQL 資料移轉小幫手 (DMA)**文件](../dma/new-updated-dma.md)
- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 的工具** 文件](../tools/new-updated-tools.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)


