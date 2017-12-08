---
title: "Trimming 元素 (ASSL) |Microsoft 文件"
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
apiname: Trimming Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Trimming
helpviewer_keywords: Trimming element
ms.assetid: 8b3bbf89-8309-4d00-9aea-a5918f0c7027
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 962e3b82e8853d00c34684c23db891617c2ff08a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="trimming-element-assl"></a>Trimming 元素 (ASSL)
  指定如何修剪資料來源的資料。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DataItem>  
   ...  
   <Trimming>...</Trimming>  
   ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*權限*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*左*|從左邊修剪資料。|  
|*權限*|從右邊修剪資料。|  
|*LeftRight*|從左邊和右邊修剪資料。|  
|*無*|不修剪資料。|  
  
 列舉型別對應至允許的值**修剪**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Trimming>。  
  
 對應目的父代的項目**修剪**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.DataItem>。  
  
## <a name="see-also"></a>請參閱＜  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
