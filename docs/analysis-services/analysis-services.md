---
title: "Analysis Services |Microsoft 文件"
ms.date: 05/11/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.custom: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- Analysis Services, about Analysis Services - Multidimensional Data
- SSAS
- Analysis Services
- SQL Server Analysis Services, about Analysis Services - Multidimensional Data
- SQL Server Analysis Services
- multidimensional data [Analysis Services]
- SSAS, about Analysis Services - Multidimensional Data
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
caps.latest.revision: "60"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: 00b88b320118df9649b546b35259ec1c8acdc7cf
ms.sourcegitcommit: 82c9868b5bf95e5b0c68137ba434ddd37fc61072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/22/2018
---
# <a name="what-is-analysis-services"></a>什麼是 Analysis Services？
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  Analysis Services 是用於決策支援和商業分析，Reporting Services 報表、 報表和用戶端應用程式，例如 Excel、 Power BI 提供的分析資料和其他資料視覺效果工具的分析資料引擎。  
  
 一般工作流程包含撰寫多維度或表格式資料模型，將模型部署為在內部部署 SQL Server Analysis Services 或 Azure Analysis Services 伺服器執行個體的資料庫、 設定週期性的資料處理和指派由使用者允許存取資料的權限。 準備就緒時，語意資料模型可以存取的用戶端應用程式支援 Analysis Services 做為資料來源。  
 
## <a name="analysis-services-on-premises-and-in-the-cloud"></a>內部部署和雲端的 Analysis Services
Analysis Services 現在是一項雲端 Azure 服務。 Azure Analysis Services 支援在 1200年或更高的相容性層級的表格式模型。 DirectQuery、資料分割、資料列層級安全性、雙向關聯性和翻譯全都支援。 如需深入了解並免費試用，請參閱 [Azure Analysis Services](https://azure.microsoft.com/en-us/services/analysis-services/)。 
  
## <a name="server-mode"></a>伺服器模式  
 當使用 SQL Server 安裝程式安裝 Analysis Services，在設定期間指定該執行個體的伺服器模式。  每個模式都會包括特定 Analysis Services 方案獨有的不同功能。   
  
-   **表格式模式**-實作記憶體中關聯式資料模型建構 （模型、 資料表、 資料行、 量值、 階層）。  

-   **多維度和資料採礦模式** - 實作 OLAP 模型化建構 (Cube、維度、量值)。 

-   **Power Pivot 模式**-在 SharePoint 中的實作 Power Pivot 和 Excel 資料模型 （Power Pivot for SharePoint 是中間層資料引擎，可載入、 查詢和重新整理裝載在 SharePoint 中的資料模型）。  
  
 單一執行個體只能設定成一個模式，稍後無法進行變更。  您可以在相同的伺服器上使用不同的模式安裝多個執行個體，但需要執行安裝程式，並指定每個執行個體的組態設定。 詳細的資訊及提供每種模式中的不同功能的比較，請參閱[比較表格式和多維度解決方案](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)。
  
## <a name="authoring-and-managing-solutions"></a>撰寫和管理解決方案  
 若要建立模型，並將它部署至伺服器，您可以使用 SQL Server Data Tools，選擇 表格式或多維度和資料採礦專案範本。 專案範本包含模型所需所有物件的資料夾。 精靈和設計工具，可協助您建立許多基本項目，例如，連接到資料來源、 關聯性、 量值和角色。 一旦您的模型資料庫部署到伺服器時，您可以使用 SQL Server Management Studio (SSMS) 來設定資料處理、 監視和管理您的伺服器和資料庫。 若要進一步了解，請參閱[工具和 Analysis Services 中使用的應用程式](../analysis-services/tools-and-applications-used-in-analysis-services.md)。 
  
## <a name="documentation-by-area"></a>依區域列出的文件  
在一般，Azure Analysis Services 的文件隨附於 Azure 文件。 和 SQL Server Analysis Services 的文件隨附於 SQL 文件集。 不過，至少對於表格式模型，如何建立和部署您的專案是不論您使用何種平台大致相同。  
   
*  [Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/)
*  [SQL Server Analysis Services 中最新消息](../analysis-services/what-s-new-in-analysis-services.md)   
*  [比較表格式和多維度解決方案](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
*  [表格式模型](../analysis-services/tabular-models/tabular-models-ssas.md)  
*  [多維度模型](../analysis-services/multidimensional-models/multidimensional-models-ssas.md)  
*  [資料採礦](../analysis-services/data-mining/data-mining-ssas.md)  
*  [Power Pivot for SharePoint](../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
*  [執行個體管理](../analysis-services/instances/analysis-services-instance-management.md)    
*  [教學課程](../analysis-services/analysis-services-tutorials-ssas.md)   
*  [開發人員文件](https://msdn.microsoft.com/library/bb500153(SQL.130).aspx)  
*  [技術參考 (SSAS)](../analysis-services/powershell/technical-reference-ssas.md)
