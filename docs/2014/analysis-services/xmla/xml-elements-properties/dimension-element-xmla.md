---
title: 維度元素 (XMLA) |Microsoft 文件
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
- Dimension Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Dimension
- urn:schemas-microsoft-com:xml-analysis#Dimension
- microsoft.xml.analysis.dimension
helpviewer_keywords:
- Dimension element
ms.assetid: 85093468-e971-4b8e-9ee4-7b264ad01711
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: f9684a8629a03bc2f0d328152b7f9f6daff1e7ba
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030353"
---
# <a name="dimension-element-xmla"></a>Dimension 元素 (XMLA)
  識別父代所代表之 cube 維度[物件](object-element-dimension-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Object>  
   ...  
   <Dimension>...</Dimension>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[物件](object-element-dimension-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `Dimension` 元素是物件識別碼，其中包含 `Object` 元素所代表之 Cube 維度的名稱。  
  
## <a name="see-also"></a>另請參閱  
 [Database 元素&#40;XMLA&#41;](database-element-xmla.md)   
 [Dimension 元素 (XMLA)](dimension-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  