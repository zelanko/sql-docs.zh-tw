---
title: Resultset 資料類型 (XMLA) |Microsoft 文件
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
- Resultset Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Resultset
- urn:schemas-microsoft-com:xml-analysis#Resultset
- Resultset
helpviewer_keywords:
- Resultset data type
ms.assetid: 45e7d7d6-1f89-4dc8-b39d-9270ea2db541
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d8a571012c82c9e4d26d9f586cf67344f19258a6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023206"
---
# <a name="resultset-data-type-xmla"></a>Resultset 資料類型 (XMLA)
  定義表示從傳回的資料的抽象基本資料類型[探索](../xml-elements-methods-discover.md)或[Execute](../xml-elements-methods-execute.md)方法呼叫。  
  
 **命名空間**描述 urn:-microsoft-schemas-microsoft-com:-xml-analysis: resultset  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Resultset>  
   <Exception>...</Exception>  
   <Messages>...</Messages>  
</Resultset>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|[MDDataSet](mddataset-data-type-xmla.md)， [olapxmla_EmptyResult](emptyresult-data-type-xmla.md)，[資料列集](rowset-data-type-xmla.md)|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[例外狀況](../xml-elements-properties/exception-element-xmla.md)，[訊息](../xml-elements-properties/messages-element-xmla.md)|  
|衍生的元素|無|  
  
## <a name="remarks"></a>備註  
 `Resultset` 資料類型是可同時包含結構描述和資料的自我描述 XML 結果集，端視要傳回的資訊類型而定。  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料型別&#40;XMLA&#41;](xml-data-types-xmla.md)  
  
  