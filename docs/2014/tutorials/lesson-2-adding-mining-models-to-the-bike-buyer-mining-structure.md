---
title: 第 2 課： 將採礦模型加入 Bike Buyer 採礦結構 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 03fe44c5-6452-4ed0-95f6-9682670c0f52
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7bcc33e35ff0cdfcd46a73f939083ea23091673d
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2018
ms.locfileid: "49462044"
---
# <a name="lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure"></a>第 2 課：將採礦模型加入 Bike Buyer 採礦結構中
  在這一課，您會將兩個採礦模型新增至您所建立的 Bike Buyer 採礦結構[第 1 課： 建立自行車買主採礦結構](../../2014/tutorials/lesson-1-creating-the-bike-buyer-mining-structure.md)。 這些採礦模型可讓您使用一個模型探索資料，使用另一個模型建立預測。  
  
 若要瀏覽如何潛在客戶可以按其特性分類，您會建立基礎的採礦模型[Microsoft 群集演算法](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)。 在下一課，您將採索此演算法如何尋找共用類似特性的客戶叢集。 例如，您會發現某些客戶很可能成為鄰居、使用自行車通勤，並具有類似的教育背景。 您可以利用這些叢集，進一步了解不同客戶彼此的關係，並使用此資訊來建立一個以特定客戶群為目標的行銷策略。  
  
 為了預測潛在客戶是否可能購買自行車，您將建立採礦模型，根據[Microsoft Decision Trees Algorithm](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md)。 此演算法會查看與每一位潛在客戶相關聯的資訊，並尋找在預測其是否會購買自行車時有用的特性。 然後它會比較之前的自行車買主與新的潛在客戶的特性值，以判斷新的潛在客戶是否有可能購買自行車。  
  
