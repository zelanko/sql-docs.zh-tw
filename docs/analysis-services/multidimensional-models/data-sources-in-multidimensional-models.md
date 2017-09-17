---
title: "多維度模型中的資料來源 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- metadata [Analysis Services]
- Analysis Services objects, data sources
- storing data [Analysis Services], data sources
- data sources [Analysis Services], about data sources
- security [Analysis Services], data sources
- data sources [Analysis Services]
- storage [Analysis Services], data sources
ms.assetid: a16469d9-9d53-4e35-9982-fc06327a9d33
caps.latest.revision: 45
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fb419325bc8490fdfb62fb044cb81c81e111e6e3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="data-sources-in-multidimensional-models"></a>多維度模型中的資料來源
  您匯入或載入多維度模型的所有資料都源自於外部資料來源。 一般來說，來源資料來自於針對報表用途所設計的資料倉儲，但是也可能來自於透過中繼者直接或間接存取的任何關聯式資料庫，例如 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝。  
  
 **中的** 資料來源 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件會指定與外部資料來源的直接連接。 除了實體位置之外，資料來源物件還會指定連接字串、資料提供者、認證，以及控制連接行為的其他屬性。  
  
 在以下的作業期間會使用資料來源物件所提供的資訊：  
  
-   取得結構描述資訊和其他中繼資料，這些資料用來將資料來源檢視產生到模型中。  
  
-   在處理期間查詢資料或將資料載入模型內。  
  
-   對多維度或使用 ROLAP 儲存模式的資料採礦模型執行查詢。  
  
-   讀取或寫入遠端資料分割。  
  
-   連接到連結的物件，以及從目標同步到來源。  
  
-   執行更新儲存在關聯式資料庫中之事實資料表資料的回寫作業。  
  
 由下而上建立多維度模型時，一開始會建立資料來源物件，然後使用該資料來源物件產生下一個物件： **資料來源檢視**。 資料來源檢視是模型中的資料抽象層， 通常會在資料來源物件之後建立，並使用來源資料庫的結構描述做為基礎。 不過，您可以選擇其他方式來建立模型，包括從 Cube 和維度開始，然後產生最能支援您的設計之結構描述。  
  
 不論您的建立方式為何，每個模型至少都需要一個指定來源資料連接的資料來源物件。 您可以在單一模型中建立多個資料來源物件，使用來自不同來源的資料，或針對特定物件改變連接屬性。  
  
 您可以將資料來源物件與模型中的其他物件分開管理。 建立資料來源之後，您可以在稍後變更其屬性，然後對模型進行前置處理以確保正確擷取資料。  
  
## <a name="related-topics-and-tasks"></a>相關主題和工作  
  
|主題|說明|  
|-----------|-----------------|  
|[支援的資料來源 &#40;SSAS - 多維度&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)|描述可在多維度模型中使用的資料來源類型。|  
|[建立資料來源 &#40;SSAS 多維度&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)|說明如何將資料來源物件加入至多維度模型。|  
|[在方案總管中刪除資料來源 &#40;SSAS 多維度&#41;](../../analysis-services/multidimensional-models/delete-a-data-source-in-solution-explorer-ssas-multidimensional.md)|使用此程序從多維度模型中刪除資料來源物件。|  
|[設定資料來源屬性 &#40;SSAS 多維度&#41;](../../analysis-services/multidimensional-models/set-data-source-properties-ssas-multidimensional.md)|描述每個屬性，並說明如何設定每個屬性。|  
|[設定模擬選項 &#40;SSAS - 多維度&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)|說明如何設定 [模擬資訊] 對話方塊中的選項。|  
  
## <a name="see-also"></a>請參閱＜  
 [資料庫物件 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [邏輯架構 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [多維度模型中的資料來源檢視](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [資料來源和繫結 &#40;SSAS 多維度 &#41;](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)  
  
  
