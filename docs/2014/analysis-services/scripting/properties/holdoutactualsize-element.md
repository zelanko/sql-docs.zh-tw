---
title: HoldoutActualSize 元素 |Microsoft Docs
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
- HoldoutActualSize
helpviewer_keywords:
- HoldoutActualSize element
ms.assetid: 606a6674-cedb-4cee-82d0-26589f084dd9
caps.latest.revision: 18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4f74b11b9032285bf45bc8b7705953adf6d58f04
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37297278"
---
# <a name="holdoutactualsize-element"></a>HoldoutActualSize 元素
  表示處理之後，鑑效組資料分割，其中包含的測試集的實際大小， [MiningStructure](../objects/miningstructure-element-assl.md)項目。 資料集內的其餘案例將用於培訓。 此屬性是唯讀的。  
  
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
|父元素|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 值`HoldoutActualSize`取決於資料來源，以及值[HoldoutMaxCases](holdoutmaxcases-element.md)， [HoldoutMaxPercent](holdoutmaxpercent-element.md)，和[HoldoutSeed](holdoutseed-element.md)。 因此，您要等到 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 處理採礦結構之後才會取得 `HoldoutActualSize` 的值。  
  
 對應至父系的元素`HoldoutActualSize`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.MiningStructure>。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 不支援在採礦結構上使用鑑效組資料分割。 因此，包含 `HoldoutMaxCases`、`HoldoutMaxPercent`、`HoldoutSeed` 或 `HoldoutActualSize` 其中一個鑑效組參數的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 指令碼語言 (ASSL) 陳述式便無法用於 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中。 如果您在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的 ASSL 陳述式中使用其中一個鑑效組參數，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 將傳回錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)   
 [HoldoutMaxCases 元素](holdoutmaxcases-element.md)   
 [HoldoutMaxPercent 元素](holdoutmaxpercent-element.md)   
 [HoldoutSeed 元素](holdoutseed-element.md)  
  
  
