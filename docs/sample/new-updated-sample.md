---
title: "SQL Server 文件已更新-範例 |Microsoft 文件"
description: "顯示更新的內容，如需 Microsoft SQL Server 的範例中最近變更過的文件的程式碼片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: 
ms.component: samples
ms.suite: sql
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.author: genemi
ms.workload: sample
ms.openlocfilehash: 363cb5dde93c628317a977082fe8697af890d51c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="new-and-recently-updated-sample-for-sql-server"></a>新增和更新最近： SQL Server 的範例



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *日期範圍的更新：* &nbsp; **2017年-09-28** &nbsp; -到- &nbsp; **2017年-12-02**
- *主旨區域：* &nbsp; **SQL Server 的範例**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


***目前無新文章列出。***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [WideWorldImporters 資料庫目錄](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-wideworldimporters-database-catalogworld-wide-importersdatabase-catalog-oltpmd"></a>1.&nbsp;[WideWorldImporters 資料庫目錄](world-wide-importers/database-catalog-oltp.md)

*更新日期︰ 2017年-11-20* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 136.  ms.author= "barbkess".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c055d0483699f06b8766ac2c999101934c14c55c 6975d5a3d1ade7b0ce34bd165bc0e9ef49299ba2  (PR=4032  ,  Filename=database-catalog-oltp.md  ,  Dirpath=docs\sample\world-wide-importers\  ,  MergeCommitSha40=7f8aebc72e7d0c8cff3990865c9f1316996a67d5) -->



可能的情況下，資料庫會 collocates 通常到相同的結構描述，以減少複雜度聯結在一起查詢的資料表。

資料庫結構描述已經過程式碼產生的一系列的另一個資料庫 WWI_Preparation 中的中繼資料資料表為基礎。 這可讓 WideWorldImporters 非常高的設計一致性、 命名的一致性和完整性。 如需方式會產生結構描述的詳細資訊，請參閱原始程式碼：[寬-world-匯入工具/生平-資料庫-指令碼](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

**資料表設計**


- 所有資料表都有單一資料行主索引鍵聯結為了簡單起見。
- 所有結構描述、 資料表、 資料行、 索引和檢查條件約束具有擴充屬性可以用來識別物件或資料行的用途的描述。 記憶體最佳化資料表是這個例外狀況，因為它們目前不支援擴充的屬性。
- 除非具有相同的左側元件另一個非叢集的索引，否則，所有外部索引鍵會自動索引。
- 自動編號資料表中，根據序列。 這些順序會更輕鬆地使用適用於所有連結的伺服器和以上的身分識別資料行相似的環境。 記憶體最佳化資料表使用 IDENTITY 資料行，因為它們不支援 SQL Server 2016 中。
- 單一序列 (TransactionID) 用於這些資料表： CustomerTransactions、 SupplierTransactions 和 StockItemTransactions。 這會顯示一組資料表可以有單一序列的方式。
- 某些資料行擁有適當的預設值。

**安全性結構描述**


為了安全性，WideWorldImporters 不允許直接存取資料的結構描述的外部應用程式。 若要隔離存取，WideWorldImporters 會使用安全性存取結構描述不保留資料，但包含檢視和預存程序。 外部應用程式會使用安全性結構描述擷取可檢視的資料。  如此一來，使用者只可執行的檢視和預存程序中的安全存取結構描述







## <a name="similar-articles"></a>類似的文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新 + 更新 (3 + 14): **Advanced Analytics sql**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (1+0)：**Analysis Services for SQL** 文件](../analysis-services/new-updated-analysis-services.md)
- [新 + 更新 (87 + 0): **Analytics Platform System sql**文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新 + 更新 (5 + 4):**連接到 SQL**文件](../connect/new-updated-connect.md)
- [新 + 更新 (0 + 1): **sql 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (2 + 2): **sql Integration Services**文件](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (10 + 9): **sql Linux**文件](../linux/new-updated-linux.md)
- [新 + 更新 (2 + 4):**關聯式資料庫供 SQL**文件](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (4 + 2): **Reporting Services SQL**文件](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (0 + 1):**範例 sql**文件](../sample/new-updated-sample.md)
- [新 + 更新 (21 + 0): **SQL 作業 Studio**文件](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新 + 更新 (5 + 1): **Microsoft SQL Server**文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (1 + 0): **SQL Server 移轉小幫手 (SSMA)**文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新 + 更新 (0 + 2): **TRANSACT-SQL**文件](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新 + 更新 (0 + 0):**資料移轉小幫手 (DMA) sql**文件](../dma/new-updated-dma.md)
- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 的工具** 文件](../tools/new-updated-tools.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)


