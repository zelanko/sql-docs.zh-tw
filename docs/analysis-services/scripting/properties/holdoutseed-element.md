---
title: "HoldoutSeed 元素 |Microsoft 文件"
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
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- HoldoutSeed
helpviewer_keywords:
- HoldoutSeed element
ms.assetid: 6b608bb3-c075-4744-9722-f5fb9fa1cc7e
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e97148f9630a125dbe6e93754c532a825de96c84
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="holdoutseed-element"></a>HoldoutSeed 元素
  指定包含測試集的可重複鑑效組資料分割的種子[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)項目。 這個種子可確保模型內容在重新處理期間會保持不變。 如果未指定或設為 0，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]建立的採礦結構名稱使用雜湊演算法的種子。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutSeed>...</ddl100_100:HoldoutSeed>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|長整數|  
|預設值|0|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 當您首次建立採礦結構時，識別碼和名稱是相同的。 不過，您可以變更採礦結構的名稱。 因此，如果您想要確保資料分割可重複，就不應該仰賴依據名稱建立的種子，而應該明確設定種子。  
  
 此外，當您建立採礦結構的複本使用**匯出**陳述式，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]會保留新的採礦結構的名稱，但將會自動產生新的識別碼。 因此，您可能會有兩個共用相同名稱但具有不同識別碼的採礦結構。 任何兩個具有相同名稱的採礦結構將會具有相同的種子。 不過，由於資料的分割也取決於來源資料，因此每個結構中資料分割的實際內容可能會不同。  
  
 新屬性**HoldoutMaxCases**， **HoldoutMaxPercent**， **HoldoutSeed**，或**HoldoutActualSize**只能用於[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]和更新版本。 因此，您必須在這些屬性前面加上新的命名空間 (如語法描述所示)，否則 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 將傳回錯誤。  
  
 **請注意**中[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]不支援使用鑑效組資料分割的採礦結構上。 因此，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]包含鑑效組參數的指令碼語言 (ASSL) 陳述式**HoldoutMaxCases**， **HoldoutMaxPercent**， **HoldoutSeed**，或**HoldoutActualSize**不能用於在[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 如果您在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的 ASSL 陳述式中使用其中一個鑑效組參數，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 將傳回錯誤。  
  
 對應目的父代的項目**HoldoutSeed**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.MiningStructure>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)   
 [HoldoutActualSize 元素](../../../analysis-services/scripting/properties/holdoutactualsize-element.md)   
 [HoldoutMaxPercent 元素](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md)   
 [HoldoutMaxCases 元素](../../../analysis-services/scripting/properties/holdoutmaxcases-element.md)  
  
  
