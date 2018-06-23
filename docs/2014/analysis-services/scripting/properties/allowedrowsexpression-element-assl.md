---
title: AllowedRowsExpression 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: ec24b11d-d11e-4369-a619-7e41a3c46159
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 99a340f2bbeb1e5d61a20b4031beeade9fbcc5c7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023207"
---
# <a name="allowedrowsexpression-element-assl"></a>AllowedRowsExpression 元素 (ASSL)
  包含定義父元素內容之布林類型的資料分析運算式 (DAX)。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CellPermission> <!-- or StandardAction -->  
   ...  
   <Expression>...</Expression>  
   ...  
</CellPermission>  
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
|父元素|[CellPermission](../objects/cellpermission-element-assl.md)， [StandardAction](../data-type/action-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如`CellPermission`項目，`Expression`元素包含邏輯 MDX 運算式來識別適用於所指定的權限的資料格[存取](access-element-assl.md)元素`CellPermission`項目。 如果 `Expression` 元素之 `CellPermission` 元素的值是空白的，系統就會忽略 `CellPermission` 元素。  
  
 若為 `StandardAction` 元素，`Expression` 元素會包含代表動作內容的 MDX 運算式。 如果 `Expression` 元素之 `StandardAction` 元素的值是空白的，系統就會忽略 `StandardAction` 元素。  
  
 在「分析管理物件」(AMO) 物件模型中對應至父系的元素是 <xref:Microsoft.AnalysisServices.CellPermission> 和 <xref:Microsoft.AnalysisServices.StandardAction>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  