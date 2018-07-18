---
title: ExecuteResponse 元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a1ff44c8e2fb23e40aac30e70c73b4d260145bfd
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979116"
---
# <a name="xml-elements---objects---executeresponse"></a>XML 元素-物件-ExecuteResponse
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  包含 Analysis services 執行個體，以回應所傳回的資訊[Execute](../../analysis-services/xmla/xml-elements-methods-execute.md)方法呼叫。  
  
 **命名空間**urn: schemas-microsoft-microsoft-schemas-microsoft-com:-分析  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ExecuteResponse>  
   <return>  
</ExecuteResponse>  
```  
  
## <a name="element-characteristics"></a>項目特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>項目關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[傳回](../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **ExecuteResponse**項目是最上層的項目之 SOAP 回應的主體內**Execute**方法。  
  
## <a name="see-also"></a>另請參閱
 [DiscoverResponse 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)   
 [物件&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-objects.md)  
  
  
