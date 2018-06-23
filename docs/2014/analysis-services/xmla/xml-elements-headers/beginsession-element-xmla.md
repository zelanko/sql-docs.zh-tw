---
title: BeginSession 元素 (XMLA) |Microsoft 文件
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
caps.latest.revision: 16
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 2982709512433e5a6b87929f3a4efba4f77138b8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034848"
---
# <a name="beginsession-element-xmla"></a>BeginSession 元素 (XMLA)
  用於 SOAP 標頭在 SOAP 要求訊息中的執行個體上啟動新的工作階段[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
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
 `BeginSession` 標頭元素屬於傳送給 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體之 SOAP 要求的一部分，而且它會在該執行個體上明確啟動新的工作階段。 SOAP 回應所傳回的 SOAP 標頭包含[工作階段](session-element-xmla.md)項目會識別新的工作階段。 這個新工作階段識別碼將使用 `Session` 標頭元素在後續的 SOAP 要求中儲存並傳送。  
  
 如果沒有傳送 `BeginSession` 標頭元素，就不會明確啟動工作階段。 如果沒有明確啟動工作階段，就無法管理該工作階段上的交易。 換句話說，您無法使用下列 XML for Analysis (XMLA) 命令： [BeginTransaction](../xml-elements-commands/begintransaction-element-xmla.md)， [CommitTransaction](../xml-elements-commands/committransaction-element-xmla.md)，和[RollbackTransaction](../xml-elements-commands/rollbacktransaction-element-xmla.md)。 所有在明確啟動之執行個體上執行的 XMLA 方法和命令都會被視為不可部分完成的交易。  
  
## <a name="see-also"></a>另請參閱  
 [EndSession 元素&#40;XMLA&#41;](endsession-element-xmla.md)   
 [工作階段項目&#40;XMLA&#41;](session-element-xmla.md)   
 [管理連接與工作階段&#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [標頭&#40;XMLA&#41;](xml-elements-headers.md)  
  
  