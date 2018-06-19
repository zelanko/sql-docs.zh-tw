---
title: 已更新 - Integration Services for SQL Server 文件 | Microsoft Docs
description: 針對 Integration Services for Microsoft SQL Server，顯示文件最新變更之已更新內容的程式碼片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.date: 04/28/2018
ms.openlocfilehash: 865a5c79c3726b36faed32d24c07c37ea4837ba2
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35406180"
---
# <a name="new-and-recently-updated-integration-services-for-sql-server"></a>新增和最近更新：Integration Services for SQL Server



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *更新日期範圍：* &nbsp; **2018-02-03** &nbsp; 至 &nbsp; **2018-04-28**
- *主旨區域：*&nbsp;**Integration Services for SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [使用 SQL Server Integration Services (SSIS) 將資料從 Excel 載入或載入至 Excel](load-data-to-from-excel-with-ssis.md)
2. [使用 SQL Server Integration Services (SSIS) 將資料從 SQL Server 載入 Azure SQL 資料倉儲](load-data-to-sql-data-warehouse.md)
3. [Scale Out 透過 SQL Server 容錯移轉叢集執行個體支援高可用性](scale-out/scale-out-failover-cluster-instance.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [安裝 Integration Services](#TitleNum_1)
2. [部署、執行和監視 Azure 上的 SSIS 套件](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-install-integration-servicesinstall-windowsinstall-integration-servicesmd"></a>1.&nbsp; [安裝 Integration Services](install-windows/install-integration-services.md)

*更新日期：2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一個](#TitleNum_2))

<!-- Source markdown line 75.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 49551f3b1138f805e6d5e0f6099a100e2f3b3e7a 97caaafc1587b2326f4c357dd5eb21f2de7d358f  (PR=5676  ,  Filename=install-integration-services.md  ,  Dirpath=docs\integration-services\install-windows\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



**Integration Services 的完整安裝**


如需 *{Included-Content-Goes-Here}* 的完整安裝，請從下列清單中選取您需要的元件：

-   **Integration Services (SSIS)**： 使用 [SQL Server 安裝精靈] 來安裝 SSIS。 選取 SSIS 時，會安裝下列項目：
    -   SQL Server 資料庫引擎上的 SSIS 目錄支援。
    -   (選擇性) SSIS Scale Out 功能，其中包含一個 Master 與若干 Worker。
    -   32 位元和 64 位元 SSIS 元件。
    -   安裝 SSIS 時，**不會**安裝設計和開發 SSIS 套件所需的工具。
-   **SQL Server 資料庫引擎**： 使用 [SQL Server 安裝精靈] 安裝資料庫引擎。 選取資料庫引擎時，可讓您建立並裝載 SSIS 目錄資料庫 (`SSISDB`)，以儲存、管理、執行及監視 SSIS 套件。
-   **SQL Server Data Tools (SSDT)**。 若要下載並安裝 SSDT，請參閱[下載 SQL Server Data Tools (SSDT)]。 安裝 SSDT 時，可讓您設計和部署 SSIS 套件。 SSDT 會安裝下列項目：
    -   SSIS 套件的設計和開發工具，包括 SSIS 設計工具。
    -   僅 32 位元 SSIS 元件。
    -   Visual Studio 的限制版本 (如果尚未安裝 Visual Studio 的話)。
    -   Visual Studio Tools for Applications (VSTA)，其為用於 SSIS 指令碼工作和指令碼元件的指令碼編輯器。
    -   SSIS 精靈，包括 [部署精靈] 和 [套件升級精靈]。
    -   SQL Server 匯入和匯出精靈。
-   **Integration Services Feature Pack for Azure**： 若要下載並安裝 Feature Pack，請參閱 [Microsoft SQL Server 2017 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=54798)。 安裝 Feature Pack 時，可讓您的套件連線到 Azure 雲端中的儲存體和分析服務，包括下列服務：



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-deploy-run-and-monitor-an-ssis-package-on-azurelift-shiftssis-azure-deploy-run-monitor-tutorialmd"></a>2.&nbsp; [部署、執行和監視 Azure 上的 SSIS 套件](lift-shift/ssis-azure-deploy-run-monitor-tutorial.md)

*更新日期：2018-04-25* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_1))

<!-- Source markdown line 99.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 07f2b752818f2e786c4380fb822099190c59f302 54de9497353bac2d6a8a87e546fc6ab9e444a734  (PR=5676  ,  Filename=ssis-azure-deploy-run-monitor-tutorial.md  ,  Dirpath=docs\integration-services\lift-shift\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



**使用 PowerShell 部署專案**


若要使用 PowerShell 將專案部署到 Azure SQL Database 上的 SSISDB，請根據您的需求調整下列指令碼。 指令碼會列舉 `$ProjectFilePath` 下的子資料夾及各個子資料夾中的專案，然後在 SSISDB 中建立相同資料夾，並將專案部署到這些資料夾。

此指令碼要求在您執行指令碼的電腦上，安裝 SQL Server Data Tools 17.x 版或 SQL Server Management Studio。

```
**Variables**

$ProjectFilePath = "C:\<folder>"
$SSISDBServerEndpoint = "<servername>.database.windows.net"
$SSISDBServerAdminUserName = "<username>"
$SSISDBServerAdminPassword = "<password>"

**Load the IntegrationServices Assembly**

[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices") | Out-Null;

**Store the IntegrationServices Assembly namespace to avoid typing it every time**

$ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"

Write-Host "Connecting to server ..."

**Create a connection to the server**

$sqlConnectionString = "Data Source=" + $SSISDBServerEndpoint + ";User ID="+ $SSISDBServerAdminUserName +";Password="+ $SSISDBServerAdminPassword + ";Initial Catalog=SSISDB"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

**Create the Integration Services object**

$integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection

**Get the catalog**

$catalog = $integrationServices.Catalogs['SSISDB']

write-host "Enumerating all folders..."

$folders = ls -Path $ProjectFilePath -Directory

if ($folders.Count -gt 0)
{
    foreach ($filefolder in $folders)
    {
        Write-Host "Creating Folder " $filefolder.Name " ..."

        # Create a new folder
        $folder = New-Object $ISNamespace".CatalogFolder" ($catalog, $filefolder.Name, "Folder description")
```







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

