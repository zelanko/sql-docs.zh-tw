---
title: "RollbackTransaction 元素 (XMLA) |Microsoft 文件"
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
- RollbackTransaction Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#RollbackTransaction
- microsoft.xml.analysis.rollbacktransaction
- urn:schemas-microsoft-com:xml-analysis#RollbackTransaction
helpviewer_keywords:
- RollbackTransaction command
ms.assetid: 40e7dc00-656f-412f-97f0-d05bf7caa196
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a74a55f0d5325ca37b47ce0544bfe7dab44dfef6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="rollbacktransaction-element-xmla"></a>RollbackTransaction 元素 (XMLA)
  目前的工作階段與執行個體上的交易回復[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <RollbackTransaction />  
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
 **RollbackTransaction**命令會回復所有使用中交易，使用明確定義**BeginTransaction**項目，目前工作階段上的。 如果使用中交易尚未存在，就會發生錯誤。 如果使用中交易已經存在，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體就會將目前工作階段之交易的參考計數遞減至零，並回復所有使用中交易。  
  
## <a name="see-also"></a>另請參閱  
 [BeginTransaction 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)   
 [取消元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)   
 [CommitTransaction 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)   
 [命令 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  

