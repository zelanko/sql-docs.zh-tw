---
title: "ServerProperties 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ServerProperties Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ServerProperties
helpviewer_keywords: ServerProperties element
ms.assetid: 8ccbef3f-1388-4fa3-b0a4-c89b89f09056
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ab839c124a555d0b7310dcdaa3517a87326329b6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="serverproperties-element-assl"></a>ServerProperties 元素 (ASSL)
  包含集合[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)與相關聯的項目[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Server>  
      ...  
   <ServerProperties>  
      <ServerProperty>...</ServerProperty>  
   </ServerProperties>  
   ...  
</Server>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|子元素|[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.ServerPropertyCollection>。  
  
## <a name="see-also"></a>請參閱＜  
 [集合 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
