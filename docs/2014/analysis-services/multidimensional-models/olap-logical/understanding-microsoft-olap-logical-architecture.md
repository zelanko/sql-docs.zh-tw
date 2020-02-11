---
title: 邏輯架構（Analysis Services-多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Analysis Services, architecture
- logical architecture [Analysis Services Multidimensional Data]
ms.assetid: 1b9cae0a-8990-4194-af5f-a1ea5f2aff06
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 074659d42e1960c5f24cf4afa20668a3d8c823b0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62725482"
---
# <a name="logical-architecture-analysis-services---multidimensional-data"></a>邏輯架構 (Analysis Services - 多維度資料)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]會使用伺服器和用戶端元件，為商業智慧應用程式提供線上分析處理（OLAP）和資料採礦[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]功能：  
  
-   
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的伺服器元件是以 Microsoft Windows 服務的形式實作。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]支援同一部電腦上的多個實例，每個[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]實例都實作為個別的 Windows 服務實例。  
  
-   用戶端使用公用標準 XML for Analysis (XMLA) 與 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 通訊；而 XMLA 是一種用於發出命令和接收回應的 SOAP 型通訊協定，並以 Web 服務的形式公開。 用戶端物件模型也可透過 XMLA 予以提供，且可使用 Managed 提供者 (例如 ADOMD.Net) 或原生 OLE DB 提供者進行存取。  
  
-   可以使用下列語言發出查詢命令：SQL、多維度運算式 (MDX) (進行分析的業界標準查詢語言)，或資料採礦延伸模組 (DMX) (資料採礦導向的業界標準查詢語言)。 也可以使用 Analysis Services 指令碼語言 (ASSL) 來管理 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫物件。  
  
 
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 也支援本機 Cube 引擎，讓中斷連接之用戶端上的應用程式可瀏覽儲存在本機的多維度資料。 如需詳細資訊，請參閱[Analysis Services 開發的用戶端架構需求](../olap-physical/client-architecture-requirements-for-analysis-services-development.md)  
  
## <a name="in-this-section"></a>本節內容  
 **邏輯架構概觀**  
 [邏輯架構總覽 &#40;Analysis Services-多維度資料&#41;](logical-architecture-overview-analysis-services-multidimensional-data.md)  
  
 **伺服器物件**  
 [伺服器物件 &#40;Analysis Services 多維度資料&#41;](server-objects-analysis-services-multidimensional-data.md)  
  
 **資料庫物件**  
 [資料庫物件 &#40;Analysis Services 多維度資料&#41;](database-objects-analysis-services-multidimensional-data.md)  
  
 **維度物件**  
 [維度物件 &#40;Analysis Services 多維資料&#41;](../../multidimensional-models-olap-logical-dimension-objects/dimension-objects-analysis-services-multidimensional-data.md)  
  
 **Cube 物件**  
 [Cube 物件 &#40;Analysis Services 多維度資料&#41;](../../multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)  
  
 **使用者存取安全性**  
 [使用者存取安全性架構](understanding-microsoft-olap-logical-architecture.md)  
  
## <a name="see-also"></a>另請參閱  
 [瞭解 Microsoft OLAP 架構](../olap-physical/understanding-microsoft-olap-architecture.md)   
 [實體架構 &#40;Analysis Services-多維度資料&#41;](../olap-physical/understanding-microsoft-olap-physical-architecture.md)  
  
  
