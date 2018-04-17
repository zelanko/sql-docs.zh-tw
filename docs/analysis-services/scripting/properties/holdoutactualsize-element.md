---
title: HoldoutActualSize 元素 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- HoldoutActualSize
helpviewer_keywords:
- HoldoutActualSize element
ms.assetid: 606a6674-cedb-4cee-82d0-26589f084dd9
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 02c225e85ee594abb21c7d96eb68f05a8ef2b435
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="holdoutactualsize-element"></a>HoldoutActualSize 元素
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]指出經過處理後，鑑效組資料分割，其中包含的測試集實際大小[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)項目。 資料集內的其餘案例將用於培訓。 此屬性是唯讀的。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutActualSize>...</ddl100_100:HoldoutActualSize>  
   ...  
</MiningStructure  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|唯讀的整數值。|  
|預設值|不適用|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 值**HoldoutActualSize**取決於資料來源，以及值[HoldoutMaxCases](../../../analysis-services/scripting/properties/holdoutmaxcases-element.md)， [HoldoutMaxPercent](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md)，和[HoldoutSeed](../../../analysis-services/scripting/properties/holdoutseed-element.md). 因此，值**HoldoutActualSize**不是等到之後，才能使用[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]處理採礦結構。  
  
 對應目的父代的項目**HoldoutActualSize**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.MiningStructure>。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支援在採礦結構上使用鑑效組資料分割。 因此，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]指令碼語言 (ASSL) 陳述式包含其中一個鑑效組參數， **HoldoutMaxCases**， **HoldoutMaxPercent**， **HoldoutSeed**，或**HoldoutActualSize**，不能用於在[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 如果您在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的 ASSL 陳述式中使用其中一個鑑效組參數，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 將傳回錯誤。  
  
## <a name="see-also"></a>請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)   
 [HoldoutMaxCases 元素](../../../analysis-services/scripting/properties/holdoutmaxcases-element.md)   
 [HoldoutMaxPercent 元素](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md)   
 [HoldoutSeed 元素](../../../analysis-services/scripting/properties/holdoutseed-element.md)  
  
  
