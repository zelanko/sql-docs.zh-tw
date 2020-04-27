---
title: 第3課：處理購物籃的採礦結構 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 095a043f-cf6f-45bb-a021-ae4e1b535c65
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ce2c2e6944d524a38edc331d2cd128ca7cf7d419
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62653851"
---
# <a name="lesson-3-processing-the-market-basket-mining-structure"></a>第 3 課：處理購物籃採礦結構
  在這一課，您將使用[INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx)語句和[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]範例資料庫中的 vAssocSeqLineItems 和 vAssocSeqOrders，來處理您在[第1課：建立購物籃採礦結構](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md)和[第2課：將採礦模型新增至購物籃採礦結構](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)中所建立的採礦結構和採礦模型。  
  
 當您處理採礦結構時，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會讀取來源資料並建立支援採礦模型的結構。 當您處理採礦模型時，採礦結構所定義的資料會透過您選擇的資料採礦演算法來傳遞。 此演算法會搜尋趨勢和模式，然後將此資訊儲存在採礦模型中。 因此，採礦模型不包含實際來源資料，而包含演算法所發現的資訊。 如需處理採礦模型的詳細資訊，請參閱[&#40;資料採礦&#41;的處理需求和考慮](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)。  
  
 唯有當您變更結構資料行或變更來源資料時，您才需要重新處理採礦結構。 如果您將採礦模型加入至已處理的採礦結構中，就可以使用 `INSERT INTO MINING MODEL` 陳述式，在現有的資料上定型新的採礦模型。  
  
 因為購物籃採礦結構包含巢狀資料表，所以您必須使用巢狀資料表結構來定義要定型的採礦資料行，並使用 `SHAPE` 命令定義從來源資料表提取定型資料的查詢。  
  
## <a name="insert-into-statement"></a>INSERT INTO 陳述式  
 若要訓練購物籃的採礦結構和其相關聯的採礦模型，請使用[INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx)語句。 陳述式中的程式碼可分成下列各部份。  
  
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
  
 接下來幾行的程式碼指定採礦結構定義的資料行。 您必須列出採礦結構的每一個資料行，且每一個資料行必須對應到來源查詢資料內包含的資料行。 您可以使用 `SKIP` 來忽略存在來源資料而不存在採礦結構中的資料行。 如需如何使用`SKIP`的詳細資訊，請參閱[INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx)。  
  
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
  
 在這一課，您使用 `OPENQUERY` 來定義來源資料。 如需有關在來源資料上定義查詢之其他方法的詳細資訊，請參閱[&#60;來源資料查詢&#62;](/sql/dmx/source-data-query)。  
  
## <a name="lesson-tasks"></a>課程工作  
 您將在這一課執行下列工作：  
  
-   處理購物籃採礦結構  
  
## <a name="processing-the-market-basket-mining-structure"></a>處理購物籃採礦結構  
  
#### <a name="to-process-the-mining-structure-by-using-insert-into"></a>若要使用 INSERT INTO 處理採礦結構  
  
1.  在**物件總管**中，以滑鼠右鍵按一下的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]實例，指向 [追加**查詢**]，然後按一下 [ **DMX**]。  
  
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
  
     來源查詢會參考[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]範例專案中所定義的資料來源。 它使用此資料來源來存取 vAssocSeqLineItems 和 vAssocSeqOrders 檢視。 這些檢視包含將用於定型採礦模型的來源資料。 如果您尚未建立此專案或這些視圖，請參閱[基本資料採礦教學](../../2014/tutorials/basic-data-mining-tutorial.md)課程。  
  
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
  
6.  **在 [檔案**] 功能表上，按一下 [**將 DMXQuery1 另存為**]。  
  
7.  在 [**另存**新檔] 對話方塊中，流覽至適當的資料夾，並`Process Market Basket.dmx`將檔案命名為。  
  
8.  在工具列上，按一下 [**執行**] 按鈕。  
  
 在查詢執行完成之後，您就可以檢視找到的模式和項目集、檢視關聯，或依據項目集、機率或重要性進行篩選。 若要查看這項資訊[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，請在中，以滑鼠右鍵按一下資料模型的名稱，然後按一下 **[流覽]**。  
  
 在下一課，您將依據您加入購物籃結構中的採礦模型來建立幾個預測。  
  
## <a name="next-lesson"></a>下一課  
 [第 4 課：執行購物籃預測](../../2014/tutorials/lesson-4-executing-market-basket-predictions.md)  
  
  
