---
title: 中繼資料 （瀏覽器索引標籤，Cube 設計師） (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.metadatapane.f1
ms.assetid: a1ace545-488d-4645-8330-56408a5e8abd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3e4aade575cdcb8260865d4a1fe9ab6f4b7941fe
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66077849"
---
# <a name="metadata-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>中繼資料 (瀏覽器索引標籤，Cube 設計師) (Analysis Services - 多維度資料)
  使用 Cube 設計師中之 [瀏覽器] 索引標籤的 [中繼資料] 窗格瀏覽 Cube 的結構，以查看相關的量值，並檢視與建立維度。 您可以向下鑽研階層、檢視可用量值與 KPI 的清單，以及複製物件的完整名稱。  
  
 您也可以將 [中繼資料] 窗格中的物件和階層拖曳到查詢建立區域，以建立新查詢或匯出可在 Excel 中瀏覽的資料。  
  
## <a name="options"></a>選項。  
 **中繼資料**  
 顯示目前檢視中可用的中繼資料。 您可以按一下 Cube 圖示，然後使用 [選取 Cube] 對話方塊選擇一個新的 Cube 或檢視方塊，藉以變更檢視 (亦即目前選取的檢視方塊或 Cube)。 您也可以按一下 [量值群組]，然後從下拉式清單中選取一個新的量值群組，以篩選 [中繼資料] 窗格中提供的物件。  
  
 將選取的項目拖曳至在 [報表] 窗格中之 [!INCLUDE[msCoName](../includes/msconame-md.md)] Office 11.0 樞紐分析表控制項的篩選、資料、資料列或資料行區域，即可顯示選取之項目的資料。  
  
 **函數**  
 在 [瀏覽器] 中顯示可用來建立查詢或資料檢視之所有函數、運算子和常數的清單。 若要使用函數，請找出您要的函數，然後將其拖曳到查詢區域中。 語法定義便會加入至文字中  
  
> [!WARNING]  
>  當您在圖形設計檢視中作業時，無法使用 [函數] 清單。  
  
 當使用表格式模型時，函數清單包含 MDX 函數和 DAX 函數。 否則，該清單只包含 MDX。 即使 DAX 運算式可能是物件定義的一部分，多維度模型也無法直接使用 DAX 函數。  
  
 提示：包含 DAX 函數的資料夾會列出以全部大寫的字母。 其他所有資料夾則包含 MDX 函數。 比方說，有個統計函數的兩個資料夾：**統計**包含相關的 DAX 函數。  
  
## <a name="context-menu"></a>操作功能表  
 以滑鼠右鍵按一下 [中繼資料] 窗格所顯示的元素，即可顯示提供下列選項的操作功能表：  
  
|選項|描述|  
|------------|-----------------|  
|**加入查詢**|按一下可將選取的物件加入至查詢建立區域的下方窗格中。|  
|**加入篩選器**|按一下可將選取的維度、屬性、階層或層級加入 [瀏覽器] 的篩選區域。<br /><br /> 注意:只有當維度、 屬性、 階層時，才會啟用此選項，或選取層級。|  
|**[複製]**|按一下即可將選取的項目加入至剪貼簿。<br /><br /> 注意:此選項會複製物件的完整的名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [工具列&#40;瀏覽器索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [在 Excel 中分析&#40;瀏覽器索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [查詢和篩選&#40;瀏覽器索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [瀏覽器&#40;Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)  
  
  
