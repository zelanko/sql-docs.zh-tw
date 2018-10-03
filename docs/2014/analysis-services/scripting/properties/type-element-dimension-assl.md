---
title: 輸入元素 (Dimension) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Type Element (Dimension)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 6a2798b1-26c7-49d8-b556-e681c69d9574
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ab2d68ab78b31373e08185c3ee816241fe82bbd1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117618"
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*規則*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Dimension](../objects/dimension-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 某些值`Type`，例如*帳戶*，決定特定行為。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*規則*|此維度是一般維度。|  
|*Time*|此維度是時間維度。 **注意：** 這個值表示此維度支援時間維度特有的功能。|  
|*地理位置*|此維度包含地理屬性。|  
|*組織*|此維度包含組織屬性。|  
|*BillOfMaterials*|此維度包含用料表屬性。|  
|*帳戶*|此維度包含帳戶相關的屬性。 **注意：** 這個值表示此維度支援帳戶維度特有的功能。|  
|*客戶*|此維度包含客戶相關的屬性。|  
|*產品*|此維度包含產品相關的屬性。|  
|*案例*|此維度包含狀況相關的屬性。|  
|*量化*|此維度包含數量的屬性。|  
|*公用程式*|此維度包含公用程式屬性。|  
|*貨幣*|此維度包含貨幣屬性。|  
|*費率*|此維度包含匯率屬性。|  
|*通路*|此維度包含通道屬性。|  
|*升級*|此維度包含促銷相關的屬性。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `Type` 允許值的列舉是 <xref:Microsoft.AnalysisServices.DimensionType>。  
  
 對應至父系的元素`Type`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Dimension>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
