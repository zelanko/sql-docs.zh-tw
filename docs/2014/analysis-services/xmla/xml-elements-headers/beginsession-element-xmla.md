---
title: BeginSession 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- BeginSession Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#BeginSession
- urn:schemas-microsoft-com:xml-analysis#BeginSession
- microsoft.xml.analysis.beginsession
helpviewer_keywords:
- BeginSession element
ms.assetid: 49873a97-58d7-42a9-ab7f-e045e2856737
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9194333e376dc8ab685057847c3f4156330d5dfa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48180058"
---
# <a name="beginsession-element-xmla"></a>BeginSession 元素 (XMLA)
  在 SOAP 要求訊息中使用 SOAP 標頭，以啟動新的工作階段的執行個體上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 **命名空間**urn: schemas-microsoft-microsoft-schemas-microsoft-com:-分析  
  
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
|資料類型和長度|None|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 `BeginSession` 標頭元素屬於傳送給 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體之 SOAP 要求的一部分，而且它會在該執行個體上明確啟動新的工作階段。 SOAP 回應所傳回的 SOAP 標頭包含[工作階段](session-element-xmla.md)項目會識別新的工作階段。 這個新工作階段識別碼將使用 `Session` 標頭元素在後續的 SOAP 要求中儲存並傳送。  
  
 如果沒有傳送 `BeginSession` 標頭元素，就不會明確啟動工作階段。 如果沒有明確啟動工作階段，就無法管理該工作階段上的交易。 換句話說，您無法使用下列 XML for Analysis (XMLA) 命令： [BeginTransaction](../xml-elements-commands/begintransaction-element-xmla.md)， [CommitTransaction](../xml-elements-commands/committransaction-element-xmla.md)，並[RollbackTransaction](../xml-elements-commands/rollbacktransaction-element-xmla.md)。 所有在明確啟動之執行個體上執行的 XMLA 方法和命令都會被視為不可部分完成的交易。  
  
## <a name="see-also"></a>另請參閱  
 [EndSession 元素&#40;XMLA&#41;](endsession-element-xmla.md)   
 [工作階段項目&#40;XMLA&#41;](session-element-xmla.md)   
 [管理連接和工作階段&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [標頭&#40;XMLA&#41;](xml-elements-headers.md)  
  
  
