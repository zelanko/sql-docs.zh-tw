---
title: Perspective 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Perspective Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Perspective
helpviewer_keywords:
- Perspective element
ms.assetid: 0442334c-8b00-4451-ad81-02e58c735e8f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7ed510b7c4b9a9c023c6bad875ed2e6293ac2ac4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168228"
---
# <a name="perspective-element-assl"></a>Perspective 元素 (ASSL)
  定義檢視方塊的詳細資料[Cube](cube-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Perspectives>  
   <<Perspective>  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <Translations>...</Translations>  
      <DefaultMeasure>...</DefaultMeasure>  
      <Dimensions>...</Dimensions>  
            <MeasureGroups>...</MeasureGroups>  
      <Calculations>...</Calculations>  
      <Kpis>...</Kpis>  
            <Actions>...</Actions>  
      <Annotations>...</Annotations>  
   </Perspective>  
</Perspectives>  
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
|父元素|[檢視方塊](../collections/perspectives-element-assl.md)|  
|子元素|[動作](../collections/actions-element-assl.md)，[註解](../collections/annotations-element-assl.md)，[計算](../collections/calculations-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)， [DefaultMeasure](measure-element-assl.md)， [描述](../properties/description-element-assl.md)，[維度](../collections/dimensions-element-assl.md)，[識別碼](../properties/id-element-assl.md)， [Kpi](../collections/kpis-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)， [MeasureGroups](../collections/groups-element-assl.md)，[名稱](../properties/name-element-assl.md)，[翻譯](../collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 檢視方塊會提供 Cube 的子集，以便選取要包含的維度、階層、屬性和其他詳細資料，以及定義要包含的資料配量。 檢視方塊是由單一 Cube 所擁有。 您無法在檢視方塊內部覆寫或加入物件。所有維度、階層和其他詳細資料都必須存在基礎 Cube 中。 此外，您也無法加入物件並將它們標示為不顯示。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.Perspective>。  
  
## <a name="see-also"></a>另請參閱  
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
