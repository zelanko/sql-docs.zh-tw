---
title: BeginTransaction 元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb4a4dea3658ad03fd6205f9076bd1cb65ca9ba7
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38038376"
---
# <a name="begintransaction-element-xmla"></a>BeginTransaction 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  開始上的 Analysis Services 執行個體的目前工作階段的交易。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <BeginTransaction />  
</Command>  
```  
  
## <a name="element-characteristics"></a>項目特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>項目關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **BeginTransaction**命令開始在目前的工作階段上使用中交易。 如果使用中交易已經存在，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體就會遞增目前工作階段之交易的參考計數。 如果沒有，此執行個體就會開始新的交易並將目前工作階段的參考計數設定為 1。 如果使用明確指定作用中的交易**BeginTransaction**命令，明確指定的交易內執行所有後續的命令。  
  
 當目前的工作階段結束而且交易的參考計數大於零時，系統就會回復所有使用中交易。  
  
 如果目前的工作階段上沒有任何明確指定的使用中交易，在目前工作階段上發出的每個命令都會在隱含定義的交易內部執行。 如果命令成功，就會認可隱含交易，但是如果命令失敗，則會回復隱含交易。  
  
## <a name="see-also"></a>另請參閱
 [Cancel 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)   
 [CommitTransaction 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)   
 [RollbackTransaction 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)   
 [命令&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
