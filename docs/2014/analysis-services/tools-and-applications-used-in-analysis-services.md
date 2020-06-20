---
title: Analysis Services 中使用的工具和應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0ddb3b7a-7464-4d04-8659-11cb2e4cf3c3
author: minewiskan
ms.author: owend
ms.openlocfilehash: 13da2ecc244c1596789a1d816bac81a13bcd4c62
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938329"
---
# <a name="tools-and-applications-used-in-analysis-services"></a>Analysis Services 中使用的工具和應用程式
  尋找在 Analysis Services 執行個體上建立 Analysis Services 模型和管理關聯資料庫所需的工具與應用程式。

## <a name="analysis-services-model-designers"></a>Analysis Services 模型設計師
 表格式與多維度模型是從 Visual Studio Shell 內建方案中的專案範本建立的。 專案範本可供設計人員建立組成 Analysis Services 方案的模型、Cube、維度及角色。

### <a name="download-sql-server-data-tools-for-business-intelligence-ssdt-bi"></a>下載 SQL Server Data Tools for Business Intelligence (SSDT-BI)
 之前稱為 Business Intelligence Development Studio (BIDS) 的 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] for Business Intelligence (SSDT-BI) 是用來建立 Analysis Services 模型、Reporting Services 報表和 Integration Services 封裝。 您可以從以下位置下載 SSDT-BI：

-   [下載 SSDT-BI for Visual Studio 2013](https://go.microsoft.com/fwlink/p/?LinkId=396526)

-   [下載 SSDT-BI for Visual Studio 2012](https://go.microsoft.com/fwlink/p/?LinkID=273673)

 如果電腦上已安裝舊版的 SSDT-BI 或 BIDS，較新的版本會與舊版並存安裝。 通常會在單一工作站上執行新版與舊版的設計工具，這樣一來，您就可以修改與特定伺服器版本繫結的專案和方案。

> [!NOTE]
>  Visual Studio 2012 和 Visual Studio 2013 版的 SSDT 有幾個下載網站。 大部分都未包括 BI 專案範本。 使用上述連結會讓您得到正確的版本。 如果您看到 [商業智慧專案範本] 資料夾，您會知道您擁有正確的 SSDT-BI 版本。 此資料夾包含 Analysis Services、Reporting Services 和 Integration Services 適用的專案範本。 依據您安裝 SSDT-BI 的方式，您也可能會看到一個額外的 SQL Server 資料庫專案範本。

 ![SSDT 中的新專案範本](media/ssdt-biprojects.png "SSDT 中的新專案範本")

## <a name="administrative-tools"></a>系統管理工具

### <a name="sql-server-management-studio"></a>SQL Server Management Studio
 Management Studio 是所有 SQL Server 功能 (包括 Analysis Services) 的主要系統管理工具。 SQL Server Management Studio 是選擇性元件。 如果您在 Windows Server 2012 的 [應用程式] 頁面上未看到該元件和其他 SQL Server 應用程式，請執行 SQL Server 安裝程式以將其新增到您的安裝。

### <a name="sql-server-profiler"></a>SQL Server Profiler
 雖然 SQL Server Profiler 已正式被取代，但它卻是監視連線、MDX 查詢執行及其他伺服器作業最簡單的方式。 SQL Server Profiler 是預設會安裝的元件。 您可以在 Windows Server 2012 的 [應用程式] 頁面上看到該元件和其他 SQL Server 應用程式。

### <a name="powershell"></a>PowerShell
 您可以使用 PowerShell 命令來執行許多系統管理工作。 如需詳細資訊，請參閱＜ [Analysis Services PowerShell](analysis-services-powershell.md) ＞。

### <a name="community-and-third-party-tools"></a>社群與協力廠商工具
 如需社群程式碼範例，請造訪 [Analysis Services codeplex 頁面](https://sqlsrvanalysissrvcs.codeplex.com/) 。 針對支援 Analysis Services 的協力廠商工具尋求建議時，[論壇](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices)會很有説明。
