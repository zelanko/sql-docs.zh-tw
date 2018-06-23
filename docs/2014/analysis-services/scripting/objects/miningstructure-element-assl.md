---
title: MiningStructure 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MiningStructure Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningStructure
helpviewer_keywords:
- MiningStructure element
ms.assetid: b943cd92-0ed8-4bd8-8fbc-7dab0534aede
caps.latest.revision: 48
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5298c78f1902ee9a8fb1ed12ecf066092a02d938
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36144812"
---
# <a name="miningstructure-element-assl"></a>MiningStructure 元素 (ASSL)
  定義一組採礦模型的結構。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningStructures>  
   <MiningStructure>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</<Description>  
      <Source>...</Source>  
      <CreatedTimestamp>...</<CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LastProcessed>...</LastProcessed>  
      <Translations>...</Translations>  
      <Language>...</Language>  
            <Collation>...</Collation>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <CacheMode>...</CacheMode>  
            <Columns>...</Columns>  
      <State>...</State>  
      <HoldoutActualSize>...</HoldoutActualSize>  
      <HoldoutMaxCases>...</HoldoutMaxCases>  
      <HoldoutMaxPercent>...</HoldoutMaxPercent>  
      <HoldoutSeed>...</HoldoutSeed>        
            <MiningStructurePermissions>...</<MiningStructurePermissions>  
            <MiningModels>...</MiningModels>  
            <Annotations>...</Annotations>  
   </MiningStructure>  
</MiningStructures>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningStructures](../collections/miningstructures-element-assl.md)|  
|子元素|[註解](../collections/annotations-element-assl.md)， [CacheMode](../properties/cachemode-element-assl.md)，[定序](../properties/collation-element-assl.md)，[資料行](../collections/columns-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)，[描述](../properties/description-element-assl.md)， [ErrorConfiguration](errorconfiguration-element-assl.md)，<br /><br /> [HoldoutActualSize](../properties/holdoutactualsize-element.md)，<br /><br /> [HoldoutMaxCases](../properties/holdoutmaxcases-element.md)，<br /><br /> [HoldoutMaxPercent](../properties/holdoutmaxpercent-element.md)，<br /><br /> [HoldoutSeed](../properties/holdoutseed-element.md)，<br /><br /> [識別碼](../properties/id-element-assl.md)，[語言](../properties/language-element-assl.md)， [LastProcessed](../properties/lastprocessed-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)， [MiningModels](../collections/miningmodels-element-assl.md)， [MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md)，[名稱](../properties/name-element-assl.md)，[來源](../properties/source-element-binding-assl.md)，[狀態](../properties/state-element-assl.md)，[翻譯](../collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 採礦結構會定義資料行和繫結。 定義採礦結構後，您可以使用該結構來定義多個採礦模型。 採礦結構及其所包含的每個採礦模型可以分開處理。  
  
> [!NOTE]  
>  鑑效組屬性 `HoldoutMaxCases`、`HoldoutMaxPercent`、`HoldoutSeed` 和 `HoldoutActualSize` 已在 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 中推出。 這些屬性可讓您在採礦結構上，針對與該結構相關聯的所有採礦模型，定義當做測試集使用的資料分割。 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 不支援這些屬性。 因此，如果您嘗試在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的執行個體上使用這些屬性，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 將會傳回錯誤。  
  
## <a name="drillthrough-to-structure-columns"></a>鑽研結構資料行  
 在[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]，新的權限項目已加入至[MiningStructurePermissions 元素&#40;ASSL&#41; ](../collections/miningstructurepermissions-element-assl.md)集合。 如果您將加入`AllowDrillthrough`權限同時[MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md)和[MiningModelPermission](miningmodelpermission-element-assl.md)鑽研的集合，從採礦模型啟用結構的方式有一個角色的成員`AllowDrillthrough`模型的權限可以查詢資料採礦模型，並傳回未包含在模型中的結構資料行。  
  
 因此，若要保護敏感性資料或個人資訊，您應該建構您的資料來源檢視來遮罩敏感性資訊，並只有在必要時，才授與採礦結構的 `AllowDrillthrough` 權限。 如需詳細資訊，請參閱[AllowDrillThrough 元素&#40;ASSL&#41;](../properties/allowdrillthrough-element-assl.md)。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.MiningStructure>。  
  
## <a name="see-also"></a>另請參閱  
 [MiningModel 元素&#40;ASSL&#41;](miningmodel-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)   
 [選取&AMP;#40;DMX&AMP;#41;](/sql/dmx/select-dmx)  
  
  
