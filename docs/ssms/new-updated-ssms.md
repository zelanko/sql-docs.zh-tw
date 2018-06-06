---
title: 已更新 - SSMS for SQL Server 文件 | Microsoft Docs
description: 顯示最近變更過的文件更新內容，SQL Server Management Studio (SSMS) for Microsoft SQL Server 的程式碼片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: ssms
ms.date: 04/28/2018
ms.openlocfilehash: 75c3dafdfea93a1cb16b9101d187c208e6de2796
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34585910"
---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>新文章和最近更新的文章：SQL Server Management Studio (SSMS) for SQL Server



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *更新日期範圍：* &nbsp; **2018-02-03** &nbsp; 至 &nbsp; **2018-04-28**
- *主題區：*&nbsp; **SQL Server Management Studio (SSMS)**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [教學課程：透過使用 SQL Server Management Studio 來連線至及查詢 SQL Server 執行個體](tutorials/connect-query-sql-server.md)
2. [教學課程：在 SQL Server Management Studio 中撰寫物件指令碼](tutorials/scripting-ssms.md)
3. [教學課程：SQL Server Management Studio 元件和設定](tutorials/ssms-configuration.md)
4. [教學課程：使用 SSMS 的其他祕訣與訣竅](tutorials/ssms-tricks.md)
5. [教學課程：使用 SQL Server Management Studio 中的範本](tutorials/templates-ssms.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [SQL Server Management Studio - 變更記錄 (SSMS)](#TitleNum_1)
2. [SQL Server Management Studio (SSMS) 教學課程](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-management-studio---changelog-ssmssql-server-management-studio-changelog-ssmsmd"></a>1.&nbsp; [SQL Server Management Studio - 變更記錄 (SSMS)](sql-server-management-studio-changelog-ssms.md)

*更新日期：2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一個](#TitleNum_2))

<!-- Source markdown line 27.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 eb641ac39386a26a76dc303f5bd55eb3f9f4c78d f560f09b51ea30b255c10f7eb86857c3090881d9  (PR=5676  ,  Filename=sql-server-management-studio-changelog-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



**[SSMS 17.6]**


版本編號：17.6<br>
組建編號：14.0.17230.0<br>
發行日期：2018 年 3 月 20 日

**新功能**


**一般 SSMS**

SQL Database 受控執行個體：

- 針對 [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)新增支援。 Azure SQL Database 受控執行個體 (預覽) 是 Azure SQL Database 的新功能，幾乎達到 100% 的 SQL Server 內部部署相容性、解決常見安全性問題的原生[虛擬網路 (VNet)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) 實作、以及有利於內部部署 SQL Server 客戶的[商務模型](https://azure.microsoft.com/pricing/details/sql-database/)。
- 支援常見的管理案例，例如：
   - 建立和改變資料庫。
   - 備份及還原資料庫。
   - 匯入、匯出、擷取及發佈資料層應用程式。
   - 檢視與改變伺服器屬性。
   - 完整的物件總管支援。
   - 撰寫資料庫物件。
   - 支援 SQL 代理程式工作。
   - 連結的伺服器支援。
- 請前往[這裡](https://azure.microsoft.com/blog/migrate-your-databases-to-a-fully-managed-service-with-azure-sql-database-managed-instance/)深入了解受控執行個體。

物件總管：
- 新增設定，以便從物件總管拖曳並置放於查詢視窗時，不強制以名稱周圍的括弧來括住。 (使用者建議 [32911933](https://feedback.azure.com/forums/908035-sql-server/suggestions/32911933) 和 [32671051](https://feedback.azure.com/forums/908035-sql-server/suggestions/32671051)。)

資料分類：
- 一般改善和 Bug 修正。

**Integration Services (IS)**

- 新增支援以部署套件至 [SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)。



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-tutorials-for-sql-server-management-studio-ssmstutorialstutorial-sql-server-management-studiomd"></a>2.&nbsp; [SQL Server Management Studio (SSMS) 教學課程](tutorials/tutorial-sql-server-management-studio.md)

*更新日期：2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_1))

<!-- Source markdown line 49.  ms.author= "mathoma".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b272c75bab04912ebb706098cf6b6a6c80d9e2b8 d453ebc8251fb83ffcb1af58c9a08bb65b3e9fa2  (PR=5676  ,  Filename=tutorial-sql-server-management-studio.md  ,  Dirpath=docs\ssms\tutorials\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



- 教學課程：使用 SSMS 對 SQL Server 進行連線與查詢

    在本教學課程中，您將學習如何連線至您的 SQL Server 執行個體。 您也將學習一些基本的 Transact-SQL (T-SQL) 命令來建立和查詢新的資料庫。

- 教學課程：在 SSMS 中撰寫物件指令碼

    在本教學課程中，您將學習如何在 SSMS 中編寫各種物件的指令碼，包括資料庫和查詢。

- 教學課程：在 SSMS 中使用範本

    在本教學課程中，您將學習如何使用在 SSMS 中預先建立的範本。 範本是鮮為人知的功能，其中存放了各種資料庫系統管理工作的大量 Transact-SQL 程式碼片段。

- 教學課程：SSMS 設定

    在本教學課程中，您將學習設定 SSMS 環境的基礎，例如變更環境配置。 本教學課程也會說明各種不同的 SSMS 元件。


- 教學課程：使用 SSMS 的其他祕訣與訣竅

    在本教學課程中，您將學習使用 SSMS 的其他秘訣與訣竅。 本教學課程包含下列項目：
    - 註解、取消註解文字
    - 縮排文字
    - 在物件總管中篩選物件
    - 存取您的 SQL Server 錯誤記錄檔
    - 尋找您的執行個體名稱








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

