---
title: "輸入元素 (Dimension) (ASSL) |Microsoft 文件"
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
apiname:
- Type Element (Dimension)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 6a2798b1-26c7-49d8-b556-e681c69d9574
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 868851d8eeeb72b4d35a7568a93c5ea7467d8204
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="type-element-dimension-assl"></a>Type 元素 (Dimension) (ASSL)
  提供有關維度內容的資訊。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Dimension>  
      ...  
   <Type>...</Type>  
   ...  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*規則*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 某些值**類型**，例如*帳戶*，判斷特定行為。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*規則*|此維度是一般維度。|  
|*Time*|此維度是時間維度。<br /><br /> 注意： 這個值表示此維度支援時間維度特有的功能。|  
|*地理位置*|此維度包含地理屬性。|  
|*組織*|此維度包含組織屬性。|  
|*BillOfMaterials*|此維度包含用料表屬性。|  
|*帳戶*|此維度包含帳戶相關的屬性。<br /><br /> 注意： 這個值表示此維度支援帳戶維度特有的功能。|  
|*客戶*|此維度包含客戶相關的屬性。|  
|*產品*|此維度包含產品相關的屬性。|  
|*案例*|此維度包含狀況相關的屬性。|  
|*量化*|此維度包含數量的屬性。|  
|*公用程式*|此維度包含公用程式屬性。|  
|*貨幣*|此維度包含貨幣屬性。|  
|*速率*|此維度包含匯率屬性。|  
|*通路*|此維度包含通道屬性。|  
|*升級*|此維度包含促銷相關的屬性。|  
  
 列舉型別對應至允許的值**類型**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.DimensionType>。  
  
 對應目的父代的項目**類型**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Dimension>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

