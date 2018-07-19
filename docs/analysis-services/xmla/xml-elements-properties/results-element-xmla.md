---
title: 結果元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7fc64d6b31f1b05d8bf5b4d1c80d75dff0583e86
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37968660"
---
# <a name="results-element-xmla"></a>results 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含的集合[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)所傳回的項目[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法使用[批次](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)命令。  
  
 **命名空間** `http://schemas.microsoft.com/analysisservices/2003/xmla-multipleresults`  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<return>  
   <results>  
      <root>...</root>  
   </results>  
</return>  
```  
  
## <a name="element-characteristics"></a>項目特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>項目關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[傳回](../../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
|子元素|[根目錄](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 如果**批次**藉由執行命令**Execute**方法**傳回**項目包含單一**結果**項目，而不是單一**根**項目。 內容**結果**項目，取決於用來執行設定**批次**命令。  
  
 針對非交易式**批次**命令**結果**項目包含一個**根**每個命令所執行的項目**批次**命令，是否在命令完成，不論成功或失敗。 針對異動**批次**命令**結果**項目只會包含一個**根**元素，其中包含內失敗之命令的錯誤資訊**批次**命令。  
  
## <a name="see-also"></a>另請參閱
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
