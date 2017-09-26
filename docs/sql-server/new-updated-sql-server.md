---
title: "已更新 - SQL Server 文件 | Microsoft Docs"
description: "針對 SQL Server，顯示文件最新變更之已更新內容的程式碼片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: sql-server
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.translationtype: HT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 7f1c64e11e1bec44a558cec10c3d1f90f4951dfd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/21/2017

---
# <a name="new-and-recently-updated-sql-server-docs"></a>新文章和最近更新的文章：SQL Server 文件



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *更新的日期範圍：* &nbsp;**2017-07-18** &nbsp; 到 &nbsp; **2017-09-11**
- *主旨區域：*&nbsp;**SQL Server**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [SQL Server 2008 R2 SP2 Release Notes](sql-server-2008-r2-sp2-release-notes.md)
2. [SQL Server 2012 版本資訊](sql-server-2012-release-notes.md)
3. [SQL Server 2012 SP1 Release Notes](sql-server-2012-sp1-release-notes.md)
4. [SQL Server 2012 SP2 Release Notes](sql-server-2012-sp2-release-notes.md)
5. [SQL Server 2012 SP3 版本資訊](sql-server-2012-sp3-release-notes.md)
6. [SQL Server 2014 Release Notes](sql-server-2014-release-notes.md)
7. [SQL Server 說明檢視器與離線內容](sql-server-help-installation.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [SQL Server 2016 的新功能](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-whats-new-in-sql-server-2016what-s-new-in-sql-server-2016md"></a>1.&nbsp;[SQL Server 2016 的新功能](what-s-new-in-sql-server-2016.md)

*Updated: 2017-09-08* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 34.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e5bc0c05f120289f09a535400a4d521e4113ae55 0607d0a9af1c9a8dd9d3d7b0606895ff23bbffdc  (PR=0  ,  Filename=what-s-new-in-sql-server-2016.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=b97cc9723d563b19c85661f5ad7049a96fc904ff) -->



- 下載「免費的」[**SQL Server 2016 Developer Edition！**](https://www.microsoft.com/en-us/cloud-platform/sql-server-editions-developers)
- 下載最新版的 [SQL Server Management Studio (SSMS)](/sql-docs/docs/ssms/download-sql-server-management-studio-ssms)。
- 有 Azure 帳戶嗎？ 啟動[已安裝 SQL Server 2016 的虛擬機器](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/)。

**SQL Server 2016 Database Engine**

- 您現在可以在 SQL Server 安裝及設定期間，設定「多個 TempDB」資料庫檔案。
- 新的「查詢存放區」可將查詢文字、執行計畫和效能計量儲存於資料庫內，使您可以輕鬆地監視效能問題並進行疑難排解。 儀表板會顯示哪些查詢使用最多時間、記憶體或 CPU 資源。
- 「時態表」是記錄所有資料變更的記錄資料表，能完整記錄發生資料變更的日期和時間。
- 在 SQL Server 中全新內建的「JSON 支援」可支援 JSON 匯入、匯出、剖析和儲存。
- 新的 **PolyBase** 查詢引擎整合了 SQL Server 與 Hadoop 或 Azure Blob 儲存體中的外部資料。 您可以匯入或匯出資料，也可以執行查詢。
- 新的 **Stretch Database** 功能可讓您動態且安全地將本機 SQL Server 資料庫的資料封存到雲端的 Azure SQL 資料庫。 SQL Server 會自動查詢本機資料，以及位於連結資料庫內的遠端資料。
- **記憶體內 OLTP：**
    - 現在支援 FOREIGN KEY、UNIQUE 和 CHECK 限制式，以及原生編譯的預存程序 OR、NOT、SELECT DISTINCT、OUTER JOIN，以及 SELECT 中的子查詢。
    - 支援上至 2TB 的資料表 (原本為 256GB)。
    - 具備針對排序的資料行存放區索引增強功能，以及 Always On 可用性群組支援。
- 新的安全性功能：
    - **Always Encrypted：**啟用時，只有具備加密金鑰的應用程式才能存取 SQL Server 2016 資料庫中加密的敏感性資料。 金鑰一律不會傳遞至 SQL Server。







## <a name="similar-articles"></a>類似的文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (3+12)：**SQL 進階分析**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (5+0)：**連線到 SQL** 文件](../connect/new-updated-connect.md)
- [新文章 + 更新文章 (5+1)：**SQL 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新文章 + 更新文章 (19+82)：**SQL Integration Services** 文件](../integration-services/new-updated-integration-services.md)
- [新文章 + 更新文章 (1+8)：**Linux for SQL** 文件](../linux/new-updated-linux.md)
- [新文章 + 更新文章 (12+1)：**SQL 關聯式資料庫**文件](../relational-databases/new-updated-relational-databases.md)
- [新文章 + 更新文章 (0+1)：**SQL Reporting Services** 文件](../reporting-services/new-updated-reporting-services.md)
- [新文章 + 更新文章 (7+1)：**Microsoft SQL Server** 文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (1+1)：**SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新文章 + 更新文章 (0+2)：**SQL Server 移轉小幫手 (SSMA)** 文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (1+4)：**SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新文章 + 更新文章 (4+1)：**Transact-SQL** 文件](../t-sql/new-updated-t-sql.md)
- [新文章 + 更新文章 (0+1)：**SQL 工具**文件](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**SQL Analysis Services** 文件](../analysis-services/new-updated-analysis-services.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 範例**文件](../sample/new-updated-sample.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)



