---
title: 瀏覽貝氏機率分類模型 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f9160b48-3beb-439c-9694-f084e1afa625
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 65b8bb26a72903644b5985d69efc8adb362fe412
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66088474"
---
# <a name="browsing-a-naive-bayes-model"></a>瀏覽貝式機率分類模型
  當您開啟使用貝氏機率分類模型**瀏覽**，具有四個不同窗格的互動式檢視器中會顯示此模型。 您可以使用此檢視器來探索相互關聯，以及取得有關模型和基礎資料的資訊。  
  
-   [相依性網路](#bkmk_DepNet)  
  
-   [屬性設定檔](#bkmk_AttProf)  
  
-   [屬性特性](#bkmk_AttChar)  
  
-   [屬性辨識](#bkmk_AttDisc)  
  
##  <a name="BKMK_Tabs"></a> 瀏覽模型  
 此檢視器的用途是要協助您探索 [!INCLUDE[msCoName](../includes/msconame-md.md)] 貝氏機率分類模型所發現之輸入與輸出屬性 (輸入與相依變數) 之間的互動。  
  
 如果您想要試驗貝氏機率分類檢視器，使用[分類精靈&#40;適用於 Excel 的資料採礦增益集&#41;](classify-wizard-data-mining-add-ins-for-excel.md)精靈] 中的資料採礦功能區中，按一下 [**進階**選項，然後變更演算法使用貝氏機率分類演算法  
  
 如需這些範例中，我們使用範例活頁簿中的來源資料和分組資料行中， **Yearly Income**，五個收入群組，從**非常低**來**極高**。 然後，貝氏機率分類模型便分析了與每個收入類別目錄相互關聯的因數。  
  
###  <a name="bkmk_DepNet"></a> 相依性網路  
 您將使用第一個時段**相依性網路**。 它會概略顯示哪些輸入與選取的結果密切相關。  
  
 ![貝氏機率分類檢視器中的相依性網路](media/dm13-nb.gif "貝氏機率分類檢視器中的相依性網路")  
  
##### <a name="explore-the-dependency-network"></a>探索相依性網路  
  
1.  首先，請按一下目標結果**Yearly Income**，它會呈現為圖形中的節點。  
  
     目標變數周圍的反白顯示節點就是在統計上與此結果相關的節點。 請使用位於檢視器底部的圖例來了解關聯性的本質。  
  
2.  按一下檢視器左側的滑動軸，並向下拖曳。  
  
     此控制項會根據相依性的強度，篩選獨立變數。 當您向下拖曳滑動軸時，圖形中只會保留最強的連結。  
  
3.  篩選圖形之後，按一下  按鈕**複製圖表檢視**。 然後，選取 Excel 中的工作表，並且按下 Ctrl+V。  
  
     此選項會複製您已經選取的檢視，包括篩選和反白顯示。  
  
 [回到頁首](#BKMK_Tabs)  
  
###  <a name="bkmk_AttProf"></a> 屬性設定檔  
 **屬性設定檔**windows 可讓您如何所有其他變數與相關的個別結果的視覺指示。  
  
##### <a name="explore-the-profiles"></a>探索設定檔  
  
1.  若要隱藏部分值，讓您能夠更輕易地比較結果，請按一下資料行標題並將它拖曳到其他資料行底下。  
  
     ![屬性在貝氏機率分類檢視器中的設定檔](media/dm13-nb-attprof.gif "屬性在貝氏機率分類檢視器中的設定檔")  
  
2.  按一下任何資料格檢視中的值分佈**採礦圖例**。  
  
     因為與不同結果相關聯的屬性會以視覺效果方式顯示，所以您可以輕鬆地識別感興趣的相互關聯，例如各地區的收入分佈狀況。  
  
3.  若要取得此檢視的基礎資料，請按一下**複製至 Excel**。 系統就會在新的工作表中產生資料表，其中顯示個別屬性與結果之間的相互關聯。 在這個 Excel 資料表中，您可以輕鬆地隱藏或篩選資料行。  
  
 [回到頁首](#BKMK_Tabs)  
  
###  <a name="bkmk_AttChar"></a> 屬性特性  
 **屬性特性**檢視對於深入檢查特定結果變數和影響因數有用處。  
  
 ![屬性在貝氏機率分類檢視器中的特性](media/dm13-nb-viewer.gif "屬性在貝氏機率分類檢視器中的特性")  
  
##### <a name="explore-the-attribute-characteristics"></a>探索屬性特性  
  
1.  按一下 **值**，然後選取的項目**值**。  
  
     當您選取目標結果時，圖形就會更新為顯示與結果關聯最強的因數，並按照重要性排序。  
  
     請注意，如果您建立模型，使用[分析關鍵影響因數&#40;適用於 Excel 的資料表分析工具&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)選項，您可以建立具有多個可預測屬性的模型。 不過，資料採礦增益集中的所有其他精靈則會限制使用一個可預測屬性。  
  
2.  按一下 **複製至 Excel**建立資料表，在新的工作表，列出所選的目標結果相關的所有屬性的分數。  
  
 [回到頁首](#BKMK_Tabs)  
  
###  <a name="bkmk_AttDisc"></a> 屬性辨識  
 **屬性辨識**檢視有助於比較兩個結果或不同的結果，與所有其他結果。  
  
 ![屬性在貝氏機率分類檢視器中的辨識](media/dm13-nb-attdisc.gif "屬性辨識在貝氏機率分類檢視器")  
  
##### <a name="explore-attribute-discrimination"></a>探索屬性辨識  
  
1.  使用控制項，**值 1**並**值 2**來選取您想要比較的結果。  
  
     比方說，在此模型沒有一些有趣的屬性在低收入群組中，因此我們在第一個下拉式清單中，選擇了最低收入群組，然後選擇**的所有其他州**第二個下拉式清單中。  
  
     屬性就會按照重要性的順序 (根據定型資料計算而來) 排序。 因此，職業是與收入最密切相關的因數 (至少這個目標群組是如此)。  
  
     若要查看確切的數據，請按一下彩色的列並檢視**採礦圖例**。  
  
2.  請注意，較低收入也與歐洲地區相互關聯。  
  
     貝氏機率分類模型不支援向下鑽研。不過，如果您想要調查與這個結果群組相關聯的案例，可以使用查詢。 在這種類型的模型上查詢的相關資訊，請參閱[貝氏機率分類模型查詢範例](data-mining/naive-bayes-model-query-examples.md)。  
  
 [回到頁首](#BKMK_Tabs)  
  
## <a name="see-also"></a>另請參閱  
 [瀏覽模型，在 Excel 中的&#40;SQL Server 資料採礦增益集&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
