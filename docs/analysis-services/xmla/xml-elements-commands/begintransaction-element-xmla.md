---
title: "BeginTransaction 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- BeginTransaction Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#BeginTransaction
- microsoft.xml.analysis.begintransaction
- http://schemas.microsoft.com/analysisservices/2003/engine#BeginTransaction
helpviewer_keywords:
- BeginTransaction command
ms.assetid: fca122fc-b57c-4ba6-849b-ca8c93cf64e9
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 677ad07e9ce6206bbc4e7946ec111f8865bcfcce
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="begintransaction-element-xmla"></a>BeginTransaction 元素 (XMLA)
  執行個體的目前工作階段上開始交易[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <BeginTransaction />  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **BeginTransaction**命令會開始在目前工作階段的作用中交易。 如果使用中交易已經存在，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體就會遞增目前工作階段之交易的參考計數。 如果沒有，此執行個體就會開始新的交易並將目前工作階段的參考計數設定為 1。 如果使用明確指定使用中交易**BeginTransaction**命令時，所有後續命令明確指定交易內執行。  
  
 當目前的工作階段結束而且交易的參考計數大於零時，系統就會回復所有使用中交易。  
  
 如果目前的工作階段上沒有任何明確指定的使用中交易，在目前工作階段上發出的每個命令都會在隱含定義的交易內部執行。 如果命令成功，就會認可隱含交易，但是如果命令失敗，則會回復隱含交易。  
  
## <a name="see-also"></a>另請參閱  
 [取消元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)   
 [CommitTransaction 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)   
 [RollbackTransaction 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)   
 [命令 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  

