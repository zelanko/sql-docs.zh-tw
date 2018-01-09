---
title: "MiningStructure 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MiningStructure Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: MiningStructure
helpviewer_keywords: MiningStructure element
ms.assetid: b943cd92-0ed8-4bd8-8fbc-7dab0534aede
caps.latest.revision: "48"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 455d874cf279e44e8381c5183d2d376e40e2a351
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="miningstructure-element-assl"></a>MiningStructure 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定義一組採礦模型的結構。  
  
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
|父元素|[MiningStructures](../../../analysis-services/scripting/collections/miningstructures-element-assl.md)|  
|子元素|[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [CacheMode](../../../analysis-services/scripting/properties/cachemode-element-assl.md)，[定序](../../../analysis-services/scripting/properties/collation-element-assl.md)，[資料行](../../../analysis-services/scripting/collections/columns-element-assl.md)， [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)， [描述](../../../analysis-services/scripting/properties/description-element-assl.md)， [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)，<br /><br /> [HoldoutActualSize](../../../analysis-services/scripting/properties/holdoutactualsize-element.md)，<br /><br /> [HoldoutMaxCases](../../../analysis-services/scripting/properties/holdoutmaxcases-element.md)，<br /><br /> [HoldoutMaxPercent](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md)，<br /><br /> [HoldoutSeed](../../../analysis-services/scripting/properties/holdoutseed-element.md)，<br /><br /> [識別碼](../../../analysis-services/scripting/properties/id-element-assl.md)，[語言](../../../analysis-services/scripting/properties/language-element-assl.md)， [LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md)， [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)， [MiningModels](../../../analysis-services/scripting/collections/miningmodels-element-assl.md)， [MiningStructurePermissions](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md)，[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)，[來源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)，[狀態](../../../analysis-services/scripting/properties/state-element-assl.md)，[翻譯](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 採礦結構會定義資料行和繫結。 定義採礦結構後，您可以使用該結構來定義多個採礦模型。 採礦結構及其所包含的每個採礦模型可以分開處理。  
  
> [!NOTE]  
>  鑑效組屬性， **HoldoutMaxCases**， **HoldoutMaxPercent**， **HoldoutSeed**，和**HoldoutActualSize**中, 導入[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. 這些屬性可讓您在採礦結構上，針對與該結構相關聯的所有採礦模型，定義當做測試集使用的資料分割。 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 不支援這些屬性。 因此，如果您嘗試在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的執行個體上使用這些屬性，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 將會傳回錯誤。  
  
## <a name="drillthrough-to-structure-columns"></a>鑽研結構資料行  
 在[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]，新的權限項目已加入至[MiningStructurePermissions 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md)集合。 如果您將加入**AllowDrillthrough**權限同時[MiningStructurePermissions](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md)和[MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md)集合，從啟用鑽研採礦模型加入結構，這類方式具有之角色的成員**AllowDrillthrough**模型的權限可以查詢資料採礦模型，並傳回未包含在模型中的結構資料行。  
  
 因此，若要保護敏感性資料或個人資訊，您應該建構您的資料來源檢視來遮罩敏感性資訊，並授與**AllowDrillthrough**只在必要時在採礦結構上的權限。 如需詳細資訊，請參閱[AllowDrillThrough 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md).  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.MiningStructure>。  
  
## <a name="see-also"></a>請參閱  
 [MiningModel 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)   
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)   
 [SELECT &#40; DMX &#41;](../../../dmx/select-dmx.md)  
  
  
