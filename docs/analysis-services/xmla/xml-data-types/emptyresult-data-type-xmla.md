---
title: EmptyResult 資料類型 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d9dd3cf815ee616c3519883a59ddcbb8fbd61eb8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="emptyresult-data-type-xmla"></a>EmptyResult 資料類型 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  定義衍生的資料類型，表示[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)不傳回資料來源的項目[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)或[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法呼叫。  
  
 **命名空間**描述 urn:-microsoft-schemas-microsoft-com:-xml-analysis: empty  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:empty">  
   <!-- All elements are inherited from Resultset -->  
</root>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|[結果集](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|無|  
|衍生的元素|[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 某些 XML for Analysis (XMLA) 命令不會傳回結果，或由於發生錯誤而無法傳回結果。 不會傳回結果的 XMLA 命令傳回**EmptyResult**資料類型、 命名空間上的**根**項目。  
  
## <a name="example"></a>範例  
 下列範例表示**根**元素傳回空的結果。  
  
```  
<return>  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:empty"/>  
</return>  
```  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料型別&#40;XMLA&#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)  
  
  
