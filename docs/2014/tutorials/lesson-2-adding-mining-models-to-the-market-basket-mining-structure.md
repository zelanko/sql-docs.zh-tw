---
title: 第 2 課：將採礦模型加入購物籃採礦結構 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d96a7a7d-35d7-4b34-abb5-f0822c256253
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b9573d9359983e33cf23533787c26039572710ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63204716"
---
# <a name="lesson-2-adding-mining-models-to-the-market-basket-mining-structure"></a>第 2 課：將採礦模型新增至購物籃採礦結構
  在這一課，您將兩個採礦模型加入購物籃採礦結構中建立[第 1 課：建立購物籃採礦結構](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md)。 這些採礦模型可讓您建立預測。  
  
 為了預測客戶可能同時購買的產品類型，您將建立兩個採礦模型，使用[Microsoft 關聯分析演算法](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)和兩個不同的值，如*MINIMUM_PROBABILTY*參數。  
  
 *MINIMUM_PROBABILTY*是[!INCLUDE[msCoName](../includes/msconame-md.md)]關聯分析演算法參數，有助於判斷採礦模型會包含藉由指定規則必須具有的最小機率的規則數目。 例如，將此值設定為 0.4 是指定只有當規則所描述的產品組合至少具有百分之四十的發生機率時，才可以產生此規則。  
  
 您將檢視變更的影響*MINIMUM_PROBABILTY*稍後的課程中的參數。  
  
