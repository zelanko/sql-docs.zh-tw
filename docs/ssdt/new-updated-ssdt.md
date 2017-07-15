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
ms.date: 06/30/2017
ms.author: genemi
ms.workload: ssdt-sql-server-data-tools
ms.translationtype: Human Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 5e43cb76dac922b3c43318b2a9f539ab19ec7bfe
ms.contentlocale: zh-tw
ms.lasthandoff: 07/03/2017

---
# 新文章和最近更新的文章：SQL Server Data Tools (SSDT)
<a id="new-and-recently-updated-sql-server-data-tools-ssdt" class="xliff"></a>



幾乎每日 Microsoft 某些現有發行項上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文件網站。 這篇文章會顯示從最近已更新的發行項的摘錄。 可能也會列出新的文章連結。

這篇文章會定期重新執行程式所產生的。 偶爾摘錄會顯示具有完美的格式，或 markdown 從來源文件。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主體：



- *日期範圍的更新：* &nbsp; **2017 年 05 月 17 日** &nbsp; 到 &nbsp; **2017 年 06 月 30 日**
- *主題區：*&nbsp; **SQL Server Data Tools (SSDT)**。




&nbsp;

## 最近建立的新文章
<a id="new-articles-created-recently" class="xliff"></a>

下列連結會跳至最近新增的新文章。


*目前無新文章列出。*



&nbsp;

## 更新的發行項、 只有摘要
<a id="updated-articles-with-excerpts" class="xliff"></a>

此區段會顯示更新從發行項的最近發生大規模的更新所收集的摘錄。

此處顯示的摘錄顯示分隔其適當語意的內容。 此外，有時摘錄分開四周實際文件中的重要的 markdown 語法。 因此，這些摘錄適用於一般指導方針。 摘錄只會讓您知道您的興趣是否值得花時間按一下，瀏覽實際的發行項。

如需這些和其他原因，不要複製程式碼從這些摘錄中，而且不採用確切真為任何文字摘錄。 相反地，請瀏覽實際的發行項。



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### 1.&nbsp; [SQL Server Data Tools (SSDT) 的變更記錄](changelog-for-sql-server-data-tools-ssdt.md)
<a id="1-nbsp-changelog-for-sql-server-data-tools-ssdtchangelog-for-sql-server-data-tools-ssdtmd" class="xliff"></a>

*Updated: 2017-05-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 21.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 cf17883ce0daf75fdf88881171bf4042558b1cf4 536fe0fe41b023a4186f494a509fa14fcbafccf4  (PR=1777  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=5bd0e1d3955d898824d285d28979089e2de6f322) -->



如需新功能和已變更的詳細文章，請瀏覽[SSDT 小組部落格](https://blogs.msdn.microsoft.com/ssdt/)。

**SSDT 17.1**

組建編號： 14.0.61705.170

**新功能**

**AS 專案：**
- 使用者可設定編碼 1400年模型上的 UI 中的資料行上的提示
- 現在是在離線模式中使用非模型相關的 IntelliSense
- 表格式模型總管 現在包含代表整個模型 （1400 compat 層級表格式模型） 可用的具名的 M 運算式的節點
- Azure Active Directory 人員選擇器類似於 Microsoft Azure 入口網站的 IAM 現在可供使用時，表格式模型中的角色成員

**資料庫專案：**
- 更新為 DacFx 17.1

**修正**

- 已修正下列問題的商業智慧設計師群組名稱已顯示在 VS2017 中的 Visual Studio 選項中的不正確
- 已修正的問題產生的報表專案方案的 Code Map 發生當機或做為專案位置
- 已修正一些問題 PowerQuery 整合的 Analysis Services 1400 compat 層級的表格式模型
- 其中指派運算子可能不是單獨的一行定義量值時的工具視窗固定在新的 DAX 編輯器中的問題
- 修正防止表格式的量值顯示重新命名檢視方塊中的量值時，更新的問題
- 已更新的整合式工作區中的 Analysis Services 引擎及修正造成 1200年的表格式專案包含翻譯上失敗的迴歸的表格式物件模型部署到 SQL Server 2016 Analysis Services 伺服器
- 修正效能問題，在新 1400年表格式資料來源非常慢 creation\deletion
- 已修正的問題，在多維度模型的 DSV 圖表無法停止轉譯如果間不同 Dsv 快速檢視變更

**DacFx 17.1**

- 加密記憶體最佳化資料表的其他身分識別資料行的資料行時，已修正的問題
- 未支援 CATALOG_COLLATION 選項的 CREATE DATABASE





&nbsp;

<a name="compactupdatedlist"/>

## Compact 文件最近才更新清單
<a id="compact-list-of-articles-updated-recently" class="xliff"></a>

此壓縮清單所提供的所有更新發行項上一節中所列的連結。

1. [SQL Server Data Tools (SSDT) 的變更記錄](#TitleNum_1)




<a name="sisters2"/>

&nbsp;

## 姊文件
<a id="sister-articles" class="xliff"></a>

本節會在 GitHub 儲存機制中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/**sql-docs-pr**](https://github.com/microsoftdocs/sql-docs-pr/)。

<!--  20170630-1150  -->

#### 具有新文章或最近更新文章的主題區
<a id="subject-areas-which-do-have-new-or-recently-updated-articles" class="xliff"></a>

- [新文章 + 更新文章 (12+2)：**SQL 進階分析**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (1+0)：**Analysis Services for SQL** 文件](../analysis-services/new-updated-analysis-services.md)
- [新文章 + 更新文章 (0+2)：**連接到 SQL** 文件](../connect/new-updated-connect.md)
- [新文章 + 更新文章 (3+0)：**SQL 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新文章 + 更新文章 (1+2)：**Integration Services for SQL** 文件](../integration-services/new-updated-integration-services.md)
- [新文章 + 更新文章 (2+8)：**Linux for SQL** 文件](../linux/new-updated-linux.md)
- [新文章 + 更新文章 (1+0):  **Master Data Services (MDS) for SQL** 文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (5+5)：**SQL 關聯式資料庫**文件](../relational-databases/new-updated-relational-databases.md)
- [新文章 + 更新文章 (2+0)：**Reporting Services for SQL** 文件](../reporting-services/new-updated-reporting-services.md)
- [新文章 + 更新文章 (0+4)：**Microsoft SQL Server** 文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新文章 + 更新文章 (1+0)：**SQL 工具**文件](../tools/new-updated-tools.md)


#### 沒有新文章或最近更新文章的主題區
<a id="subject-areas-which-have-no-new-or-recently-updated-articles" class="xliff"></a>

- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 範例**文件](../sample/new-updated-sample.md)
- [新文章 + 更新文章 (0+0)：**SQL Server 移轉小幫手 (SSMA)** 文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+0)：**Transact-SQL** 文件](../t-sql/new-updated-t-sql.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)


&nbsp;


