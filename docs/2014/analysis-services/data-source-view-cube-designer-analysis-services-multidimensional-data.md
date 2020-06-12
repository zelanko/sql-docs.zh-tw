---
title: 資料來源視圖（Cube 結構索引標籤，Cube 設計師）（Analysis Services 多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.cubebuilder.datasourcepane.f1
ms.assetid: 1e39c910-5c10-4624-be27-ca02a461b46b
author: minewiskan
ms.author: owend
ms.openlocfilehash: a922f23cf667068ff51c315563b8fc3b35fceefe
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528986"
---
# <a name="data-source-view-cube-structure-tab-cube-designer-analysis-services---multidimensional-data"></a>資料來源檢視 (Cube 結構索引標籤，Cube 設計師) (Analysis Services - 多維度資料)
  使用 **[資料來源檢視]** 窗格，即可檢視來自與所選取 Cube 相關聯之資料來源檢視的資料表和資料行。 此窗格會用來建立量值群組和量值，方法是從 **[資料來源檢視]** 窗格中，將資料行拖曳至 **[量值]** 窗格中。  
  
## <a name="options"></a>選項  
 **[資料來源檢視]**  
 顯示與所選取 Cube 相關聯的資料來源檢視。  
  
 **(移動視點)**  
 按一下窗格右下角的捲軸之間，即可選取要檢視的 [資料來源檢視]**** 窗格區域。  
  
