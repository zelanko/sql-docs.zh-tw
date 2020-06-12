---
title: 流覽類神經網路模型 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- mining models, viewing
- mining model, neural network
- neural networks
- dependency network
ms.assetid: e4224cb7-115b-4889-ac07-03f096fb55fc
author: minewiskan
ms.author: owend
ms.openlocfilehash: e47f887425c2294785bd6e6624961727bf65eb17
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527724"
---
# <a name="browsing-a-neural-network-model"></a>瀏覽類神經網路模型
  當您使用 [瀏覽]**** 開啟類神經網路或羅吉斯迴歸模型時，該模型會在類似於 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 類神經網路檢視器的互動式檢視器中顯示。 此檢視器可協助您探索相互關聯，以及取得有關模型和基礎資料之模式的資訊。

##  <a name="explore-the-model"></a><a name="BKMK_Tabs"></a>探索模型
 以 [!INCLUDE[msCoName](../includes/msconame-md.md)] 類神經網路或羅吉斯迴歸演算法為基礎的模型很相似，因為它們都會將資料分析成已知輸入與輸出之間的一組連接。 [瀏覽]**** 檢視器可協助您使用下列控制項來探索這些連接：

-   [變數](#BKMK_Variables)

-   [輸入](#BKMK_Inputs)

-   [輸出](#BKMK_Outputs)

 如果您想要試驗這個檢視器，可以使用[分類精靈 &#40;適用於 Excel 的資料採礦增益集&#41;](classify-wizard-data-mining-add-ins-for-excel.md) 精靈來建立模型，並且使用 [演算法參數]**** 對話方塊中的 [進階]**** 選項，將演算法變更為 Microsoft 羅吉斯迴歸。

###  <a name="variables"></a><a name="BKMK_Variables"></a>變數
 [變數]**** 窗格會按照輸入變數作用於模型的順序，顯示這些變數的清單。 您可以使用 [輸入]**** 和 [輸出]**** 控制項來篩選模型，並影響顯示的變數及其順序。

 在判斷客戶比較可能屬於自行車購買者類別目錄或非購買者類別目錄時，您可以使用此檢視器來探索最重要的因數。

 ![測試對選取屬性結果的影響](media/dm13-neuralnet-agebuyer1.gif "測試對選取屬性結果的影響")

##### <a name="explore-variables"></a>探索變數

1.  在指定目前篩選的情況下，[變數]**** 窗格一開始會按照最重要屬性的順序排序。 垂直線的長度表示因數的強度。

     在此範例中，您可以看見收入是最具影響力的因數，其次是地區。 另一方面，擁有許多部車和多個小孩的客戶不太可能會購買自行車。

2.  在 [變數]**** 窗格中，按一下 [屬性]**** 的資料行標題。

     透過針對屬性排序，您就可以查看針對每個輸入資料行建立的分類收納。 具有離散值的資料行 (例如職業) 會按照常值「分類收納」** (Bin)。

3.  請注意針對 [年齡]**** 和 [收入]**** 找到的值範圍。

     如果任何輸入資料行是數字 (亦即，整個資料行都是連續數值資料類型)，這些數字就會儲存或分類收納成離散範圍。

     就 Income 而言，此資料行已經細分為群組，例如 78.4-154.06 (代表最高收入範圍)。

     ![排序以檢視變數分類收納的方式](media/dm13-nn-bucketing-variables.gif "排序以檢視變數分類收納的方式")

     如果您想要不同的群組，就應該使用[重定標籤 &#40;SQL Server 資料採礦增益集&#41;](relabel-sql-server-data-mining-add-ins.md) 工具或 Excel 函數來建立新的收入類別目錄，然後再建立模型。

4.  按一下 [喜好 Yes]****，將圖形還原成預設檢視。

     根據預設，此檢視會按照第一個結果值的 [喜好]**** 值來排序。 您可以針對 [輸出]**** 中的 [值 1]**** 和 [值 2]**** 選擇新的值，藉以變更指派給第一個和第二個資料行的結果。

5.  將滑鼠游標暫時放在圖表中最頂端的彩色列上。

     工具提示隨即出現，其中包含「重要性」** 分數、一對「機率」** 分數，以及一對「增益」** 值。

    -   **重要性**的計算範圍是整個資料集，而且可在指定所有輸入的情況下，識別與目標結果最相關的屬性。 此檢視器會按照重要性分數排序圖表中的值。

    -   **機率**的計算範圍是整個資料集內，目標結果的每組屬性值配對。

    -   **增益**會告知您這個特定屬性值配對在促成不同結果方面的有用程度。

     注意：不論您將滑鼠游標放在哪個資料行上方，工具提示都會包含相同的資訊。

 [回到頁首](#BKMK_Tabs)

###  <a name="inputs"></a><a name="BKMK_Inputs"></a>輸入
 [輸入]**** 窗格可讓您選擇一組輸入並且套用該組輸入當成模型的篩選，以便根據定型資料，查看這些選擇對於結果的影響

##### <a name="explore-inputs"></a>探索輸入

1.  假設您想要鎖定特定群組，並且查看最能影響該群組之購買行為的因數。

     在 [**輸入**] 窗格中，按一下 [屬性] 底下的資料 **\<All>** 格，然後選取 [ ** ****年齡**]。

     針對 [值]****，選取最年輕的年齡類別目錄。

2.  請注意，即使您針對特定的年齡群組篩選，太平洋地區還是會顯示在清單頂端附近。 這是因為太平洋地區的客戶購買自行車的可能性高於其他地區的客戶。

     由於地區是您無法影響的條件，因此，若要從考量中移除此變數並查看其他因數，您可以再次變更輸入。

     在 [輸入]**** 窗格中，按一下 [年齡]**** 底下的空白資料格，然後選取 [區域]****。

     針對 [值]****，選取 [歐洲]****。

3.  繼續加入輸入篩選，將焦點放在特別感興趣的群組上。

     例如，針對輸入屬性，新增 [性別]****，並且選取 [女性]**** 作為值。

     ![測試對選取屬性結果的影響](media/dm13-neuralnet-agebuyer2.gif "測試對選取屬性結果的影響")

     請注意變數的清單如何變更。 現在，[收入]**** 是預測目標結果的最重要變數。

     您套用輸入篩選的順序不會影響結果。

 [回到頁首](#BKMK_Tabs)

###  <a name="outputs"></a><a name="BKMK_Outputs"></a>產出
 在 [輸出]**** 窗格中，您可以選擇自己感興趣的結果。 類神經網路可讓您指定任意數目的結果資料行，不過，加入更多輸出會增加模型的複雜度，而且可能需要更長的處理時間。

 若要比較兩個輸出，您必須將這些輸出指定為 [預測]**** 或 [僅預測]**** 資料行。

##### <a name="explore-outputs"></a>探索輸出

1.  使用 [輸出屬性]**** 清單來選取屬性。

2.  從 [值 1] 和 [值 2] 清單中選取兩個結果。 輸出屬性的這兩個狀態將會在 **[變數]** 窗格中做比較。

 [回到頁首](#BKMK_Tabs)

## <a name="more-about-neural-network-models"></a>進一步了解類神經網路模型
 此檢視器中的資訊是使用這個模型類型特有的預存程序，從伺服器中擷取而來：System.Microsoft.AnalysisServices.System.DataMining.NeuralNet.GetAttributeScores。

 如果您想要使用增益集來建立具有多個可預測屬性的模型，請使用 [進階]**** 模型選項。

 如需詳細資訊，請參閱[建立採礦結構 &#40;SQL Server 資料採礦增益集&#41;](create-mining-structure-sql-server-data-mining-add-ins.md) 和[將模型加入結構 &#40;適用於 Excel 的資料採礦增益集&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)。

## <a name="see-also"></a>另請參閱
 [在 Excel 中流覽模型 &#40;SQL Server 資料採礦增益集&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)


