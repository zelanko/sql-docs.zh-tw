---
title: 導出成員表單編輯器 （計算索引標籤，Cube 設計工具） (Analysis Services-多維度資料) |Microsoft 文件
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.cubeeditor.calculationexpression.calculatedmember.f1
ms.assetid: f7719b9e-b1e6-4792-90a6-30d9d8eb1196
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a697e65ae650726e59a2ddb515746f5ef1ebb63e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136316"
---
# <a name="calculated-member-form-editor-calculations-tab-cube-designer-analysis-services---multidimensional-data"></a>導出成員表單編輯器 (計算索引標籤，Cube 設計師) (Analysis Services - 多維度資料)
  在 Cube 設計師中，使用 **[計算]** 索引標籤上的 **[導出成表單編輯器]** 窗格，即可建立或修改導出成員。  
  
 **請注意** 這個窗格只會在表單檢視中顯示。  
  
## <a name="options"></a>選項。  
 **名稱**  
 鍵入導出成員的名稱。  
  
 **父屬性**  
 展開以檢視 [父階層]、[父成員] 和 [變更] 選項。  
  
 **父階層**  
 在選取的 Cube 中，選取要包含導出成員的維度和階層。 選取 MEASURES 即可定義導出量值。  
  
 **父成員**  
 選取將在其下方出現導出成員的成員。  
  
 **請注意** 如果 **[父階層]** 指定 MEASURES 以外的階層，才可以使用此選項。  
  
 **變更**  
 選取即可顯示 [選取父成員] 對話方塊，然後選擇 [父成員] 的成員。 如需 [選取父成員] 對話方塊的詳細資訊，請參閱[選取父成員對話方塊 &#40;Analysis Services - 多維度資料&#41;](select-parent-member-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **運算式**  
 展開以檢視或編輯導出成員的多維度運算式 (MDX) 運算式。  
  
 從 **[計算工具]** 窗格中，將選取的元素拖曳到這個選項，以包括所選元素的 MDX 語法。  
  
> [!NOTE]  
>  建議將此運算式評估為字串或數值。  
  
 **其他屬性**  
 展開以檢視 [格式字串]、[可見]、[非空白行為]、[色彩運算式] 和 [字型運算式] 選項。  
  
 **格式字串**  
 鍵入用來將導出成員所傳回值格式化的 MDX 格式字串，或是選取預先定義的格式字串。  
  
 如需 MDX 格式字串的詳細資訊，請參閱 [FORMAT_STRING 內容 &#40;MDX&#41;](multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md)。  
  
 **Visible**  
 選取 [True] 即可讓用戶端應用程式看見導出成員。  
  
 **非空白行為**  
 為導出成員選取用來解析 MDX 中之 NON EMPTY 查詢的量值名稱。 如果 **[非空白行為]** 屬性為空白，就必須重複評估導出成員來決定成員是否為空白。 如果 **[非空白行為]** 屬性包含量值的名稱，且指定的量值是空白的，就會將導出成員視為空白。  
  
> [!WARNING]  
>  此屬性已被取代。 請勿設定。 請參閱[Deprecated Analysis Services Features in SQL Server 2014](deprecated-analysis-services-features-in-sql-server-2014.md)如需詳細資訊。  
  
 **色彩運算式**  
 展開以檢視 [前景色彩] 和 [背景色彩] 選項。  
  
 **前景色彩**  
 鍵入會提供導出成員之前景色彩的 MDX 運算式。  
  
 從 **[計算工具]** 窗格中，將選取的元素拖曳到這個選項，以包括所選元素的 MDX 語法。  
  
 按一下色彩選擇按鈕即可顯示 [色彩] 對話方塊，並將指定色彩的 RGB (紅-綠-藍) 值插入 MDX 運算式。 如需 RGB 值的詳細資訊，請參閱 [FORE_COLOR 及 BACK_COLOR 內容 &#40;MDX&#41;](multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md)。  
  
 **背景色彩**  
 鍵入會提供導出成員之背景色彩的 MDX 運算式。  
  
 從 **[計算工具]** 窗格中，將選取的元素拖曳到這個選項，以包括所選元素的 MDX 語法。  
  
 按一下色彩選擇按鈕即可顯示 [色彩] 對話方塊，並將指定色彩的 RGB (紅-綠-藍) 值插入 MDX 運算式。 如需 RGB 值的詳細資訊，請參閱 [FORE_COLOR 及 BACK_COLOR 內容 &#40;MDX&#41;](multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents.md)。  
  
 **字型運算式**  
 展開以檢視 [字型名稱]、[字型大小] 和 [字型旗標] 選項。  
  
 **字型名稱**  
 鍵入會提供用於導出成員之字型名稱的 MDX 運算式。  
  
 從 **[計算工具]** 窗格中，將選取的元素拖曳到這個選項，以包括所選元素的 MDX 語法。  
  
 按一下字型選擇按鈕即可顯示 **[字型]** 對話方塊，並將指定字型的屬性值插入 MDX 運算式。 如需屬性值的詳細資訊，請參閱[建立和使用屬性值 &#40;MDX&#41;](creating-and-using-property-values-mdx.md)。  
  
 **字型大小**  
 鍵入會提供用於導出成員之字型大小的 MDX 運算式。  
  
 從 **[計算工具]** 窗格中，將選取的元素拖曳到這個選項，以包括所選元素的 MDX 語法。  
  
 按一下字型選擇按鈕即可顯示 **[字型]** 對話方塊，並將指定字型的屬性值插入 MDX 運算式。 如需屬性值的詳細資訊，請參閱[建立和使用屬性值 &#40;MDX&#41;](creating-and-using-property-values-mdx.md)。  
  
 **字型旗標**  
 鍵入會提供包含導出成員所用字型的字型旗標 (例如底線或粗體字) 之點陣圖值的 MDX 運算式。  
  
 從 **[計算工具]** 窗格中，將選取的元素拖曳到這個選項，以包括所選元素的 MDX 語法。  
  
 按一下字型選擇按鈕即可顯示 **[字型]** 對話方塊，並將指定字型的屬性值插入 MDX 運算式。 如需屬性值的詳細資訊，請參閱[建立和使用屬性值 &#40;MDX&#41;](creating-and-using-property-values-mdx.md)。  
  
## <a name="see-also"></a>另請參閱  
 [計算](multidimensional-models-olap-logical-cube-objects/calculations.md)   
 [建立導出的成員](multidimensional-models/create-calculated-members.md)   
 [Cube 設計師&#40;Analysis Services-多維度資料&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [計算&#40;Cube 設計師&#41; &#40;Analysis Services-多維度資料&#41;](calculations-cube-designer-analysis-services-multidimensional-data.md)   
 [工具列&#40;計算索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](toolbar-calculations-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [指令碼組合管理&#40;計算索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](script-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [計算工具&#40;計算索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](calculation-tools-cube-designer-analysis-services-multidimensional-data.md)   
 [命名集表單編輯器&#40;計算索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](named-set-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [指令碼編輯器&#40;計算索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](script-editor-calculations-cube-designer-analysis-services-multidimensional-data.md)  
  
  