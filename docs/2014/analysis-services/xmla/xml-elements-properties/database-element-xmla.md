---
title: Database 元素 (XMLA) |Microsoft 文件
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
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: f1b643a12ab1dbf2dc151fe91a8663b138e581ec
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022485"
---
# <a name="database-element-xmla"></a>Database 元素 (XMLA)
  識別包含父代所代表之維度的資料庫[物件](object-element-dimension-xmla.md)項目。  
  
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
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[物件](object-element-dimension-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `Database` 元素是物件識別碼，其中包含含有 `Object` 元素所代表之維度的 Analysis Services 資料庫名稱。  
  
## <a name="see-also"></a>另請參閱  
 [Cube 元素&#40;XMLA&#41;](cube-element-xmla.md)   
 [維度元素&#40;XMLA&#41;](dimension-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  