## <a name="alter-mining-structure-statement"></a>ALTER MINING STRUCTURE 陳述式  
 若要將包含巢狀的資料表至採礦結構的採礦模型，您使用[ALTER MINING STRUCTURE &#40;DMX&#41; ](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016)陳述式。 陳述式中的程式碼可分成下列各部份：  
  
-   識別採礦結構  
  
-   命名採礦模型  
  
-   定義索引鍵資料行  
  
-   定義輸入資料行和可預測資料行  
  
-   定義巢狀資料表資料行  
  
-   識別演算法和參數變更  
  
 下面是 `ALTER MINING STRUCTURE` 陳述式的一般範例，它會將採礦模型加入至包含巢狀資料表資料行的結構：  
  
```  
ALTER MINING STRUCTURE [<Mining Structure Name>]  
ADD MINING MODEL [<Mining Model Name>]  
(  
    [<key column>],  
    <mining model column> <usage>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
) USING <algorithm>( <algorithm parameters> )  
```  
  
 程式碼的第一行會識別將加入採礦模型的現有採礦結構：  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
```  
  
 程式碼的下一行命名要加入採礦結構中的採礦模型：  
  
```  
ADD MINING MODEL [<mining model name>]  
```  
  
 如需命名物件中的資料採礦延伸模組 (DMX) 的資訊，請參閱[識別碼&#40;DMX&#41;](/sql/dmx/identifiers-dmx)。  
  
 接下來幾行的程式碼會定義採礦結構中將由採礦模型使用的資料行：  
  
```  
[<key column>],  
<mining model columns> <usage>,  
```  
  
 您只能使用已經存在採礦結構中的資料行。  
  
 採礦模型資料行清單中的第一個資料行必須是採礦結構中的索引鍵資料行。 不過，您就不必輸入`KEY`之後索引鍵的資料行指定使用方式。 這是因為當您建立了採礦結構時，已經將資料行定義為索引鍵。  
  
 其餘幾行會指定新採礦模型中資料行的使用方式。 您可以使用下列語法來指定要用於預測之採礦模型中的資料行：  
  
```  
<column name> PREDICT,  
```  
  
 如果您沒有指定使用方式，就不需要在清單中加入資料採礦結構資料行。 參考資料採礦結構所使用的所有資料行都會自動供以該結構為基礎的採礦模型使用。 不過，除非您指定了使用方式，否則此模型將無法使用這些資料行進行定型。  
  
 程式碼的最後一行定義將用來產生採礦模型的演算法和演算法參數。  
  
```  
) USING <algorithm>( <algorithm parameters> )  
```  
  
## <a name="lesson-tasks"></a>課程工作  
 您將在這一課執行下列工作：  
  
-   使用預設機率，將關聯採礦模型加入至結構  
  
-   使用修改的機率，將關聯採礦模型加入至結構  
  
## <a name="adding-an-association-mining-model-to-the-structure-using-the-default-minimumprobability"></a>使用預設 MINIMUM_PROBABILITY 將關聯採礦模型加入到結構中  
 第一個工作是新增新的採礦模型加入購物籃採礦結構將會根據[!INCLUDE[msCoName](../includes/msconame-md.md)]使用的預設值的關聯分析演算法*MINIMUM_PROBABILITY*。  
  
#### <a name="to-add-an-association-mining-model"></a>加入關聯採礦模型  
  
1.  中**物件總管**，以滑鼠右鍵按一下執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向**新查詢**，然後按一下**DMX**。  
  
     此時會開啟 [查詢編輯器] 且包含新的空白查詢。  
  
    > [!NOTE]  
    >  若要針對特定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫建立 DMX 查詢，請以滑鼠右鍵按一下該資料庫，而非執行個體。  
  
2.  將 `ALTER MINING STRUCTURE` 陳述式的一般範例複製到空白查詢中。  
  
3.  取代下列項目：  
  
    ```  
    <mining structure name>   
    ```  
  
     成為：  
  
    ```  
    [Market Basket]  
    ```  
  
4.  取代下列項目：  
  
    ```  
    <mining model name>   
    ```  
  
     成為：  
  
    ```  
    [Default Association]  
    ```  
  
5.  取代下列項目：  
  
    ```  
    [<key column>],  
    <mining model columns>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
    ```  
  
     成為：  
  
    ```  
    OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    ```  
  
     在此情況下，`[Products]` 資料表已指定為可預測資料行`.`。此外，`[Model]` 資料行會包含在巢狀資料表資料行的清單中，因為它是巢狀資料表的索引鍵資料行。  
  
    > [!NOTE]  
    >  請記住，巢狀索引鍵與案例索引鍵不同。 案例索引鍵是案例的唯一識別碼，而巢狀索引鍵則是您想要建立模型的屬性。  
  
6.  取代下列項目：  
  
    ```  
    USING <algorithm>( <algorithm parameters> )  
    ```  
  
     成為：  
  
    ```  
    Using Microsoft_Association_Rules  
    ```  
  
     現在，產生的陳述式應該如下所示：  
  
    ```  
    ALTER MINING STRUCTURE [Market Basket]  
    ADD MINING MODEL [Default Association]  
    (  
        OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    )  
    Using Microsoft_Association_Rules  
    ```  
  
7.  在 **檔案**功能表上，按一下**另存 DMXQuery1.dmx 為**。  
  
8.  在 [**另存新檔**] 對話方塊中，瀏覽至適當的資料夾，並將檔案命名`Default_Association_Model.dmx`。  
  
9. 在工具列上，按一下**Execute**  按鈕。  
  
## <a name="adding-an-association-mining-model-to-the-structure-changing-the-default-minimumprobability"></a>變更預設 MINIMUM_PROBABILITY 以便將關聯採礦模型加入到結構中  
 下一項工作是根據 [!INCLUDE[msCoName](../includes/msconame-md.md)] 關聯分析演算法，將新的採礦模型加入至購物籃採礦結構中，並將 MINIMUM_PROBABILITY 的預設值變更為 0.01。 變更參數將導致 [!INCLUDE[msCoName](../includes/msconame-md.md)] 關聯分析演算法建立更多規則。  
  
#### <a name="to-add-an-association-mining-model"></a>加入關聯採礦模型  
  
1.  中**物件總管**，以滑鼠右鍵按一下執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向**新查詢**，然後按一下**DMX**。  
  
     此時會開啟 [查詢編輯器] 且包含新的空白查詢。  
  
2.  將 `ALTER MINING STRUCTURE` 陳述式的一般範例複製到空白查詢中。  
  
3.  取代下列項目：  
  
    ```  
    <mining structure name>   
    ```  
  
     成為：  
  
    ```  
    Market Basket  
    ```  
  
4.  取代下列項目：  
  
    ```  
    <mining model name>   
    ```  
  
     成為：  
  
    ```  
    [Modified Association]  
    ```  
  
5.  取代下列項目：  
  
    ```  
    <mining model columns>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
    ```  
  
     成為：  
  
    ```  
    OrderNumber,  
    [Products] PREDICT (  
            [Model]  
        )  
    ```  
  
     在此情況下，`[Products]` 資料表已指定為可預測資料行。 此外，`[MODEL]` 資料行會包含在清單中，因為它是巢狀資料表中的索引鍵資料行。  
  
6.  取代下列項目：  
  
    ```  
    USING <algorithm>( <algorithm parameters> )  
    ```  
  
     成為：  
  
    ```  
    USING Microsoft_Association_Rules (Minimum_Probability = 0.1)  
    ```  
  
     現在，產生的陳述式應該如下所示：  
  
    ```  
    ALTER MINING STRUCTURE [Market Basket]  
    ADD MINING MODEL [Modified Assocation]  
    (  
        OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    )  
    USING Microsoft_Association_Rules (Minimum_Probability = 0.1)  
    ```  
  
7.  在 **檔案**功能表上，按一下**另存 DMXQuery1.dmx 為**。  
  
8.  在 [**另存新檔**] 對話方塊中，瀏覽至適當的資料夾，並將檔案命名`Modified Association_Model.dmx`。  
  
9. 在工具列上，按一下**Execute**  按鈕。  
  
 在下一課，您將處理購物籃採礦結構及其相關聯的採礦模型。  
  
## <a name="next-lesson"></a>下一課  
 [第 3 課：處理購物籃採礦結構](../../2014/tutorials/lesson-3-processing-the-market-basket-mining-structure.md)  
  
  
