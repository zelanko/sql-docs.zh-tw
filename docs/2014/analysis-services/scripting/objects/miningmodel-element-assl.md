---
title: MiningModel 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MiningModel Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModel
helpviewer_keywords:
- MiningModel element
ms.assetid: a61d935f-c8f6-457d-ad0c-44f58bb286f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7b6661d5718e36913fd9f706bd1912912e0b17fd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48221358"
---
# <a name="miningmodel-element-assl"></a>MiningModel 元素 (ASSL)
  定義單一資料採礦模型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningModels>  
      <MiningModel>  
      <Name>...</Name>  
            <ID>...</ID>  
      <Description>...</<Descrip  
            <Algorithm>...</Algorithm>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LastProcessed>...</LastProcessed>  
      <AlgorithmParameters>...</AlgorithmParameters>  
      <AllowDrillThrough>...</AllowDrillThrough>  
      <Translations>...</Translations>  
      <Columns>...</Columns>  
      <State>...</State>  
      <MiningModelPermissions>...</MiningModelPermissions>  
      <Language>...</Language>  
            <Collation>...</Collation>  
            <Annotations>...</Annotations>  
            <ddl100_100:FoldingParameters>   </FoldingParameters>  
   </MiningModel>  
</MiningModels>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningModels](../collections/miningmodels-element-assl.md)|  
|子元素|[演算法](../properties/algorithm-element-assl.md)， [AlgorithmParameters](algorithmparameter-element-assl.md)， [AllowDrillThrough](../properties/allowdrillthrough-element-assl.md)，[註解](../collections/annotations-element-assl.md)，[定序](../properties/collation-element-assl.md)， [資料行](../collections/columns-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)，[描述](../properties/description-element-assl.md)，[識別碼](../properties/id-element-assl.md)，[語言](../properties/language-element-assl.md)， [LastProcessed](../properties/lastprocessed-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)， [MiningModelPermissions](../collections/miningmodelpermissions-element-assl.md)，[名稱](../properties/name-element-assl.md)，[狀態](../properties/state-element-assl.md)， [翻譯](../collections/translations-element-assl.md)，<br /><br /> [FoldingParameters](../properties/foldingparameters-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 採礦模型的 `FoldingParameters` 元素供伺服器內部使用，不支援用於 DDL 陳述式。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.MiningModel>。  
  
## <a name="see-also"></a>另請參閱  
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
