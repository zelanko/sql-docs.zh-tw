---
title: "更新資料格 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- modifying cells
- XMLA, cells
- updating cells
- cells [Analysis Services]
- XML for Analysis, cells
ms.assetid: a1c61496-36ee-4bce-98d9-d13440d349aa
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f35a02cdbc620801bc7d999a8dbb74b02918db56
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="updating-cells-xmla"></a>更新資料格 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]您可以使用[UpdateCells](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)命令以變更為 cube 回寫啟用的 cube 中的一個或多個資料格的值。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]每個資料分割，其中包含要更新的資料格個別的回寫資料表中儲存更新的資訊。  
  
> [!NOTE]  
>  **UpdateCells**命令不支援 cube 回寫期間的配置。 若要使用配置的回寫，您應該使用[陳述式](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)要傳送的多維度運算式 (MDX) UPDATE 陳述式命令。 如需詳細資訊，請參閱[UPDATE CUBE 陳述式 &#40;MDX &#41;](../../mdx/mdx-data-manipulation-update-cube.md).  
  
## <a name="specifying-cells"></a>指定資料格  
 [儲存格](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)屬性**UpdateCells**命令包含要更新之資料格。 識別每個儲存格**儲存格**屬性使用該資料格的序數。 就概念而言，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]如同 cube 是數字在 cube 中的資料格*p*-維陣列，其中*p*是軸的數目。 資料格的處理順序是以資料列為主。 下圖顯示計算資料格序數的公式。  
  
 ![若要計算的資料格的序數位置的公式](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/media/cellordinalformula.gif "公式來計算的資料格的序數位置")  
  
 一旦您知道資料格的序數時，您可以指示中的資料格的預期的值[值](../../analysis-services/xmla/xml-elements-properties/value-element-xmla.md)屬性[儲存格](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)屬性。  
  
## <a name="see-also"></a>請參閱  
 [Update 元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [在 Analysis Services 中使用 XMLA 進行開發](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
