---
title: "已更新-SQL Server 文件 |Microsoft 文件"
description: "顯示更新的內容，如需 SQL Server 中最近變更過的文件的程式碼片段。"
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
ms.date: 05/23/2017
ms.author: genemi
ms.translationtype: Human Translation
ms.sourcegitcommit: 96f6a7eeb03fdc222d0e5b42bcfbf05c25d11db6
ms.openlocfilehash: 7fba3b05943b93c0a2c0e76c2d0d5f2696a48d1c
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="new-and-recently-updated-sql-server-docs"></a>新的與最近的更新： SQL Server 文件



幾乎每日 Microsoft 某些現有發行項上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文件網站。 這篇文章會顯示從最近已更新的發行項的摘錄。 可能也會列出新的文章連結。

這篇文章會定期重新執行程式所產生的。 偶爾摘錄會顯示具有完美的格式，或 markdown 從來源文件。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主體：



- *日期範圍的更新：* &nbsp; **2017年-05-01** &nbsp; -到- &nbsp; **2017年-05-23**
- *主旨區域：* &nbsp; **SQL Server**。




&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新的發行項、 只有摘要

此區段會顯示更新從發行項的最近發生大規模的更新所收集的摘錄。

此處顯示的摘錄顯示分隔其適當語意的內容。 此外，有時摘錄分開四周實際文件中的重要的 markdown 語法。 因此，這些摘錄適用於一般指導方針。 摘錄只會讓您知道您的興趣是否值得花時間按一下，瀏覽實際的發行項。

如需這些和其他原因，不要複製程式碼從這些摘錄中，而且不採用確切真為任何文字摘錄。 相反地，請瀏覽實際的發行項。



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-2017-release-notessql-server-2017-release-notesmd"></a>1.&nbsp;[SQL Server 2017 版本資訊](sql-server-2017-release-notes.md)

*Updated: 2017-05-17* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 28.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 84e7a2a49f2893d49380db1ad75695d9a4fd59b2 27a145ad30c10fd667f926d2e092b88c0ba586c5 -->



**SQL Server 2017 CTP 2.1 (可能 2017)**

**文件 (CTP 2.1)**

- **問題和客戶的影響：**文件 [！包含 [ssSQLv14_md..有限 /includes/sssqlv14-md.md)]，內容會包含 [！包含 [ssSQL15_md../includes/sssql15-md.md)] 文件集。  中的特定發行項的內容 [！包含 [ssSQLv14_md../includes/sssqlv14-md.md)]，將會利用註明**套用至**。 
- **問題和客戶的影響：**沒有離線內容適用於 [！包含 [ssSQLv14_md../includes/sssqlv14-md.md)]。

**SQL Server Reporting Services (CTP 2.1)**


