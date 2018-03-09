---
title: "已更新 - Integration Services for SQL Server 文件 | Microsoft Docs"
description: "針對 Integration Services for Microsoft SQL Server，顯示文件最新變更之已更新內容的程式碼片段。"
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: ssis
ms.date: 02/03/2018
ms.openlocfilehash: 8bfcdc3fb1033620d351ecaee2c79910c475dd94
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-integration-services-for-sql-server"></a>新增和最近更新：Integration Services for SQL Server



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- 更新日期範圍：&nbsp;**2017 年 12 月 3 日**&nbsp;-至-&nbsp;**2018 年 2 月 3 日**
- *主旨區域：*&nbsp;**Integration Services for SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [瀏覽所有主體對話方塊](catalog/browse-all-principals-dialog-box.md)
2. [設定對話方塊](catalog/configure-dialog-box.md)
3. [資料夾屬性對話方塊](catalog/folder-properties-dialog-box.md)
4. [Integration Services (SSIS) 目錄 Transact-SQL 參考](catalog/integration-services-ssis-catalog-transact-sql-reference.md)
5. [Integration Services (SSIS) 伺服器與目錄](catalog/integration-services-ssis-server-and-catalog.md)
6. [套件屬性對話方塊](catalog/package-properties-dialog-box.md)
7. [專案屬性對話方塊](catalog/project-properties-dialog-box.md)
8. [專案版本對話方塊](catalog/project-versions-dialog-box.md)
9. [設定參數值對話方塊](catalog/set-parameter-value-dialog-box.md)
10. [SSIS 目錄](catalog/ssis-catalog.md)
11. [驗證對話方塊](catalog/validate-dialog-box.md)
12. [檢視 Integration Services 伺服器上的套件清單](catalog/view-the-list-of-packages-on-the-integration-services-server.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [排程 Azure 上的 SSIS 套件執行](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-schedule-the-execution-of-an-ssis-package-on-azurelift-shiftssis-azure-schedule-packagesmd"></a>1.&nbsp; [排程 Azure 上的 SSIS 套件執行](lift-shift/ssis-azure-schedule-packages.md)

更新日期：2018 年 1 月 18 日 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 28.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 be778f8096559da9b84670382deb11f56c129971 640dd3cb59a88ccbc4cf6eab363a45e284f6b873  (PR=4662  ,  Filename=ssis-azure-schedule-packages.md  ,  Dirpath=docs\integration-services\lift-shift\  ,  MergeCommitSha40=6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f) -->



您必須先將 SQL Database 伺服器新增至內部部署 SQL Server 作為連結的伺服器，才能在內部部署環境中使用 SQL Server Agent 來排程執行 Azure SQL Database 伺服器上所儲存的套件。

1.  **設定連結的伺服器**

    ```
    -- Add the SSISDB database on your Azure SQL Database as a linked server to your SQL Server on premises
    EXEC sp_addlinkedserver
        @server='myLinkedServer', -- Name your linked server
        @srvproduct='',
        @provider='sqlncli', -- Use SQL Server native client
        @datasrc='<server_name>.database.windows.net', -- Add your Azure SQL Database server endpoint
        @location='',
        @provstr='',
        @catalog='SSISDB'  -- Add SSISDB as the initial catalog
    ```

2.  **設定連結的伺服器認證**

    ```
    -- Add your Azure SQL DB server admin credentials
    EXEC sp_addlinkedsrvlogin
        @rmtsrvname = 'myLinkedServer',
        @useself = 'false',
        @rmtuser = 'myUsername', -- Add your server admin username
        @rmtpassword = 'myPassword' -- Add your server admin password
    ```

3.  **設定連結的伺服器選項**

    ```
    EXEC sp_serveroption 'myLinkedServer', 'rpc out', true;
    ```

如需詳細資訊，請參閱[建立連結的伺服器](lift-shift/../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)和[連結的伺服器](lift-shift/../../relational-databases/linked-servers/linked-servers-database-engine.md)。







## <a name="similar-articles-about-new-or-updated-articles"></a>新文章或更新文章的類似文章

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區


- [新文章 + 更新文章 (1+3)：&nbsp;**Advanced Analytics for SQL** 文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (0+1)：&nbsp;**Analytics Platform System for SQL** 文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新文章 + 更新文章 (0+1)：&nbsp;**連線到 SQL** 文件](../connect/new-updated-connect.md)
- [新文章 + 更新文章 (0+1)：&nbsp;**Database Engine for SQL** 文件](../database-engine/new-updated-database-engine.md)
- [新文章 + 更新文章 (12+1)：**Integration Services for SQL** 文件](../integration-services/new-updated-integration-services.md)
- [新文章 + 更新文章 (6+2)：&nbsp; **Linux for SQL** 文件](../linux/new-updated-linux.md)
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
- [新文章 + 更新文章 (0+0)：**SQL 範例**文件](../sample/new-updated-sample.md)
- [新文章 + 更新文章 (0+0)：**SQL Server 移轉小幫手 (SSMA)** 文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+0)：**SQL 的工具** 文件](../tools/new-updated-tools.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)


