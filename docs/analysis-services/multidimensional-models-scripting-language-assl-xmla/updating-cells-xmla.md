---
title: 更新資料格 (XMLA) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 308b65da3e19847406176b220203cc754fa74245
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="updating-cells-xmla"></a>更新資料格 (XMLA)
  您可以使用[UpdateCells](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)命令以變更為 cube 回寫啟用的 cube 中的一個或多個資料格的值。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 每個資料分割，其中包含要更新的資料格個別的回寫資料表中儲存更新的資訊。  
  
> [!NOTE]  
>  **UpdateCells**命令不支援 cube 回寫期間的配置。 若要使用配置的回寫，您應該使用[陳述式](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)要傳送的多維度運算式 (MDX) UPDATE 陳述式命令。 如需詳細資訊，請參閱[UPDATE CUBE 陳述式&#40;MDX&#41;](../../mdx/mdx-data-manipulation-update-cube.md)。  
  
## <a name="specifying-cells"></a>指定資料格  
 [儲存格](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)屬性**UpdateCells**命令包含要更新之資料格。 識別每個儲存格**儲存格**屬性使用該資料格的序數。 就概念而言，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]如同 cube 是數字在 cube 中的資料格*p*-維陣列，其中*p*是軸的數目。 資料格的處理順序是以資料列為主。 下圖顯示計算資料格序數的公式。  
  
 ![若要計算的資料格的序數位置的公式](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/media/cellordinalformula.gif "公式來計算的資料格的序數位置")  
  
 一旦您知道資料格的序數時，您可以指示中的資料格的預期的值[值](../../analysis-services/xmla/xml-elements-properties/value-element-xmla.md)屬性[儲存格](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)屬性。  
  
## <a name="see-also"></a>另請參閱  
 [Update 元素 & #40;XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [使用 Analysis Services 中的 XMLA 進行開發](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
