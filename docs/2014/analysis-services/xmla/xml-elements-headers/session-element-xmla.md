---
title: Session 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Session Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.session
- http://schemas.microsoft.com/analysisservices/2003/engine#Session
- urn:schemas-microsoft-com:xml-analysis#Session
helpviewer_keywords:
- Session element
ms.assetid: 884ed090-968e-41d3-97e5-6d12787467da
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a2f18754a2ef7d44a2a85bb9da78378bc631ecd0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48080388"
---
# <a name="session-element-xmla"></a>Session 元素 (XMLA)
  在 SOAP 要求訊息中使用 SOAP 標頭，以識別現有的明確工作階段的執行個體上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 **命名空間**urn: schemas-microsoft-microsoft-schemas-microsoft-com:-分析  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <Session  
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
|資料類型和長度|None|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|None|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|SessionId|必要的 `String` 屬性，可識別要使用的工作階段。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會使用全域唯一識別碼 (GUID) 來識別工作階段。|  
  
## <a name="remarks"></a>備註  
 `Session` 標頭元素會在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體上識別現有且明確啟動的工作階段。 `Session` 元素屬於下列訊息類型中 SOAP 標頭的一部分：  
  
-   包含的 SOAP 回應[BeginSession](session-element-xmla.md) SOAP 標頭項目。  
  
-   SOAP 要求，識別要執行的工作階段[Discover](../xml-elements-methods-discover.md)或是[Execute](../xml-elements-methods-execute.md)方法。  
  
 工作階段識別碼並不保證工作階段會維持有效狀態。 在 `Session` 元素中指定的工作階段可能會過期。 例如，如果工作階段逾時或是與工作階段有關的連接中斷，則此工作階段可能會過期。 如果此工作階段過期而不再有效，則 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會結束此工作階段，並回復目前進行中的任何交易。 與不再有效的工作階段識別碼一起傳送的任何 SOAP 訊息都會失敗，而且會出現一個 SOAP 錯誤，表示找不到指定的工作階段。  
  
 如果 `Session` 元素沒有當做 SOAP 要求的一部分傳送，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體就會在 `Discover` 或 `Execute` 方法呼叫的持續時間內隱含地啟動工作階段，然後在方法呼叫完成時結束該工作階段。  
  
## <a name="see-also"></a>另請參閱  
 [EndSession 元素&#40;XMLA&#41;](endsession-element-xmla.md)   
 [管理連接和工作階段&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [標頭&#40;XMLA&#41;](xml-elements-headers.md)  
  
  