- **問題和客戶的影響：**如果您有 SQL Server Reporting Services 和 Power BI 報表伺服器在相同電腦，並解除安裝其中一個，您將不再能夠連線到其餘的報表伺服器與報表伺服器組態管理員。
- **因應措施**若要解決此問題，您必須執行下列作業之後解除安裝其中一個伺服器。

    1. 啟動命令提示字元，以系統管理員模式。
    2. 前往剩餘的報表伺服器安裝所在目錄。

        *Power BI 報表伺服器的預設位置： C:\Program Files\Microsoft Power BI 報表伺服器*

        *SQL Server Reporting Services 的預設位置： C:\Program Files\Microsoft SQL Server 報告的服務*

    3. 接著移至下一個資料夾。 這會是*SSRS*或*PBIRS*根據剩餘的項目。
    4. 移至 WMI 資料夾。
    5. 執行下列命令：

        ```
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        您可以忽略下列錯誤，如果您看到它。

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

**TSqlLanguageService.msi (CTP 2.1)**


- **問題和客戶的影響：** 2016年的版本的電腦上安裝之後*TSqlLanguageService.msi* （透過 SQL 安裝程式或安裝為獨立可轉散發套件） v13.* (SQL 2016) 的版本*Microsoft.SqlServer.Management.SqlParser.dll*和*Microsoft.SqlServer.Management.SystemMetadataProvider.dll*會移除。 任何有相依的這些組件的 2016年版本的應用程式將會再停止運作，提供類似的錯誤：*錯誤： 無法載入檔案或組件 ' Microsoft.SqlServer.Management.SqlParser，Version = 13.0.0.0，Culture = neutral，PublicKeyToken = 89845dcd8080cc91' 或其中一個相依性。系統找不到指定的檔案。*




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-what39s-new-in-sql-server-2017what-s-new-in-sql-server-2017md"></a>2.&nbsp;[什麼 & #39 的新 SQL Server 2017](what-s-new-in-sql-server-2017.md)

*Updated: 2017-05-22* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1))

<!-- Source markdown line 31.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b3e965f62414af06d42f88497958a4bca67befce 82ad09ae9a917f26db3e2210b5cf89585e0e4c4e -->



**新功能 SQL Server 2017 CTP 2.1 (可能 2017)**

* * SQL Server Database Engine * *

- 新的 DMF [sys.dm_db_log_stats../ relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md） 已引入來公開摘要層級的屬性以及有關交易記錄檔。適用於監視交易記錄檔的健全狀況。  
- 此 CTP 中包含錯誤修正和資料庫引擎的效能改進。
- 如需詳細的 2017年清單 CTP 增強功能，在先前的 CTP 版本中，請參閱 [What's New in SQL Server 2017 (Database Engine)../ database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md）。

**SQL Server Reporting Services (SSRS)**

- 無法再供透過 SQL Server 安裝程式 CTP 2.1 為準，安裝 SQL Server Reporting Services。
- 註解現在可供報表。 註解可讓您加入至報表中的檢視方塊，並在您的組織與其他人共同作業。 您也可以包含附件與您的註解。
- 如需更詳細的 SSRS 什麼是新的資訊，包括從舊版本的詳細資訊，請參閱 [最新消息中 Reporting Services../ reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md）。 
- Power BI 報表伺服器的相關資訊，請參閱[開始使用 Power BI 報表伺服器](https://powerbi.microsoft.com/documentation/reportserver-get-started/)。

**SQL Server 機器學習服務**

- 在此 CTP 中沒有任何新的機器學習服務功能。
- 何謂更詳細的機器學習服務新的資訊，包括從先前的 Ctp 的詳細資訊，請參閱 [What's New 在 SQL Server 機器學習服務../ advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md）。  

**SQL Server Analysis Services (SSAS)**

- 此 CTP 中沒有任何 SSAS 新功能。  
- 如需有關改善和 bug 修正，在此版本的詳細資訊，請參閱 [What's New 在 SQL Server 2017 Analysis Services../ analysis-services/what-s-new-in-sql-server-analysis-services-2017.md）。  





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Compact 文件最近才更新清單

此壓縮清單所提供的所有更新發行項上一節中所列的連結。

1. [SQL Server 2017 版本資訊](#TitleNum_1)
2. [什麼 & #39 的新 SQL Server 2017](#TitleNum_2)


<a name="sisters2"/>

&nbsp;

## <a name="sister-articles"></a>姊文件

此區段會列出最近已更新的發行項相同的 GitHub 儲存機制中的其他主體區域中的相似的文件。


&nbsp;

[Microsoft /**sql-文件-pr** ](https://github.com/microsoftdocs/sql-docs-pr/) GitHub.com 上的儲存機制：

- [最近才更新：**關聯式資料庫和 Microsoft SQL Server**文件](/sql/relational-databases/relational-databases-new-updated-sql-docs-pr)
- [最近才更新： **Microsoft SQL Server**文件](/sql/sql-server/sql-server-new-updated-sql-docs-pr)
- [最近才更新： **SQL Server 中的 TRANSACT-SQL**文件](/sql/t-sql/t-sql-new-updated-sql-docs-pr)


&nbsp;

<!--
[Microsoft/**azure-docs**](https://github.com/microsoft/azure-docs/) repository on GitHub.com:

- [Sisters list for **azure-docs** repo](https://docs.microsoft.com/azure/sql-server-new-updated-azure-docs/#sisters2)
-->

&nbsp;



