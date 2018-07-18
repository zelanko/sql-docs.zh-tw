---
title: 已更新 - SQL Server 文件 | Microsoft Docs
description: 針對 SQL Server，顯示文件最新變更之已更新內容的程式碼片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: sql-server
ms.date: 04/28/2018
ms.openlocfilehash: 9ccf32a232b501bb3184786af0c48dc7214b1936
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32686648"
---
# <a name="new-and-recently-updated-sql-server-docs"></a>新文章和最近更新的文章：SQL Server 文件



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *更新日期範圍：* &nbsp; **2018-02-03** &nbsp; 至 &nbsp; **2018-04-28**
- *主旨區域：*&nbsp;**SQL Server**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [如何參與 SQL Server 文件](sql-server-docs-contribute.md)
2. [SQL Server 隱私權補充](sql-server-privacy.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [SQL Server 2012 Service Pack 版本資訊](#TitleNum_1)
2. [SQL Server 2016 版本資訊](#TitleNum_2)
3. [SQL Server 文件](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-2012-service-pack-release-notessql-server-2012-sp4-release-notesmd"></a>1.&nbsp; [SQL Server 2012 Service Pack 版本資訊](sql-server-2012-sp4-release-notes.md)

*更新日期：2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一個](#TitleNum_2))

<!-- Source markdown line 57.  ms.author= craigg.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ce108992ea942b4a11f30d67a1a52d7f26868caa a6269ba2cb2d3b3b54aebf5087dc4d513e476a96  (PR=5676  ,  Filename=sql-server-2012-sp4-release-notes.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



- **自動軟體式 NUMA 資料分割** - 在 SQL 2014 SP2 中，於伺服器層級啟用追蹤旗標 8079 時會導入「自動[軟體式 NUMA](https://msdn.microsoft.com/library/ms345357(SQL.120).aspx)」資料分割。 在啟動期間啟用追蹤旗標 8079 時，SQL Server 2014 SP2 會查閱硬體配置，並在系統報告每個 NUMA 節點上有 8 個或更多個 CPU 時自動設定軟體式 NUMA。 自動軟體式 NUMA 會以感知超執行緒 (HT/邏輯處理器) 的方式運作。 其他節點的分割和建立可藉由增加接聽程式數目、調整以及網路和加密功能，來調整背景處理的規模。 建議先使用自動軟體式 NUMA 測試工作負載的效能，再於生產環境中將它開啟。

**Service Pack 3 版本資訊**


**下載頁面**

- [SQL Server 2012 SP3 Feature Pack](http://go.microsoft.com/fwlink/?linkid=615935)
- [SQL Server 2012 SP3 Express](http://go.microsoft.com/fwlink/?linkid=692144)

如需詳細資訊以根據您目前安裝的版本識別要下載的檔案名稱與位置，請參閱 [SQL Server 2012 Service Pack 3 版本資訊](https://support.microsoft.com/help/3072779/sql-server-2012-service-pack-3-release-information)中的＜選取正確的下載檔案＞一節。

**Service Pack 2 版本資訊**


**下載頁面**

- [SQL Server 2012 SP2 Feature Pack](http://go.microsoft.com/fwlink/?LinkID=401008)
- [SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)

使用下表，根據您目前安裝的版本來識別要下載的檔案位置與名稱。 下載頁面會提供系統需求與基本安裝指示。

|如果您目前安裝的版本是...|而且您想要...|下載並安裝...|



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-server-2016-release-notessql-server-2016-release-notesmd"></a>2.&nbsp; [SQL Server 2016 版本資訊](sql-server-2016-release-notes.md)

*更新日期：2018-04-27* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_1) | [下一個](#TitleNum_3))

<!-- Source markdown line 25.  ms.author= craigg.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a15210866acf524dae49f3a7fd7957c9ffa6a78a 7257cb2017779242cbb8fa2b562f4b102502e942  (PR=5695  ,  Filename=sql-server-2016-release-notes.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=d1c114b98fea55d2d4829dffdb25daf1b3f73dc2) -->



  本文描述 SQL Server 2016 版 (包括 Service Pack) 的限制和問題。 如需新功能的相關資訊，請參閱 [SQL Server 2016 的新功能](https://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2016)。

- 從**[評估中心](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)** 下載 SQL Server 2016
- Azure 虛擬機器小型：擁有 Azure 帳戶嗎？  接著前往 **[這裡](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/)** 來啟動已安裝 SQL Server 2016 SP1 的虛擬機器。
- 下載 SSMS：如要取得最新版的 SQL Server Management Studio，請參閱 **[下載 SQL Server Management Studio (SSMS)]**。

**<a name="bkmk_2016sp2"></a>SQL Server 2016 Service Pack 2 (SP2)**


SQL Server 2016 SP2 包含 2016 SP1 之後發行的所有累計更新，截至並且包含 CU8。

- [下載 Microsoft SQL Server 2016 Service Pack 2 (SP2)](https://go.microsoft.com/fwlink/?linkid=869608)
- 如需完整的更新清單，請參閱 [SQL Server 2016 Service Pack 2 版本資訊](https://support.microsoft.com/help/4052908/sql-server-2016-service-pack-2-release-information)



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-sql-server-documentationsql-server-technical-documentationmd"></a>3.&nbsp; [SQL Server 文件](sql-server-technical-documentation.md)

*更新日期：2018-04-27* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_2))

<!-- Source markdown line 77.  ms.author= craigg.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0262010ba39785a6d46b42f8469fb17701f13008 c69a83236391d039381a93c65ebbb2efa53e11b8  (PR=5695  ,  Filename=sql-server-technical-documentation.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=d1c114b98fea55d2d4829dffdb25daf1b3f73dc2) -->




<!-- : : : m-r -->
**試用 SQL Server！**
- 從評估中心下載：[下載 SQL Server for Windows](http://go.microsoft.com/fwlink/?LinkID=829477)
- 從評估中心下載：下載 SQL Server Management Studio (SSMS)
- 從評估中心下載：下載 SQL Server Data Tools (SSDT)
- 建立虛擬機器：[取得含 SQL Server 的虛擬機器](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)





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

