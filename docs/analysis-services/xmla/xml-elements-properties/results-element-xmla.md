---
title: 結果元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a963b9128f6639ba9cd67bdfbd560d31f396ae41
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="results-element-xmla"></a>results 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含集合[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)所傳回的項目[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法使用[批次](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)命令。  
  
 **命名空間** `http://schemas.microsoft.com/analysisservices/2003/xmla-multipleresults`  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<return>  
   <results>  
      <root>...</root>  
   </results>  
</return>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[傳回](../../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
|子元素|[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 如果**批次**命令由執行**Execute**方法，**傳回**元素包含單一**結果**而不是項目單一**根**項目。 內容**結果**項目相依於用來執行的設定**批次**命令。  
  
 針對非交易式**批次**命令，**結果**元素包含一個**根**每個命令所執行的項目**批次**命令，是否在命令完成成功或失敗。 針對交易式**批次**命令，**結果**元素包含只有一個**根**元素，其中包含命令中失敗的錯誤資訊**批次**命令。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
