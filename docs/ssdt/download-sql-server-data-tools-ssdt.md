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
ms.translationtype: Human Translation
ms.sourcegitcommit: 5bd0e1d3955d898824d285d28979089e2de6f322
ms.openlocfilehash: 7aaa4c48419bf24357b2bef95c40d721d1ab2f2a
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="download-sql-server-data-tools-ssdt"></a>下載 SQL Server Data Tools (SSDT)

**[SQL Server Data Tools](https://msdn.microsoft.com/mt186501)** 是一款免費下載的新式開發工具，可用來建置 SQL Server 關聯式資料庫、Azure SQL Database、Integration Services 封裝、Analysis Services 資料模型以及 Reporting Services 報表。 有了 SSDT，您便可設計和部署任何 SQL Server 內容類型，就像在 Visual Studio 中開發應用程式一樣容易。 此版本支援 SQL Server 2017 到 SQL Server 2005，並提供設計環境，以新增 SQL Server 2016 中的新功能。  
    
    
![下載](../ssdt/media/download.png)。[下載適用於 Visual Studio 2015 的 SQL Server Data Tools 17.1](https://go.microsoft.com/fwlink/?linkid=849393)

![下載](../ssdt/media/download.png)。[下載 Data-Tier Application Framework (DacFx) 17.1](https://www.microsoft.com/download/details.aspx?id=55255)

## <a name="sql-server-data-tools"></a>SQL Server Data Tools   
**版本資訊**  
  
版本號碼：17.1  
此版本的組建編號：14.0.61705.170
  
 **新功能**
 - AS 非模型相關 IntelliSense 的離線支援 (例如，醒目提示、陳述式完成及參數資訊)
 - 表格式模型總管新增內容，以顯示 M 運算式
 - 用於在表格式模型中設定角色成員的 Azure Active Directory 人員選擇器
 - 在定義 1400 模型時，UI 中的編碼提示支援
 - 數個 AS 專案 Bug 修正
 - 數個 DacFx Bug 修正

 **已知問題**
 - 在 1400 相容性層級 AS 模型中建立新資料來源時，若您選取以檔案為基礎的資料來源且在建立資料來源之前取消按 [取消]，表格式編輯器 (Moder.bim) 會變成唯讀。 您只要關閉表格式編輯器，然後從方案總管重新予以開啟，就能解決這個問題。

[變更記錄](changelog-for-sql-server-data-tools-ssdt.md)中提供完整的變更清單

 > 若要在 Visual Studio 2017 中使用 SQL Server Data Tools，請參閱下方的[這個](#use-ssdt-in-visual-studio-2017)章節

  **可用語言**  
  
 此版本的 SSDT 提供下列語言版本：  
[中文 (中華人民共和國)]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x804) | 
[中文 (台灣)]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x404) | 
[英文 (美國)]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x409) | 
[法文]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x40c)  
[德文]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x407) | 
[義大利文]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x410) | 
[日文]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x411) | 
[韓文]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x412) | 
[葡萄牙文 (巴西)]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x416) | 
[俄文]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x419) | 
[西班牙文]( https://go.microsoft.com/fwlink/?linkid=849393&clcid=0x40a)  

**ISO 映像**

SSDT 的 ISO 映像提供了另一種方式，可讓您用來安裝 SSDT 或設定系統管理安裝點。 ISO 是一個獨立的檔案，內含 SSDT 需要的所有元件，而且隨時啟動下載管理員皆可下載，非常適合網路頻寬有限或不穩的情況使用。 下載後，ISO 可掛載為磁碟機或燒錄至 DVD。

[中文 (中華人民共和國)]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x804) |
[中文 (台灣)]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x404) |
[英文 (美國)]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x409) |
[法文]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x40c)  
[德文]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x407) |
[義大利文]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x410) |
[日文]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x411) |
[韓文]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x412) |
[葡萄牙文 (巴西)]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x416) |
[俄文]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x419) |
[西班牙文]( https://go.microsoft.com/fwlink/?linkid=849399&clcid=0x40a)

## <a name="download-visual-studio"></a>下載 Visual Studio

* [**下載 Visual Studio Community 2015**](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)

## <a name="installing-ssdt-without-visual-studio-pre-installed"></a>在沒有預先安裝 Visual Studio 的情況下安裝 SSDT

如果您的電腦上未安裝 Visual Studio，安裝適用於 Visual Studio 2015 的 SSDT 也會安裝 Visual Studio 2015 的最低「整合模式 Shell」版本。 這個 Visual Studio 版本可在您想要的任意數目電腦上免費安裝及使用。 其提供所有 SQL Server 專案類型，加上 SQL Server 物件總管及其他 SQL 工具體驗。

如果您已在電腦上安裝 [Visual Studio 2015 Community 版本 (或更新版本)](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)，安裝 SSDT 會將一組完整 SQL Server 工具新增到您的現有 Visual Studio 安裝中。 Visual Studio 包括許多您可能會想用的功能，例如 原始程式碼控制整合及非 SQL 語言支援。 建議您使用 Visual Studio 2015 Community 或更新版本，以在開發 T-SQL 時取得最佳體驗。

## <a name="supported-sql-versions"></a>支援的 SQL 版本
  
|專案範本|支援的 SQL 平台|  
|-------------------|--------------------|  
關聯式資料庫|  SQL Server 2005* - SQL Server 2017 <br /><br />Azure SQL Database<br /><br />Azure SQL 資料倉儲 (僅支援查詢；尚不支援資料庫專案)<br /><br />  * SQL Server 2005 支援已被取代，<br /><br /> 請改為官方支援的 SQL 版本|
  |Analysis Services 模型<br /><br />Reporting Services 報表 | SQL Server 2008 – SQL Server 2017|
  |Integration Services 封裝| SQL Server 2012 – SQL Server 2017    |
  
## <a name="next-steps"></a>後續的步驟  
安裝 SSDT 後，請逐步完成這些教學課程，了解如何使用 SSDT 建立資料庫、封裝、資料模型及報表：  
  
-   [專案導向的離線資料庫開發](https://msdn.microsoft.com/library/hh272702(v=vs.103).aspx)  
  
-   [SSIS 教學課程：建立簡易 ETL 封裝](https://msdn.microsoft.com/library/ms169917.aspx)  
  
-   [Analysis Services 教學課程](https://msdn.microsoft.com/library/hh231701.aspx)  
  
-   [建立基本資料表報表 (SSRS 教學課程)](https://msdn.microsoft.com/library/ms167305.aspx)  
  
## <a name="use-ssdt-in-visual-studio-2017"></a>在 Visual Studio 2017 中使用 SSDT 

* [**下載 Visual Studio 2017**](https://www.visualstudio.com/) ([依版本比較 Visual Studio 2017 功能 (英文)](https://www.visualstudio.com/vs/compare/))

若要使用關聯式資料庫專案，我們建議在安裝期間檢查「資料儲存和處理」工作負載。 SSDT 資料庫專案支援也包括一些其他工作負載，包含「Azure」、「ASP.Net 和網頁程式開發」，以及「.Net Core 跨平台開發」。

> [!NOTE]
> Visual Studio 2017 中的 SSDT 資料庫專案目前最多支援到 SQL Server 2016。  SQL Server 2017 的支援即將在 Visual Studio 2017 更新中推出。

如果您搭配使用 SSDT 與 Visual Studio 2017，請安裝 AS 和 RS 元件：
* [Analysis Services (英文)](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)
* [Reporting Services (英文)](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)


## <a name="see-also"></a>另請參閱  
[Visual Studio 中的 SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[SSDT MSDN 論壇](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[SSDT 團隊部落格](http://blogs.msdn.com/b/ssdt/)  
[SSDT Connect 意見反應](https://connect.microsoft.com/SQLServer/Feedback)  
[SSDT 文件](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[DACFx API 參考](https://msdn.microsoft.com/library/dn645454.aspx)  
[下載 SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  

