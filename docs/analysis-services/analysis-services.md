---
title: "Analysis Services | Microsoft Docs"
ms.date: "03/28/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "Analysis Services, 關於 Analysis Services - 多維度資料"
  - "SSAS"
  - "Analysis Services"
  - "SQL Server Analysis Services, 關於 Analysis Services - 多維度資料"
  - "SQL Server Analysis Services"
  - "多維度資料 [Analysis Services]"
  - "SSAS, 關於 Analysis Services - 多維度資料"
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
caps.latest.revision: 60
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 60
---
# Analysis Services
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 是用於決策支援和商業分析的線上分析資料引擎，可提供報表和用戶端應用程式 (例如 Power BI、Excel、Reporting Services 報表和其他資料視覺效果工具) 的分析資料。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的一般工作流程包括編寫多維度或表格式資料模型、將模型以資料庫方式部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體、處理資料庫以載入該資料庫及資料或中繼資料、設定資料重新整理，然後指派權限以允許使用者進行資料存取。 準備好開始執行時，任何支援 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 作為資料來源的用戶端應用程式，即可存取這個多用途語意資料模型。  
  
 模型會填入外部資料系統中的資料，通常是在 SQL Server 或 Oracle 關聯式資料庫引擎上裝載的資料倉儲 (表格式模型支援其他資料來源類型)。 模型不僅會指定查詢物件 (例如 Cube)，也會指定維度 (可用於多個 Cube、計算和 KPI 以封裝商務邏輯) 以及互動 (例如瀏覽和鑽研行為)。  
 
## <a name="analysis-services-on-premises-and-in-the-cloud"></a>內部部署和雲端的 Analysis Services
Analysis Services 現在是一項雲端 Azure 服務。 目前為預覽階段的 Azure Analysis Services 支援 1200 相容性層級的表格式模型。 DirectQuery、資料分割、資料列層級安全性、雙向關聯性和翻譯全都支援。 如需深入了解並免費試用，請參閱 [Azure Analysis Services](https://azure.microsoft.com/en-us/services/analysis-services/)。 
  
## <a name="server-mode"></a>伺服器模式  
 使用 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 安裝程式安裝 Analysis Services 時，您可以在組態期間指定該執行個體的伺服器模式。  每個模式都會包括特定 Analysis Services 方案獨有的不同功能。  
  
-   **多維度和資料採礦模式** - 實作 OLAP 模型化建構 (Cube、維度、量值)。  
  
-   **表格式模式** - 實作記憶體內部關聯式資料模型建構 (模型、資料表、資料行)。  
  
     可以使用最新的功能在預設相容性層級 1200 建立表格式模型，或在較舊的 1103 相容性層級上建立。 相容性層級之間有些重大差異。 如需層級如何比較的資訊，請參閱 [Analysis Services 中表格式模型的相容性層級](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。  
  
-   **Power Pivot 模式** - 在 SharePoint 中實作 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 和 Excel 資料模型 ([!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for SharePoint 是中間層資料引擎，可載入、查詢及重新整理 SharePoint 中所裝載的資料模型)。  
  
 單一執行個體只能設定成一個模式，稍後無法進行變更。  您可以在相同的伺服器上使用不同的模式安裝多個執行個體，但需要執行安裝程式，並指定每個執行個體的組態設定。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 功能會因版本而異。 如需詳細資訊，請參閱 [SQL Server 2016 的版本及支援功能](../sql-server/sql-server-2016-的版本及支援功能.md)。 
  
## <a name="authoring-solutions"></a>編寫方案  
 若要建立模型，您可以使用 SQL Server Data Tools (請參閱 [Analysis Services 中使用的工具和應用程式](../analysis-services/tools-and-applications-used-in-analysis-services.md))，選擇表格式或多維度及資料採礦專案範本。 專案範本包含模型所需所有物件的資料夾。 精靈有助於建立許多基本項目，例如資料來源、資料來源檢視、維度、Cube 和角色。  
  
## <a name="documentation-by-area"></a>依區域列出的文件  
Analysis Services 的文件會組織成若干章節，這些章節會對應到您所建立的專案類型。 從下列連結進行選擇，以深入了解每一種模式或功能領域。  
   
 ![小型檔案資料夾圖示](../analysis-services/media/filefolder-small.png "小型檔案資料夾圖示") [新功能](../analysis-services/what-s-new-in-analysis-services.md)  
  
 ![小型檔案資料夾圖示](../analysis-services/media/filefolder-small.png "小型檔案資料夾圖示") [比較表格式和多維度解決方案](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)  
  
 ![小型檔案資料夾圖示](../analysis-services/media/filefolder-small.png "小型檔案資料夾圖示") [表格式模型](../analysis-services/tabular-models/tabular-models-ssas.md)  
  
 ![小型檔案資料夾圖示](../analysis-services/media/filefolder-small.png "小型檔案資料夾圖示") [多維度模型](../analysis-services/multidimensional-models/multidimensional-models-ssas.md)  
  
 ![小型檔案資料夾圖示](../analysis-services/media/filefolder-small.png "小型檔案資料夾圖示") [資料採礦](../analysis-services/data-mining/data-mining-ssas.md)  
  
 ![小型檔案資料夾圖示](../analysis-services/media/filefolder-small.png "小型檔案資料夾圖示") [ Power Pivot for SharePoint](../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
  
 ![小型檔案資料夾圖示](../analysis-services/media/filefolder-small.png "小型檔案資料夾圖示") [Analysis Services 執行個體管理](../analysis-services/instances/analysis-services-instance-management.md)  
   
 ![小型檔案資料夾圖示](../analysis-services/media/filefolder-small.png "小型檔案資料夾圖示") [Analysis Services 教學課程](../analysis-services/analysis-services-tutorials-ssas.md)  
  
![小型檔案資料夾圖示](../analysis-services/media/filefolder-small.png "小型檔案資料夾圖示") [Analysis Services Developer Documentation](https://msdn.microsoft.com/library/bb500153(SQL.130).aspx) (Analysis Services 開發人員文件)  
 
![小型檔案資料夾圖示](../analysis-services/media/filefolder-small.png "小型檔案資料夾圖示") [技術參考 (SSAS)](../analysis-services/powershell/technical-reference-ssas.md)