---
title: 邏輯架構 (Analysis Services-多維度資料) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6b6b33ffbf59cf05bc5455d3daac437e9e79407c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34023245"
---
# <a name="understanding-microsoft-olap-logical-architecture"></a>了解 Microsoft OLAP 邏輯架構
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]會使用伺服器和用戶端元件提供線上分析處理 (OLAP) 和商業智慧應用程式的資料採礦功能：  
  
-   [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的伺服器元件是以 Microsoft Windows 服務的形式實作。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]支援多個執行個體的相同電腦上，每個執行個體的[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]實作為 Windows 服務的個別執行個體。  
  
-   用戶端使用公用標準 XML for Analysis (XMLA) 與 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 通訊；而 XMLA 是一種用於發出命令和接收回應的 SOAP 型通訊協定，並以 Web 服務的形式公開。 用戶端物件模型也可透過 XMLA 予以提供，且可使用 Managed 提供者 (例如 ADOMD.Net) 或原生 OLE DB 提供者進行存取。  
  
-   可以使用下列語言發出查詢命令：SQL、多維度運算式 (MDX) (進行分析的業界標準查詢語言)，或資料採礦延伸模組 (DMX) (資料採礦導向的業界標準查詢語言)。 也可以使用 Analysis Services 指令碼語言 (ASSL) 來管理 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫物件。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 也支援本機 Cube 引擎，讓中斷連接之用戶端上的應用程式可瀏覽儲存在本機的多維度資料。 如需詳細資訊，請參閱[Analysis Services 開發的用戶端架構需求](../../../analysis-services/multidimensional-models/olap-physical/client-architecture-requirements-for-analysis-services-development.md)  
  
## <a name="in-this-section"></a>本節內容  
 **邏輯架構概觀**  
 [邏輯架構概觀 & #40;Analysis Services-多維度資料 & #41;](../../../analysis-services/multidimensional-models/olap-logical/logical-architecture-overview-analysis-services-multidimensional-data.md)  
  
 **伺服器物件**  
 [伺服器物件 & #40;Analysis Services-多維度資料 & #41;](../../../analysis-services/multidimensional-models/olap-logical/server-objects-analysis-services-multidimensional-data.md)  
  
 **資料庫物件**  
 [資料庫物件 & #40;Analysis Services-多維度資料 & #41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
 **維度物件**  
 [維度物件 & #40;Analysis Services-多維度資料 & #41;](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimension-objects-analysis-services-multidimensional-data.md)  
  
 **Cube 物件**  
 [Cube 物件 & #40;Analysis Services-多維度資料 & #41;](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)  
  
 **使用者存取安全性**  
 [使用者存取安全性架構](http://msdn.microsoft.com/library/71b44e10-2bd0-44f7-8de9-7c8f5b7ac082)  
  
## <a name="see-also"></a>另請參閱  
 [了解 Microsoft OLAP 架構](../../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)   
 [實體架構 & #40;Analysis Services-多維度資料 & #41;](../../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-physical-architecture.md)  
  
  
