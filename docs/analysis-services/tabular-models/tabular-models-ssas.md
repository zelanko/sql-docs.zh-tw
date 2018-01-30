---
title: "表格式模型 |Microsoft 文件"
ms.custom: 
ms.date: 01/29/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: edeea89c1d767364f4f087d0f4b2e6d566895c52
ms.sourcegitcommit: c77a8ac1ab372927c09bf241d486e96881b61ac9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/29/2018
---
# <a name="tabular-models"></a>表格式模型
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]表格式模型是記憶體中或在 DirectQuery 模式中，從後端關聯式資料來源存取資料直接執行的 Analysis Services 資料庫。  
  
 記憶體內部是預設值。 使用的圖案狀態壓縮演算法和多執行緒的查詢處理器，分析引擎能夠快速存取表格式模型物件和資料透過報表用戶端應用程式，例如 Power BI 與 Excel。  
  
 如果模型太大無法納入記憶體中，或資料的變動程度不適合進行合理處理策略時，可使用 DirectQuery 這個替代的查詢模式。 在此版本中，DirectQuery 可搭配記憶體內部模型實現較佳的同位檢查，因為它支援其他資料來源、能夠處理 DirectQuery 模型計算出的資料表和資料行，具有可連接後端資料庫的 DAX 運算式，以保障資料列層級安全性，並支援查詢最佳化，可提供比舊版更快速的輸送量。
  
 您可在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中使用表格式模型專案範本所提供的設計介面以建立模型、資料表、關聯性和 DAX 運算式，藉此撰寫表格式模型。 您可以從多個來源匯入資料，然後加入關聯性、計算資料表和資料行、量值、KPI、階層及翻譯，來充實模型。  
  
 模型可以再部署到 Azure Analysis Services 或 SQL Server Analysis Services 的執行個體設定為表格式伺服器模式。 可以管理已部署表格式模型 SQL Server Management Studio 中，就像多維度模型一樣。 您也可以對其進行資料分割以最佳化處理，並使用以角色為基礎的安全性提供資料列層級的安全性。  
  
## <a name="in-this-section"></a>本節內容  
 [表格式模型方案](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md)-本節中的主題說明建立和部署表格式模型方案。
  
 [表格式模型資料庫](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)-本節中的主題說明管理已部署的表格式模型方案。
  
 [表格式模型資料存取](../../analysis-services/tabular-models/tabular-model-data-access.md)-本節中的主題描述連接到部署表格式模型方案。
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 的新功能](../../analysis-services/what-s-new-in-analysis-services.md)   
 [比較表格式和多維度解決方案](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [工具和 Analysis Services 中使用的應用程式](../../analysis-services/tools-and-applications-used-in-analysis-services.md)   
 [DirectQuery 模式](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Analysis Services 中表格式模型的相容性層級](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
