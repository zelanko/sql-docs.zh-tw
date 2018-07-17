---
title: 第 3 課： 處理購物籃採礦結構 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 095a043f-cf6f-45bb-a021-ae4e1b535c65
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0d14fe6f8cbfae7370c0b02626f54758d4159d83
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37297578"
---
# <a name="lesson-3-processing-the-market-basket-mining-structure"></a>第 3 課：處理購物籃採礦結構
  在這一課，您將使用[插入&#40;DMX&#41; ](/sql/dmx/insert-into-dmx)陳述式的 vAssocSeqLineItems 和 vAssocSeqOrders 從[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]範例資料庫來處理採礦結構和採礦模型在中建立[第 1 課： 建立購物籃採礦結構](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md)並[第 2 課： Adding Mining Models to Market Basket Mining Structure&lt](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)。  
  
 當您處理採礦結構時，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會讀取來源資料並建立支援採礦模型的結構。 當您處理採礦模型時，採礦結構所定義的資料會透過您選擇的資料採礦演算法來傳遞。 此演算法會搜尋趨勢和模式，然後將此資訊儲存在採礦模型中。 因此，採礦模型不包含實際來源資料，而包含演算法所發現的資訊。 如需有關處理採礦模型的詳細資訊，請參閱 <<c0> [ 處理需求和考量&#40;資料採礦&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)。</c0>  
  
 唯有當您變更結構資料行或變更來源資料時，您才需要重新處理採礦結構。 如果您將採礦模型加入至已處理的採礦結構中，就可以使用 `INSERT INTO MINING MODEL` 陳述式，在現有的資料上定型新的採礦模型。  
  
 因為購物籃採礦結構包含巢狀資料表，所以您必須使用巢狀資料表結構來定義要定型的採礦資料行，並使用 `SHAPE` 命令定義從來源資料表提取定型資料的查詢。  
  
## <a name="insert-into-statement"></a>INSERT INTO 陳述式  
 若要定型購物籃採礦結構及其相關聯的採礦模型，使用[插入&#40;DMX&#41; ](/sql/dmx/insert-into-dmx)陳述式。 陳述式中的程式碼可分成下列各部份。  
  
-   識別採礦結構  
  
-   列出採礦結構中的資料行  
  
-   使用 `SHAPE` 定義定型資料  
  
 下面是 `INSERT INTO` 陳述式的一般範例：  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
(  
   <mining structure columns>  
   [<nested table>]  
   ( SKIP, <skipped column> )  
)  
SHAPE {  
  OPENQUERY([<datasource>],'<SELECT statement>') }  
APPEND  
(   
  {OPENQUERY([<datasource>],'<nested SELECT statement>')  
}  
RELATE [<case key>] TO [<foreign key>]  
) AS [<nested table>]  
```  
  
 程式碼的第一行識別您將定型的採礦結構：  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
```  
  
 接下來幾行的程式碼指定採礦結構定義的資料行。 您必須列出採礦結構的每一個資料行，且每一個資料行必須對應到來源查詢資料內包含的資料行。 您可以使用 `SKIP` 來忽略存在來源資料而不存在採礦結構中的資料行。 如需有關如何使用`SKIP`，請參閱 < [INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx)。  
  
```  
(  
   <mining structure columns>  
   [<nested table>]  
   ( SKIP, <skipped column> )  
)  
```  
  
 程式碼的最後幾行定義將用於定型採礦結構的資料。 因為來源資料包含在兩份資料表內，所以您將使用 `SHAPE` 使兩份資料表彼此相關。  
  
```  
SHAPE {  
  OPENQUERY([<datasource>],'<SELECT statement>') }  
APPEND  
(   
  {OPENQUERY([<datasource>],''<nested SELECT statement>'')  
}  
RELATE [<case key>] TO [<foreign key>]  
) AS [<nested table>]  
```  
  
 在這一課，您使用 `OPENQUERY` 來定義來源資料。 如需其他方法的來源資料定義查詢的資訊，請參閱[&#60;來源資料查詢&#62;](/sql/dmx/source-data-query)。  
  
## <a name="lesson-tasks"></a>課程工作  
 您將在這一課執行下列工作：  
  
-   處理購物籃採礦結構  
  
## <a name="processing-the-market-basket-mining-structure"></a>處理購物籃採礦結構  
  
#### <a name="to-process-the-mining-structure-by-using-insert-into"></a>若要使用 INSERT INTO 處理採礦結構  
  
1.  中**物件總管**，以滑鼠右鍵按一下執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向**新查詢**，然後按一下**DMX**。  
  
     此時會開啟 [查詢編輯器] 且包含新的空白查詢。  
  
2.  將 INSERT INTO 陳述式的一般範例複製到空白查詢中。  
  
3.  取代下列項目：  
  
    ```  
    [<mining structure>]  
    ```  
  
     成為：  
  
    ```  
    Market Basket  
    ```  
  
4.  取代下列項目：  
  
    ```  
    <mining structure columns>  
    [<nested table>]  
    ( SKIP, <skipped column> )  
    ```  
  
     成為：  
  
    ```  
    [OrderNumber],  
    [Products]   
    (SKIP, [Model])  
    ```  
  
     陳述式中的 `Products` 會參考 SHAPE 陳述式所定義的 Products 資料表。 `SKIP` 用來忽略 Model 資料行，此資料行在來源資料中做為索引鍵，但在採礦結構中沒有使用。  
  
5.  取代下列項目：  
  
    ```  
    SHAPE {  
      OPENQUERY([<datasource>],'<SELECT statement>') }  
    APPEND  
    (   
      {OPENQUERY([<datasource>],'<nested SELECT statement>')  
    }  
    RELATE [<case key>] TO [<foreign key>]  
    ) AS [<nested table>]  
    ```  
  
     成為：  
  
    ```  
    SHAPE {  
      OPENQUERY([Adventure Works DW],'SELECT OrderNumber  
                FROM vAssocSeqOrders ORDER BY OrderNumber')}  
    APPEND  
    (   
      {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, Model FROM   
        dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')  
    }  
    RELATE OrderNumber to OrderNumber   
    ) AS [Products]  
    ```  
  
     來源查詢會參考[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]中所定義的資料來源[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]範例專案。 它使用此資料來源來存取 vAssocSeqLineItems 和 vAssocSeqOrders 檢視。 這些檢視包含將用於定型採礦模型的來源資料。 如果您尚未建立這個專案或這些檢視，請參閱[83c8-9df5dddfeb9c"&gt;basic Data Mining Tutorial&lt](../../2014/tutorials/basic-data-mining-tutorial.md)。  
  
     在 `SHAPE` 命令內，您將使用 `OPENQUERY` 來定義兩項查詢。 第一項查詢定義父資料表，第二項查詢定義巢狀資料表。 兩份資料表利用同時存在於其中的 OrderNumber 資料行而彼此相關。  
  
     現在，完整的陳述式應該如下所示：  
  
    ```  
    INSERT INTO MINING STRUCTURE [Market Basket]  
    (  
       [OrderNumber],[Products] (SKIP, [Model])  
    )  
    SHAPE {  
      OPENQUERY([Adventure Works DW],'SELECT OrderNumber  
                FROM vAssocSeqOrders ORDER BY OrderNumber')}  
    APPEND  
    (   
      {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, Model FROM   
        dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')  
    }  
    RELATE OrderNumber to OrderNumber   
    ) AS [Products]  
    ```  
  
6.  在 **檔案**功能表上，按一下**另存 DMXQuery1.dmx 為**。  
  
7.  在 [**另存新檔**] 對話方塊中，瀏覽至適當的資料夾，並將檔案命名`Process Market Basket.dmx`。  
  
8.  在工具列上，按一下**Execute**  按鈕。  
  
 在查詢執行完成之後，您就可以檢視找到的模式和項目集、檢視關聯，或依據項目集、機率或重要性進行篩選。 若要檢視此資訊，請在[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，以滑鼠右鍵按一下 資料模型的名稱，然後按一下**瀏覽**。  
  
 在下一課，您將依據您加入購物籃結構中的採礦模型來建立幾個預測。  
  
## <a name="next-lesson"></a>下一課  
 [第 4 課：執行購物籃預測](../../2014/tutorials/lesson-4-executing-market-basket-predictions.md)  
  
  
