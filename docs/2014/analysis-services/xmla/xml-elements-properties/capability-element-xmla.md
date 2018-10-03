---
title: Capability 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Capability Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Capability
- http://schemas.microsoft.com/analysisservices/2003/engine#Capability
- microsoft.xml.analysis.capability
helpviewer_keywords:
- Capability element
ms.assetid: 544a733e-77fc-48a0-8f92-9cd1fdbcf824
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7c6fd189a44ec34283e87cd220f2c582f982ffa9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48105338"
---
# <a name="capability-element-xmla"></a>Capability 元素 (XMLA)
  表示父項中的通訊協定功能的支援[ProtocolCapabilities](../xml-elements-headers/protocolcapabilities-element-xmla.md)標頭項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ProtocolCapabilities>  
   ...  
   <Capability>...</Capability>  
   ...  
</ProtocolCapabilities>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ProtocolCapabilities](../xml-elements-headers/protocolcapabilities-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 `Capability`項目表示的包含的應用程式，都支援特定功能，例如二進位或壓縮， `ProtocolCapabilities` SOAP 標頭在 SOAP 要求，或執行個體中的標頭項目[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]包含`ProtocolCapabilities`SOAP 回應的 SOAP 標頭中的標頭項目。 `Capability` 元素的值就是要支援之功能的名稱。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支援下表中所列的功能。  
  
|功能名稱|描述|  
|---------------------|-----------------|  
|sx|二進位 XML 支援|  
|xpress|壓縮支援|  
  
## <a name="see-also"></a>另請參閱  
 [管理連接和工作階段&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
