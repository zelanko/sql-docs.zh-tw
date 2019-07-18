---
title: 合併資料分割 (XMLA) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 419ebd0d67b65213fde7393430aedec14249b2ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63261634"
---
# <a name="merging-partitions-xmla"></a>合併資料分割 (XMLA)
  如果資料分割有相同的彙總設計與結構，您可以使用來合併資料分割[MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla) XML for Analysis (XMLA) 命令。 合併資料分割是管理資料分割時要執行的一項重要的動作，特別是那些包含依日期分割的歷程記錄資料之資料分割。  
  
 例如，財務 Cube 可能使用兩個資料分割：  
  
-   一個資料分割代表今年的財務資料，基於效能目的使用即時關聯式 OLAP (ROLAP) 儲存設定。  
  
-   另一個資料分割包含往年的財務資料，基於儲存目的使用多維度 OLAP (MOLAP) 儲存設定。  
  
 兩個資料分割使用不同的儲存設定，但是使用相同的彙總設計。 而不是處理跨多年歷程記錄資料結尾的一年的 cube，您可以改為使用**MergePartitions**前幾年到資料分割合併的資料分割目前年度的命令。 如此便可保存資料，而不需要將時間耗費在 Cube 的完整處理上。  
  
## <a name="specifying-partitions-to-merge"></a>指定要合併的資料分割  
 當**MergePartitions**命令執行時，儲存在指定之來源資料分割的彙總資料[來源](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)屬性中指定的目標資料分割加入[目標](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla)屬性。  
  
> [!NOTE]  
>  **來源**屬性可包含多個資料分割物件參考。 不過，**目標**屬性不能。  
  
 為了能夠成功合併，在指定的資料分割**來源**並**目標**必須包含相同的量值群組，並使用相同的彙總設計。 否則，系統將發生錯誤。  
  
 指定之資料分割**來源**會在後刪除**MergePartitions**命令成功完成。  
  
## <a name="examples"></a>範例  
  
### <a name="description"></a>描述  
 下列範例會合併中的所有資料分割**Customer Counts**量值群組**Adventure Works** cube 中**Adventure Works DW**範例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的資料庫**Customers_2004**資料分割。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [在 Analysis Services 中使用 XMLA 進行開發](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
