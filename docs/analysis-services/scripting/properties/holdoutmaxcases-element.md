---
title: HoldoutMaxCases 元素 |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 156363473a9354041ef4dfa9f9807e7b0d797214
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="holdoutmaxcases-element"></a>HoldoutMaxCases 元素
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  指定要用於鑑效組資料分割，其中包含的測試集的資料來源中的最大案例數目[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)項目。 資料集內的其餘案例將用於培訓。 值為 0 表示可當做測試集的案例數目沒有任何限制。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutMaxCases>...</ddl100_100:HoldoutMaxCases>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|大於 0 的整數。|  
|預設值|0|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如果您將值指定兩個**HoldoutMaxPercent**和**HoldoutMaxCases**，演算法會限制測試集較小的兩個值。  
  
 如果**HoldoutMaxCases**設為預設值是 0，且值未設定為**HoldoutMaxPercent**，演算法就會將整個資料集用於培訓。  
  
 新屬性**HoldoutMaxCases**， **HoldoutMaxPercent**， **HoldoutSeed**，或**HoldoutActualSize**只能用於[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]和更新版本。 因此，您必須在這些屬性前面加上新的命名空間 (如語法描述所示)，否則 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 將傳回錯誤。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支援在採礦結構上使用鑑效組資料分割。 因此，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]指令碼語言 (ASSL) 陳述式包含其中一個鑑效組參數， **HoldoutMaxCases**， **HoldoutMaxPercent**， **HoldoutSeed**，或**HoldoutActualSize**，不能用於在[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 如果您在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的 ASSL 陳述式中使用其中一個鑑效組參數，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 將傳回錯誤。  
  
 對應目的父代的項目**HoldoutMaxCases**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.MiningStructure>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)   
 [HoldoutMaxPercent 元素](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md)   
 [HoldoutSeed 元素](../../../analysis-services/scripting/properties/holdoutseed-element.md)   
 [HoldoutActualSize 元素](../../../analysis-services/scripting/properties/holdoutactualsize-element.md)  
  
  
