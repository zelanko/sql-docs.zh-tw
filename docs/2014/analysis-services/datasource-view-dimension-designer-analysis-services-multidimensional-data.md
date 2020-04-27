---
title: 資料來源視圖（維度結構索引標籤，維度設計師）（Analysis Services 多維度資料） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.datasourcepane.f1
ms.assetid: c4bd3c5e-8986-448f-b9db-3551f50f0696
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 38d61436f6245024dcc477d39b7b2589234658ee
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66082350"
---
# <a name="data-source-view-dimension-structure-tab-dimension-designer-analysis-services---multidimensional-data"></a>資料來源檢視 (維度結構索引標籤，維度設計師) (Analysis Services - 多維度資料)
  使用 [資料來源檢視]**** 窗格，即可從與選取之維度相關聯的資料來源檢視中檢視資料表和資料行。 此窗格會用來建立屬性 (attribute)、成員屬性 (property)、階層以及層級，方式是藉由從 [資料來源檢視]**** 窗格拖曳資料行至 ****[屬性] 或 [階層和層級]**** 窗格。  
  
## <a name="options"></a>選項。  
 **[資料來源檢視]**  
 顯示與選取之維度相關聯的資料來源檢視。  
  
 **(移動視點)**  
 按一下窗格右下角的捲軸之間，即可選取要檢視的 [資料來源檢視]**** 窗格區域。  
  
## <a name="diagram-context-menu"></a>圖表內容功能表  
 以滑鼠右鍵按一下 [資料來源檢視]**** 窗格中的圖表背景，即可顯示提供下表所列出之選項的內容功能表。  
  
 **顯示資料表**  
 顯示 [顯示資料表]**** 對話方塊。 如需 [顯示資料表]**** 對話方塊的詳細資訊，請參閱[顯示資料表對話方塊 &#40;Analysis Services - 多維度資料&#41;](show-table-dialog-box-analysis-services-multidimensional-data.md)。  
  
 **顯示所有資料表**  
 在窗格中顯示與維度相關聯之資料來源檢視中包含的所有資料表。  
  
 **僅顯示使用過的資料表**  
 在窗格中只顯示關聯資料來源檢視之維度所使用的那些資料表。  
  
 **顯示易記名稱**  
 選取即可顯示窗格中之物件的易記名稱。  
  
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
 顯示與維度相關聯之資料來源檢視的 [資料來源檢視設計工具]****。 如需**資料來源檢視設計工具**的詳細資訊，請參閱[資料來源檢視設計工具 &#40;Analysis Services - 多維度資料&#41;](data-source-view-designer-analysis-services-multidimensional-data.md)。  
  
 **顯示資料來源檢視於**  
 選取下列其中一個選項，以下列模式來切換檢視 [資料來源檢視]**** 窗格：  
  
-   圖表  
  
     顯示與目前維度相關聯之資料表與資料行的圖表。  
  
-   樹狀結構  
  
     顯示包含與目前維度相關聯之資料表與資料行的樹狀檢視。  
  
 **複製圖表來源**  
 選取與維度相關聯之資料來源檢視中包含的其中一個圖表，即可將它顯示在 [資料來源檢視]**** 窗格中。  
  
 **縮放**  
 選取可用的顯示比例選項。  
  
 **屬性**  
 針對與維度相關聯的資料來源檢視，顯示 [SQL Server Data Tools]**** 中的 [屬性]**** 視窗。  
  
## <a name="table-context-menu"></a>資料表內容功能表  
 以滑鼠右鍵按一下 [資料來源檢視]**** 窗格中的資料表或檢視名稱，即可顯示提供下表所列出之選項的內容功能表。  
  
 **顯示相關資料表**  
 在窗格中顯示與資料來源檢視中所選取資料表相關的資料表。  
  
 **隱藏資料表**  
 從窗格中移除資料表。  
  
 **探索資料**  
 顯示所選取資料表的 [瀏覽資料]**** 對話方塊。  
  
 **編輯資料來源檢視**  
 針對包含選取之資料表的資料來源視圖，顯示**資料來源視圖設計**工具。 如需**資料來源檢視設計工具**的詳細資訊，請參閱[資料來源檢視設計工具 &#40;Analysis Services - 多維度資料&#41;](data-source-view-designer-analysis-services-multidimensional-data.md)。  
  
 **屬性**  
 在 [SQL Server Data Tools]**** 中顯示所選資料表的 [屬性]**** 視窗。  
  
## <a name="column-context-menu"></a>資料行內容功能表  
 以滑鼠右鍵按一下 [資料來源檢視]**** 窗格中的資料表或檢視內的資料行，即可顯示提供下表所列出之選項的內容功能表。  
  
 **從資料行新增屬性**  
 在窗格中顯示與資料來源檢視中所選取資料表相關的資料表。  
  
 **探索資料**  
 顯示包含所選取資料行之資料表的 [瀏覽資料]**** 對話方塊。  
  
 **編輯資料來源檢視**  
 顯示包含所選取資料行之資料來源視圖的**資料來源視圖設計**工具。 如需**資料來源檢視設計工具**的詳細資訊，請參閱[資料來源檢視設計工具 &#40;Analysis Services - 多維度資料&#41;](data-source-view-designer-analysis-services-multidimensional-data.md)。  
  
 **屬性**  
 在 [SQL Server Data Tools]**** 中顯示所選資料行的 [屬性]**** 視窗。  
  
## <a name="relationship-context-menu"></a>關聯性內容功能表  
 以滑鼠右鍵按一下 [資料來源檢視]**** 窗格中的關聯性，即可顯示提供下表所列出之選項的內容功能表。  
  
 **編輯資料來源檢視**  
 顯示包含所選取關聯性之資料來源視圖的**資料來源視圖設計**工具。 如需**資料來源檢視設計工具**的詳細資訊，請參閱[資料來源檢視設計工具 &#40;Analysis Services - 多維度資料&#41;](data-source-view-designer-analysis-services-multidimensional-data.md)。  
  
 **屬性**  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，顯示所選取關聯性的 [屬性]**** 視窗。  
  
## <a name="see-also"></a>另請參閱  
 [維度結構 &#40;維度設計師&#41; &#40;Analysis Services-多維度資料&#41;](dimension-structure-dimension-designer-analysis-services-multidimensional-data.md)   
 [工具列 &#40;維度結構索引標籤、維度設計師&#41; &#40;Analysis Services-多維度資料&#41;](toolbar-dimension-structure-designer-analysis-services-multidimensional-data.md)   
 [屬性 &#40;維度結構索引標籤、維度設計師&#41; &#40;Analysis Services 多維度資料&#41;](attributes-dimension-designer-analysis-services-multidimensional-data.md)   
 [階層 &#40;維度結構索引標籤、維度設計師&#41; &#40;Analysis Services-多維度資料&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
