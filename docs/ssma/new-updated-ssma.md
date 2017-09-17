---
title: "已更新-SSMA for SQL Server 文件 |Microsoft 文件"
description: "顯示程式碼片段的最近變更過的文件的 SQL Server 移轉小幫手 (SSMA) 的 Microsoft SQL Server 的更新內容。"
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
ms.workload: ssma-sql-server-migration-assistant
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 68df82bc7da6d7ef5aed3522c06704fb92bb0982
ms.contentlocale: zh-tw
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-migration-assistant-ssma"></a>新增和更新最近： SQL Server 移轉小幫手 (SSMA)



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *日期範圍的更新：* &nbsp; **2017年-07-18** &nbsp; -到- &nbsp; **2017年-09-11**
- *主旨區域：* &nbsp; **SQL Server 移轉小幫手**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結跳至最近新增的新發行項。


***目前無新文章列出。***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

此區段會顯示更新所收集從最近曾發生大規模的更新發行項的摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單所提供的摘錄的一節中所列的所有更新文章連結。

1. [什麼 &#39; s SSMA for DB2 中的新 (DB2ToSQL)](#TitleNum_1)
2. [SQL Server 移轉小幫手](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-what39s-new-in-ssma-for-db2-db2tosqldb2what-s-new-in-ssma-for-db2-db2tosqlmd"></a>1.&nbsp;[什麼 &#39; s SSMA for DB2 中的新 (DB2ToSQL)](db2/what-s-new-in-ssma-for-db2-db2tosql.md)

*更新日期︰ 2017年-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 24.  ms.author= "Shamikg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c5dfb378ac578f54935a8a1fa7194398f3631017 f4427d1857894ad348cef5c92fbf6b51d00ee652  (PR=3070  ,  Filename=what-s-new-in-ssma-for-db2-db2tosql.md  ,  Dirpath=docs\ssma\db2\  ,  MergeCommitSha40=0b832a9306244210e693bde7c476269455e9b6d8) -->



**SSMA v7.4**

V7.4 版的 SSMA for DB2 會包含下列變更：
- **查詢逾時**選項現在時仍可使用在來源和目標結構描述物件探索。
![查詢逾時選項...-/media/query-timeout_red.png)

- 品質和轉換的度量，而改善了目標的修正程式，根據客戶的意見反應。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA v7.4 的必要條件。 此外，開頭 v7.4，32 位元版本的 SSMA 會停止。

**SSMA v7.3**

V7.3 版的 SSMA for DB2 會包含下列變更：
- 改善的品質和轉換的度量根據客戶的意見反應目標的修正程式。
- 透過下列項目公開 SSMA 擴充性架構：
  - 匯出至 SQL Server Data Tools (SSDT) 專案的功能。
    -   您現在可以在 SSDT 專案，從 SSMA 匯出結構描述指令碼。 您可以使用結構描述指令碼來進行額外的結構描述變更及部署您的資料庫。
![另存 SSDT 專案命令../media/export-schema-scripts_red.png)
  - 可供 SSMA 執行自訂轉換執行的程式庫。
    - 您現在可以建構自訂語法轉換和 SSMA 先前未處理的轉換可以處理的程式碼。
      - 這個部落格文章，指示如何建構自訂轉換子可用[擴充 SQL Server 移轉小幫手的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      - 轉換的範例專案可以是下載此[部落格文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)。

**SSMA v7.2**

V7.2 版的 SSMA for DB2 會包含下列變更：
- 改善的品質和轉換的度量根據客戶的意見反應目標的修正程式。
- 遙測增強功能提供更好的資料點，來解決客戶問題，並改善 SSMA 的轉換比率。



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-server-migration-assistantsql-server-migration-assistantmd"></a>2.&nbsp;[SQL Server 移轉小幫手](sql-server-migration-assistant.md)

*更新日期︰ 2017年-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_1))

<!-- Source markdown line 36.  ms.author= "Shamikg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 340d718e85fa73c6722862a0a7ba90239b247389 b29f4be2b6d208fd6038c2f9e1c7f0b7bd6b9ed7  (PR=3070  ,  Filename=sql-server-migration-assistant.md  ,  Dirpath=docs\ssma\  ,  MergeCommitSha40=0b832a9306244210e693bde7c476269455e9b6d8) -->



**支援的來源和目標版本**

對於支援的來源，請檢閱 SSMA 下載下載中心上的資訊。

SSMA 支援下列版本的目標。

- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- Azure SQL Database
- 在 Windows 和 Linux （預覽） 上的 SQL Server 2017
- * * Azure SQL 資料倉儲

* * SSMA for Oracle 只有才支援此目標。









## <a name="similar-articles"></a>類似的文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

此區段會列出最近已更新的發行項，在我們的公用 GitHub.com 儲存機制中的其他主體區域中的非常類似文件： [MicrosoftDocs/sql 的文件](https://github.com/MicrosoftDocs/sql-docs/)。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新 + 更新 (3 + 12): **Advanced Analytics sql**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新 + 更新 (5 + 0):**連接到 SQL**文件](../connect/new-updated-connect.md)
- [新 + 更新 (5 + 1): **sql 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (19 + 82): **sql Integration Services**文件](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (1 + 8): **sql Linux**文件](../linux/new-updated-linux.md)
- [新 + 更新 (12 + 1):**關聯式資料庫供 SQL**文件](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (0 + 1): **Reporting Services SQL**文件](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (7 + 1): **Microsoft SQL Server**文件](../sql-server/new-updated-sql-server.md)
- [新 + 更新 (1 + 1): **SQL Server Data Tools (SSDT)**文件](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (0 + 2): **SQL Server 移轉小幫手 (SSMA)**文件](../ssma/new-updated-ssma.md)
- [新 + 更新 (1 + 4): **SQL Server Management Studio (SSMS)**文件](../ssms/new-updated-ssms.md)
- [新 + 更新 (4 + 1): **TRANSACT-SQL**文件](../t-sql/new-updated-t-sql.md)
- [新 + 更新 (0 + 1): **Tools for SQL**文件](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新 + 更新 (0 + 0): **sql Analysis Services**文件](../analysis-services/new-updated-analysis-services.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新 + 更新 (0 + 0): **Master Data Services (MDS) sql**文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 範例**文件](../sample/new-updated-sample.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)



