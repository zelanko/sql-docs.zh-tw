---
title: HoldoutSeed 元素 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
f1_keywords:
- HoldoutSeed
helpviewer_keywords:
- HoldoutSeed element
ms.assetid: 6b608bb3-c075-4744-9722-f5fb9fa1cc7e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b97d88ee83d92d22f72db13d20ce37bb6ea9da08
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48097595"
---
# <a name="holdoutseed-element"></a>HoldoutSeed 元素
  指定包含測試的一組可重複鑑效組資料分割的種子[MiningStructure](../objects/miningstructure-element-assl.md)項目。 這個種子可確保模型內容在重新處理期間會保持不變。 如果未指定或設為 0，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]建立的採礦結構名稱使用雜湊演算法的種子。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutSeed>...</ddl100_100:HoldoutSeed>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|長整數|  
|預設值|0|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 當您首次建立採礦結構時，識別碼和名稱是相同的。 不過，您可以變更採礦結構的名稱。 因此，如果您想要確保資料分割可重複，就不應該仰賴依據名稱建立的種子，而應該明確設定種子。  
  
 此外，當您建立一份採礦結構使用`EXPORT`陳述式，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]會保留新的採礦結構的名稱，但將會自動產生新的識別碼。 因此，您可能會有兩個共用相同名稱但具有不同識別碼的採礦結構。 任何兩個具有相同名稱的採礦結構將會具有相同的種子。 不過，由於資料的分割也取決於來源資料，因此每個結構中資料分割的實際內容可能會不同。  
  
 新的屬性`HoldoutMaxCases`， `HoldoutMaxPercent`， `HoldoutSeed`，或`HoldoutActualSize`僅適用於[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]和更新版本。 因此，您必須在這些屬性前面加上新的命名空間 (如語法描述所示)，否則 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 將傳回錯誤。  
  
 **附註**中[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]不支援使用鑑效組資料分割的採礦結構上。 因此，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]包含鑑效組參數的指令碼語言 (ASSL) 陳述式`HoldoutMaxCases`， `HoldoutMaxPercent`， `HoldoutSeed`，或`HoldoutActualSize`無法用於[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 如果您在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的 ASSL 陳述式中使用其中一個鑑效組參數，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 將傳回錯誤。  
  
 對應至父系的元素`HoldoutSeed`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.MiningStructure>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)   
 [HoldoutActualSize 元素](holdoutactualsize-element.md)   
 [HoldoutMaxPercent 元素](holdoutmaxpercent-element.md)   
 [HoldoutMaxCases 元素](holdoutmaxcases-element.md)  
  
  
