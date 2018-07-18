---
title: 瀏覽器 （Cube 設計師） (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.view.f1
ms.assetid: efb5ee1c-de50-4bfc-83ff-08a4f03c3ece
caps.latest.revision: 26
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bfa10bce2a4cd6462d1555b6b45fe375c6c68e04
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37236168"
---
# <a name="browser-cube-designer-analysis-services---multidimensional-data"></a>瀏覽器 (Cube 設計師) (Analysis Services - 多維度資料)
  使用 Cube 設計師中的 **[瀏覽器]** 索引標籤，瀏覽 Cube 中的維度、量值和 KPIS。 在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]中， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Cube 瀏覽器已與 MDX 查詢設計工具整合，並提供一個圖形使用者介面來協助您建立 MDX 查詢、篩選與配量 Cube，以及向下鑽研到階層。  
  
 **[瀏覽器]** 索引標籤有兩種模式： **設計模式** 和 **查詢模式**。 在任一種模式下，您都可以使用 **[中繼資料]** 窗格中的物件瀏覽 Cube，或者您可以將成員從 **[中繼資料]** 窗格拖曳到查詢區域中，以建立可擷取您要使用之資料的 MDX 查詢。  
  
 **瀏覽及查詢使用圖形設計模式**  
  
 下圖顯示圖形 **[設計模式]** 中的 **[瀏覽器]** 介面。  
  
 ![Analysis Services MDX 查詢設計工具，設計檢視](media/rsqd-dsawas-mdx-designmode.gif "Analysis Services MDX 查詢設計工具，設計檢視")  
  
 當您在圖形設計模式中，如果**自動執行**(![自動執行查詢](media/rsqdicon-autoexecute.gif "自動執行查詢")) 工具列上的切換按鈕已選取，**瀏覽器**執行查詢每次您拖放到 [資料] 窗格上的中繼資料物件。 您也可以手動執行查詢使用**執行查詢**(![執行查詢](media/rsqdicon-run.gif "執行查詢")) 工具列上的按鈕。  
  
 若要將圖形化查詢設計工具變更為 **[查詢]** 模式，並使用 MDX 陳述式的文字，請按一下工具列上的 **[設計模式]** 按鈕。  
  
 **瀏覽及查詢使用 MDX 文字模式**  
  
 當您處於 MDX 測試設計模式下時，可以直接使用 MDX。 **[中繼資料]** 窗格仍然可以使用，因此您可以將物件加入至查詢設計區域，而且您可以從 **[函數]** 窗格中的清單拖放 MDX 函數與運算子。  
  
 下圖顯示 [查詢模式] 的 **[瀏覽器]** 介面。  
  
 ![Analysis Services MDX 查詢設計工具，查詢檢視](media/rsqd-dsawas-mdx-querymode.gif "Analysis Services MDX 查詢設計工具，查詢檢視")  
  
 您可以開始在圖形設計模式下作業、加入任何所需的物件、將配量加入至 Cube，然後切換到文字模式以擴充所產生的預設 MDX 查詢，並加入其他成員屬性和資料格屬性。  
  
 **[中繼資料]** 窗格會顯示 **[中繼資料]** 和 **[函數]** 的索引標籤。 從 **[中繼資料]** 索引標籤中，可以將維度、階層、KPI 和量值拖曳至查詢設計區域中。 您可以將 **[函數]** 索引標籤上的函數拖曳至查詢設計區域。 當您執行查詢時，查詢設計區域會顯示 MDX 查詢的結果。 您也可以按一下 **[工具列]** 上的 **[在 Excel 中進行分析]** ，以便將資料匯出至 Microsoft Office Excel，並在樞紐分析表中檢視使用者檢視的結果。下列幾節會針對 **[瀏覽器]** 的各種模式，更詳細地描述其中的工具列和所有窗格。  
  
 請注意，當您在文字模式中，作業**自動執行**(![自動執行查詢](media/rsqdicon-autoexecute.gif "自動執行查詢")) 不能使用工具列上的切換按鈕。 不過，您可以手動方式執行查詢使用**執行查詢**(![執行查詢](media/rsqdicon-run.gif "執行查詢")) 工具列上的按鈕。  
  
## <a name="sections"></a>區段  
 **工具列**  
 工具列中包含可以在設計檢視或查詢檢視中使用的工具。 如需工具列及其功能用法的詳細資訊，請參閱[工具列 &#40;瀏覽器索引標籤，Cube 設計師&#41; &#40;Analysis Services - 多維度資料&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)。  
  
 **在 Excel 中進行分析**  
 使用 [在 Excel 中進行分析] 功能，將 Cube 資料的目前選取範圍傳送至 Cube，讓您可以在樞紐分析表中預覽資料。 資料目前的選取範圍是以您從 **[中繼資料]** 窗格加入的詞彙，以及您可能使用篩選和查詢建立函數定義的所有篩選。 如需詳細資訊，請參閱[在 Excel 中進行分析 &#40;瀏覽器索引標籤，Cube 設計師&#41; &#40;Analysis Services - 多維度資料&#41;](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md)。  
  
 **中繼資料**  
 使用 [中繼資料] 窗格檢視 Cube 所包含的物件、向下鑽研到階層，以及瀏覽和使用量值。 在 **[報表]** 窗格中選取資料並檢視與其相關聯的資料之後。 如需此窗格的詳細資訊，請參閱[中繼資料 &#40;瀏覽器索引標籤，Cube 設計師&#41; &#40;Analysis Services - 多維度資料&#41;](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md)。  
  
 **篩選與查詢**  
 使用設計介面的這個區域建立 MDX 查詢，方法是，從 [中繼資料] 窗格拖放物件，然後針對來源 Cube 或維度指定篩選條件。 如需詳細資訊，請參閱[查詢和篩選 &#40;瀏覽器索引標籤，Cube 設計師&#41; &#40;Analysis Services - 多維度資料&#41;](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Cube 物件&#40;Analysis Services-多維度資料&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)   
 [多維度模型中的 cube](multidimensional-models/cubes-in-multidimensional-models.md)   
 [Cube 設計師&#40;Analysis Services-多維度資料&#41;](cube-designer-analysis-services-multidimensional-data.md)  
  
  
