---
title: Database 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Database Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.database
- http://schemas.microsoft.com/analysisservices/2003/engine#Database
- urn:schemas-microsoft-com:xml-analysis#Database
helpviewer_keywords:
- Database element
ms.assetid: 2ded06c4-4eaf-4ccb-a416-41ee51ced8bc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5861be2ad0f5975ef5b95c3f4b077a065b560e02
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171958"
---
# <a name="database-element-xmla"></a>Database 元素 (XMLA)
  識別包含父元素所代表之維度的資料庫[物件](object-element-dimension-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Object>  
   ...  
   <Database>...</Database>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[物件](object-element-dimension-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 `Database` 元素是物件識別碼，其中包含含有 `Object` 元素所代表之維度的 Analysis Services 資料庫名稱。  
  
## <a name="see-also"></a>另請參閱  
 [Cube 元素&#40;XMLA&#41;](cube-element-xmla.md)   
 [維度項目&#40;XMLA&#41;](dimension-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