## <a name="alter-mining-structure-statement"></a>ALTER MINING STRUCTURE 陳述式  
 若要將採礦模型加入採礦結構，您使用[ALTER MINING STRUCTURE &#40;DMX&#41; ](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016)陳述式。 陳述式中的程式碼可分成下列各部份：  
  
-   識別採礦結構  
  
-   命名採礦模型  
  
-   定義索引鍵資料行  
  
-   定義輸入資料行和可預測資料行  
  
-   識別演算法和參數變更  
  
 以下是 ALTER MINING MODEL 陳述式的一般範例：  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
ADD MINING MODEL [<mining model name>]  
(  
    [<key column>],  
    <mining model columns>,  
) USING <algorithm name>( <algorithm parameters> )  
WITH FILTER (<expression>)  
```  
  
 程式碼的第一行會識別將加入採礦模型的現有採礦結構：  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
```  
  
 程式碼的下一行命名要加入採礦結構中的採礦模型：  
  
```  
ADD MINING MODEL [<mining model name>]  
```  
  
 如需命名的物件，在 DMX 中的資訊，請參閱[識別碼&#40;DMX&#41;](/sql/dmx/identifiers-dmx)。  
  
 接下來幾行的程式碼定義採礦結構中將由採礦模型使用的資料行：  
  
```  
[<key column>],  
<mining model columns>  
```  
  
 您只能使用已存在於採礦結構中的資料行，且清單中的第一個資料行必須是採礦結構中的索引鍵資料行。  
  
 程式碼的下一行定義產生採礦模型的採礦演算法，以及您可以在演算法上設定的演算法參數：  
  
```  
) USING <algorithm name>( <algorithm parameters> )  
```  
  
 如需您可以調整之演算法參數的詳細資訊，請參閱[Microsoft Decision Trees Algorithm](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md)並[Microsoft 群集演算法](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)。  
  
 您可以使用下列語法來指定採礦模型中要用於預測的資料行：  
  
```  
<mining model column> PREDICT  
```  
  
 程式碼的最後一行是選擇性的，可定義在定型及測試模型時所套用的篩選。 如需如何將篩選套用至採礦模型的詳細資訊，請參閱[採礦模型的篩選&#40;Analysis Services-Data Mining&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)。  
  
## <a name="lesson-tasks"></a>課程工作  
 您將在這一課執行下列工作：  
  
-   使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 決策樹演算法，將決策樹採礦模型加入 Bike Buyer 結構中  
  
-   使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 群集演算法，將群集採礦模型加入 Bike Buyer 結構中  
  
-   因為您要查看所有情況的結果，所以請先不要對任一模型新增篩選。  
  
## <a name="adding-a-decision-tree-mining-model-to-the-structure"></a>將決策樹採礦模型加入結構中  
 第一步是加入以 [!INCLUDE[msCoName](../includes/msconame-md.md)] 決策樹演算法為基礎的採礦模型。  
  
#### <a name="to-add-a-decision-tree-mining-model"></a>若要加入決策樹採礦模型  
  
1.  在**物件總管] 中**，以滑鼠右鍵按一下執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向**新查詢**，然後按一下**DMX**以開啟 [查詢編輯器及新的空白查詢。  
  
2.  將 ALTER MINING STRUCTURE 陳述式的一般範例複製到空白查詢中。  
  
3.  取代下列項目：  
  
    ```  
    <mining structure name>   
    ```  
  
     成為：  
  
    ```  
    [Bike Buyer]  
    ```  
  
4.  取代下列項目：  
  
    ```  
    <mining model name>   
    ```  
  
     成為：  
  
    ```  
    Decision Tree  
    ```  
  
5.  取代下列項目：  
  
    ```  
    <mining model columns>,  
    ```  
  
     成為：  
  
    ```  
    (  
       CustomerKey,  
       [Age],  
       [Bike Buyer] PREDICT,  
       [Commute Distance],  
       [Education],  
       [Gender],  
       [House Owner Flag],  
       [Marital Status],  
       [Number Cars Owned],  
       [Number Children At Home],  
       [Occupation],  
       [Region],  
       [Total Children],  
       [Yearly Income]  
    ```  
  
     在此案例中，`[Bike Buyer]` 資料行已指定為 PREDICT 資料行。  
  
6.  取代下列項目：  
  
    ```  
    USING <algorithm name>( <algorithm parameters> )   
    ```  
  
     成為：  
  
    ```  
    Using Microsoft_Decision_Trees  
    WITH DRILLTHROUGH  
    ```  
  
     WITH DRILLTHROUGH 陳述式可讓您探索用於建立採礦模型的案例。  
  
     現在，產生的陳述式應該如下所示：  
  
    ```  
    ALTER MINING STRUCTURE [Bike Buyer]  
    ADD MINING MODEL [Decision Tree]  
    (  
       CustomerKey,  
       [Age],  
       [Bike Buyer] PREDICT,  
       [Commute Distance],  
       [Education],  
       [Gender],  
       [House Owner Flag],  
       [Marital Status],  
       [Number Cars Owned],  
       [Number Children At Home],  
       [Occupation],  
       [Region],  
       [Total Children],  
       [Yearly Income]  
    ) USING Microsoft_Decision_Trees  
    WITH DRILLTHROUGH  
    ```  
  
7.  在 **檔案**功能表上，按一下**另存 DMXQuery1.dmx 為**。  
  
8.  在 [**另存新檔**] 對話方塊中，瀏覽至適當的資料夾，並將檔案命名`DT_Model.dmx`。  
  
9. 在工具列上，按一下**Execute**  按鈕。  
  
## <a name="adding-a-clustering-mining-model-to-the-structure"></a>將群集採礦模型加入結構中  
 現在可以將採礦模型加入以 [!INCLUDE[msCoName](../includes/msconame-md.md)] 群組演算法為基礎的 Bike Buyer 採礦結構中。 因為群集採礦模型將使用採礦結構中定義的所有資料行，所以您可以利用捷徑，以省略採礦資料行之定義的方式，將此模型加入結構中。  
  
#### <a name="to-add-a-clustering-mining-model"></a>若要加入群集採礦模型  
  
1.  在**物件總管] 中**，以滑鼠右鍵按一下執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向**新查詢**，然後按一下**DMX**若要開啟 [查詢編輯器以及新的空白查詢。  
  
2.  將 ALTER MINING STRUCTURE 陳述式的一般範例複製到空白查詢中。  
  
3.  取代下列項目：  
  
    ```  
    <mining structure name>   
    ```  
  
     成為：  
  
    ```  
    [Bike Buyer]  
    ```  
  
4.  取代下列項目：  
  
    ```  
    <mining model>   
    ```  
  
     成為：  
  
    ```  
    Clustering Model  
    ```  
  
5.  刪除下面這一行：  
  
    ```  
    (  
        [<key column>],  
        <mining model columns>,  
    )  
    ```  
  
6.  取代下列項目：  
  
    ```  
    USING <algorithm name>( <algorithm parameters> )  
    ```  
  
     成為：  
  
    ```  
    USING Microsoft_Clustering  
    ```  
  
     現在，完整的陳述式應該如下所示：  
  
    ```  
    ALTER MINING STRUCTURE [Bike Buyer]  
    ADD MINING MODEL [Clustering]  
    USING Microsoft_Clustering   
    ```  
  
7.  在 **檔案**功能表上，按一下**另存 DMXQuery1.dmx 為**。  
  
8.  在 [**另存新檔**] 對話方塊中，瀏覽至適當的資料夾，並將檔案命名`Clustering_Model.dmx`。  
  
9. 在工具列上，按一下**Execute**  按鈕。  
  
 在下一課，您將處理模型和採礦結構。  
  
## <a name="next-lesson"></a>下一課  
 [第 3 課：處理自行車買主採礦結構](../../2014/tutorials/lesson-3-processing-the-bike-buyer-mining-structure.md)  
  
  
