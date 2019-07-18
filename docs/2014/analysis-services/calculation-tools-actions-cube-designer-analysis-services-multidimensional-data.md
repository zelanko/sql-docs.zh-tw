---
title: 計算工具 （動作索引標籤，Cube 設計師） (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionsview.calculationtoolspane.f1
ms.assetid: a3370370-43cd-4cc2-bb9f-c0d988b96f05
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 087f5f5e3383fd66244541fea35160946936bc1c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66088341"
---
# <a name="calculation-tools-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>計算工具 (動作索引標籤，Cube 設計師) (Analysis Services - 多維度資料)
  使用 Cube 設計師之 **[動作]** 索引標籤上的 **[計算工具]** 窗格，即可瀏覽可以在動作、鑽研動作和報表動作中使用的中繼資料、函數以及範本。  
  
## <a name="options"></a>選項。  
 **中繼資料**  
 顯示選取之 Cube 的中繼資料。  
  
 將選取的元素拖曳至 [動作表單編輯器]  、[鑽研動作表單編輯器]  或 [報表動作表單編輯器]  窗格，即可在窗格中選取的位置包含該元素的多維度運算式 (MDX) 語法。  
  
 **函數**  
 顯示運算式和條件可用的函數。  
  
 將選取的元素拖曳至 **[動作表單編輯器]** 、 **[鑽研動作表單編輯器]** 或 **[報表動作表單編輯器]** 窗格，即可在窗格中選取的位置包含該元素的 MDX 語法。  
  
> [!NOTE]  
>  在專案模式中， **[計算工具]** 對話方塊會從名為 MDXFunctions.xml 的 XML 檔案 (包含在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中) 讀取此選項的資訊。 在線上模式中，此選項的資訊是從執行個體的 MDSCHEMA_FUNCTIONS 結構描述資料列集擷取。  
  
 **範本**  
 顯示動作可用之預先定義的範本。  
  
 將選取的元素拖曳至 **[動作表單編輯器]** 、 **[鑽研動作表單編輯器]** 或 **[報表動作表單編輯器]** 窗格，即可在窗格中選取的位置包含該元素的 MDX 語法。  
  
## <a name="context-menu"></a>操作功能表  
 以滑鼠右鍵按一下 [計算工具]  窗格中的元素，即可顯示提供下列選項的操作功能表：  
  
|選項|定義|  
|------------|----------------|  
|**[複製]**|選取即可將 **[中繼資料]** 或 **[函數]** 中選取的元素複製到剪貼簿。<br /><br /> 請注意，此選項仍未顯示是否**範本**已選取。 也請注意此選項會停用，是否選取的成員無法複製，這類**集**資料夾中顯示之維度**中繼資料**中顯示的函式，函式群組資料夾**函式**。|  
|**篩選成員**|選取即可顯示 **[篩選成員]** 對話方塊，並篩選針對 **[中繼資料]** 中選取之元素顯示的成員。 如需 [篩選成員]  對話方塊的詳細資訊，請參閱[篩選成員對話方塊 &#40;Analysis Services - 多維度資料&#41;](filter-members-dialog-box-analysis-services-multidimensional-data.md)。<br /><br /> 請注意，才會顯示此選項**中繼資料**已選取。 也請注意在 選取屬性的層級時，才會啟用此選項**中繼資料**。|  
|**新增範本**|選取即可根據選取的範本將新動作、鑽研動作或報表動作加入至 Cube，並分別顯示 **[動作表單編輯器]** 、 **[鑽研動作表單編輯器]** 或 **[報表動作表單編輯器]** 。<br /><br /> 注意:只有選取 **[中繼資料]** 時，才會顯示此選項。|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 指令碼基礎觀念 &#40;Analysis Services&#41;](multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [動作&#40;Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [工具列&#40;動作索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [動作組合管理&#40;動作索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [動作表單編輯器&#40;動作索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [鑽研動作表單編輯器&#40;動作索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](drillthrough-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [報表動作表單編輯器&#40;動作索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
