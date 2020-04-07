---
title: SQL 伺服器 2014 分析服務 |微軟文件
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
ms.sourcegitcommit: 8f99d15c5b23d9f3c08a77e2b8bea5772f570493
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/07/2020
ms.locfileid: "80760299"
---
# <a name="sql-server-2014-analysis-services"></a>SQL Server 2014 Analysis Services

  SQL Server 2014 分析服務是決策支援和商業智慧 (BI) 解決方案中使用的分析數據引擎,為業務報告和用戶端應用程式(如 Excel、報告服務報告和其他第三方 BI 工具)提供分析數據。 

## <a name="about-sql-server-analysis-services-documentation"></a>關於 SQL 伺服器分析服務文件

文件按版本分隔。 您目前位於 SQL Server 2014 分析服務文件中。

- 要瞭解有關 SQL Server 2012 和更早版本的更多內容,請參閱[SQL Server 早期版本文件](https://docs.microsoft.com/previous-versions/sql/)。
- 要瞭解有關 SQL Server 2014 的資訊,請參閱[SQL Server 2014 的線上書籍](../2014-toc/index.yml)
- 要瞭解有關 SQL Server 2016 及更高版本的更多內容,請參閱[分析服務文件](https://docs.microsoft.com/analysis-services/)。
- 要瞭解有關 Azure 分析服務的更多詳細資訊,請參閱[Azure 分析服務文件](https://docs.microsoft.com/azure/analysis-services/)。

## <a name="analysis-services-workflow"></a>分析服務工作流

典型的工作流包括構建 OLAP 或表格數據模型,將模型作為資料庫部署到伺服器實例,處理資料庫以載入數據,然後分配允許數據存取的許可權。 準備好開始執行時，任何支援 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 作為資料來源的用戶端應用程式，即可存取這個多用途資料模型。  
  
 要建立模型,請使用 SQL Server 資料工具(請參閱[分析服務中使用的工具和應用程式](tools-and-applications-used-in-analysis-services.md)),選擇表格或多維和資料挖掘專案範本。 專案範本包含模型所需所有物件的資料夾。 您可以使用精靈來建立所有基本項目，例如資料來源、資料來源檢視、維度、Cube 和角色。  
  
 模型會填入外部資料系統中的資料，通常是在 SQL Server 或 Oracle 關聯式資料庫引擎上裝載的資料倉儲 (表格式模型支援其他資料來源類型)。 模型不僅會指定查詢物件 (例如 Cube)，也會指定維度 (可用於多個 Cube、計算和 KPI 以封裝商務邏輯) 以及互動 (例如瀏覽和鑽研行為)。  
  
 要使用模型,它將部署到在特定伺服器模式下運行資料庫的伺服器實例,使數據可供通過 Excel 或其他應用程式進行連接的授權使用者使用。  
  
 您可以在三種伺服器模式之一安裝實例:  
  
-   當做表格式執行個體，執行表格式模型。  
  
-   當做多維度和資料採礦執行個體，執行 OLAP Cube 和資料採礦模型 (這是預設值)。  
  
-   當做 PowerPivot for SharePoint，在 SharePoint 中執行 PowerPivot 和 Excel 資料模型 (PowerPivot for SharePoint 是中間層資料引擎，可載入、查詢及重新整理 SharePoint 中所裝載的資料模型)。  
  
 相同資料引擎，三種不同的使用方式。 請注意，安裝期間會設定伺服器模式，而且之後無法變更。 如果您需要不同的模式，應該安裝新的執行個體。  
  
 Analysis Services 的基本文件集會組織成若干章節，這些章節會對應到您所建立的專案類型。 從下列連結進行選擇，以深入了解每一種模式或功能領域。  
  
 **依區域瀏覽內容**  
 ![小資料夾圖示](../../2014/integration-services/media/filefolder-small.gif "小型檔案資料夾圖示")[比較表格和多維解決方案&#40;SSAS&#41;](comparing-tabular-and-multidimensional-solutions-ssas.md)  
  
 ![小資料夾圖示](../../2014/integration-services/media/filefolder-small.gif "小型檔案資料夾圖示")[分析服務實體管理](instances/analysis-services-instance-management.md)  
  
 ![小型資料夾圖示](../../2014/integration-services/media/filefolder-small.gif "小型檔案資料夾圖示")[表式建模&#40;SSAS 表格&#41;](tabular-models/tabular-models-ssas.md)  
  
 ![小型資料夾圖示](../../2014/integration-services/media/filefolder-small.gif "小型檔案資料夾圖示")[多維建模&#40;SSAS&#41;](multidimensional-models/multidimensional-models-ssas.md)  
  
 ![小型目錄圖示](../../2014/integration-services/media/filefolder-small.gif "小型檔案資料夾圖示")[資料挖掘&#40;SSAS&#41;](data-mining/data-mining-ssas.md)  
  
 [共用點&#40;SSAS&#41;](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)![的小資料夾圖示](../../2014/integration-services/media/filefolder-small.gif "小型檔案資料夾圖示")電源透視  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 功能會因版本而異。 Standard 版中可以使用多維度和資料採礦模型，但是功能少於較高的版本。 表格式模型和 PowerPivot for SharePoint 是高階功能，無法在 Standard 版授權之下使用。 如需詳細資訊，請參閱＜ [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [分析服務教程&#40;SSAS&#41;](analysis-services-tutorials-ssas.md)   
 [安裝 SQL 伺服器 2014](../database-engine/install-windows/installation-for-sql-server.md)   
 [開發人員指南&#40;分析服務&#41;](analysis-services-developer-documentation.md)   
 [SQL 伺服器資源中心](https://go.microsoft.com/fwlink/?linkID=219676)   
 [SQLCat.com](https://go.microsoft.com/fwlink/?linkID=220963)  
  
  
