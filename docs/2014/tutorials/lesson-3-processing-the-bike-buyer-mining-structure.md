---
title: 第 3 課：處理自行車買主採礦結構 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e748c2cd-339d-4e82-82f1-be2d0fc41b61
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2e3f85016b32884b9a6b809e28d20d9985f97cd9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62655803"
---
# <a name="lesson-3-processing-the-bike-buyer-mining-structure"></a>第 3 課：處理自行車買主採礦結構
  在這一課，您將使用 INSERT INTO 陳述式和從的 vTargetMail 檢視[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]範例資料庫來處理採礦結構和採礦模型中建立[第 1 課：建立自行車買主採礦結構](../../2014/tutorials/lesson-1-creating-the-bike-buyer-mining-structure.md)和[第 2 課：將採礦模型加入 Bike Buyer 採礦結構](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md)。  
  
 當您處理採礦結構時，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會讀取來源資料並建立支援採礦模型的結構。 當您處理採礦模型時，採礦結構所定義的資料會透過您選擇的資料採礦演算法來傳遞。 此演算法會搜尋趨勢和模式，然後將此資訊儲存在採礦模型中。 因此，採礦模型不包含實際來源資料，而包含演算法所發現的資訊。 如需有關處理採礦模型的詳細資訊，請參閱 <<c0> [ 處理需求和考量&#40;資料採礦&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)。</c0>  
  
 只有當您變更結構資料行或變更來源資料時，才需要重新處理採礦結構。 如果您將採礦模型加入已處理的採礦結構中，您可以使用 INSERT INTO MINING MODEL 陳述式來定型新的採礦模型。  
  
## <a name="train-structure-template"></a>定型結構範本  
 若要定型採礦結構及其相關聯的採礦模型，使用[插入&#40;DMX&#41; ](/sql/dmx/insert-into-dmx)陳述式。 陳述式中的程式碼可分成下列各部份：  
  
-   識別採礦結構  
  
-   列出採礦結構中的資料行  
  
-   定義定型資料  
  
 以下是 INSERT INTO 陳述式的一般範例：  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
(  
   <mining structure columns>  
)  
OPENQUERY([<datasource>],'<SELECT statement>')  
```  
  
 程式碼的第一行識別您將定型的採礦結構：  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
```  
  
 程式碼的下一行指定採礦結構定義的資料行。 您必須列出採礦結構的每一個資料行，且每一個資料行必須對應到來源查詢資料內包含的資料行。  
  
```  
(  
   <mining structure columns>  
)  
```  
  
 程式碼的最後一行定義將用來定型採礦結構的資料：  
  
```  
OPENQUERY([<datasource>],'<SELECT statement>')  
```  
  
 在這一課，您使用 `OPENQUERY` 來定義來源資料。 定義來源查詢的其他方法的相關資訊，請參閱[&#60;來源資料查詢&#62;](/sql/dmx/source-data-query)。  
  
## <a name="lesson-tasks"></a>課程工作  
 您將在這一課執行下列工作：  
  
-   處理自行車買主採礦結構  
  
## <a name="processing-the-predictive-mining-structure"></a>處理預測採礦結構  
  
#### <a name="to-process-the-mining-structure-by-using-insert-into"></a>若要使用 INSERT INTO 處理採礦結構  
  
1.  中**物件總管**，以滑鼠右鍵按一下執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向**新查詢**，然後按一下**DMX**。  
  
     此時會開啟 [查詢編輯器] 且包含新的空白查詢。  
  
2.  將 INSERT INTO 陳述式的一般範例複製到空白查詢中。  
  
3.  取代下列項目：  
  
    ```  
    [<mining structure name>]   
    ```  
  
     成為：  
  
    ```  
    Bike Buyer  
    ```  
  
4.  取代下列項目：  
  
    ```  
    <mining structure columns>  
    ```  
  
     成為：  
  
    ```  
    [Customer Key],  
    [Age],  
    [Bike Buyer],  
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
  
5.  取代下列項目：  
  
    ```  
    OPENQUERY([<datasource>],'<SELECT statement>')  
    ```  
  
     成為：  
  
    ```  
    OPENQUERY([Adventure Works DW],  
       'SELECT CustomerKey, Age, BikeBuyer,  
             CommuteDistance,EnglishEducation,  
             Gender,HouseOwnerFlag,MaritalStatus,  
             NumberCarsOwned,NumberChildrenAtHome,   
             EnglishOccupation,Region,TotalChildren,  
             YearlyIncome   
        FROM dbo.vTargetMail')  
    ```  
  
     OPENQUERY 陳述式會參考 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 資料來源來存取 vTargetMail 檢視表。 此檢視包含將用來定型採礦模型的來源資料。  
  
     現在，完整的陳述式應該如下所示：  
  
    ```  
    INSERT INTO MINING STRUCTURE [Bike Buyer]  
    (  
       [Customer Key],  
       [Age],  
       [Bike Buyer],  
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
    )  
    OPENQUERY([Adventure Works DW],  
       'SELECT CustomerKey, Age, BikeBuyer,  
             CommuteDistance,EnglishEducation,  
             Gender,HouseOwnerFlag,MaritalStatus,  
             NumberCarsOwned,NumberChildrenAtHome,   
             EnglishOccupation,Region,TotalChildren,  
             YearlyIncome   
        FROM dbo.vTargetMail')  
    ```  
  
6.  在 **檔案**功能表上，按一下**另存 DMXQuery1.dmx 為**。  
  
7.  在 [**另存新檔**] 對話方塊中，瀏覽至適當的資料夾，並將檔案命名`Process Bike Buyer Structure.dmx`。  
  
8.  在工具列上，按一下**Execute**  按鈕。  
  
 在下一課，您將探索這一課加入採礦結構中的採礦模型內容。  
  
## <a name="next-lesson"></a>下一課  
 [第 4 課：瀏覽 Bike Buyer 採礦模型](../../2014/tutorials/lesson-4-browsing-the-bike-buyer-mining-models.md)  
  
  
