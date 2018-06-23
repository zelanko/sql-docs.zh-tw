---
title: PartitionID 元素 (XMLA) |Microsoft 文件
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
- PartitionID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#PartitionID
- urn:schemas-microsoft-com:xml-analysis#PartitionID
- microsoft.xml.analysis.partitionid
helpviewer_keywords:
- PartitionID element
ms.assetid: 19f06454-9719-488e-aeb6-3fc879313351
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 54631af41d95d7ab149f853c6c94b7af1965f1ca
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031088"
---
# <a name="partitionid-element-xmla"></a>PartitionID 元素 (XMLA)
  識別父元素中包含物件參考的資料分割。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Object> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <PartitionID>...</PartitionID>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|如果上階或父系=<br />                        [Source](source-element-xmla.md)、[Target](../xml-elements-properties/target-element-xmla.md)<br /><br /> 基數 = 1-1：只出現一次的必要元素。<br /><br /> 如果上階或父系= All others：<br /><br /> 基數 = 0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Object](object-element-xmla.md)、[ParentObject](parentobject-element-xmla.md)、[Source](source-element-xmla.md)、[Target](../xml-elements-properties/target-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  