---
title: "已更新 - Reporting Services for SQL Server 文件 | Microsoft Docs"
description: "針對 Reporting Services for Microsoft SQL Server，顯示文件最新變更之已更新內容的程式碼片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: 
ms.component: reporting-services
ms.suite: pro-bi
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: 
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.author: genemi
ms.workload: reporting-services
ms.openlocfilehash: fc35b1dc39ded10eaf20f503fb561562ce55da98
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="new-and-recently-updated-reporting-services-for-sql-server"></a>新增和最近更新：Reporting Services for SQL Server



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *更新的日期範圍：* &nbsp; **2017-09-28** &nbsp; 到 &nbsp; **2017-12-02**
- *主旨區域：* &nbsp; **Reporting Services for SQL Server**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [SQL Server Reporting Services 的變更記錄檔](change-log-sql-server-reporting-services.md)
2. [使用 Reporting Services 的 REST API 進行開發](developer/rest-api.md)
3. [SharePoint 網站上的報表檢視器 Web 組件](report-server-sharepoint/report-viewer-web-part-sharepoint-site.md)
4. [報表檢視器網頁組件的 SharePoint 網站設定](report-server-sharepoint/report-viewer-web-part-sharepoint-site-settings.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [安裝 SQL Server Reporting Services](#TitleNum_1)
2. [將 SQL Server Reporting Services 報表檢視器網頁組件部署至 SharePoint 頁面](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-install-sql-server-reporting-servicesinstall-windowsinstall-reporting-servicesmd"></a>1.&nbsp;[安裝 SQL Server Reporting Services](install-windows/install-reporting-services.md)

*更新日期：2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一個](#TitleNum_2))

<!-- Source markdown line 66.  ms.author= "asaxton".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c959622d4d10a71ed598256e8e284130eb49af5b 77dc1b4f6696e911ed036fc27724ff8a96b79f57  (PR=4150  ,  Filename=install-reporting-services.md  ,  Dirpath=docs\reporting-services\install-windows\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    > The default path is C:\Program Files\Microsoft SQL Server Reporting Services.

7. 成功安裝之後，選取 [設定報表伺服器] 啟動 Reporting Services 設定管理員。

    ![設定報表伺服器--media/install-reporting-services/report-server-install-configure.png)

**設定報表伺服器**


在安裝程式中選取 [設定報表伺服器] 後，您會看到**報表伺服器設定管理員**。 如需詳細資訊，請參閱[報表伺服器設定管理員--reporting-services-configuration-manager-native-mode.md)。

您需要[建立報表伺服器資料庫--ssrs-report-server-create-a-report-server-database.md)以完成 Reporting Services 的初始設定。 SQL Server Database 伺服器需要完成此步驟。

**在其他伺服器上建立資料庫**


如果您要在其他電腦的資料庫伺服器上建立報表伺服器資料庫，您需要將報表伺服器的服務帳戶變更成資料庫伺服器可辨識的認證。

報表伺服器預設使用虛擬服務帳戶。 如果嘗試在其他伺服器上建立資料庫，您可能會在「套用連線權限」步驟收到下列錯誤。

`System.Data.SqlClient.SqlException (0x80131904): Windows NT user or group '(null)' not found. Check the name again.`

若要解決錯誤，您可以將服務帳戶變更成網路服務或網域帳戶。 將服務帳戶變更為網路服務，會套用報表伺服器電腦帳戶內容中的權限。

如需詳細資訊，請參閱[設定報表伺服器服務帳戶--configure-the-report-server-service-account-ssrs-configuration-manager.md)。

**Windows 服務**


安裝時會建立 Windows 服務。 它會顯示為 **SQL Server Reporting Services**。 服務名稱是 **SQLServerReportingServices**。



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-deploy-the-sql-server-reporting-services-report-viewer-web-part-on-a-sharepoint-sitereport-server-sharepointdeploy-report-viewer-web-partmd"></a>2.&nbsp;[將 SQL Server Reporting Services 報表檢視器網頁組件部署至 SharePoint 頁面](report-server-sharepoint/deploy-report-viewer-web-part.md)

*更新日期：2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_1))

<!-- Source markdown line 129.  ms.author= "asaxton".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 99275aa597f491bb09688060b3f713406e2f0624 a282486da6df55154212c98fa06c7e62e66c8350  (PR=4150  ,  Filename=deploy-report-viewer-web-part.md  ,  Dirpath=docs\reporting-services\report-server-sharepoint\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



您可嘗試使用 PowerShell 刪除網頁組件，但此做法沒有直接命令。 如需指令碼範例，請參閱 [How to delete web parts from the web part Gallery](https://gallery.technet.microsoft.com/office/How-to-delete-Web-Parts-1132701f) (如何刪除網頁組件庫的網頁組件)。

**支援的語言**


網頁組件支援下列語言：

* 英文 (en)
* 德文 (de)
* 西班牙文 (sp)
* 法文 (fr)
* 義大利文 (it)
* 日文 (ja)
* 韓文 (ko)
* 葡萄牙文 (pt)
* 俄文 (ru)
* 中文 (簡體 - zh-HANS 與 zh-CHS)







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


