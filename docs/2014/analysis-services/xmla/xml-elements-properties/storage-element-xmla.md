---
title: Storage 元素 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Storage Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.storage
- urn:schemas-microsoft-com:xml-analysis#Storage
- http://schemas.microsoft.com/analysisservices/2003/engine#Storage
helpviewer_keywords:
- Storage element
ms.assetid: c3590af8-a24b-4fd3-b846-17edbd399b6d
caps.latest.revision: 10
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 8bccf119846d699d653a480f6479412b46dcc4f9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36144597"
---
# <a name="storage-element-xmla"></a>Storage 元素 (XMLA)
  指定以位元組為單位，所使用的存放裝置的最大數量[DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md)命令來設計彙總。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DesignAggregations>  
   ...  
   <Storage>...</Storage>  
   ...  
</DesignAggregations>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|長整數|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  