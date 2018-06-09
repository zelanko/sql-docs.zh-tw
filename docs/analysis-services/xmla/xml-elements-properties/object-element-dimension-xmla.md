---
title: 物件元素 (Dimension) (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6b321a6c26edb4f569b4174d64a0a50b8ac23ae6
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34575760"
---
# <a name="object-element-dimension-xmla"></a>Object 元素 (Dimension) (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含維度的物件參考的父[插入](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)，[更新](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)，或[卸除](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)執行命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Insert> <!-- or any of the parent elements in the Element relationships table -->  
...  
   <Object>  
      <Database>...</Database>  
      <Cube>...</Cube>  
      <Dimension>...</Dimension>  
   </Object>  
...  
</Insert>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[卸除](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)，[插入](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)，[更新](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|  
|子元素|[Cube](../../../analysis-services/xmla/xml-elements-properties/cube-element-xmla.md)，[資料庫](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)，[維度](../../../analysis-services/xmla/xml-elements-properties/dimension-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
