---
title: 測試篩選過的模型（基本資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f0d74f8c-600d-4df5-a742-695e6947a071
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: baa4910b2849c4eb2dd04c6d0115c83683ee8bea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63044064"
---
# <a name="testing-a-filtered-model-basic-data-mining-tutorial"></a>測試篩選過的模型 (基本資料採礦教學課程)
  既然您已判斷`TM_Decision_Tree`模型是最正確的，您將會自訂模型，以更符合[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]目標郵寄行銷活動的需求。 具體而言，行銷部門想要知道男性和女性客戶之間是否有任何差異。 這項資訊可協助該部門決定要使用哪些雜誌來登廣告，以及使用哪些產品當做郵寄活動的特色產品。  
  
## <a name="using-filters"></a>使用篩選  
 篩選可讓您輕鬆地根據資料子集來建立模型。 篩選只會套用到模型中，而且不會變更基礎資料來源。  
  
 在這一課，您將建立一個依性別篩選的模型，以便預測對於男性和女性購買行為最有影響力的特性。  
  
 首先，您會建立`TM_Decision_Tree`模型的複本。  
  
#### <a name="to-copy-the-decision-tree-model"></a>若要複製決策樹模型  
  
1.  在[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的方案總管中，選取 [ **BasicDataMining**]。  
  
2.  按一下 **[採礦模型]** 索引標籤。  
  
3.  以滑鼠右鍵`TM_Decision_Tree`按一下模型，然後選取 [新增] [**採礦模型]。**  
  
4.  在 [**模型名稱**] 欄位中`TM_Decision_Tree_Male`，輸入。  
  
5.  按一下 [確定]  。  
  
 接下來，建立一個篩選來選取此模型的客戶 (根據客戶的性別)。  
  
#### <a name="to-create-a-case-filter-on-a-mining-model"></a>若要建立採礦模型的案例篩選  
  
1.  以滑鼠右鍵按一下`TM_Decision_Tree_Male` [採礦模型] 以開啟快捷方式功能表。  
  
     -- 或 --  
  
     選取此模型。 在 **[採礦模型]** 功能表上，選取 **[設定模型篩選器]**。  
  
2.  在 [模型篩選器]**** 對話方塊的 [採礦結構資料行]**** 文字方塊中，按一下方格中的上方資料列。  
  
     下拉式清單只會顯示該資料表中的資料行名稱。  
  
3.  在 [採礦結構資料行] 文字方塊中，選取 [**性別**]。  
  
     文字方塊左側的圖示會變更，指出選取的項目是資料表或資料行。  
  
4.  按一下 [**運算子**] 文字方塊，然後從清單中選取等於（=）運算子。  
  
5.  按一下 [**值**] 文字方塊，然後輸入**M**。  
  
6.  在方格中，按下一個資料列。  
  
7.  按一下 **[確定]** 以關閉 [**模型篩選器**] 對話方塊。  
  
     篩選會顯示在 [**屬性**] 視窗中。 或者，您可以從 [**屬性**] 視窗啟動 [**模型篩選器**] 對話方塊。  
  
8.  重複上述步驟，但這次請在 [ `TM_Decision_Tree_Female` **值**] 文字方塊中為模型命名並輸入**F** 。  
  
## <a name="process-the-filtered-models"></a>處理篩選過的模型  
 模型要等到部署及處理之後，才可以使用。 如需處理模型的詳細資訊，請參閱在[目標郵寄結構中處理模型 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/processing-models-in-the-targeted-mailing-structure-basic-data-mining-tutorial.md)。  
  
#### <a name="to-process-the-filtered-model"></a>若要處理篩選過的模型  
  
1.  以滑鼠右鍵按一下`TM_Decision_Tree_Male`模型，然後選取 [處理] [**採礦結構] 和 [所有模型**s]  
  
2.  按一下 [**執行**] 來處理新的模型。  
  
3.  處理完成之後，請按一下兩個處理視窗上的 [**關閉**]。  
  
     您現在會在 [**採礦模型**] 索引標籤中顯示兩個新模型。  
  
## <a name="evaluate-the-results"></a>評估結果  
 檢視結果，並評估篩選過之模型的正確性，就像之前三個模型的處理方式一樣。 如需詳細資訊，請參閱  
  
 [流覽決策樹模型 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
 [使用增益圖測試精確度 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
#### <a name="to-explore-the-filtered-models"></a>若要探索篩選過的模型  
  
1.  在 [**資料採礦設計師**] 中選取 [**採礦模型檢視器**] 索引標籤。  
  
2.  在 [採礦模型] 方塊中`TM_Decision_Tree_Male`，選取。  
  
3.  將幻燈片**放映層級**設為`3`。  
  
4.  將 [**背景**] 值`1`變更為。  
  
5.  將游標放在標示為 [**全部**] 的節點上方，以查看自行車購買者與非自行車購買者的數目。  
  
6.  針對`TM_Decision_Tree_Female`，重複步驟 1-5。  
  
7.  探索的結果`TM_Decision_Tree` ，以及針對性別篩選的模型。 與所有自行車買主相較之下，男性和女性自行車買主與未篩選的自行車買主具有一些共同的特性，但是這三種買主也有一些有趣的差異。 這是可用來開發[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]行銷活動的實用資訊。  
  
#### <a name="to-test-the-lift-of-the-filtered-models"></a>若要測試篩選過之模型的增益  
  
1.  在[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的資料採礦設計師中，切換至 [**挖掘精確度圖表**] 索引標籤，然後選取 [**輸入選擇**] 索引標籤。  
  
2.  在 [**選取要用於精確度圖表的資料集**] 群組方塊中，選取 [**使用採礦結構測試案例**]。  
  
3.  在資料採礦設計師的 [**輸入選擇**] 索引標籤上，于 [**選取可預測的採礦模型資料行以顯示在增益圖中**] 底下，選取 [**同步處理預測資料行和值**] 核取方塊。  
  
4.  在 [**可預測的資料行名稱**] 資料行中，確認已為每個模型選取 [**自行車購買**者]。  
  
5.  在 [**顯示**] 資料行中，選取每個模型。  
  
6.  在 [**預測值**] 資料行`1`中，選取。  
  
7.  選取 [增益**圖**] 索引標籤以顯示增益圖。  
  
     您現在會注意到有三個決策樹模型與隨機猜測模型相較之下都有了顯著提升，而且也優於群集模型和貝氏機率分類模型。  
  
## <a name="related-tasks"></a>相關工作  
 如需篩選的詳細資訊，請參閱[&#40;Analysis Services 資料採礦&#41;的採礦模型篩選](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)。  
  
 如需如何將篩選套用至嵌套資料表的範例，請參閱[&#40;Analysis Services 資料採礦&#41;中的中繼資料採礦教學](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)課程。  
  
## <a name="previous-task-in-lesson"></a>本課程的前一項工作  
 [使用增益圖測試精確度 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>下一課  
 [第6課：建立和使用預測 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [元資料採礦教學課程 &#40;Analysis Services-資料採礦&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [採礦模型工作和操作說明](../../2014/analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [從採礦模型刪除篩選](../../2014/analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)   
 [&#40;Analysis Services 的採礦模型篩選-資料採礦&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  
