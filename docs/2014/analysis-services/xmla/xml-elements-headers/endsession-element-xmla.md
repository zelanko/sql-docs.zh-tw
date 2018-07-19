---
title: EndSession 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- EndSession Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#EndSession
- urn:schemas-microsoft-com:xml-analysis#EndSession
- microsoft.xml.analysis.endsession
helpviewer_keywords:
- EndSession element
ms.assetid: e64f1da4-5c83-40a2-b15e-837f5451bafa
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 32c76318f05dbb628dd23de825203429ee0a22f3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37148119"
---
# <a name="endsession-element-xmla"></a>EndSession 元素 (XMLA)
  在 SOAP 要求訊息中使用 SOAP 標頭，若要結束的執行個體上現有的工作階段[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 **命名空間**urn: schemas-microsoft-microsoft-schemas-microsoft-com:-分析  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <EndSession  
         xmlns="urn:schemas-microsoft-com:xml-analysis"  
         SessionId="string" />  
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
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|無|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|SessionId|必要的 `String` 屬性，可識別要結束的工作階段。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會使用全域唯一識別碼 (GUID) 來識別工作階段。|  
  
## <a name="remarks"></a>備註  
 `EndSession` 標頭元素屬於傳送至 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體上現有且明確啟動之工作階段的 SOAP 要求的一部分。 如果 `EndSession` 標頭元素已傳送，但是其中包含不再有效的工作階段識別碼，系統就會傳回一個 SOAP 錯誤，表示找不到工作階段。  
  
## <a name="see-also"></a>另請參閱  
 [BeginSession 元素&#40;XMLA&#41;](session-element-xmla.md)   
 [工作階段項目&#40;XMLA&#41;](session-element-xmla.md)   
 [管理連接和工作階段&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [標頭&#40;XMLA&#41;](xml-elements-headers.md)  
  
  
