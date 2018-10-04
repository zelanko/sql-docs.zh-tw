---
title: 目標元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97d198e823acb9bf3c8915e18cbf723032f81b58
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079788"
---
# <a name="target-element-xmla"></a>Target 元素 (XMLA)
  表示期間合併的目標資料分割[MergePartitions](../xml-elements-commands/mergepartitions-element-xmla.md)命令。  
  
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
|資料類型和長度|None|  
|預設值|None|  
|基數|1-n：出現一次以上的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MergePartitions](../xml-elements-commands/mergepartitions-element-xmla.md)|  
|子元素|[CubeID](id-element-xmla.md)， [DatabaseID](databaseid-element-xmla.md)， [MeasureGroupID](measuregroupid-element-xmla.md)， [PartitionID](partitionid-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `Target`項目是單一磁碟分割所在的來源資料分割中，內容則是所指定的物件參考[來源](sources-element-xmla.md)項目之父代`MergePartitions`項目，要合併。  
  
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
  
  
