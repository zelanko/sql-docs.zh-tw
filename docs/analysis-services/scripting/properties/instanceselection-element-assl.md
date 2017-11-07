---
title: "InstanceSelection 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- InstanceSelection Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- InstanceSelection element
ms.assetid: 908a2da9-274c-40d2-87dc-4641cb8d77e6
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4587536131aa3484846bc241a08be866a30d1da6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="instanceselection-element-assl"></a>InstanceSelection 元素 (ASSL)
  提供一個提示給用戶端應用程式，以便根據清單中的預期項目數目來建議應該如何顯示項目清單。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <InstanceSelection>...</InstanceSelection>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*無*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下列其中一個字串：  
  
|值|說明|  
|-----------|-----------------|  
|*無*|不要顯示選擇清單。 允許使用者直接輸入值。|  
|*下拉式清單*|項目數目夠小，足以顯示在下拉式清單中。|  
|*清單*|項目數目太大，無法顯示在下拉式清單中，但不需要篩選。|  
|*FilteredList*|項目數目夠大，因此使用者必須篩選要顯示的項目。|  
|*[Mandatoryfilter]*|項目數目非常大，所以一定要經過篩選才能顯示。|  
  
 列舉型別對應至允許的值**InstanceSelection**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.InstanceSelection>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

