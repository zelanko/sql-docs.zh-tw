---
title: 資料區域與地圖 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- data regions
ms.assetid: 3afb8874-b36c-4e44-a0d8-80d2f7135fb1
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 45ad6ab1b05dba67c15f2a75b99c490ed9339f0d
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56298466"
---
# <a name="data-regions-and-maps-report-builder-and-ssrs"></a>資料區域與地圖 (報表產生器及 SSRS)
  資料區是報表中的一個物件，可顯示報表資料集中的資料。 報表資料可以顯示為資料表、矩陣或清單中的數字和文字。可以以圖形方式顯示在圖表或量測計中，也可以根據地圖中的地理背景顯示。 資料表、矩陣與清單都是以 *Tablix* 資料區為基礎，可在需要時擴充以顯示資料集中的所有資料。 Tablix 資料區支援多個資料列與資料行群組，而且同時支援靜態與動態資料列和資料行。 圖表會使用各種圖表格式顯示多個數列和類別目錄群組。 量測計則會顯示資料集的單一值或彙總值。 地圖會將空間資料顯示為地圖元素，其外觀會隨著資料集中的彙總資料而改變。  
  
 您可以將資料區域或地圖儲存成報表組件。 [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="table"></a>資料表  
 資料表是逐一呈現資料列的資料區域。 資料表資料行是靜態的：您可以在設計報表時決定資料行的數目。 資料表資料列是動態的：它們會向下展開以容納資料。 您可以將群組加入至資料表，然後資料表就會依據選取的欄位或運算式組織資料。 如需將資料表新增至報表的資訊，請參閱[資料表 &#40;報表產生器及 SSRS&#41;](tables-report-builder-and-ssrs.md)。  
  
## <a name="matrix"></a>矩陣  
 「矩陣」(Matrix) 也稱為交叉資料表。 矩陣資料區域同時包含動態資料行和資料列：它們會展開以容納資料。 矩陣可以有動態資料行和資料列，以及靜態資料行和資料列。 資料行或資料列可以包含其他資料行或資料列，而且可用來分組資料。 如有關將矩陣加入至報表的詳細資訊，請參閱[矩陣&#40;報表產生器及 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)  
  
## <a name="list"></a>清單  
 「清單」(List) 是呈現依自由形式來安排之資料的資料區域。 您可以安排報表項目來建立一份表單，將文字方塊、影像和其他資料區域放在清單內的任何位置。 將清單加入報表的相關資訊，請參閱[列出&#40;報表產生器及 SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)。  
  
## <a name="chart"></a>圖表  
 圖表會以圖形方式來呈現資料。 橫條圖、圓形圖和折線圖都是圖表的範例，但另外還有許多其他支援的樣式。 將圖表加入至報表的相關資訊，請參閱[圖表&#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)。  
  
## <a name="gauge"></a>量測計  
 量測計會將資料呈現成範圍，其中包含指向範圍內特定值的指標。 量測計是用來顯示關鍵效能指標 (KPI) 和其他標準。 量測計的範例包括線性和循環。 如需有關將量測計加入至報表的詳細資訊，請參閱 <<c0> [ 量測計&#40;報表產生器及 SSRS&#41;](gauges-report-builder-and-ssrs.md)。</c0>  
  
## <a name="map"></a>地圖  
 地圖可讓您根據地理背景呈現資料。 地圖資料可以是來自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢的空間資料、ESRI 形狀檔，或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Bing 地圖底圖。 空間資料由多組座標所組成，這些座標會定義表示形狀或區域的多邊形、表示路線或路徑的線條與以標記表示的點。 您可以讓彙總資料與地圖元素產生關聯，來自動改變其色彩和大小。 例如，可以根據銷售量來改變商店的標記類型，或者根據速限來改變的色彩。 如需詳細資訊，請參閱[地圖 &#40;報表產生器及 SSRS&#41;](maps-report-builder-and-ssrs.md)。  
  
## <a name="data-regions-in-the-report-layout"></a>報表配置中的資料區  
 您可以將多個資料區加入至報表。 資料區會成長到可以容納所連結之報表資料集中的資料。 例如，依年度顯示每個產品銷售量的矩陣，其資料列群組是以產品名稱為基礎，而資料行群組則是以年度為基礎。 當您執行報表時，矩陣會針對每個產品向下展開頁面，並針對每個年度沿著頁面展開。 放在報表設計介面上之矩陣旁的圖表會顯示在轉譯之報表中展開的矩陣旁邊。 資料區在頁面上轉譯的方式會根據報表的輸出格式，遵循一組規則進行。 例如，為協助控制圖表和矩陣在頁面上轉譯的方式，您可以使用矩形做為容器或在清單中同時套疊兩個資料區。 如需詳細資訊，請參閱 [頁面配置和轉譯 &#40;報表產生器及 SSRS&#41;](page-layout-and-rendering-report-builder-and-ssrs.md)。  
  
## <a name="nested-data-regions"></a>巢狀資料區  
 您可以將資料區放在其他資料區內，成為巢狀結構。 例如，如果您要在資料庫中建立每個銷售人員的銷售記錄，您可以建立一份含有文字方塊和影像的清單，以便顯示員工的相關資訊，然後再將資料表和圖表資料區域加入至清單，以便顯示員工的銷售記錄。 如需詳細資訊，請參閱 [巢狀資料區 &#40;報表產生器及 SSRS&#41;](nested-data-regions-report-builder-and-ssrs.md)。  
  
## <a name="multiple-data-regions-linked-to-the-same-dataset"></a>連結至相同資料集的多個資料區域  
 您可以將多個資料區域連結至相同的資料集，以便提供相同資料的不同檢視。 例如，您可以在資料表和圖表中顯示相同的資料。 也可以撰寫報表來提供資料表的互動式排序按鈕，讓您在排序資料表時，就會自動排序圖表。 如需詳細資訊，請參閱 [將多個資料區連結至相同的資料集 &#40;報表產生器及 SSRS&#41;](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)。  
  
## <a name="data-for-a-data-region"></a>資料區的資料  
 每個 Tablix、圖表和量測計都是針對顯示單一資料集中的資料而設計。 地圖會顯示來自相同或不同資料集的空間資料和分析資料。 您也可以使用下列方式，包含來自從未連結到資料區之資料集的值：  
  
-   彙總與排序順序不相依的值，或限定為不同資料集範圍的群組。  
  
-   從不同資料集中的名稱/值組查閱值。  
  
 如需詳細資訊，請參閱[運算式 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [報表撰寫概念 &#40;報表產生器及 SSRS&#41;](report-authoring-concepts-report-builder-and-ssrs.md)   
 [報表、報表組件和報表定義 &#40;報表產生器及 SSRS&#41;](reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [頁面配置和轉譯 &#40;報表產生器及 SSRS&#41;](page-layout-and-rendering-report-builder-and-ssrs.md)   
 [教學課程&#40;報表產生器&#41;](../report-builder-tutorials.md)   
 [Reporting Services 教學課程 &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)  
  
  
