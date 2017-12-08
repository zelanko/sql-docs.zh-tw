---
title: "DbSchemaName 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
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
apiname: DbSchemaName Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DbSchemaName
helpviewer_keywords: DbSchemaName element
ms.assetid: ae0f0edd-7b76-400d-a288-39a36d2a746b
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e45aa795d343b11323bedf7430de85bef321050d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="dbschemaname-element-assl"></a>DbSchemaName 元素 (ASSL)
  包含父元素所識別之資料表中所使用的結構描述名稱[DbTableName](../../../analysis-services/scripting/properties/dbtablename-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<TableBinding> <!-- or TableNotification -->  
   ...  
   <DbSchemaName>...</DbSchemaName>  
   ...  
</TableBinding>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[TableBinding](../../../analysis-services/scripting/data-type/tablebinding-data-type-assl.md)， [TableNotification](../../../analysis-services/scripting/objects/tablenotification-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應至父系的項目**DbSchemaName**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.TableBinding>和<xref:Microsoft.AnalysisServices.TableNotification>。  
  
## <a name="see-also"></a>請參閱＜  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
