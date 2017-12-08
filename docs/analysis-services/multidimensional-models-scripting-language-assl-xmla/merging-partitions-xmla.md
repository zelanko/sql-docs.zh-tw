---
title: "合併資料分割 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- merging partitions [XMLA]
- XMLA, partitions
- partitions [Analysis Services], XML for Analysis
- XML for Analysis, partitions
ms.assetid: 657e1d4d-6d50-40f8-a771-7b20c9d865f8
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 90d92549184a5dc3a93123a86870d3905f38791a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="merging-partitions-xmla"></a>合併資料分割 (XMLA)
  如果資料分割有相同的彙總設計與結構，您可以合併資料分割使用[MergePartitions](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md) XML for Analysis (XMLA) 命令。 合併資料分割是管理資料分割時要執行的一項重要的動作，特別是那些包含依日期分割的歷程記錄資料之資料分割。  
  
 例如，財務 Cube 可能使用兩個資料分割：  
  
-   一個資料分割代表今年的財務資料，基於效能目的使用即時關聯式 OLAP (ROLAP) 儲存設定。  
  
-   另一個資料分割包含往年的財務資料，基於儲存目的使用多維度 OLAP (MOLAP) 儲存設定。  
  
 兩個資料分割使用不同的儲存設定，但是使用相同的彙總設計。 而不是處理跨多年歷程記錄資料結尾的一年的 cube，您可以改為使用**MergePartitions**目前年度的合併資料分割資料分割到往年的命令。 如此便可保存資料，而不需要將時間耗費在 Cube 的完整處理上。  
  
## <a name="specifying-partitions-to-merge"></a>指定要合併的資料分割  
 當**MergePartitions**命令執行時，在指定的來源資料分割中儲存的彙總資料[來源](../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)屬性中指定的目標資料分割加入[目標](../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)屬性。  
  
> [!NOTE]  
>  **來源**屬性可以包含多個資料分割物件參考。 不過，**目標**屬性不能。  
  
 為了能夠成功合併，在指定的資料分割**來源**和**目標**必須包含相同的量值群組，並使用相同的彙總設計。 否則，系統將發生錯誤。  
  
 在指定的資料分割**來源**後刪除**MergePartitions**命令成功完成。  
  
## <a name="examples"></a>範例  
  
### <a name="description"></a>Description  
 下列範例會合併中的所有資料分割**Customer Counts**量值群組**Adventure Works** cube 中**Adventure Works DW**範例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫到**Customers_2004**磁碟分割。  
  
### <a name="code"></a>程式碼  
  
```  
<MergePartitions xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Sources>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2001</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2002</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2003</PartitionID>  
    </Source>  
  </Sources>  
  <Target>  
    <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    <CubeID>Adventure Works DW</CubeID>  
    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
    <PartitionID>Internet_Sales_2004</PartitionID>  
  </Target>  
</MergePartitions>  
```  
  
## <a name="see-also"></a>請參閱＜  
 [在 Analysis Services 中使用 XMLA 進行開發](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