## <a name="diagram-context-menu"></a>圖表內容功能表  
 以滑鼠右鍵按一下 [資料來源檢視]**** 窗格的圖表背景，即可顯示提供下列選項的操作功能表：  
  
 **顯示資料表**  
 顯示 [顯示資料表]**** 對話方塊。 如需 [顯示資料表]**** 對話方塊的詳細資訊，請參閱[顯示資料表對話方塊 &#40;Analysis Services - 多維度資料&#41;](show-table-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **顯示所有資料表**  
 在窗格中顯示與 Cube 相關聯之資料來源檢視包含的所有資料表。  
  
 **僅顯示使用過的資料表**  
 在窗格中只顯示相關聯資料來源檢視之 Cube 所使用的資料表。  
  
 **顯示易記名稱**  
 選取在窗格中顯示物件的易記名稱。  
  
 **全選**  
 選取窗格中的所有物件。  
  
 **尋找資料表**  
 顯示 [尋找資料表]**** 對話方塊。 如需 [尋找資料表]**** 對話方塊的詳細資訊，請參閱[尋找資料表對話方塊 &#40;Analysis Services - 多維度資料&#41;](find-table-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **排列資料表**  
 選取 [切換到對角線配置]**** 或 [切換到矩形配置]**** 之後，會根據指定的配置來排列窗格中的物件。  
  
 **切換到對角線配置**  
 選取以對角線模式排列物件。  
  
> [!NOTE]  
>  唯有選取 [切換到矩形配置]**** 之後，才會顯示此選項。  
  
 **切換到矩形配置**  
 選取以矩形模式排列物件。  
  
> [!NOTE]  
>  唯有選取 [切換到對角線配置]**** 之後，才會顯示此選項。  
  
 **編輯資料來源檢視**  
 顯示與物件相關聯之資料來源檢視的資料來源檢視設計師。 如需資料來源檢視設計工具的詳細資訊，請參閱[資料來源檢視設計工具 &#40;Analysis Services - 多維度資料&#41;](data-source-view-designer-analysis-services-multidimensional-data.md)。  
  
 **顯示資料來源檢視於**  
 選取下列其中一個選項，以下列模式來切換檢視 [資料來源檢視]**** 窗格：  
  
-   圖表  
  
     顯示與目前 Cube 相關聯之資料表和資料行的圖表。  
  
-   樹狀結構  
  
     顯示樹狀檢視，其中包含與目前 Cube 相關聯的資料表和資料行。  
  
 **複製圖表來源**  
 選取與 Cube 相關聯之資料來源檢視所包含的其中一個圖表，以顯示在 [資料來源檢視]**** 窗格中。  
  
 **縮放**  
 選取可用的顯示比例選項。  
  
 **屬性**  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中顯示與 Cube 相關聯之資料來源檢視的 [屬性]**** 視窗。  
  
## <a name="table-context-menu"></a>資料表內容功能表  
 以滑鼠右鍵按一下 [資料來源檢視]**** 窗格中的資料表或檢視名稱，即可顯示提供下列選項的操作功能表：  
  
 **顯示相關資料表**  
 在窗格中顯示與資料來源檢視中所選取資料表相關的資料表。  
  
 **隱藏資料表**  
 從窗格中移除資料表。  
  
 **探索資料**  
 顯示所選取資料表的 [瀏覽資料]**** 對話方塊。  
  
 **編輯資料來源檢視**  
 針對包含選定資料表的資料來源檢視顯示 [資料來源檢視設計師]。 如需資料來源檢視設計工具的詳細資訊，請參閱[資料來源檢視設計工具 &#40;Analysis Services - 多維度資料&#41;](data-source-view-designer-analysis-services-multidimensional-data.md)。  
  
 **從資料表新增量值群組**  
 在 [量值]**** 窗格中，依據所選取資料表定義新的量值群組。  
  
> [!NOTE]  
>  只有在 [量值]**** 窗格中的量值群組尚未參考資料表時，才會啟用此選項。  
  
 **屬性**  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中顯示所選取資料表的 [屬性]**** 視窗。  
  
## <a name="column-context-menu"></a>資料行內容功能表  
 在 [資料來源檢視]**** 窗格中，以滑鼠右鍵按一下資料表或檢視中的資料行名稱，即可顯示提供下列選項的操作功能表：  
  
 **從資料行新增量值**  
 在 [量值]**** 窗格中，依據所選取資料行定義新的量值。  
  
 **探索資料**  
 顯示包含所選取資料行之資料表的 [瀏覽資料]**** 對話方塊。  
  
 **編輯資料來源檢視**  
 針對包含選定資料行的資料來源檢視顯示 [資料來源檢視設計師]。 如需資料來源檢視設計工具的詳細資訊，請參閱[資料來源檢視設計工具 &#40;Analysis Services - 多維度資料&#41;](data-source-view-designer-analysis-services-multidimensional-data.md)。  
  
 **屬性**  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中顯示所選取資料行的 [屬性]**** 視窗。  
  
## <a name="relationship-context-menu"></a>關聯性內容功能表  
 以滑鼠右鍵按一下 [資料來源檢視]**** 窗格中的關聯性，即可顯示提供下列選項的操作功能表：  
  
 **編輯資料來源檢視**  
 顯示包含所選取關聯性之資料來源檢視的資料來源檢視設計師。 如需資料來源檢視設計工具的詳細資訊，請參閱[資料來源檢視設計工具 &#40;Analysis Services - 多維度資料&#41;](data-source-view-designer-analysis-services-multidimensional-data.md)。  
  
 **屬性**  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，顯示所選取關聯性的 [屬性]**** 視窗。  
  
## <a name="see-also"></a>另請參閱  
 [工具列 &#40;Cube 結構索引標籤、Cube 設計工具&#41; &#40;Analysis Services 多維度資料&#41;](toolbar-cube-structure-cube-designer-analysis-services-multidimensional-data.md)   
 [量值 &#40;Cube 結構索引標籤、Cube 設計工具&#41; &#40;Analysis Services 多維度資料&#41;](measures-cube-structure-cube-designer-analysis-services-multidimensional-data.md)   
 [維度 &#40;Cube 結構索引標籤、Cube 設計工具&#41; &#40;Analysis Services 多維度資料&#41;](dimensions-cube-structure-cube-designer-analysis-services-multidimensional-data.md)   
 [Cube 結構 &#40;Cube 設計師&#41; &#40;Analysis Services 多維度資料&#41;](cube-structure-cube-designer-analysis-services-multidimensional-data.md)  
  
  
