---
title: EmptyResult 資料類型 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- EmptyResult Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#EmptyResult
- olapxmla_EmptyResult
- urn:schemas-microsoft-com:xml-analysis#EmptyResult
helpviewer_keywords:
- EmptyResult data type
ms.assetid: 63818123-acbb-4220-9d60-1aa20a7326a1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dc22612f18faa91e6cd668c022f036aadb9ef176
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48088540"
---
# <a name="emptyresult-data-type-xmla"></a>EmptyResult 資料類型 (XMLA)
  定義衍生的資料類型，表示[根](../xml-elements-properties/root-element-xmla.md)不傳回資料來源的項目[Discover](../xml-elements-methods-discover.md)或是[Execute](../xml-elements-methods-execute.md)方法呼叫。  
  
 **命名空間**urn: schemas-microsoft-microsoft-schemas-microsoft-com:-分析： 空白  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:empty">  
   <!-- All elements are inherited from Resultset -->  
</root>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[結果集](resultset-data-type-xmla.md)|  
|衍生資料類型|None|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|None|  
|衍生的元素|[根目錄](../xml-elements-properties/root-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 某些 XML for Analysis (XMLA) 命令不會傳回結果，或由於發生錯誤而無法傳回結果。 沒有傳回結果的 XMLA 命令會傳回 `EmptyResult` 資料類型，亦即 `root` 元素的命名空間。  
  
## <a name="example"></a>範例  
 下列範例代表針對空白結果所傳回的 `root` 元素。  
  
```  
<return>  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:empty"/>  
</return>  
```  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料型別&#40;XMLA&#41;](xml-data-types-xmla.md)  
  
  
