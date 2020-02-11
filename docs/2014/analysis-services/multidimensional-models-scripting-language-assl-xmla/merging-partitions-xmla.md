---
title: 合併資料分割（XMLA） |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
ms.openlocfilehash: 4f09255372478bdb9956b64283c8b94477598239
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62702039"
---
# <a name="merging-partitions-xmla"></a>合併資料分割 (XMLA)
  如果資料分割具有相同的匯總設計與結構，您可以使用 XML for Analysis （XMLA）中的[MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla)命令來合併資料分割。 合併資料分割是管理資料分割時要執行的一項重要的動作，特別是那些包含依日期分割的歷程記錄資料之資料分割。  
  
 例如，財務 Cube 可能使用兩個資料分割：  
  
-   一個資料分割代表今年的財務資料，基於效能目的使用即時關聯式 OLAP (ROLAP) 儲存設定。  
  
-   另一個資料分割包含往年的財務資料，基於儲存目的使用多維度 OLAP (MOLAP) 儲存設定。  
  
 兩個資料分割使用不同的儲存設定，但是使用相同的彙總設計。 您不需要在年底時處理跨多年歷程記錄資料的 Cube，只要改用 `MergePartitions` 命令將今年的資料分割合併到往年的資料分割中。 如此便可保存資料，而不需要將時間耗費在 Cube 的完整處理上。  
  
## <a name="specifying-partitions-to-merge"></a>指定要合併的資料分割  
 當`MergePartitions`命令執行時，會將儲存在[source](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)屬性中指定之來源分割區的匯總資料，加入[目標](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla)屬性中指定的目標資料分割。  
  
> [!NOTE]  
>  
  `Source` 屬性可包含一個以上的資料分割物件參考。 不過，`Target` 屬性則不可以。  
  
 為了能夠成功合併，在 `Source` 與 `Target` 中指定的資料分割，必須由相同的量值群組包含，並使用相同的彙總設計。 否則便會發生錯誤。  
  
 在 `Source` 中指定的資料分割會在 `MergePartitions` 命令成功完成後刪除。  
  
## <a name="examples"></a>範例  
  
### <a name="description"></a>描述  
 下列範例會將「**艾德工作」 DW**範例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫中 [ **Customer** count] 量值群組內的所有資料分割，合併到**Customers_2004** **的資料分割**中。  
  
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
  
  
