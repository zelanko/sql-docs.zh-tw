---
title: XML for Analysis (XMLA) 參考 |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4e8c3645175d8d1f3251fd621825f5a542669cbb
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34576760"
---
# <a name="xml-for-analysis--xmla-reference"></a>XML for Analysis (XMLA) 參考
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]   

Azure Analysis Services 和 SQL Server Analysis Services 使用 XML for Analysis (XMLA) 通訊協定，用戶端應用程式與 Analysis Services 執行個體間的通訊。 在最基本的層級上，其他用戶端程式庫 (例如 ADOMD.NET 和 AMO) 會以 XMLA 建構要求及解碼回應，當做 Analysis Services 執行個體 (以獨佔方式使用 XMLA) 的中繼。  
  
 若要支援探索和操作資料的表格式和多維度模式中，XMLA 規格會定義兩種普遍可存取的方法，[探索](../../analysis-services/xmla/xml-elements-methods-discover.md)和[Execute](../../analysis-services/xmla/xml-elements-methods-execute.md)，和XML 項目和資料類型的集合。 由於 XML 允許鬆散偶合的用戶端與伺服器架構，因此這兩種方法會處理採用 XML 格式的傳入和傳出資訊。 

Analysis Services 與 XMLA 1.1  規格，但還擴充它包含資料定義和管理功能，實為註解上**探索**和**Execute**方法。 擴充的 XML 語法來為 Tabular Model Scripting Language (TMSL) 和 Analysis Services 指令碼語言 (ASSL)。 

TMSL 是語法命令和物件模型定義的相容性層級 1200年 （含） 以上的表格式模型資料庫。 TMSL 與 Analysis Services 通訊透過 XMLA 通訊協定，其中`XMLA.Execute`方法接受 JSON 型陳述式以 TMSL 指令碼，以及傳統的 XML 架構指令碼在 Analysis Services 指令碼語言 (ASSL xmla) 中。 若要進一步了解，請參閱[Tabular Model Scripting Language (TMSL) 參考](../tabular-model-scripting-language-tmsl-reference.md)。

ASSL 是語法命令和物件模型定義多維度模型資料庫和表格式模式資料庫相容性層級 1103年或更低。 這個定義是根據 XMLA 規格而不會中斷它。 不論您只使用 XMLA 還是 XMLA 和 ASSL 一起使用，都會確保以 XMLA 為根據的互通性。 若要進一步了解，請參閱[Analysis Services 指令碼語言 (ASSL xmla)](../scripting/analysis-services-scripting-language-assl-for-xmla.md)。
  
 身為開發人員，您可以為介面使用 XMLA，如果解決方案需求指定標準通訊協定，例如 XML、 SOAP 和 HTTP。 開發人員和管理員也可以使用 XMLA 臨機操作為基礎來從伺服器擷取資訊或執行命令。 
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[XML 資料類型 (XMLA)](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)|描述 XMLA 規格中的資料類型。|  
|[XML 項目-命令 (XMLA)](../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)|Execute 方法呼叫期間可以使用命令項目內的項目。|  
|[XML 項目-命令 (XMLA)](../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)|Execute 方法呼叫期間可以使用命令項目內的項目。|  
|[XML 項目-標頭 (XMLA)](../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)| Microsoft Analysis Services 所實作的標頭元素。|  
|[XML 項目-屬性 (XMLA)](../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)| 代表屬性資訊和 XMLA 標頭、 方法、 物件、 命令和資料類型值的項目。|  
|[XML 項目-方法-探索 (XMLA)](../../analysis-services/xmla/xml-elements-methods-discover.md)| 從 Analysis Services 的執行個體中擷取資訊，例如可用的資料庫或有關特定物件的詳細資料的清單。|  
|[XML 項目-方法-執行 (XMLA)](../../analysis-services/xmla/xml-elements-methods-execute.md)| 將 XML for Analysis (XMLA) 命令傳送到 Analysis Services 的執行個體。|  
|[XML 項目物件-DiscoverResponse (XMLA)](../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)| 包含探索方法呼叫的回應中的 Analysis Services 執行個體所傳回的資訊。|  
|[XML 項目物件-ExecuteResponse (XMLA)](../../analysis-services/xmla/xml-elements-objects-executeresponse.md)| 包含 Execute 方法呼叫的回應中的 Analysis Services 執行個體所傳回的資訊。|  
|[XML 項目-物件 (XMLA)](../../analysis-services/xmla/xml-elements-objects.md)| Analysis Services 所實作的物件。|  
|[XML for Analysis 合規性 (XMLA)](../../analysis-services/xmla/xml-for-analysis-compliance-xmla.md)|描述符合 XMLA 1.1 規格的層級。|  
  
## <a name="see-also"></a>另請參閱
 [XML for Analysis 結構描述資料列集](../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
 [使用 ADOMD.NET 來開發](../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)  
 [使用分析管理物件 &#40;AMO&#41; 來開發](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)  
