---
title: 流覽貝氏貝氏機率分類模型 |Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66088474"
---
# <a name="browsing-a-naive-bayes-model"></a>瀏覽貝式機率分類模型
  當您使用 **[流覽]** 來開啟簡單的貝氏機率分類模型時，該模型會顯示在具有四個不同窗格的互動式檢視器中。 您可以使用此檢視器來探索相互關聯，以及取得有關模型和基礎資料的資訊。  
  
-   [相依性網路](#bkmk_DepNet)  
  
-   [屬性設定檔](#bkmk_AttProf)  
  
-   [屬性特性](#bkmk_AttChar)  
  
-   [屬性辨識](#bkmk_AttDisc)  
  
##  <a name="explore-the-model"></a><a name="BKMK_Tabs"></a>探索模型  
 此檢視器的用途是要協助您探索 [!INCLUDE[msCoName](../includes/msconame-md.md)] 貝氏機率分類模型所發現之輸入與輸出屬性 (輸入與相依變數) 之間的互動。  
  
 如果您想要試驗簡單的貝氏機率分類檢視器，請使用 [分類] Wizard &#40;[資料採礦] 功能區中的 [[適用于 Excel 的資料採礦增益集&#41;](classify-wizard-data-mining-add-ins-for-excel.md) Wizard]，按一下 [ **Advanced** ] 選項，然後將演算法變更為 [使用簡單的貝氏機率分類演算法]  
  
 在這些範例中，我們使用範例活頁簿中的來源資料，並將資料行（**每年收入**）分組成五個收入群組，從**極低**到**非常高**。 然後，貝氏機率分類模型便分析了與每個收入類別目錄相互關聯的因數。  
  
###  <a name="dependency-network"></a><a name="bkmk_DepNet"></a>相依性網路  
 您將使用的第一個視窗是相依性**網路**。 它會概略顯示哪些輸入與選取的結果密切相關。  
  
 ![貝氏機率分類檢視器中的相依性網路](media/dm13-nb.gif "貝氏機率分類檢視器中的相依性網路")  
  
##### <a name="explore-the-dependency-network"></a>探索相依性網路  
  
1.  首先，按一下 [目標結果] [**年收入**]，這會以圖形中的節點表示。  
  
     目標變數周圍的反白顯示節點就是在統計上與此結果相關的節點。 請使用位於檢視器底部的圖例來了解關聯性的本質。  
  
2.  按一下檢視器左側的滑動軸，並向下拖曳。  
  
     此控制項會根據相依性的強度，篩選獨立變數。 當您向下拖曳滑動軸時，圖形中只會保留最強的連結。  
  
3.  篩選圖形之後，請按一下 [**複製圖形視圖**] 按鈕。 然後，選取 Excel 中的工作表，並且按下 Ctrl+V。  
  
     此選項會複製您已經選取的檢視，包括篩選和反白顯示。  
  
 [回到頁首](#BKMK_Tabs)  
  
###  <a name="attribute-profiles"></a><a name="bkmk_AttProf"></a> 屬性設定檔  
 [**屬性設定檔**] 視窗可讓您以視覺方式指出所有其他變數與個別結果的關聯。  
  
##### <a name="explore-the-profiles"></a>探索設定檔  
  
1.  若要隱藏部分值，讓您能夠更輕易地比較結果，請按一下資料行標題並將它拖曳到其他資料行底下。  
  
     ![貝氏機率分類檢視器中的屬性設定檔](media/dm13-nb-attprof.gif "貝氏機率分類檢視器中的屬性設定檔")  
  
2.  按一下任何資料格，即可在 [**挖掘圖例**] 中查看值的分佈。  
  
     因為與不同結果相關聯的屬性會以視覺效果方式顯示，所以您可以輕鬆地識別感興趣的相互關聯，例如各地區的收入分佈狀況。  
  
3.  若要取得此視圖的基礎資料，請按一下 [**複製到 Excel**]。 系統就會在新的工作表中產生資料表，其中顯示個別屬性與結果之間的相互關聯。 在這個 Excel 資料表中，您可以輕鬆地隱藏或篩選資料行。  
  
 [回到頁首](#BKMK_Tabs)  
  
###  <a name="attribute-characteristics"></a><a name="bkmk_AttChar"></a>屬性特性  
 [**屬性特性**] 視圖適用于深入檢查特定結果變數和貢獻因素。  
  
 ![貝氏機率分類檢視器中的屬性特性](media/dm13-nb-viewer.gif "貝氏機率分類檢視器中的屬性特性")  
  
##### <a name="explore-the-attribute-characteristics"></a>探索屬性特性  
  
1.  按一下 [**值**]，然後從**值**中選取一個專案。  
  
     當您選取目標結果時，圖形就會更新為顯示與結果關聯最強的因數，並按照重要性排序。  
  
     請注意，如果您使用 [[分析關鍵影響因數] &#40;[適用于 Excel 的資料表分析工具&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md) ] 選項建立模型，則可以建立具有一個以上可預測屬性的模型。 不過，資料採礦增益集中的所有其他精靈則會限制使用一個可預測屬性。  
  
2.  按一下 [**複製到 Excel** ]，在新的工作表中建立資料表，列出與所選目標結果相關之所有屬性的分數。  
  
 [回到頁首](#BKMK_Tabs)  
  
###  <a name="attribute-discrimination"></a><a name="bkmk_AttDisc"></a>屬性辨識  
 **屬性**辨識視圖有助於比較兩個結果，或一個結果與其他所有結果。  
  
 ![貝氏機率分類檢視器中的屬性辨識](media/dm13-nb-attdisc.gif "貝氏機率分類檢視器中的屬性辨識")  
  
##### <a name="explore-attribute-discrimination"></a>探索屬性辨識  
  
1.  使用 [**值 1** ] 和 [**值 2**] 控制項來選取您想要比較的結果。  
  
     例如，在此模型中，「低收入」群組中有一些有趣的屬性，因此我們在第一個下拉式清單中選擇最低的「收入」群組，然後在第二個下拉式清單中選擇 [**其他所有狀態**]。  
  
     屬性就會按照重要性的順序 (根據定型資料計算而來) 排序。 因此，職業是與收入最密切相關的因數 (至少這個目標群組是如此)。  
  
     若要查看確切的圖形，請按一下彩色列，並查看 [**挖掘圖例**]。  
  
2.  請注意，較低收入也與歐洲地區相互關聯。  
  
     貝氏機率分類模型不支援向下鑽研。不過，如果您想要調查與這個結果群組相關聯的案例，可以使用查詢。 如需這種模型類型之查詢的詳細資訊，請參閱[貝氏貝氏機率分類模型查詢範例](data-mining/naive-bayes-model-query-examples.md)。  
  
 [回到頁首](#BKMK_Tabs)  
  
## <a name="see-also"></a>另請參閱  
 [在 Excel 中流覽模型 &#40;SQL Server 資料採礦增益集&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
