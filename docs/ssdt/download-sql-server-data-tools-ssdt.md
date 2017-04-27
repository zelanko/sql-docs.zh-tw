---
title: "下載 SQL Server Data Tools (SSDT) | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "安裝 SSDT, 下載 SSDT, 最新的 SSDT"
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 681ad2f6d7aeb88db45dde3f2e695db672b97dbd
ms.lasthandoff: 04/11/2017

---
# <a name="download-sql-server-data-tools-ssdt"></a>下載 SQL Server Data Tools (SSDT)

**[SQL Server Data Tools](https://msdn.microsoft.com/mt186501)** 是一款免費下載的新式開發工具，可用來建置 SQL Server 關聯式資料庫、Azure SQL Database、Integration Services 封裝、Analysis Services 資料模型以及 Reporting Services 報表。 有了 SSDT，您便可設計和部署任何 SQL Server 內容類型，就像在 Visual Studio 中開發應用程式一樣容易。 此版本支援 SQL Server 2016 到 SQL Server 2005，並提供設計環境，能在 SQL Server 2016 中新增新功能。  
    
    
| ![下載這篇文章](../ssdt/media/download.png) 下載適用於 Visual Studio 2015 的 SQL Server Data Tools  | 下載資料層應用程式架構 (DacFx) ||
|:---|:---|:---|
|**[下載 SQL Server Data Tools (16.5)](https://msdn.microsoft.com/mt186501)**|[**下載 DacFx 及 SqlPackage.exe (16.5)**](https://www.microsoft.com/download/details.aspx?id=54106) |供生產環境使用的目前 GA 版本。|
|[**下載 SQL Server Data Tools - 候選版**](../ssdt/sql-server-data-tools-ssdt-release-candidate.md)| [**下載 DacFx 及 SqlPackage.exe - 候選版**](../ssdt/sql-server-data-tools-ssdt-release-candidate.md) |包含對 SQL Server vNext 的支援。|



## <a name="download-visual-studio"></a>下載 Visual Studio

* [**下載 Visual Studio Community 2015**](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)

### <a name="use-ssdt-in-visual-studio-2017"></a>在 Visual Studio 2017 中使用 SSDT

* [**下載 Visual Studio 2017**](https://www.visualstudio.com/) ([依版本比較 Visual Studio 2017 功能 (英文)](https://www.visualstudio.com/vs/compare/))

若要使用關聯式資料庫專案，我們建議在安裝期間檢查「資料儲存和處理」工作負載。 SSDT 資料庫專案支援也包括一些其他工作負載，包含「Azure」、「ASP.Net 和網頁程式開發」，以及「.Net Core 跨平台開發」。

如果您搭配使用 SSDT 與 Visual Studio 2017，請安裝 AS 和 RS 元件：
* [Analysis Services (英文)](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)
* [Reporting Services (英文)](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)


## <a name="installing-ssdt-without-visual-studio-pre-installed"></a>在沒有預先安裝 Visual Studio 的情況下安裝 SSDT

如果您的電腦上未安裝 Visual Studio，安裝適用於 Visual Studio 2015 的 SSDT 也會安裝 Visual Studio 2015 的最低「整合模式 Shell」版本。 這個 Visual Studio 版本可在您想要的任意數目電腦上免費安裝及使用。 其提供所有 SQL Server 專案類型，加上 SQL Server 物件總管及其他 SQL 工具體驗。

如果您已在電腦上安裝 [Visual Studio 2015 Community 版本 (或更新版本)](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)，安裝 SSDT 會將一組完整 SQL Server 工具新增到您的現有 Visual Studio 安裝中。 Visual Studio 包括許多您可能會想用的功能，例如 原始程式碼控制整合及非 SQL 語言支援。 建議您使用 Visual Studio 2015 Community 或更新版本，以在開發 T-SQL 時取得最佳體驗。

## <a name="supported-sql-versions"></a>支援的 SQL 版本
  
|專案範本|支援的 SQL 平台|  
|-------------------|--------------------|  
關聯式資料庫|  SQL Server 2005* - SQL Server 2016 <br /><br />Azure SQL Database<br /><br />Azure SQL 資料倉儲 (僅支援查詢；尚不支援資料庫專案)<br /><br />  * SQL Server 2005 支援已被取代，<br /><br /> 請改為官方支援的 SQL 版本|
  |Analysis Services 模型<br /><br />Reporting Services 報表 | SQL Server 2008 - SQL Server 2016|
  |Integration Services 封裝| SQL Server 2012 - SQL Server 2016    |
  
## <a name="next-steps"></a>後續的步驟  
安裝 SSDT 後，請逐步完成這些教學課程，了解如何使用 SSDT 建立資料庫、封裝、資料模型及報表：  
  
-   [專案導向的離線資料庫開發](https://msdn.microsoft.com/library/hh272702(v=vs.103).aspx)  
  
-   [SSIS 教學課程：建立簡易 ETL 封裝](https://msdn.microsoft.com/library/ms169917.aspx)  
  
-   [Analysis Services 教學課程](https://msdn.microsoft.com/library/hh231701.aspx)  
  
-   [建立基本資料表報表 (SSRS 教學課程)](https://msdn.microsoft.com/library/ms167305.aspx)  
  
## <a name="see-also"></a>另請參閱  
[Visual Studio 中的 SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[SSDT MSDN 論壇](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT 團隊部落格](http://blogs.msdn.com/b/ssdt/)  
[SSDT Connect 意見反應](https://connect.microsoft.com/SQLServer/Feedback)  
[SSDT 文件](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[DACFx API 參考](https://msdn.microsoft.com/library/dn645454.aspx)  
[下載 SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  

