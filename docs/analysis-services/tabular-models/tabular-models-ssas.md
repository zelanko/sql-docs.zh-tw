---
title: "表格式模型 (SSAS) |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f1f324d1ba1b4ba9299c4d29e565d09d1f71fb2c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="tabular-modeling-ssas"></a>表格式模型化 (SSAS)
  表格式模型是一種 Analysis Services 資料庫，其會在記憶體內部或以 DirectQuery 模式執行，並直接從後端的關聯式資料來源存取資料。  
  
 記憶體內部是預設值。 記憶體內部分析引擎採用最先進的壓縮演算法和多執行緒查詢處理器，可透過 Microsoft Excel 和 Microsoft [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]等報表用戶端應用程式快速存取表格式模型物件和資料。  
  
 如果模型太大無法納入記憶體中，或資料的變動程度不適合進行合理處理策略時，可使用 DirectQuery 這個替代的查詢模式。 在此版本中，DirectQuery 可搭配記憶體內部模型實現較佳的同位檢查，因為它支援其他資料來源、能夠處理 DirectQuery 模型計算出的資料表和資料行，具有可連接後端資料庫的 DAX 運算式，以保障資料列層級安全性，並支援查詢最佳化，可提供比舊版更快速的輸送量。
  
 您可在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中使用表格式模型專案範本所提供的設計介面以建立模型、資料表、關聯性和 DAX 運算式，藉此撰寫表格式模型。 您可以從多個來源匯入資料，然後加入關聯性、計算資料表和資料行、量值、KPI、階層及翻譯，來充實模型。  
  
 接著，即可將模型部署至已設為表格式伺服器模式的 Analysis Services 執行個體，再由其中的用戶端報表應用程式連接至模型。 您可以在 SQL Server Management Studio 中管理已部署的模型，就像是管理多維度模型一樣。 您也可以對其進行資料分割以最佳化處理，並使用以角色為基礎的安全性提供資料列層級的安全性。  
  
## <a name="in-this-section"></a>本節內容  
 [表格式模型方案 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md)  - 本節中的主題描述如何建立和部署表格式模型方案。
  
 [表格式模型資料庫 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)  - 本節中的主題描述如何管理已部署的表格式模型方案。
  
 [表格式模型資料存取](../../analysis-services/tabular-models/tabular-model-data-access.md)  - 本節中的主題描述如何連接至已部署的表格式模型方案。
  
## <a name="see-also"></a>請參閱＜  
 [Analysis Services 的新功能](../../analysis-services/what-s-new-in-analysis-services.md)   
 [比較表格式和多維度解決方案 &#40;SSAS&#41;](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [工具和 Analysis Services 中使用的應用程式](../../analysis-services/tools-and-applications-used-in-analysis-services.md)   
 [DirectQuery 模式 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Analysis Services 中表格式模型的相容性層級](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
