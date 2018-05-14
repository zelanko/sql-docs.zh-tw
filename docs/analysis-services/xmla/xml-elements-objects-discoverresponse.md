---
title: DiscoverResponse 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1650c2e50f4051bd30d0e47736de4d798b44745f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="xml-elements---objects---discoverresponse"></a>XML 項目物件-DiscoverResponse
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  包含執行個體所傳回的資訊[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]回應[探索](../../analysis-services/xmla/xml-elements-methods-discover.md)方法呼叫。  
  
 **命名空間**描述 urn:-microsoft-schemas-microsoft-com:-分析  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DiscoverResponse>  
   <return>  
</DiscoverResponse>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[傳回](../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **DiscoverResponse**項目是最上層的項目之 SOAP 回應的主體內**探索**方法。  
  
## <a name="see-also"></a>另請參閱  
 [ExecuteResponse 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-objects-executeresponse.md)   
 [物件&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-objects.md)  
  
  
