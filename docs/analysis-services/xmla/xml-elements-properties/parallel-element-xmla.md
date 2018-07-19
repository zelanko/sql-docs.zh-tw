---
title: Parallel 元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 88e7cf2387c8ee45936b5de21f529e142142d02c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38050407"
---
# <a name="parallel-element-xmla"></a>Parallel Element (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  指定多少處理作業平行執行的使用父系[批次](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Batch>  
   ....  
   <Parallel maxParallel="Integer">  
      <!-- An XMLA process command -->  
   </Parallel>  
   ....  
</Batch>  
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
|父元素|[批次](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)|  
|子元素|[Process 元素](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|maxParallel|選擇性 **Integer** 屬性。 表示要以平行方式執行命令的最大執行緒數目。 如果未指定，或設為 0，Analysis Services 執行個體決定最佳的電腦上可用的處理器數目為基礎的執行緒數目。|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
