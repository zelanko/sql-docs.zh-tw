---
title: 更新儲存格 (XMLA) |微軟文件
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- modifying cells
- XMLA, cells
- updating cells
- cells [Analysis Services]
- XML for Analysis, cells
ms.assetid: a1c61496-36ee-4bce-98d9-d13440d349aa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f0eab50aa7e70aedee93eef2cefee648e6ceb5c9
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "81387888"
---
# <a name="updating-cells-xmla"></a>更新資料格 (XMLA)
  可以使用[UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla)命令更改多維數據集中啟用的多維數據集中一個或多個單元格的值,以便多維數據集回寫。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將更新的資訊儲存在包含要更新的單元格的每個分區的單獨回[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]寫 表中。  
  
> [!NOTE]  
>  `UpdateCells` 命令不支援在 Cube 回寫期間的配置。 要使用分配的寫回,應使用[語句](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla)命令發送多維表達式 (MDX) 更新語句。 有關詳細資訊,請參閱[更新多維資料集語句&#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-update-cube)。  
  
## <a name="specifying-cells"></a>指定資料格  
 命令[Cell](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla)的`UpdateCells`Cell 屬性包含要更新的儲存格。 您可以使用資料格的序數，來識別 `Cell` 屬性中的每個資料格。 從概念[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]上講,對多維數據集中的單元格進行數位,就像多維數據集是*p-* 維陣列一樣,其中*p*是座標軸數。 資料格的處理順序是以資料列為主。 下圖顯示計算資料格序數的公式。  
  
 ![計算資料格序數位置的公式](../../analysis-services/dev-guide/media/cellordinalformula.gif "計算資料格序數位置的公式")  
  
 知道單元格的元數后,可以在[Cell](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla)屬性[的 Value](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/value-element-xmla)屬性中指示單元格的預期值。  
  
## <a name="see-also"></a>另請參閱  
 [更新元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [在 Analysis Services 中使用 XMLA 進行開發](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
