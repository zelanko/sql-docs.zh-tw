---
title: 目標元素 (XMLA) |Microsoft 文件
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
api_name:
- Target Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.target
- http://schemas.microsoft.com/analysisservices/2003/engine#Target
- urn:schemas-microsoft-com:xml-analysis#Target
helpviewer_keywords:
- Target element
ms.assetid: 9a69a777-5f34-4e94-b470-6bab2a98df8b
caps.latest.revision: 14
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: cd34f3102d477d9a2e89af8c8ba7e5ff2d37ef62
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133315"
---
# <a name="target-element-xmla"></a>Target 元素 (XMLA)
  表示期間合併的目標分割區[MergePartitions](../xml-elements-commands/mergepartitions-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MergePartitions>  
   <Target>  
      <DatabaseID>...</DatabaseID>  
      <CubeID>...</CubeID>  
      <MeasureGroupID>...</MeasureGroupID>  
      <PartitionID>...</PartitionID>  
   </Target>  
</MergePartitions>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-n：出現一次以上的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MergePartitions](../xml-elements-commands/mergepartitions-element-xmla.md)|  
|子元素|[CubeID](id-element-xmla.md)， [DatabaseID](databaseid-element-xmla.md)， [MeasureGroupID](measuregroupid-element-xmla.md)， [PartitionID](partitionid-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `Target`項目是單一資料分割所在的來源資料分割中，內容則是所指定的物件參考[來源](sources-element-xmla.md)父元素之`MergePartitions`項目，要合併。  
  
## <a name="example"></a>範例  
 下列範例會將 Internet Sales 量值群組的四個資料分割都結合至 `Internet_Sales_2004` 目標資料分割中。 此範例會參考 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 範例 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 資料庫的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Cube。  
  
```  
<MergePartitions xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Sources>  
     <Source>  
        <DatabaseID>database</DatabaseID>  
        <CubeID>Adventure Works DW</CubeID>  
        <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
        <PartitionID>Internet_Sales_2001</PartitionID>  
     </Source>  
     <Source>  
      <DatabaseID>database</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2002</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>database</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2003</PartitionID>  
    </Source>  
  </Sources>  
  <Target>    <DatabaseID>database</DatabaseID>    <CubeID>Adventure Works DW</CubeID>    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>    <PartitionID>Internet_Sales_2004</PartitionID>  </Target>  
</MergePartitions>  
```  
  
## <a name="see-also"></a>另請參閱  
 [Source 元素&#40;XMLA&#41;](source-element-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  