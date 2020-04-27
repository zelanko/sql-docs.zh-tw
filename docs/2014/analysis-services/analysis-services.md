---
title: SQL Server 2014 Analysis Services |Microsoft Docs
ms.custom: ''
ms.date: 04/06/2020
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, about Analysis Services - Multidimensional Data
- SSAS
- Analysis Services
- SQL Server Analysis Services, about Analysis Services - Multidimensional Data
- SQL Server Analysis Services
- multidimensional data [Analysis Services]
- SSAS, about Analysis Services - Multidimensional Data
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 986356e6ebf7697bf0b425553f6803659a0fc5cb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "80760299"
---
# <a name="sql-server-2014-analysis-services"></a>SQL Server 2014 Analysis Services

  SQL Server 2014 Analysis Services 是用於決策支援和商業智慧（BI）解決方案的分析資料引擎，可供應商務報表和用戶端應用程式（例如 Excel、Reporting Services 報表和其他協力廠商 BI 工具）的分析資料。 

## <a name="about-sql-server-analysis-services-documentation"></a>關於 SQL Server Analysis Services 檔

檔會以版本分隔。 您目前處於 SQL Server 2014 Analysis Services 檔。

- 若要深入瞭解 SQL Server 2012 和更早版本，請參閱[SQL Server 舊版檔](https://docs.microsoft.com/previous-versions/sql/)。
- 若要深入瞭解 SQL Server 2014，請參閱《[線上叢書》 SQL Server 2014](../2014-toc/index.yml)
- 若要深入瞭解 SQL Server 2016 和更新版本，請參閱[Analysis Services 檔](https://docs.microsoft.com/analysis-services/)。
- 若要深入瞭解 Azure Analysis Services，請參閱[azure Analysis Services 檔](https://docs.microsoft.com/azure/analysis-services/)。

## <a name="analysis-services-workflow"></a>Analysis Services 工作流程

一般工作流程包括建立 OLAP 或表格式資料模型、將模型當做資料庫部署至伺服器實例、處理資料庫以載入資料，然後指派許可權以允許資料存取。 準備好開始執行時，任何支援 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 作為資料來源的用戶端應用程式，即可存取這個多用途資料模型。  
  
 若要建立模型，請使用 SQL Server Data Tools （請參閱[Analysis Services 中使用的工具和應用程式](tools-and-applications-used-in-analysis-services.md)），選擇表格式或多維度和資料採礦專案範本。 專案範本包含模型所需所有物件的資料夾。 您可以使用精靈來建立所有基本項目，例如資料來源、資料來源檢視、維度、Cube 和角色。  
  
 模型會填入外部資料系統中的資料，通常是在 SQL Server 或 Oracle 關聯式資料庫引擎上裝載的資料倉儲 (表格式模型支援其他資料來源類型)。 模型不僅會指定查詢物件 (例如 Cube)，也會指定維度 (可用於多個 Cube、計算和 KPI 以封裝商務邏輯) 以及互動 (例如瀏覽和鑽研行為)。  
  
 若要使用模型，它會部署到以特定伺服器模式執行資料庫的伺服器實例，讓資料可供透過 Excel 或其他應用程式連接的授權使用者使用。  
  
 您可以使用下列三種伺服器模式之一來安裝實例：  
  
-   當做表格式執行個體，執行表格式模型。  
  
-   當做多維度和資料採礦執行個體，執行 OLAP Cube 和資料採礦模型 (這是預設值)。  
  
-   當做 PowerPivot for SharePoint，在 SharePoint 中執行 PowerPivot 和 Excel 資料模型 (PowerPivot for SharePoint 是中間層資料引擎，可載入、查詢及重新整理 SharePoint 中所裝載的資料模型)。  
  
 相同資料引擎，三種不同的使用方式。 請注意，安裝期間會設定伺服器模式，而且之後無法變更。 如果您需要不同的模式，應該安裝新的執行個體。  
  
 Analysis Services 的基本文件集會組織成若干章節，這些章節會對應到您所建立的專案類型。 從下列連結進行選擇，以深入了解每一種模式或功能領域。  
  
 **依區域瀏覽內容**  
 [比較表格式和多維度方案 &#40;SSAS&#41;的](comparing-tabular-and-multidimensional-solutions-ssas.md)![小型檔案資料夾圖示](../../2014/integration-services/media/filefolder-small.gif "小型檔案資料夾圖示")  
  
 ![小型檔案資料夾圖示](../../2014/integration-services/media/filefolder-small.gif "小型檔案資料夾圖示") [Analysis Services 實例管理](instances/analysis-services-instance-management.md)  
  
 ![小型檔案資料夾圖示](../../2014/integration-services/media/filefolder-small.gif "小型檔案資料夾圖示")[表格式模型化 &#40;SSAS 表格式&#41;](tabular-models/tabular-models-ssas.md)  
  
 ![小型檔案資料夾圖示](../../2014/integration-services/media/filefolder-small.gif "小型檔案資料夾圖示")多[維度模型化 &#40;SSAS&#41;](multidimensional-models/multidimensional-models-ssas.md)  
  
 ![小型檔案資料夾圖示](../../2014/integration-services/media/filefolder-small.gif "小型檔案資料夾圖示")[資料採礦 &#40;SSAS&#41;](data-mining/data-mining-ssas.md)  
  
 [&#40;SSAS&#41;](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)的![小型檔案資料夾圖示](../../2014/integration-services/media/filefolder-small.gif "小型檔案資料夾圖示")PowerPivot for SharePoint  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 功能會因版本而異。 Standard 版中可以使用多維度和資料採礦模型，但是功能少於較高的版本。 表格式模型和 PowerPivot for SharePoint 是高階功能，無法在 Standard 版授權之下使用。 如需詳細資訊，請參閱＜ [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services SSAS &#40;教學課程&#41;](analysis-services-tutorials-ssas.md)   
 [SQL Server 2014 的安裝](../database-engine/install-windows/installation-for-sql-server.md)   
 [開發人員指南 &#40;Analysis Services&#41;](analysis-services-developer-documentation.md)   
 [SQL Server 資源中心](https://go.microsoft.com/fwlink/?linkID=219676)   
 [SQLCat.com](https://go.microsoft.com/fwlink/?linkID=220963)  
  
  
