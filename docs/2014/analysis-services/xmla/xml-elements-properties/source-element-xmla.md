---
title: Source 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Source Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Source
- http://schemas.microsoft.com/analysisservices/2003/engine#Source
- microsoft.xml.analysis.source
helpviewer_keywords:
- Source element
ms.assetid: 4d4665ae-e20f-4baf-ab0f-848660caf500
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 06c69de2879b2298b180b6dd487fe2dc28f09684
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48095718"
---
# <a name="source-element-xmla"></a>Source 元素 (XMLA)
  表示期間合併的來源資料分割[MergePartitions](../xml-elements-commands/mergepartitions-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Sources>  
   <Source>  
      <DatabaseID>...</DatabaseID>  
      <CubeID>...</CubeID>  
      <MeasureGroupID>...</MeasureGroupID>  
      <PartitionID>...</PartitionID>  
   </Source>  
</Sources>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|1-n：出現一次以上的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[來源](sources-element-xmla.md)|  
|子元素|[CubeID](id-element-xmla.md)， [DatabaseID](databaseid-element-xmla.md)， [MeasureGroupID](measuregroupid-element-xmla.md)， [PartitionID](partitionid-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `Source` 元素是物件參考，它指向要合併至 `Target` 父元素之 `MergePartitions` 元素所指定的目標資料分割中的單一資料分割。  
  
## <a name="example"></a>範例  
 下列範例會將 `Internet Sales` 量值群組的四個資料分割都結合至 `Internet_Sales_2004` 目標資料分割中。 此範例會參考**Adventure Works** cube[!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)]範例[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫。  
  
```  
<MergePartitions xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Sources>  
     <Source>        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>        <CubeID>Adventure Works</CubeID>        <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>        <PartitionID>Internet_Sales_2001</PartitionID>     </Source>     <Source>        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>        <CubeID>Adventure Works</CubeID>      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>      <PartitionID>Internet_Sales_2002</PartitionID>    </Source>    <Source>      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>      <PartitionID>Internet_Sales_2003</PartitionID>    </Source>  
  </Sources>  
  <Target>  
    <DatabaseID Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2004</PartitionID>  
  </Target>  
</MergePartitions>  
```  
  
## <a name="see-also"></a>另請參閱  
 [Target 項目&#40;XMLA&#41;](../xml-elements-properties/target-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
