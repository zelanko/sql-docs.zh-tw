---
title: Session 元素 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Session Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.session
- http://schemas.microsoft.com/analysisservices/2003/engine#Session
- urn:schemas-microsoft-com:xml-analysis#Session
helpviewer_keywords:
- Session element
ms.assetid: 884ed090-968e-41d3-97e5-6d12787467da
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c033153f19ce1456b0558a95a85ad6caab778be5
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="session-element-xmla"></a>Session 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]在 SOAP 要求訊息中使用 SOAP 標頭，來識別現有的明確工作階段的執行個體上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 **命名空間**描述 urn:-microsoft-schemas-microsoft-com:-分析  
  
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
|SessionId|需要**字串**屬性，可識別要使用工作階段。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會使用全域唯一識別碼 (GUID) 來識別工作階段。|  
  
## <a name="remarks"></a>備註  
 **工作階段**標頭項目上識別現有且明確啟動工作階段[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。 **工作階段**項目是在下列類型的訊息的 SOAP 標頭的一部分：  
  
-   SOAP 回應，其中包含[BeginSession](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md) SOAP 標頭項目。  
  
-   識別要執行的工作階段的 SOAP 要求[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)或[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
 工作階段識別碼並不保證工作階段會維持有效狀態。 指定的工作階段**工作階段**項目可能會過期。 例如，如果工作階段逾時或是與工作階段有關的連接中斷，則此工作階段可能會過期。 如果此工作階段過期而不再有效，則 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會結束此工作階段，並回復目前進行中的任何交易。 與不再有效的工作階段識別碼一起傳送的任何 SOAP 訊息都會失敗，而且會出現一個 SOAP 錯誤，表示找不到指定的工作階段。  
  
 如果**工作階段**項目不會傳送 SOAP 要求，一部分[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體會以隱含方式開始的工作階段的持續時間**探索**或**Execute**方法呼叫中，然後再結束方法呼叫完成該工作階段。  
  
## <a name="see-also"></a>請參閱  
 [EndSession 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)   
 [管理連接和工作階段 &#40;XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [標頭 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
