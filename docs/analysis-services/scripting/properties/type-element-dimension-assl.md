---
title: 輸入元素 (Dimension) (ASSL) |Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3af3168c39f685702154bb7c76435bd1d241a642
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37990310"
---
# <a name="type-element-dimension-assl"></a>Type 元素 (Dimension) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|父元素|[Dimension](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 某些值**型別**，例如*帳戶*，決定特定行為。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
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
|*費率*|此維度包含匯率屬性。|  
|*通路*|此維度包含通道屬性。|  
|*升級*|此維度包含促銷相關的屬性。|  
  
 列舉型別對應至允許的值**型別**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.DimensionType>。  
  
 對應至父系的元素**型別**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Dimension>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
