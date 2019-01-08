---
title: 合併資料分割 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- merging partitions [XMLA]
- XMLA, partitions
- partitions [Analysis Services], XML for Analysis
- XML for Analysis, partitions
ms.assetid: 657e1d4d-6d50-40f8-a771-7b20c9d865f8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6a7a72e385dd6cfb4d0d83d3afab346dab8c85ef
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53367340"
---
# <a name="merging-partitions-xmla"></a>合併資料分割 (XMLA)
  如果資料分割有相同的彙總設計與結構，您可以使用來合併資料分割[MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla) XML for Analysis (XMLA) 命令。 合併資料分割是管理資料分割時要執行的一項重要的動作，特別是那些包含依日期分割的歷程記錄資料之資料分割。  
  
 例如，財務 Cube 可能使用兩個資料分割：  
  
-   一個資料分割代表今年的財務資料，基於效能目的使用即時關聯式 OLAP (ROLAP) 儲存設定。  
  
-   另一個資料分割包含往年的財務資料，基於儲存目的使用多維度 OLAP (MOLAP) 儲存設定。  
  
 兩個資料分割使用不同的儲存設定，但是使用相同的彙總設計。 您不需要在年底時處理跨多年歷程記錄資料的 Cube，只要改用 `MergePartitions` 命令將今年的資料分割合併到往年的資料分割中。 如此便可保存資料，而不需要將時間耗費在 Cube 的完整處理上。  
  
## <a name="specifying-partitions-to-merge"></a>指定要合併的資料分割  
 當`MergePartitions`命令執行時，儲存在指定之來源資料分割的彙總資料[來源](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)屬性中指定的目標資料分割加入[目標](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla)屬性。  
  
> [!NOTE]  
>  `Source` 屬性可包含一個以上的資料分割物件參考。 不過，`Target` 屬性則不可以。  
  
 為了能夠成功合併，在 `Source` 與 `Target` 中指定的資料分割，必須由相同的量值群組包含，並使用相同的彙總設計。 否則，系統將發生錯誤。  
  
 在 `Source` 中指定的資料分割會在 `MergePartitions` 命令成功完成後刪除。  
  
## <a name="examples"></a>範例  
  
### <a name="description"></a>描述  
 下列範例會合併中的所有資料分割**Customer Counts**量值群組**Adventure Works** cube 中**Adventure Works DW**範例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的資料庫**Customers_2004**資料分割。  
  
### <a name="code"></a>程式碼  
  
```  
<MergePartitions xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
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
 [在 Analysis Services 中使用 XMLA 進行開發](developing-with-xmla-in-analysis-services.md)  
  
  
