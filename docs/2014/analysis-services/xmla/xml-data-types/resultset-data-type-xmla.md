---
title: Resultset 資料類型 (XMLA) |Microsoft Docs
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4d4e95d3e2b85971271cff4b1365b44e5a30ba0c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37155069"
---
# <a name="resultset-data-type-xmla"></a>Resultset 資料類型 (XMLA)
  定義代表從傳回的資料的抽象基本資料類型[Discover](../xml-elements-methods-discover.md)或是[Execute](../xml-elements-methods-execute.md)方法呼叫。  
  
 **命名空間**urn: schemas-microsoft-microsoft-schemas-microsoft-com:-分析： 結果集  
  
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
  
  
