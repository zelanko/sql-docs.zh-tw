---
title: 時序群集模型的採礦模型內容 (Analysis Services-資料採礦) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining model content, sequence clustering models
- sequence clustering algorithms [Analysis Services]
ms.assetid: 68e1934a-e147-4d53-b122-fa15e3fd5485
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 12aad369e9a8614041bccaa08ee507d723c6c51f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083571"
---
# <a name="mining-model-content-for-sequence-clustering-models-analysis-services---data-mining"></a>時序群集模型的採礦模型內容 (Analysis Services - 資料採礦)
  本主題描述使用 Microsoft 時序群集演算法的模型專用的採礦模型內容。 如需與適用於所有模型類型採礦模型內容相關的一般及統計詞彙說明，請參閱[採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-analysis-services-data-mining.md)。  
  
## <a name="understanding-the-structure-of-a-sequence-clustering-model"></a>了解時序群集模型的結構  
 時序群集模型擁有代表模型及其中繼資料的單一父節點 (NODE_TYPE = 1)。 標示為 **(All)** 的父節點擁有相關的時序節點 (NODE_TYPE = 13)，會列出在定型資料中偵測到的所有轉換。  
  
 ![時序群集模型的結構](../media/modelcontent-seqclust.gif "時序群集模型的結構")  
  
 演算法也會根據建立模型 (例如 Customer Demographics 等等) 時，在隨附的資料和其他任何輸入屬性中發現的轉換，建立多個群集。 每個群集 (NODE_TYPE = 5) 都包含自己的時序節點 (NODE_TYPE = 13)，其中只會列出產生該特定群集時使用的轉換。 從時序節點中，您可以向下鑽研來顯示個別狀態轉換的詳細資料 (NODE_TYPE = 14)。  
  
 如需時序與狀態轉換的說明與範例，請參閱 [Microsoft 時序叢集演算法](microsoft-sequence-clustering-algorithm.md)。  
  
## <a name="model-content-for-a-sequence-clustering-model"></a>時序群集模型的模型內容  
 本節會針對採礦模型內容中與時序群集具有特定相關的資料行，提供其他資訊。  
  
 MODEL_CATALOG  
 模型儲存位置所在資料庫的名稱。  
  
 MODEL_NAME  
 模型的名稱。  
  
 ATTRIBUTE_NAME  
 永遠為空白。  
  
 NODE_NAME  
 節點的名稱。 目前是與 NODE_UNIQUE_NAME 相同的值。  
  
 NODE_UNIQUE_NAME  
 節點的唯一名稱。  
  
 NODE_TYPE  
 時序群集模型會輸出下列節點類型：  
  
