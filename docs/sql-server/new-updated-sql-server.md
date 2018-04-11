---
title: 已更新 - SQL Server 文件 | Microsoft Docs
description: 針對 SQL Server，顯示文件最新變更之已更新內容的程式碼片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: sql-server
ms.date: 02/03/2018
ms.openlocfilehash: bcbf9a579fce8d27eaa53471190dbe850774c146
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2018
---
# <a name="new-and-recently-updated-sql-server-docs"></a>新文章和最近更新的文章：SQL Server 文件



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- 更新日期範圍：&nbsp;**2017 年 12 月 3 日**&nbsp;-至-&nbsp;**2018 年 2 月 3 日**
- *主旨區域：*&nbsp;**SQL Server**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [升級在 Windows Server 2008/2008 R2/2012 叢集上執行的 SQL Server 執行個體](failover-clusters/windows/upgrade-sql-server-failover-cluster-instance-2008-2012.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [SQL Server 離線說明和說明檢視器](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-offline-help-and-help-viewersql-server-help-installationmd"></a>1.&nbsp; [SQL Server 離線說明和說明檢視器](sql-server-help-installation.md)

更新日期：2017 年 12 月 19 日 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 67.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ea491fdc173a54fb4cdb3dfa2e26bd206d1cc45d 22444427a48064b76088d19d1ffae0a885bfe2a7  (PR=4338  ,  Filename=sql-server-help-installation.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=f2fde1c324466530f92006561a9a29decb711e1b) -->



   說明檢視器會開啟至 [管理內容] 索引標籤。

2. 若要安裝最新說明內容套件，請選擇 [安裝來源] 下方的 [線上]。

   ![HelpViewer2_ManageContent_OnlineSource](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-onlinesource.png)

   >[!NOTE]
   > 若要從磁碟進行安裝 (SQL Server 2014 說明)，請選擇 [安裝來源] 下的 [磁碟]，並指定磁碟位置。

   [管理內容] 索引標籤上的 [本機存放區路徑] 會顯示本機電腦上安裝內容的位置。 如果您想要變更位置，請按一下 [移動]，並在 [到] 欄位中輸入不同資料夾路徑，然後按一下 [確定]。
   如果說明安裝在變更本機存放區路徑後失敗，請關閉並重新開啟說明檢視器，並確保新的位置出現在本機存放區路徑中，然後重試安裝。

3. 按一下您想要安裝的每個內容套件 (書籍) 旁邊的 [新增]。
   若要安裝所有 SQL Server 說明內容，請新增 SQL Server 下的全部 13 本書籍。

4. 按一下右下方的 [更新]。
   會使用新增的書籍自動更新左側的說明目錄。

   ![HelpViewer2_ManageContent_AddContent](../sql-server/media/sql-server-help-installation/helpviewer2-managecontent-addcontent.png)

> [!NOTE]
> 並非 SQL Server 目錄中的所有頂端節點標題都完全符合對應可下載說明書籍的名稱。 TOC 標題對應至書籍名稱，如下所示：

| 內容窗格 | SQL Server 書籍 |
|-----|-----|
|Analysis Services 語言參考 | Analysis Services (MDX) 語言參考|
|Data Analysis Expressions (DAX) 參考 | Data Analysis Expressions (DAX) 參考|
|資料採礦延伸模組 (DMX) 參考 | 資料採礦延伸模組 (DMX) 參考|
|適用於 SQL Server 的開發人員指南 | SQL Server 開發人員參考資料|
|下載 SQL Server Management Studio | Transact-SQL|







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


