---
title: ProtocolCapabilities 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ProtocolCapabilities Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.protocolcapabilities
- http://schemas.microsoft.com/analysisservices/2003/engine#ProtocolCapabilities
- urn:schemas-microsoft-com:xml-analysis#ProtocolCapabilities
helpviewer_keywords:
- ProtocolCapabilities element
ms.assetid: f923896a-3f32-46a3-9543-388c30b3465d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 12e4cac0c9846582c40213048e71c7f3793ff736
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219038"
---
# <a name="protocolcapabilities-element-xmla"></a>ProtocolCapabilities 元素 (XMLA)
  在 SOAP 要求訊息中使用 SOAP 標頭，來識別的執行個體之間的通訊協定功能[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]和用戶端應用程式。  
  
 **命名空間** http://schemas.microsoft.com/analysisservices/2003/engine  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <ProtocolCapabilities xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
         <Capability>...</Capability>  
      </ProtocolCapabilities>  
      ...  
   </soap:Header>  
   <soap:Body>  
      ...  
   </soap:Body>  
</soap:Envelope>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[功能](../xml-elements-properties/capability-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `ProtocolCapabilities` 元素可讓用戶端應用程式隨時與 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體交涉通訊協定功能，例如二進位 XML 或壓縮支援。 通訊協定交涉包含下列步驟：  
  
1.  用戶端應用程式所傳送的 SOAP 要求，包括識別其通訊協定功能`ProtocolCapabilities`元素當做 SOAP 標頭的一部分。  
  
2.  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體收到並處理此 SOAP 要求。  
  
3.  如果 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體與提出要求的應用程式具有相同的通訊協定功能，此執行個體就會傳送 SOAP 回應 (包含 SOAP 要求中傳送的相同 `ProtocolCapabilities` 元素)，表示通訊協定已經成功交涉。 否則，通訊協定功能不會成功交涉，而且此執行個體會傳回 SOAP 錯誤。  
  
 成功交涉通訊協定功能，時間長度用戶端應用程式之後，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]根據工作階段是否明確或隱含的執行個體使用特定通訊協定而定：  
  
-   為明確工作階段會使用建立的其中一個[BeginSession](session-element-xmla.md)標頭項目。 為明確工作階段中，傳送新的用戶端應用程式之前，都會使用交涉的通訊協定`ProtocolCapabilities`項目或工作階段隨即結束。  
  
-   隱含工作階段是指 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體所建立而且用戶端應用程式在提交 SOAP 要求時並未明確指定的工作階段。 若為隱含工作階段，交涉的通訊協定就只會使用到 SOAP 要求完成為止。  
  
 通訊協定功能不需要明確交涉。 也就是用戶端應用程式並沒有包含`ProtocolCapabilities`元素當做 SOAP 要求的一部分。 如果 SOAP 要求沒有包含 `ProtocolCapabilities` 元素，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體就會使用與 SOAP 要求相同的格式進行回應。  
  
## <a name="see-also"></a>另請參閱  
 [管理連接和工作階段&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [標頭&#40;XMLA&#41;](xml-elements-headers.md)  
  
  