|節點類型識別碼|描述|  
|------------------|-----------------|  
|1 (模型)|模型的根節點|  
|5 (群集)|包含群集中的節點計數、屬性的清單，以及描述群集中之值的統計資料。|  
|13 (時序)|包含群集中內含之轉換的清單。|  
|14 (轉換)|利用第一個資料列包含起始狀態，而其他所有資料列包含連續狀態的資料表，以及支援與機率統計資料，描述事件的時序。|  
  
 NODE_GUID  
 空白。  
  
 NODE_CAPTION  
 與用於顯示目的之節點相關聯的標籤或標題。  
  
 您可以在使用模型時重新命名群集標題，不過，如果您關閉模型，則不會保留新名稱。  
  
 CHILDREN_CARDINALITY  
 節點所擁有子系數目的估計。  
  
 **模型根** ：基數值等於叢集數目加 1。 如需詳細資訊，請參閱 [基數](#bkmk_cardinality)。  
  
 **叢集節點** ：基數一律為 1，因為每個叢集都有一個單一子節點，其中包含叢集中的時序清單。  
  
 **時序節點** ：基數表示該叢集中包含之轉換的數目。 例如，模型根之時序節點的基數會告訴您整個模型中發現的轉換數目。  
  
 PARENT_UNIQUE_NAME  
 節點之父系的唯一名稱。  
  
 任何根層級的節點都會傳回 NULL。  
  
 NODE_DESCRIPTION  
 與節點標題相同。  
  
 NODE_RULE  
 永遠為空白。  
  
 MARGINAL_RULE  
 永遠為空白。  
  
 NODE_PROBABILITY  
 **模型根** ：一律為 0。  
  
 **叢集節點** ：在模型中，經過叢集的已調整機率。 已調整的機率總和不為 1，因為在時序群集中使用的群集方法允許多個群集中的部分成員資格。  
  
 **時序節點** ：一律為 0。  
  
 **轉換節點** ：一律為 0。  
  
 MARGINAL_PROBABILITY  
 **模型根** ：一律為 0。  
  
 **叢集節點** ：與 NODE_PROBABILITY 相同的值。  
  
 **時序節點** ：一律為 0。  
  
 **轉換節點** ：一律為 0。  
  
 NODE_DISTRIBUTION  
 包含機率和其他資訊的資料表。 如需詳細資訊，請參閱 [NODE_DISTRIBUTION 資料表](#bkmk_NODEDIST)。  
  
 NODE_SUPPORT  
 支援這個節點的轉換數目。 因此，如果在定型資料中有 30 個「產品 A 後面跟著產品 B」時序範例，則總支援為 30。  
  
 **模型根** ：模型中的轉換總數。  
  
 **叢集節點** ：叢集的原始支援，表示將案例提供給此叢集之定型案例的數目。  
  
 **時序節點** ：一律為 0。  
  
 **轉換節點** ：在叢集中代表特定轉換之案例的百分比。 可以為 0，或者可以有正值。 透過取得叢集節點的原始支援計算，然後乘以群集的機率。  
  
 您可以透過這個值了解提供給轉換的定型案例數目。  
  
 MSOLAP_MODEL_COLUMN  
 不適用。  
  
 MSOLAP_NODE_SCORE  
 不適用。  
  
 MSOLAP_NODE_SHORT_CAPTION  
 與 NODE_DESCRIPTION 相同。  
  
## <a name="understanding-sequences-states-and-transitions"></a>了解時序、狀態與轉換  
 時序群集模型所擁有的唯一結構結合兩種物件與非常不同的資訊類型：第一種為群集，而第二種為狀態轉換。  
  
 時序群集建立的群集類似於 Microsoft 群集演算法建立的群集。 每個群集都有一個設定檔和特性。 但是在時序群集中，每個群集還會另外包含一個單一子節點，其中會列出該群集中的時序。 每個時序節點都包含多個子節點，其中詳細描述狀態轉換以及機率。  
  
 模型中所包含的時序幾乎永遠都比您可以在任何單一案例中找到的時序還多，因為時序可以鏈結在一起。 Microsoft Analysis Services 會儲存不同狀態的指標，讓您可以計算每個轉換發生的次數。 您也可以尋找關於時序發生次數的資訊，並與整組觀察到的狀態相較，測量發生的機率。  
  
 下表摘要說明如何將資訊儲存在模型中，以及如何讓節點產生關聯。  
  
|節點|擁有子節點|NODE_DISTRIBUTION 資料表|  
|----------|--------------------|------------------------------|  
|模型根|多個叢集節點<br /><br /> 包含整個模型之時序的節點|列出模型中的所有產品以及支援和機率。<br /><br /> 由於群集方法允許多個群集中的部分成員資格，支援和機率可以有小數值。 也就是說，每個案例潛在都可以屬於多個群集，而不是只計算單一案例一次。 因此，決定最終的群集成員資格時，該值會依據該群集的機率進行調整。|  
|模型的時序節點|多個轉換節點|列出模型中的所有產品以及支援和機率。<br /><br /> 由於模型的時序數目是已知的，因此，在此層級針對支援和機率的計算相當直接：<br /><br /> 支援 = 案例的計數<br /><br /> 機率 = 模型中每個時序的原始機率。 所有機率的加總應該為 1。|  
|個別的叢集節點|僅包含該群集之時序的節點|列出群集中的所有產品，但是僅針對屬於群集特性的產品，提供支援與機率值。<br /><br /> 支援代表此群集中每個案例的已調整支援值。 機率值為調整過的機率。|  
|適用於個別群集的時序節點|僅包含該群集中時序之轉換的多個節點|與個別叢集節點中的資訊完全相同。|  
|轉換|無子系|列出第一個相關狀態的轉換。<br /><br /> 支援是調整過的支援值，表示參與每個轉換的案例。 機率是調整過的機率，以百分比表示。|  
  
###  <a name="bkmk_NODEDIST"></a> NODE_DISTRIBUTION 資料表  
 NODE_DISTRIBUTION 資料表會針對特定群集的轉換和時序，提供詳細的機率與支援資訊。  
  
 系統一律會將資料列加入到轉換資料表中，代表可能的 `Missing` 值。 如需有關哪些資訊`Missing`值含義及它如何影響計算，請參閱[遺漏值&#40;Analysis Services-Data Mining&#41;](missing-values-analysis-services-data-mining.md)。  
  
 支援與機率的計算會根據計算應用於定型案例或完成的模型而有所不同。 這是因為預設的群集方法 Expectation Maximization (EM) 假設任何案例都可以屬於一個以上的群集。 計算模型中案例的支援時，可以使用原始計數和原始機率。 不過，群集中任何特定時序的機率都必須透過所有可能之時序和群集組合的總和加權。  
  
###  <a name="bkmk_cardinality"></a> 基數  
 在群集模型中，父節點的基數一般會告訴您該模型中有多少群集。 不過，時序群集模型在群集層級有兩種節點：其中一種節點包含群集，而另一種節點則包含整個模型的時序清單。  
  
 因此，若要了解模型中的群集數目，您可以取得 (All) 節點的 NODE_CARDINALITY 值後減 1。 例如，如果模型建立 9 個群集，模型根的基數為 10。 這是因為模型包含 9 個叢集節點，每個節點都有自己的時序節點，再加上標示群集 10 (代表模型的時序) 的額外時序節點。  
  
## <a name="walkthrough-of-structure"></a>結構的逐步解說  
 範例可能有助於釐清儲存資訊的方式，以及解譯的方式。 例如，您可以使用下列查詢找出最大的訂單，也就是基礎 [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] 資料中，觀察最長的鏈結：  
  
```  
USE AdventureWorksDW2012  
SELECT DISTINCT OrderNumber, Count(*)  
FROM vAssocSeqLineItems  
GROUP BY OrderNumber  
ORDER BY Count(*) DESC  
```  
  
 從這些結果中，您會發現訂單號碼 'SO72656'、'SO58845' 及 'SO70714' 包含最大的時序，其中每個時序都有 8 個項目。 您可以利用訂單識別碼檢視特定訂單的詳細資料，以查看所購買的項目以及在哪個訂單中。  
  
|OrderNumber|LineNumber|[模型]|  
|-----------------|----------------|-----------|  
|SO58845|1|Mountain-500|  
|SO58845|2|LL Mountain Tire|  
|SO58845|3|Mountain Tire Tube|  
|SO58845|4|Fender Set - Mountain|  
|SO58845|5|Mountain Bottle Cage|  
|SO58845|6|Water Bottle|  
|SO58845|7|Sport-100|  
|SO58845|8|Long-Sleeve Logo Jersey|  
  
 不過，購買 Mountain-500 的部分客戶可能會購買不同的產品。 您可以檢視模型中的時序清單，藉以檢視 Mountain-500 後面的所有產品。 下列程序使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中提供的兩個檢視器，引導您逐步檢視這些時序：  
  
#### <a name="to-view-related-sequences-by-using-the-sequence-clustering-viewer"></a>使用時序群集檢視器檢視相關的時序  
  
1.  在 [物件總管] 中，以滑鼠右鍵按一下 [時序群集] 模型，然後選取 [瀏覽]。  
  
2.  在時序叢集檢視器中，按一下 [狀態轉換]  索引標籤。  
  
3.  在 [叢集]  下拉式清單中，確認有選取 [母體擴展 (全部)]  。  
  
4.  將窗格左側的滑動軸一直向上移動，即可顯示所有連結。  
  
5.  在圖表中找出 **Mountain-500**，然後按一下圖表中的節點。  
  
6.  反白顯示的那些行會指向下一個狀態 (在 Mountain-500 之後購買的產品)，而數字則表示機率。 在一般模型內容檢視器中比較這些狀態與結果。  
  
#### <a name="to-view-related-sequences-by-using-the-generic-model-content-viewer"></a>使用一般模型內容檢視器檢視相關的時序  
  
1.  在 [物件總管] 中，以滑鼠右鍵按一下 [時序群集] 模型，然後選取 [瀏覽]。  
  
2.  從檢視器下拉式清單中，選取 [Microsoft 一般內容樹狀檢視器]  。  
  
3.  在 [節點標題]  窗格中，按一下名稱為 [叢集 16 的時序層級]  的節點。  
  
4.  在 [節點詳細資料] 窗格中，尋找 NODE_DISTRIBUTION 資料列，然後在巢狀資料表中按一下任意位置。  
  
     上方資料列永遠供遺漏值使用。 此資料列為時序狀態 0。  
  
5.  按向下鍵或使用捲軸，向下移到巢狀資料表，直到您看到 Mountain-500 資料列為止。  
  
     此資料列為時序狀態 20。  
  
    > [!NOTE]  
    >  您可以使用程式設計的方式，取得特定時序狀態的資料列號碼，但是如果您只是在瀏覽，只將巢狀資料表複製到 Excel 活頁簿可能比較容易。  
  
6.  返回 [節點標題] 窗格，然後展開 [叢集 16 的時序層級]  節點 (如果尚未展開)。  
  
7.  在其子節點中尋找 [時序狀態 20 的轉換資料列]  。 按一下轉換節點。  
  
8.  NODE_DISTRIBUTION 巢狀資料表包含下列產品和機率。 在時序叢集檢視器的 [狀態轉換]  索引標籤中比較這些狀態與結果。  
  
 下表顯示 NODE_DISTRIBUTION 資料表的結果，以及顯示在圖形檢視器中的捨入機率值。  
  
|產品|支援 (NODE_DISTRIBUTION 資料表)|機率 (NODE_DISTRIBUTION 資料表)|機率 (從圖形)|  
|-------------|------------------------------------------|------------------------------------------------|--------------------------------|  
|Missing|48.447887|0.138028169|(未顯示)|  
|Cycling Cap|10.876056|0.030985915|0.03|  
|Fender Set - Mountain|80.087324|0.228169014|0.23|  
|Half-Finger Gloves|0.9887324|0.002816901|0.00|  
|Hydration Pack|0.9887324|0.002816901|0.00|  
|LL Mountain Tire|51.414085|0.146478873|0.15|  
|Long-Sleeve Logo Jersey|2.9661972|0.008450704|0.01|  
|Mountain Bottle Cage|87.997183|0.250704225|0.25|  
|Mountain Tire Tube|16.808451|0.047887324|0.05|  
|Short-Sleeve Classic Jersey|10.876056|0.030985915|0.03|  
|Sport-100|20.76338|0.05915493|0.06|  
|Water Bottle|18.785915|0.053521127|0.25|  
  
 雖然我們一開始從定型資料中選取的案例包含產品 'Mountain-500' 後面接著 'LL Mountain Tire'，您還是可以看到有很多其他可能的時序。 若要找出任何特定群集的詳細資訊，您必須重複將群集中時序的清單向下鑽研至每個狀態或產品之實際轉換的程序。  
  
 您可以從一個特定群集中列出的時序跳到轉換資料列。 您可以從該轉換資料列判斷下一個是哪個產品，並跳回時序清單中的那個產品。 藉由為每個第一個和第二個狀態重複此程序，您就可以處理冗長的狀態鏈結。  
  
## <a name="using-sequence-information"></a>使用時序資訊  
 時序群集的常見案例為追蹤使用者在網站上的點選行為。 例如，如果資料來自 AdventureWorks 電子商務網站上的客戶購買記錄，產生的時序群集模型可用於推斷使用者行為、重新設計電子商務網站以解決導覽問題，或提升銷售量。  
  
 例如，分析可能顯示使用者永遠遵循特定的產品鏈結，而與人口統計無關。 同時，您可能會發現使用者經常在按一下特定產品後就離開網站。 根據這個發現，您可能會詢問您可以提供哪些其他路徑給使用者，誘使使用者停留在網站上。  
  
 如果您沒有用於分類使用者的其他資訊，則您只要使用時序資訊，就可以收集導覽的相關資料，讓您更了解整體行為。 不過，如果您可以收集客戶的相關資訊，並將該資訊比對您的客戶資料庫，您可以結合群集與時序預測的力量，或根據導覽至目前頁面的路徑，為使用者提供量身訂做的建議。  
  
 時序群集模型所編譯的其他大量狀態與轉換資訊用途為，判斷哪些可能的路徑從來沒有使用過。 例如，如果您有許多訪客到第 1-4 頁，但是這些訪客從來沒有繼續前進到第 5 頁，您可能會調查是否有任何問題造成不會導覽到第 5 頁。 方法是，查詢模型內容，然後對照可能路徑的清單進行比對。  這些圖形會告訴您網站中的所有導覽路徑可以使用程式設計方式，或者使用各種網站分析工具建立。  
  
 若要找出如何藉由查詢模型內容取得觀察之路徑的清單，以及如何在時序叢集模型上查看查詢的其他範例，請參閱 [時序叢集模型查詢範例](clustering-model-query-examples.md)。  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-analysis-services-data-mining.md)   
 [Microsoft 時序叢集演算法](microsoft-sequence-clustering-algorithm.md)   
 [時序叢集模型查詢範例](clustering-model-query-examples.md)  
  
  
