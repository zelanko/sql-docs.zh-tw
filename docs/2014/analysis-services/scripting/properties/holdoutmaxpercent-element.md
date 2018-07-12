---
title: HoldoutMaxPercent 元素 |Microsoft Docs
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
topic_type:
- apiref
f1_keywords:
- HoldoutMaxPercent
helpviewer_keywords:
- HoldoutMaxPercent element
ms.assetid: e375cc51-5f9d-4252-98a1-326ca0dbbf83
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 53689f28351a4a5505f1c1bc1d4c8a9586074704
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37278144"
---
# <a name="holdoutmaxpercent-element"></a>HoldoutMaxPercent 元素
  將用於鑑效組資料分割，其中包含的測試集的資料來源中指定之案例的最大百分比[MiningStructure](../objects/miningstructure-element-assl.md)項目。 其餘案例將用於培訓。 值為 0 表示可當做測試集的案例數目沒有任何限制。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutMaxPercent>...</ddl100_100:HoldoutMaxPercent>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|介於 0 和 99 之間的整數。|  
|預設值|30|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如果您同時針對 `HoldoutMaxPercent` 和 `HoldoutMaxCases` 指定值，此演算法就會將測試集限制為這兩個值當中較小的值。  
  
 如果 `HoldoutMaxCases` 設定為預設值 0，而且尚未針對 `HoldoutMaxPercent` 設定任何值，此演算法就會將完整的資料集用於培訓。  
  
 新的屬性`HoldoutMaxCases`， `HoldoutMaxPercent`， `HoldoutSeed`，或`HoldoutActualSize`僅適用於[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]和更新版本。 因此，您必須在這些屬性前面加上新的命名空間 (如語法描述所示)，否則 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 將傳回錯誤。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支援在採礦結構上使用鑑效組資料分割。 因此，包含 `HoldoutMaxCases`、`HoldoutMaxPercent`、`HoldoutSeed` 或 `HoldoutActualSize` 其中一個鑑效組參數的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 指令碼語言 (ASSL) 陳述式便無法用於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中。 如果您在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的 ASSL 陳述式中使用其中一個鑑效組參數，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 將傳回錯誤。  
  
 對應至父系的元素`HoldoutMaxPercent`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.MiningStructure>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)   
 [HoldoutMaxCases 元素](holdoutmaxcases-element.md)   
 [HoldoutSeed 元素](holdoutseed-element.md)   
 [HoldoutActualSize 元素](holdoutactualsize-element.md)  
  
  
