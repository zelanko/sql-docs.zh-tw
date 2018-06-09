---
title: 方法 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 15f930695e13d824e70da748dad20cf574e9bc38
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34579140"
---
# <a name="xml-elements---methods"></a>XML 項目-方法
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  XML for Analysis (XMLA) 通訊協定會使用兩種方法，**探索**和**Execute**來提供應用程式存取的 Analysis Services 執行個體上的資訊的標準方式。 由於這些方法是使用簡易物件存取通訊協定 (SOAP) 叫用的，因此它們會接受使用 XML 格式的輸入並以 XML 格式傳遞輸出。 Analysis Services 會實作這兩種方法，遵照 XML for Analysis 1.1 規格。  
  
## <a name="in-this-section"></a>本節內容  
 下列主題說明 Analysis Services 所實作的 XMLA 方法。  
  
|方法|描述|  
|------------|-----------------|  
|[Discover 方法&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)|從 Analysis Services 的執行個體中擷取資訊，例如可用的資料庫或有關特定物件的詳細資料的清單。 與擷取的資料**探索**方法取決於參數傳遞給它的值。|  
|[Execute 方法&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)|將 XMLA 命令傳送至 Analysis Services 的執行個體。 這包括涉及資料傳輸的要求，例如擷取或更新伺服器資料的要求。|  
  
## <a name="see-also"></a>另請參閱
 [XML 項目&#40;XMLA&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [XML 資料型別&#40;XMLA&#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [XML 項目&#40;XMLA&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  
