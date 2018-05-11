---
title: Capability 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile"
ms.openlocfilehash: a53bcd66141dfb367cc54239d9d8faab0e0e6576
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="capability-element-xmla"></a>Capability 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  表示父系中的通訊協定功能的支援[ProtocolCapabilities](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md)標頭項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ProtocolCapabilities>  
   ...  
   <Capability>...</Capability>  
   ...  
</ProtocolCapabilities>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ProtocolCapabilities](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **功能**項目表示的 包含的應用程式，都支援特定功能，例如二進位或壓縮， **ProtocolCapabilities**標頭中的項目SOAP 標頭在 SOAP 要求，或執行個體[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]包含**ProtocolCapabilities** SOAP 回應的 SOAP 標頭中的標頭項目。 值**功能**項目是必須支援功能的名稱。  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支援下表中所列的功能。  
  
|功能名稱|描述|  
|---------------------|-----------------|  
|sx|二進位 XML 支援|  
|xpress|壓縮支援|  
  
## <a name="see-also"></a>另請參閱  
 [管理連接和工作階段 & #40;XMLA & #41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
