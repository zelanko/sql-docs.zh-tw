---
title: 輸入元素 (Dimension) (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4455b2f18f19f3e884be07ed4bed344bf1485bd1
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
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
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*一般*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 某些值**類型**，例如*帳戶*，判斷特定行為。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*一般*|此維度是一般維度。|  
|*Time*|此維度是時間維度。<br /><br /> 注意： 這個值表示此維度支援時間維度特有的功能。|  
|*Geography*|此維度包含地理屬性。|  
|*組織*|此維度包含組織屬性。|  
|*BillOfMaterials*|此維度包含用料表屬性。|  
|*帳戶*|此維度包含帳戶相關的屬性。<br /><br /> 注意： 這個值表示此維度支援帳戶維度特有的功能。|  
|*客戶*|此維度包含客戶相關的屬性。|  
|*產品*|此維度包含產品相關的屬性。|  
|*案例*|此維度包含狀況相關的屬性。|  
|*數量*|此維度包含數量的屬性。|  
|*公用程式*|此維度包含公用程式屬性。|  
|*貨幣*|此維度包含貨幣屬性。|  
|*速率*|此維度包含匯率屬性。|  
|*通路*|此維度包含通道屬性。|  
|*促銷*|此維度包含促銷相關的屬性。|  
  
 列舉型別對應至允許的值**類型**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.DimensionType>。  
  
 對應目的父代的項目**類型**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Dimension>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
