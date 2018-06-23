---
title: 格式元素 (ASSL) |Microsoft 文件
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
- Format Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Format
helpviewer_keywords:
- Format element
ms.assetid: 881ea707-52a7-46f7-ba16-ac2ec44eca22
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b7434ba5d6e2db8d2a2e665fa333799b6b2e9eb8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136957"
---
# <a name="format-element-assl"></a>Format 元素 (ASSL)
  包含所需的格式[DataItem](../data-type/dataitem-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DataItem>  
   ...  
   <Format>...</Format>  
      ...  
</DataItem>  
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
|父元素|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 允許的值為`Format`項目是 Microsoft Office Excel 格式，以及字串*TrimRight*， *TrimLeft*， *TrimAll*，和*TrimNone*。 進行修剪， *TrimRight*是預設值。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|任何 Excel 格式字串|資料會根據指定的具名或自訂格式字串格式化。 您可以提供 Excel 支援的任何格式字串。|  
|*TrimAll*|從左邊和右邊修剪資料。|  
|*TrimLeft*|從左邊修剪資料。|  
|*TrimNone*|不修剪資料。|  
|*TrimRight*|從右邊修剪資料。|  
  
 對應目的父代的項目`Format`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.DataItem>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  