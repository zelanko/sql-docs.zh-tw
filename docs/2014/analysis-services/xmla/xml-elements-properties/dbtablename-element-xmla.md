---
title: DbTableName 元素 (XMLA) |Microsoft 文件
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
- DbTableName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#DbTableName
- microsoft.xml.analysis.dbtablename
- urn:schemas-microsoft-com:xml-analysis#DbTableName
helpviewer_keywords:
- DbTableName element
ms.assetid: 0ffda645-2a88-4f42-8929-9d7385c19a74
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: d45f49175336cb6df34f528529c00a5ae8d20633
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031495"
---
# <a name="dbtablename-element-xmla"></a>DbTableName 元素 (XMLA)
  包含父代所使用的資料表名稱[TableNotification](tablenotification-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<TableNotification>  
   ...  
   <DbTableName>...</DbTableName>  
   ...  
</TableNotification>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[TableNotification](tablenotification-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [DbSchemaName 元素&#40;XMLA&#41;](name-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  