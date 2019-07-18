---
title: 計算工具 （計算索引標籤，Cube 設計師） (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.calculationsview.calculationtoolspane.f1
ms.assetid: b1aa8a1a-6532-45d2-8f53-d3e211d7197a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ff0f13ec91ef1e8796ed5ebd5ccf3cc37ff2f354
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66088283"
---
# <a name="calculation-tools-calculations-tab-cube-designer-analysis-services---multidimensional-data"></a>計算工具 (計算索引標籤，Cube 設計師) (Analysis Services - 多維度資料)
  使用 Cube 設計師之 **[計算]** 索引標籤上的 **[計算工具]** 窗格，即可瀏覽可在計算中使用的中繼資料、函數以及範本。  
  
## <a name="options"></a>選項  
 **中繼資料**  
 顯示選取之 Cube 的中繼資料。  
  
 將選取的元素拖曳至 [指令碼編輯器]、[導出成員表單編輯器] 或 [命名集表單編輯器] 窗格，即可在窗格中選取的位置包含該元素的多維度運算式 (MDX) 語法。  
  
 **函數**  
 顯示運算式和條件可用的函數。  
  
 將選取的元素拖曳至 **[指令碼編輯器]** 、 **[導出成員表單編輯器]** 或 **[命名集表單編輯器]** 窗格，即可在窗格中選取的位置包含該元素的 MDX 語法。  
  
> [!NOTE]  
>  在專案模式中， **[計算工具]** 對話方塊會從名為 MDXFunctions.xml 的 XML 檔案 (包含在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中) 讀取此選項的資訊。 在線上模式中，此選項的資訊是從執行個體的 MDSCHEMA_FUNCTIONS 結構描述資料列集擷取。  
  
 **範本**  
 顯示導出成員、命名集以及指令碼命令可用之預先定義的範本。  
  
 將選取的元素拖曳至 **[指令碼編輯器]** 、 **[導出成員表單編輯器]** 或 **[命名集表單編輯器]** 窗格，即可在窗格中選取的位置包含該元素的 MDX 語法。  
  
## <a name="context-menu"></a>操作功能表  
 以滑鼠右鍵按一下 [計算工具]  窗格中的元素，即可顯示提供下列選項的內容功能表：  
  
 **[複製]**  
 選取即可將 **[中繼資料]** 或 **[函數]** 中選取的元素複製到剪貼簿。  
  
> [!NOTE]  
>  如果已選取 **[範本]** ，則不會顯示此選項。  
  
> [!NOTE]  
>  如果選取的成員無法複製 (例如 **[中繼資料]** 中顯示之維度的 **[集]** 資料夾或 **[函數]** 中顯示之函數的函數群組資料夾)，則會停用此選項。  
  
 **篩選成員**  
 選取即可顯示 **[篩選成員]** 對話方塊，並篩選針對 **[中繼資料]** 中選取之元素顯示的成員。 如需 [篩選成員]  對話方塊的詳細資訊，請參閱[篩選成員對話方塊 &#40;Analysis Services - 多維度資料&#41;](filter-members-dialog-box-analysis-services-multidimensional-data.md)。  
  
> [!NOTE]  
>  只有選取 **[中繼資料]** 時，才會顯示此選項。  
  
> [!NOTE]  
>  只有在 **[中繼資料]** 中選取屬性的層級時，才會啟用此選項。  
  
 **新增範本**  
 選取即可根據選取的 Cube 指令碼範本來加入新的導出成員、命名集或指令碼命令，並顯示適合該命令 (以表單檢視) 的 [指令碼編輯器]  、[導出成員表單編輯器]  或 [命名集表單編輯器]  ，或將 [指令碼編輯器]  窗格的內容捲動至 Cube 指令碼中命令的位置 (以指令碼檢視)。  
  
> [!NOTE]  
>  只有選取 **[中繼資料]** 時，才會顯示此選項。  
  
## <a name="see-also"></a>另請參閱  
 [Cube 設計師&#40;Analysis Services-多維度資料&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [工具列&#40;計算索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](toolbar-calculations-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [指令碼組合管理&#40;計算索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](script-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [導出成員表單編輯器&#40;計算索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](calculated-member-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [命名集表單編輯器&#40;計算索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](named-set-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [指令碼編輯器&#40;計算索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](script-editor-calculations-cube-designer-analysis-services-multidimensional-data.md)   
 [計算&#40;Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](calculations-cube-designer-analysis-services-multidimensional-data.md)  
  
  
