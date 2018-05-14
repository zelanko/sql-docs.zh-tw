---
title: RollbackTransaction 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f01725ea3f718b95f0ae4eaf4b88bd6636085d0
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="rollbacktransaction-element-xmla"></a>RollbackTransaction 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
 [BeginTransaction 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)   
 [Cancel 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)   
 [CommitTransaction 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)   
 [命令 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
