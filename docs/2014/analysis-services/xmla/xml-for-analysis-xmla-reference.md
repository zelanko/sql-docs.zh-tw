---
title: XML for Analysis (XMLA) 參考 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, reference
- XMLA, reference
ms.assetid: 88045e05-ce47-4e28-999b-7f9c74af9faf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fde04360c7b6af1c9bf6aa906328e5031eb76c32
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164438"
---
# <a name="xml-for-analysis--xmla-reference"></a>XML for Analysis (XMLA) 參考
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 您可以使用 XML for Analysis (XMLA) 通訊協定來處理用戶端應用程式與 Analysis Services 執行個體之間的所有通訊。 在最基本的層級上，其他用戶端程式庫 (例如 ADOMD.NET 和 AMO) 會以 XMLA 建構要求及解碼回應，當做 Analysis Services 執行個體 (以獨佔方式使用 XMLA) 的中繼。  
  
 為了支援探索和操作資料的多維度和表格式格式，XMLA 規格定義兩種普遍可存取的方法， [Discover](xml-elements-methods-discover.md)並[Execute](xml-elements-methods-execute.md)，和XML 元素和資料類型的集合。 由於 XML 允許鬆散偶合的用戶端與伺服器架構，因此這兩種方法會處理採用 XML 格式的傳入和傳出資訊。 Analysis Services 與 XMLA 1.1  規格相容，但是也會擴充它來包含資料定義與操作功能，實作為 `Discover` 和 `Execute` 方法上的註解。 擴充的 XML 語法稱為 Analysis Services 指令碼語言 (ASSL)。 ASSL 會根據 XMLA 規格建立，而不會打破此規格。 不論您只使用 XMLA 還是 XMLA 和 ASSL 一起使用，都會確保以 XMLA 為根據的互通性。  
  
 身為程式設計人員，如果解決方案需求指定標準通訊協定 (例如 XML、SOAP 和 HTTP)，您可以使用 XMLA 當做程式設計介面。 程式設計人員和系統管理員也可以隨選使用 XMLA，以擷取伺服器中的資訊或執行命令。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[XML 項目&#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)|描述 XMLA 規格中的元素。|  
|[XML 資料型別&#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)|描述 XMLA 規格中的資料類型。|  
|[XML for Analysis 符合&#40;XMLA&#41;](xml-for-analysis-compliance-xmla.md)|描述符合 XMLA 1.1 規格的層級。|  
  
## <a name="related-sections"></a>相關章節  
 [使用 Analysis Services 開發的指令碼語言&#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)  
  
 [XML for Analysis 結構描述資料列集](../schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
 [使用 ADOMD.NET 來開發](../multidimensional-models/adomd-net/developing-with-adomd-net.md)  
  
 [使用分析管理物件開發&#40;AMO&#41;](../multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)  
  
## <a name="see-also"></a>另請參閱  
 [了解 Microsoft OLAP 架構](../multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
