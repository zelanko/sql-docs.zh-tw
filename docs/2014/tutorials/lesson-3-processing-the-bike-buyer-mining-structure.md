---
title: 第3課：處理自行車購買者的採礦結構 |Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "62655803"
---
# <a name="lesson-3-processing-the-bike-buyer-mining-structure"></a>第 3 課：處理自行車買主採礦結構
  在這一課，您將使用[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]範例資料庫中的 INSERT INTO 語句和 vTargetMail view，來處理您在[第1課：建立自行車購買者採礦結構](../../2014/tutorials/lesson-1-creating-the-bike-buyer-mining-structure.md)和[第2課：將採礦模型加入自行車購買者採礦結構](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md)中所建立的採礦結構和採礦模型。  
  
 當您處理採礦結構時，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會讀取來源資料並建立支援採礦模型的結構。 當您處理採礦模型時，採礦結構所定義的資料會透過您選擇的資料採礦演算法來傳遞。 此演算法會搜尋趨勢和模式，然後將此資訊儲存在採礦模型中。 因此，採礦模型不包含實際來源資料，而包含演算法所發現的資訊。 如需處理採礦模型的詳細資訊，請參閱[&#40;資料採礦&#41;的處理需求和考慮](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)。  
  
 只有當您變更結構資料行或變更來源資料時，才需要重新處理採礦結構。 如果您將採礦模型加入已處理的採礦結構中，您可以使用 INSERT INTO MINING MODEL 陳述式來定型新的採礦模型。  
  
## <a name="train-structure-template"></a>定型結構範本  
 若要將採礦結構和其相關聯的採礦模型定型，請使用[INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx)語句。 陳述式中的程式碼可分成下列各部份：  
  
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
  
 在這一課，您使用 `OPENQUERY` 來定義來源資料。 如需有關定義來源查詢之其他方法的詳細資訊，請參閱[&#60;來源資料查詢&#62;](/sql/dmx/source-data-query)。  
  
## <a name="lesson-tasks"></a>課程工作  
 您將在這一課執行下列工作：  
  
-   處理自行車買主採礦結構  
  
## <a name="processing-the-predictive-mining-structure"></a>處理預測採礦結構  
  
#### <a name="to-process-the-mining-structure-by-using-insert-into"></a>若要使用 INSERT INTO 處理採礦結構  
  
1.  在**物件總管**中，以滑鼠右鍵按一下的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]實例，指向 [追加**查詢**]，然後按一下 [ **DMX**]。  
  
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
  
6.  **在 [檔案**] 功能表上，按一下 [**將 DMXQuery1 另存為**]。  
  
7.  在 [**另存**新檔] 對話方塊中，流覽至適當的資料夾，並`Process Bike Buyer Structure.dmx`將檔案命名為。  
  
8.  在工具列上，按一下 [**執行**] 按鈕。  
  
 在下一課，您將探索這一課加入採礦結構中的採礦模型內容。  
  
## <a name="next-lesson"></a>下一課  
 [第 4 課：瀏覽自行車買主採礦模型](../../2014/tutorials/lesson-4-browsing-the-bike-buyer-mining-models.md)  
  
  
