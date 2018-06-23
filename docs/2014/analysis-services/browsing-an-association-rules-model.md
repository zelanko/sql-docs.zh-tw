---
title: 瀏覽關聯規則模型 |Microsoft 文件
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mining models, browsing
- mining model, association
- mining models, viewing
- association [data mining]
ms.assetid: faffe208-7a64-4ec6-825f-ecbaa79caff7
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4db0b96fe2520a7d9a7aee82ff8d0a3996b730b8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133826"
---
# <a name="browsing-an-association-rules-model"></a>瀏覽關聯規則模型
  當您開啟關聯模型使用**瀏覽**，會顯示此模型中的互動式檢視器中的關聯規則檢視器類似[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  此檢視器可讓您快速查看相互關聯的項目，並顯示可用於預測或提出建議的規則。  
  
##  <a name="BKMK_ViewerTabs"></a> 瀏覽模型  
 當您開啟使用建立採礦模型[!INCLUDE[msCoName](../includes/msconame-md.md)]關聯規則演算法**瀏覽**視窗包含下列檢視，每一個設計，可讓您瀏覽此模型的不同層面：  
  
-   [項目集](#BKMK_Itemsets)  
  
-   [規則](#BKMK_Rules)  
  
-   [相依性網路](#BKMK_Dependency)  
  
 記下每個索引標籤上，選項**顯示完整名稱**。 透過選取這個選項，您可以顯示或隱藏項目集的來源資料表，以及縮短或增長規則或項目集的名稱。 當您的案例資料和屬性資料來自不同資料來源時，這個選項特別有用。  
  
 若要試驗關聯模型，您可以使用範例資料活頁簿之 [關聯] 索引標籤上的範例資料，然後使用所有預設值建立關聯模型。 您也可以建立購物籃分析模型，並開啟該使用**瀏覽**。  
  
###  <a name="BKMK_Itemsets"></a> 項目集  
 **項目集** 索引標籤是很好的起點，開始探索關聯模型。 此索引標籤會顯示常被模型湊在一起的項目清單。  
  
 ![關聯模型中的項目清單](media/dm13-association-itemsets.gif "關聯模型中的項目清單")  
  
 您可以在購物籃模型中找到項目集的最常見範例，在此模型中，項目集表示許多客戶會同時購買的產品配對或組合。 不過，根據您分組及排序項目的方式，項目集可能包含客戶在一段時間內訂購的影片序列，或傾向在特定位置發生的事件。  
  
 *項目集*可以只包含一個項目、 兩個、 三個或許多不過，設定為模型的最大項目集大小。 針對每個項目集，檢視器會顯示項目集*支援*，*機率*，和*大小*。 支援和機率是用來排名項目集的主體統計資料，並且是關聯模型所產生的規則。 這些值也可用來計算及描述其重要性。  
  
 **支援**。 支援表示包含此項目的案例數目或輸入資料的資料列數。 例如，如果項目集包含兩個項目存在於購物車中的數字**支援**資料行會指出來源資料中的項目組合的發生多少次。  
  
 **大小**。 藉由變更項目集大小，您可以控制項目集清單的長度。 如果您不想要查看單一產品清單中的，變更選項，**項目集大小下限**、 2 或多個。  增加項目集大小下限來限制清單，讓您能夠尋找非常特定的模式， 而且可能會在處理非常龐大的資料集時相當有用。  
  
 您可以篩選會顯示在 [] 索引標籤上，藉由變更的項目集數目**最小支援**和**最大資料列**值。 如果您增加**最小支援**值，清單會顯示較少的項目集，但項目集將會是較常見的輸入資料中的。 至於常見是否相同重要則是另一個問題，您可以瀏覽使用**規則** 索引標籤。  
  
 請注意，變更支援值或其他控制項上**項目集** 索引標籤只會變更的項目會顯示，所以不會影響基礎模型。 如果您想要產生多或更少項目集，或限制其大小，您應該使用參數，`MINIMUM_SUPPORT`和`MAXIMUM_SUPPORT`，可用於**演算法參數** 對話方塊。  
  
##### <a name="explore-the-itemsets-list"></a>探索項目集清單  
  
1.  按一下**支援**資料行來排序最高到最低的支援。 如此可讓您了解客戶最常購買的項目。  
  
2.  若要將焦點放在特定的項目集的感興趣，超出數千種組合可能的話，請輸入某些文字**篩選項目集**方塊。  
  
     我們在此輸入`Gloves`。 當您套用篩選時，系統會重新整理清單，並只顯示包含手套的項目集。 如此可讓您專注於客戶購買手套及其他一些項目的交易。  
  
     **[篩選項目集]** 選項也會顯示您先前已用過的篩選清單。  
  
3.  值變更**項目集大小下限**篩選出只手套及其他項目購買的客戶。  
  
4.  按一下下拉式清單選項**顯示**，以控制屬性的顯示方式：  
  
    -   **顯示屬性名稱和值**  
  
    -   **只顯示屬性值**  
  
    -   **只顯示屬性名稱**  
  
     注意名稱有何改變。 在購物籃模型案例中，此模型是建立在多位客戶購買之產品的巢狀資料表上，因此屬性名稱通常是產品名稱，而清單中顯示的產品會標示為 `Existing`，表示客戶確實購買此項目。  
  
     `Existing` 的相反是 `Missing`，在資料採礦中調查時是相當有用的屬性。 例如，假設項目集 A + B 因此是非常受歡迎您想要尋找客戶購買的項目，但沒有項目 b您無法使用預測查詢，並擷取與其中一個，但沒有其他交易執行這項操作，並且進行那些進一步的分析。 如需如何在關聯模型建立預測查詢的資訊，請參閱[關聯模型查詢範例](data-mining/association-model-query-examples.md)SQL Server 線上叢書中  
  
5.  若要強制使用新的篩選準則重新顯示的項目集清單，您可以選取或清除**顯示完整名稱**核取方塊。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Rules"></a> 規則  
 **規則**索引標籤結合項目集和它們的相對值的資訊。  
  
 ![關聯模型所建立的規則清單](media/dm13-association-rules.gif "關聯模型所建立的規則清單")  
  
 *機率*代表之資料集中包含目標項目組合的案例的比例。 機率是統計的概念類似*信心*，並提供您的規則結果可能性的指示進行。 您可以變更的值**最小機率**此窗格來篩選顯示的規則。  
  
 值**最小機率**最初看到的是建立模型時演算法所使用的臨界值。 完成模型之後，您無法降低此值，不過您可以增加此值，只顯示更高機率的項目。  
  
 *重要性*設計來測量規則的效益。 很常見的規則可能非常普遍，而擁有較少的資訊價值。 重要性越高，規則對於預測結果便越有價值。 在[購物籃分析&#40;適用於 Excel 的資料表 AnalysisTools&#41; ](shopping-basket-analysis-table-analysistools-for-excel.md)工具中，重要性可結合項目來判斷銷售量而言可能最重要的組合的價格。  
  
##### <a name="explore-the-rules-list"></a>探索規則清單  
  
1.  再試一次按一下欄標題，**機率**，**重要性**，和**規則**— 若要查看資料有何改變。  
  
2.  使用**篩選規則**選項輸入值，並專注於目標規則。  
  
     例如，如果您想查看預測客戶可能在購買手套時一起購買之項目的所有規則，請在文字方塊中輸入「手套」，然後重新整理窗格。  
  
     **[篩選項目集]** 選項也會顯示您先前已用過的篩選清單。  
  
3.  若要強制清單規則，以重新顯示使用篩選準則，您可以選取或清除**顯示完整名稱**核取方塊。  
  
4.  使用選項，**顯示**來控制規則名稱的顯示方式。  
  
5.  設定的值**最大資料列**選項為 100，然後再按一下**複製至 Excel**。  
  
     請注意，變更此值不會影響模型中的資料量，而只會控制顯示清單中的資料列數。 此選項適合搭配超大型模型使用。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Dependency"></a> 相依性網路  
 **相依性網路** 索引標籤是項目之間的相互關聯的視覺效果對應。 圖形中的每個橢圓形 (稱為*節點*) 代表的屬性 / 值組，例如"Vest = Existing"或"Age = 1-30"。  連接橢圓形的每一行 (稱為*邊緣*) 代表相互關聯類型。  
  
 ![關聯模型的相依性網路圖形](media/dm13-association-dependencynetwork.gif "關聯模型的相依性網路圖形")  
  
##### <a name="explore-the-dependency-network"></a>探索相依性網路  
  
1.  按一下**尋找**按鈕，並使用**尋找節點**對話方塊輸入感興趣的項目。  
  
     例如，輸入「手套」，然後最大化視窗中的圖表，就可以輕鬆查看結果。  
  
     包含項目的節點會醒目提示，而指向節點的箭頭表示連接項目的規則。  
  
     箭頭方向表示規則方向。 例如，如果購買手套的客戶也可能購買背心，箭頭會從「手套」節點開始，並終止於「背心」節點。  
  
     若要取得這項規則的其他統計資料，您可以按一下**規則**索引標籤上，尋找有描述的規則，「 手套-現有 」-> 「 背心-現有。")  
  
2.  按一下並拖曳檢視器左側的滑桿。  
  
     此滑桿具有篩選規則機率的作用。 降低滑桿只顯示最強的規則。  
  
3.  按一下**複製至 Excel** ，將目前視窗的快照集複製到 Excel。  
  
     您將無法使用圖表，您將複製到 Excel。如果您需要互動式網路圖形，請使用[檢視資料採礦模型在 Visio 中&#40;資料採礦增益集&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md)。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
## <a name="more-about-association-models"></a>進一步了解關聯模型  
 您可以使用**瀏覽**功能，開啟及瀏覽使用 Microsoft 關聯規則演算法建立的任何模型。 這包括使用建立的模型[購物籃分析&#40;適用於 Excel 的資料表 AnalysisTools&#41; ](shopping-basket-analysis-table-analysistools-for-excel.md)工具**資料表分析工具**功能區中，或在[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
 如果您使用購物籃分析工具建立關聯規則模型，許多進階選項將會自動為您設定。  
  
 如果您想要設定進階的參數或最小機率和支援，請使用 alter[關聯精靈&#40;適用於 Excel 的資料採礦用戶端&#41;](associate-wizard-data-mining-client-for-excel.md)精靈 中，或建立您自己的模型使用[將模型加入結構&#40;適用於 Excel 的資料採礦增益集&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)模型選項。  
  
-   **項目集：** 當您建立模型時，您也可以控制的值指派到 MINIMUM_PROBABILITY 參數而產生的項目集數目。 此參數可在 [演算法參數] 對話方塊中。  
  
-   **規則：** [!INCLUDE[msCoName](../includes/msconame-md.md)]關聯規則演算法會使用機率值來限制所產生的規則數目。 您可以設定 `MINIMUM_PROBABILITY` 或 `MINIMUM _IMPORTANCE` 參數來控制規則數目。  
  
 如需有關如何設定進階的參數的詳細資訊，請參閱[資料採礦演算法&#40;SQL Server 資料採礦增益集&#41;](data-mining-algorithms-sql-server-data-mining-add-ins.md)。  
  
## <a name="see-also"></a>另請參閱  
 [瀏覽模型，在 Excel 中的&#40;SQL Server 資料採礦增益集&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  