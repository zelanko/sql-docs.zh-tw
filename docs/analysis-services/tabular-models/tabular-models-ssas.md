---
title: "表格式模型 |Microsoft 文件"
ms.custom: 
ms.date: 02/21/2018
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
ms.openlocfilehash: 2df607b47e4bb2a5a770e27d1bceb5a6d7e6ebbc
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/23/2018
---
# <a name="tabular-models"></a>表格式模型
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
表格式模型是一種 Analysis Services 資料庫，其會在記憶體內部或以 DirectQuery 模式執行，並直接從後端的關聯式資料來源存取資料。 使用的圖案狀態壓縮演算法和多執行緒的查詢處理器，分析引擎送交快速存取表格式模型物件和資料透過報表用戶端應用程式，例如 Power BI 與 Excel。  
  
 記憶體中模型都是預設值，DirectQuery 為替代的查詢模式的模型，就是太大無法納入記憶體中，或資料的變動程度不適合進行合理處理策略。 DirectQuery 會達到同位檢查的記憶體中模型支援廣泛的資料來源能夠處理導出的資料表和資料行，在 DirectQuery 模型中，透過 DAX 運算式，以連線到後端資料庫中，且查詢的資料列層級安全性導致更快速的輸送量的最佳化。
  
 您可在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中使用表格式模型專案範本所提供的設計介面以建立模型、資料表、關聯性和 DAX 運算式，藉此撰寫表格式模型。 您可以從多個來源匯入資料，然後加入關聯性、計算資料表和資料行、量值、KPI、階層及翻譯，來充實模型。  
  
 模型可以再部署到 Azure Analysis Services 或 SQL Server Analysis Services 的執行個體設定為表格式伺服器模式。 SQL Server Management Studio 中，可以管理已部署表格式模型。 當您的模型成長時，它們可以進行資料分割以最佳化處理和保護，以資料列層級使用以角色為基礎的安全性。  
  
## <a name="in-this-section"></a>本節內容  
 [表格式模型方案](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md)-本節文章說明建立和部署表格式模型方案。
  
 [表格式模型資料庫](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)-本節文章說明管理已部署的表格式模型方案。
  
 [表格式模型資料存取](../../analysis-services/tabular-models/tabular-model-data-access.md)-本節文章說明連接到部署表格式模型方案。
  
## <a name="see-also"></a>另請參閱  
 [新功能 Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [比較表格式和多維度解決方案](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [工具和 Analysis Services 中使用的應用程式](../../analysis-services/tools-and-applications-used-in-analysis-services.md)   
 [DirectQuery 模式](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [相容性層級](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
