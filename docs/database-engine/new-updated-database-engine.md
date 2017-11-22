---
title: "已更新 - 資料庫引擎文件 | Microsoft Docs"
description: "顯示最近變更過的文件更新內容，資料庫引擎的程式碼片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: barbkess
ms.service: 
ms.component: database-engine
ms.suite: sql
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: 
ms.workload: database-engine
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.author: genemi
ms.openlocfilehash: a367634760aba2b3293df230a427f10bc49feffa
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="new-and-recently-updated-database-engine-docs"></a>新的與最近的更新：資料庫引擎文件
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]


Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *更新的日期範圍：* &nbsp; **2017-09-11** &nbsp; 到 &nbsp; **2017-09-27**
- *主旨區域：* &nbsp; **資料庫引擎**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [將功能新增至 SQL Server 的執行個體 (安裝)](install-windows/add-features-to-an-instance-of-sql-server-setup.md)
2. [從命令提示字元安裝 SQL Server](install-windows/install-sql-server-from-the-command-prompt.md)
3. [使用設定檔安裝 SQL Server](install-windows/install-sql-server-using-a-configuration-file.md)
4. [商務持續性與資料庫復原 - SQL Server](sql-server-business-continuity-dr.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [從命令提示字元安裝更新](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-installing-updates-from-the-command-promptinstall-windowsinstalling-updates-from-the-command-promptmd"></a>1.&nbsp; [從命令提示字元安裝更新](install-windows/installing-updates-from-the-command-prompt.md)

*更新於：2017-09-12* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 48.  ms.author= "mikeray".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 04abb23d0682c23654a55e7926d2140f0b6ae408 a4bb1e27ae99460a66da72848ace1417b148f85c  (PR=3122  ,  Filename=installing-updates-from-the-command-prompt.md  ,  Dirpath=docs\database-engine\install-windows\  ,  MergeCommitSha40=1df54edd5857ac2816fa4b164d268835d9713638) -->



- 更新電腦上所有的 ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] 執行個體及所有共用的元件，例如 ..!NCLUDE-NotShown--ssISnoversion--../../includes/ssisnoversion-md.md)] 和管理工具：

```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances.
```

- 移除 ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] 單一執行個體的更新及所有共用的元件，例如 ..!NCLUDE-NotShown--ssISnoversion--../../includes/ssisnoversion-md.md)] 和管理工具：

```
    <package_name>.exe /qs /Action=RemovePatch /InstanceName=MyInstance.
```

- 只移除 ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] 共用元件的更新，例如 ..!NCLUDE-NotShown--ssISnoversion--../../includes/ssisnoversion-md.md)] 和管理工具：

```
    <package_name>.exe /qs /Action=RemovePatch
```







## <a name="similar-articles"></a>類似的文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (0+1)：**SQL 的進階分析**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (0+1)：**SQL 的 Analysis Services** 文件](../analysis-services/new-updated-analysis-services.md)
- [新文章 + 更新文章 (4+1)：**SQL 的資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新文章 + 更新文章 (17+0)：**SQL 的 Integration Services** 文件](../integration-services/new-updated-integration-services.md)
- [新文章 + 更新文章 (3+0)：**SQL 適用的 Linux** 文件](../linux/new-updated-linux.md)
- [新文章 + 更新文章 (1+1)：**SQL 的關聯式資料庫**文件](../relational-databases/new-updated-relational-databases.md)
- [新文章 + 更新文章 (2+0)：**SQL 的 Reporting Services** 文件](../reporting-services/new-updated-reporting-services.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新文章 + 更新文章 (0+1)：**Transact-SQL** 文件](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**連線到 SQL** 文件](../connect/new-updated-connect.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 範例**文件](../sample/new-updated-sample.md)
- [新文章 + 更新文章 (0+0)：**Microsoft SQL Server** 文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (0+0)：**SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新文章 + 更新文章 (0+0)：**SQL Server 移轉小幫手 (SSMA)** 文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+0)：**SQL 的工具** 文件](../tools/new-updated-tools.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)


