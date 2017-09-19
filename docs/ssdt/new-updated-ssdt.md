---
title: "已更新 - SSDT for SQL Server 文件 | Microsoft Docs"
description: "顯示最近變更過的文件更新內容，SQL Server Data Tools (SSDT) for Microsoft SQL Server 的程式碼片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.workload: ssdt-sql-server-data-tools
ms.translationtype: HT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 8ae9a49443525524cf7f6ffceba4fb44984c7052
ms.contentlocale: zh-tw
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-data-tools-ssdt"></a>新文章和最近更新的文章：SQL Server Data Tools (SSDT)



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *更新的日期範圍：* &nbsp;**2017-07-18** &nbsp; 到 &nbsp; **2017-09-11**
- *主題區：*&nbsp; **SQL Server Data Tools (SSDT)**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [SQL Server Data Tools - 授權條款](sql-server-data-tools-license-terms-vs2017.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [SQL Server Data Tools (SSDT) 的變更記錄](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-changelog-for-sql-server-data-tools-ssdtchangelog-for-sql-server-data-tools-ssdtmd"></a>1.&nbsp; [SQL Server Data Tools (SSDT) 的變更記錄](changelog-for-sql-server-data-tools-ssdt.md)

*更新日期： 2017-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 23.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 536fe0fe41b023a4186f494a509fa14fcbafccf4 e5bc7b76c1755f5a1af77f6cd63d8e8691dafe7b  (PR=2927  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=71a2cbf181c94c4c1aff877614aadf890b2496e0) -->



**適用於 Visual Studio 2017 (15.3.0 預覽) 的 SSDT**

組建編號︰14.0.16121.0

**新功能**


此預覽為適用於 Visual Studio 2017 的第一個 SSDT 版本。 此版本加入了獨立式網頁安裝體驗，適用於 Visual Studio 2017 15.3 (或更新版本) 的 SQL Server Database、Analysis Services、Reporting Services 與 Integration Services 專案。


**已知問題**

- 安裝程式未當地語系化。
- SSIS 未當地語系化。
- 當 *ExecuteOutofProcess* 設定為 *True* 時，SSIS 執行封裝工作不支援偵錯。 此問題僅適用偵錯。 透過 DTExec.exe 或 SSIS 目錄進行的儲存、部署及執行則不受到影響。
- 如需完整變更清單，請參閱[變更記錄--changelog-for-sql-server-data-tools-ssdt.md)。
- 在 [SSDT Connect 意見反應](https://connect.microsoft.com/SQLServer/Feedback)網站報告問題。
- 包含協力廠商延伸模組的 SSIS 套件無法切換，以將目標設為其他伺服器版本。


**適用於 Visual Studio 2015 的 SSDT 17.2**

組建編號︰14.0.61707.300

**新功能**



**AS 專案：**
- 在 1400 相容性層級表格式模型中，現在可以在進階安全性的 [角色] 對話方塊中設定「物件層級安全性」。
- 在 VS2017 的 SSDT AS 專案中，AS Azure 模型中沒有電子郵件地址之使用者的新 AAD 角色成員選擇。
- SSDT AS 表格式專案中自訂 ADAL 認證快取行為的新 AS Azure [一律提示] 專案屬性。


**修正**


**一般**
- SQL Server 2017 的已更新商標參考。

**AS 專案**
- 認可 DAX 量值變更和其他模型編輯時，對改善體驗所進行的大幅效能修正。
- 修正使用 1400 相容性層級表格式模型之 Analysis Services 專案中的一些 PowerQuery 整合問題。
- 修正 VS2017 的多維專案中可能無法載入設計彙總設計工具的問題。







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



