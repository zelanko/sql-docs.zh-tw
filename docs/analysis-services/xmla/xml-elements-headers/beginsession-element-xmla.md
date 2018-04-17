---
title: BeginSession 元素 (XMLA) |Microsoft 文件
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
- BeginSession Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#BeginSession
- urn:schemas-microsoft-com:xml-analysis#BeginSession
- microsoft.xml.analysis.beginsession
helpviewer_keywords:
- BeginSession element
ms.assetid: 49873a97-58d7-42a9-ab7f-e045e2856737
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b35ff5467daa888cfc9eefa47a7e2cf48b037946
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="beginsession-element-xmla"></a>BeginSession 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]用於 SOAP 標頭在 SOAP 要求訊息中的執行個體上啟動新的工作階段[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 **命名空間**描述 urn:-microsoft-schemas-microsoft-com:-分析  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">  
   <soap:Header>  
      ...  
      <BeginSession  
         xmlns="urn:schemas-microsoft-com:xml-analysis" />  
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
  
## <a name="remarks"></a>備註  
 **BeginSession**標頭元素屬於的 SOAP 要求傳送至[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體，且明確啟動新的工作階段的執行個體上。 SOAP 回應所傳回的 SOAP 標頭包含[工作階段](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)項目會識別新的工作階段。 這個新的工作階段識別項可儲存及後續使用的 SOAP 要求中傳送**工作階段**標頭項目。  
  
 如果**BeginSession**不會傳送標頭項目、 尚未明確啟動工作階段。 如果沒有明確啟動工作階段，就無法管理該工作階段上的交易。 換句話說，您無法使用下列 XML for Analysis (XMLA) 命令： [BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)， [CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)，和[RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)。 所有在明確啟動之執行個體上執行的 XMLA 方法和命令都會被視為不可部分完成的交易。  
  
## <a name="see-also"></a>請參閱  
 [EndSession 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)   
 [Session 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)   
 [管理連接和工作階段 &#40;XMLA &#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [標頭 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-headers/xml-elements-headers.md)  
  
  
