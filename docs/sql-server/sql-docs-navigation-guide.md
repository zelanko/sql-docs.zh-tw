---
title: SQL Server 文件導覽提示
description: 瀏覽 SQL Server 技術文件的提示與訣竅 - 說明中樞頁面、目錄、標頭等內容，以及如何使用階層連結以及如何使用版本篩選。
ms.date: 08/12/2020
ms.prod: sql
ms.technology: release-landing
ms.reviewer: ''
ms.custom: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || >= sql-server-linux-2017'
ms.openlocfilehash: 98fd46528437cd9a82ec7d47539db230b8be8eb8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97409394"
---
# <a name="sql-server-docs-navigation-guide"></a>SQL Server 文件導覽指南

本主題提供巡覽 SQL Server 技術文件空間的一些提示和技巧。  

## <a name="hub-page"></a>中樞頁面

您可以在 [https://aka.ms/sqldocs](https://aka.ms/sqldocs) 找到 SQL Server 中樞頁面，它是尋找相關 SQL Server 內容的進入點。

您隨時可以選取 SQL Server 技術文件集中每個頁面頂端標頭的 [SQL 文件]  來巡覽回此頁面： 

![標頭中的 SQL 文件](media/sql-server-docs-navigation-guide/sql-docs-in-header.png)

## <a name="offline-documentation"></a>離線文件

如果您想要在離線系統上檢視 SQL Server 文件，您有兩個選項。 您可以在 SQL Server 技術文件中建立 PDF，或使用 [SQL Server 離線說明檢視器](sql-server-help-installation.md)下載離線內容。 

若您想要建立 PDF，請選取每個目錄底部的 [下載 PDF]  連結。


![下載 PDF](media/sql-server-docs-navigation-guide/download-pdf.png)

## <a name="toc-symbols"></a>TOC 符號 

目錄 (TOC) 中其結尾具有 `>` 的項目，表示會帶您前往具有不同目錄的技術文件。 

![TOC 中的單一胡蘿蔔箭號](media/sql-server-docs-navigation-guide/single-carrots-in-sql-docs-toc.png)

TOC 中具有 `>>` 的項目，表示會帶您離開 docs.microsoft.com。 

![TOC 導覽標記](media/sql-server-docs-navigation-guide/double-carrots-in-sql-docs-toc.png)

若您巡覽到這些頁面中的其中之一，您可以選取每個目錄頂端的 [歡迎使用 SQL Server >] 項目來返回主要 SQL Server 技術頁面與目錄。 

![巡覽回 SQL TOC](media/sql-server-docs-navigation-guide/navigate-back-to-sql-toc.png)

## <a name="toc-search"></a>TOC 搜尋 
在 docs.microsoft.com 上，您可以使用頂端的篩選搜尋方塊來在目錄中搜尋內容： 

![使用篩選方塊](media/sql-server-docs-navigation-guide/sql-docs-toc-filter.gif)

## <a name="version-filter"></a>版本篩選
SQL Server 技術文件提供數個 SQL Server 版本及變體的內容。 不同 SQL Server 版本和變體間的功能可能會有所差異，因此內容本身有時候也會有所差異。 

您可以使用[版本篩選](versioning-system-monikers-ui-sql-server.md)來確保您正在查看適當 SQL Server 版本及變體的內容： 

![SQL 文件版本篩選](media/sql-server-docs-navigation-guide/sql-docs-version-filter.gif)

選取 [所有 SQL]  \> [不隱藏任何內容]  可確保您能看見所有內容，且版本篩選沒有隱藏任何項目。 [不隱藏任何內容]  選項可能會顯示相同文章中許多不同版本 SQL Server 的相關內容，這可能會有衝突、不清楚或令人困惑。 [不建議例行性地使用 [不隱藏任何內容]  選項](versioning-system-monikers-ui-sql-server.md#anchor-allsql-hidenothing)。 

## <a name="breadcrumbs"></a>階層連結

您可以在標頭的下方及目錄的上方找到階層連結，該階層連結會指出目前文章在目錄中的位置。  這不僅有助於將內容設為您正在閱讀的內容類型，還可以讓您巡覽回目錄樹狀結構：

![SQL 文件階層連結](media/sql-server-docs-navigation-guide/sql-docs-bread-crumbs.gif)

## <a name="article-section-navigation"></a>文章區段導覽

右側瀏覽窗格可讓您快速巡覽至文章內的區段，以及識別您在文章中的位置。  

![右側導覽](media/sql-server-docs-navigation-guide/sql-docs-right-hand-navigation.gif)


## <a name="submit-docs-feedback"></a>提交文件意見反應

若您在文章中發現錯誤，您可以捲動到頁面底部，選取 [內容意見反應]  來提交該文章的意見反應給 SQL 內容小組。

![Git 問題內容意見反應](media/sql-server-get-help/git-issues.png)

您也可以在 [https://aka.ms/sqldocsfeedback](https://aka.ms/sqldocsfeedback) 提交一般文件意見反應及建議。 

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

![編輯 SQL 文件](media/sql-server-docs-navigation-guide/edit-sql-docs.gif)

## <a name="next-steps"></a>後續步驟

- 開始使用 [SQL Server 技術文件](index.yml)。
- 如需提交意見反應或取得 SQL Server 協助的詳細資訊，請參閱[取得協助](sql-server-get-help.md)頁面。 
- 若要快速存取所有快速入門和教學課程，請參閱[教育性 SQL 資源](../sql-server/educational-sql-resources.yml)。
