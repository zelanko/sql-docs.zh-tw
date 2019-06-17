---
title: 第 5 課：執行預測查詢 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0037bd2f-aa2d-464b-bf86-b0210f0438b1
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a5f4d6dd79f62541e207df688349f694680e2421
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62822310"
---
# <a name="lesson-5-executing-prediction-queries"></a>第 5 課：執行預測查詢
  在這一課，您將使用[SELECT FROM\<模型 > 預測 JOIN (DMX)](/sql/dmx/select-from-model-cases-dmx)形式的 SELECT 陳述式來建立兩種不同預測基礎的決策樹模型中建立[第 2 課：將採礦模型加入關聯採礦結構](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)。 這些預測類型定義如下。  
  
 單一查詢  
 進行預測時，使用單一查詢提供特定的值。 例如，您可以將輸入傳遞到查詢 (例如，計算距離、區域碼，或客戶的孩童數目) 來判斷單一客戶是否可能是自行車購買者。 單一查詢會根據這些輸入傳回一個值，表示該客戶購買自行車的可能性。  
  
 批次查詢  
 使用批次查詢來判斷潛在客戶資料表中，誰有可能購買自行車。 例如，如果行銷部門提供客戶和客戶屬性之清單給您，您可以使用批次預測來判斷資料表中誰有可能購買自行車。  
  
 [SELECT FROM\<模型 > 預測 JOIN (DMX)](/sql/dmx/select-from-model-cases-dmx)形式的 SELECT 陳述式包含三個部分：  
  
-   結果傳回的採礦模型資料行和預測函數的清單。 這些結果也可以包含來源資料的輸入資料行。  
  
-   定義用來建立預測資料的來源查詢。 例如，在批次查詢中，這可能是一份客戶名單。  
  
-   採礦模型資料行和來源資料之間的對應。 如果這些名稱相符，您就可以使用 NATURAL 語法，並省略資料行對應。  
  
 您可以使用預測函數，進一步加強查詢。 預測函數提供其他資訊，例如發生預測的機率，並提供對培訓資料集的預測支援。 如需有關預測函數的詳細資訊，請參閱[函式&#40;DMX&#41;](/sql/dmx/functions-dmx)。  
  
 此教學課程中的預測是以 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 範例資料庫中的 ProspectiveBuyer 資料表為基礎。 ProspectiveBuyer 資料表包含潛在客戶及其相關聯特性的清單。 此資料表的客戶與用來建立決策樹採礦模型的客戶無關。  
  
 您也可以在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中使用預測查詢產生器來建立預測。  
  
## <a name="lesson-tasks"></a>課程工作  
 您將在這一課執行下列工作：  
  
-   建立單一查詢來判斷特定客戶是否有可能購買自行車。  
  
-   建立批次查詢來判斷客戶資料表中列出的碼些客戶可能購買自行車。  
  
## <a name="singleton-query"></a>單一查詢  
 第一個步驟是使用[FROM&#60;模型&#62;PREDICTION JOIN &#40;DMX&#41; ](/sql/dmx/select-from-model-cases-dmx)單一預測查詢中。 以下是單一陳述式的一般範例：  
  
```  
SELECT <select list> FROM [<mining model name>]   
NATURAL PREDICTION JOIN  
(SELECT '<value>' AS [<column>], ...)  
AS [<input alias>]  
```  
  
 第一行程式碼會定義在採礦模型中應該由查詢傳回的資料行，並且指定用來產生預測的採礦模型：  
  
```  
SELECT <select list> FROM [<mining model name>]   
```  
  
 接下來幾行的程式碼定義您用來建立預測的客戶特性：  
  
```  
NATURAL PREDICTION JOIN  
(SELECT '<value>' AS [<column>], ...)  
AS [<input alias>]  
ORDER BY <expression>  
```  
  
 如果您指定 NATURAL PREDICTION JOIN，伺服器會根據資料行名稱來比對模型的每一個資料行與輸入的資料行。 如果資料行名稱不符，就會忽略這些資料行。  
  
#### <a name="to-create-a-singleton-prediction-query"></a>若要建立單一預測查詢  
  
1.  中**物件總管**，以滑鼠右鍵按一下執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向**新查詢**，然後按一下**DMX**。  
  
     此時會開啟 [查詢編輯器] 且包含新的空白查詢。  
  
2.  將單一陳述式的一般範例複製到空白查詢中。  
  
3.  取代下列項目：  
  
    ```  
    <select list>   
    ```  
  
     成為：  
  
    ```  
    [Bike Buyer] AS Buyer, PredictHistogram([Bike Buyer]) AS Statistics  
    ```  
  
     AS 陳述式是用來建立查詢傳回之資料行的別名。 [PredictHistogram](/sql/dmx/predicthistogram-dmx)函式會傳回有關預測，包括機率和支援的統計資料。 如需可用於預測陳述式的函式的詳細資訊，請參閱[函式&#40;DMX&#41;](/sql/dmx/functions-dmx)。  
  
4.  取代下列項目：  
  
    ```  
    [<mining model>]   
    ```  
  
     成為：  
  
    ```  
    [Decision Tree]  
    ```  
  
5.  取代下列項目：  
  
    ```  
    (SELECT '<value>' AS [<column name>], ...)  AS t  
    ```  
  
     成為：  
  
    ```  
    (SELECT 35 AS [Age],  
      '5-10 Miles' AS [Commute Distance],  
      '1' AS [House Owner Flag],  
      2 AS [Number Cars Owned],  
      2 AS [Total Children]) AS t  
    ```  
  
     現在，完整的陳述式應該如下所示：  
  
    ```  
    SELECT  
       [Bike Buyer] AS Buyer,  
       PredictHistogram([Bike Buyer]) AS Statistics  
    FROM  
       [Decision Tree]  
    NATURAL PREDICTION JOIN  
    (SELECT 35 AS [Age],  
       '5-10 Miles' AS [Commute Distance],  
       '1' AS [House Owner Flag],  
       2 AS [Number Cars Owned],  
       2 AS [Total Children]) AS t  
    ```  
  
6.  在 **檔案**功能表上，按一下**另存 DMXQuery1.dmx 為**。  
  
7.  在 [**另存新檔**] 對話方塊中，瀏覽至適當的資料夾，並將檔案命名`Singleton_Query.dmx`。  
  
8.  在工具列上，按一下**Execute**  按鈕。  
  
     此查詢傳回有關具有指定特性的客戶是否會購買自行車的預測，以及有關該預測的統計資料。  
  
## <a name="batch-query"></a>批次查詢  
 下一個步驟是使用[FROM&#60;模型&#62;PREDICTION JOIN &#40;DMX&#41; ](/sql/dmx/select-from-model-cases-dmx)批次預測查詢中。 以下是批次陳述式的一般範例：  
  
```  
SELECT TOP <number> <select list>   
FROM [<mining model name>]  
PREDICTION JOIN  
OPENQUERY([<datasource>],'<SELECT statement>')  
  AS [<input alias>]  
ON <on clause, mapping,>  
WHERE <where clause, boolean expression,>  
ORDER BY <expression>  
```  
  
 如同在單一查詢一樣，程式碼的前兩行定義在採礦模型中由查詢傳回的資料行，以及用來產生預測的採礦模型名稱。 頂端\<數字 > 陳述式指定數目或所指定之結果的查詢只會傳回\<編號 >。  
  
 接下來幾行的程式碼定義預測所依據的來源資料。  
  
```  
OPENQUERY([<datasource>],'<SELECT statement>')  
  AS [<input alias>]  
```  
  
 對於擷取來源資料的方法，您有幾個選項，但在此教學課程中，您將使用 OPENQUERY。 如需可用選項的詳細資訊，請參閱[&#60;來源資料查詢&#62;](/sql/dmx/source-data-query)。  
  
 下一行定義採礦模型中的來源資料行與來源資料中資料行之間的對應：  
  
```  
ON <column mappings>  
```  
  
 WHERE 子句篩選預測查詢所傳回的結果：  
  
```  
WHERE <where clause, boolean expression,>  
```  
  
 程式碼的最後一行和選擇性的行會指定結果排序所依據的資料行：  
  
```  
ORDER BY <expression> [DESC|ASC]  
```  
  
 使用 ORDER BY 中使用的最上層的組合\<數字 > 陳述式，以篩選所傳回的結果。 例如，在此預測中，您將按預測的正確機率排序，傳回前十個自行車買主。 您可以使用 [DESC|ASC] 語法來控制顯示結果的順序。  
  
#### <a name="to-create-a-batch-prediction-query"></a>若要建立批次預測查詢  
  
1.  中**物件總管**，以滑鼠右鍵按一下執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向**新查詢**，然後按一下**DMX**。  
  
     此時會開啟 [查詢編輯器] 且包含新的空白查詢。  
  
2.  將批次陳述式的一般範例複製到空白查詢中。  
  
3.  取代下列項目：  
  
    ```  
    <select list>   
    ```  
  
     成為：  
  
    ```  
    SELECT  
      TOP 10  
      t.[LastName],  
      t.[FirstName],  
      [Decision Tree].[Bike Buyer],  
      PredictProbability([Bike Buyer])  
    ```  
  
     TOP 10 子句指定查詢只傳回前十個結果。 此查詢中的 ORDER BY 陳述式是按預測的正確機率來排序結果，因此，只傳回十個最可能的結果。  
  
4.  取代下列預留位置：  
  
    ```  
    [<mining model>]   
    ```  
  
     改為模型的名稱：  
  
    ```  
    [Decision Tree]  
    ```  
  
5.  取代下列泛用 OPENQUERY 陳述式：  
  
    ```  
    OPENQUERY([<datasource>],'<SELECT statement>')  
    ```  
  
     改為參考目前 Adventureworks 資料倉儲的陳述式，例如：  
  
    ```  
    OPENQUERY([Adventure Works DW 2014],  
      'SELECT  
        [LastName],  
        [FirstName],  
        [MaritalStatus],  
        [Gender],  
        [YearlyIncome],  
        [TotalChildren],  
        [NumberChildrenAtHome],  
        [Education],  
        [Occupation],  
        [HouseOwnerFlag],  
        [NumberCarsOwned]  
      FROM  
        [dbo].[ProspectiveBuyer]  
      ') AS t  
    ```  
  
6.  取代下列泛用語法：  
  
    ```  
    <ON clause, mapping,>   
    WHERE <where clause, boolean expression,>  
    ORDER BY <expression>  
    ```  
  
     改為此模型和輸入資料集所需的資料行對應：  
  
    ```  
    [Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
      [Decision Tree].[Gender] = t.[Gender] AND  
      [Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
      [Decision Tree].[Total Children] = t.[TotalChildren] AND  
      [Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
      [Decision Tree].[Education] = t.[Education] AND  
      [Decision Tree].[Occupation] = t.[Occupation] AND  
      [Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
      [Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
    WHERE [Decision Tree].[Bike Buyer] =1  
    ORDER BY PredictProbability([Bike Buyer]) DESC  
    ```  
  
     指定 `DESC`，先列出具有最高機率的結果。  
  
     現在，完整的陳述式應該如下所示：  
  
    ```  
    SELECT  
      TOP 10  
      t.[LastName],  
      t.[FirstName],  
      [Decision Tree].[Bike Buyer],  
      PredictProbability([Bike Buyer])  
    FROM  
      [Decision Tree]  
    PREDICTION JOIN  
      OPENQUERY([Adventure Works DW 2014],  
        'SELECT  
          [LastName],  
          [FirstName],  
          [MaritalStatus],  
          [Gender],  
          [YearlyIncome],  
          [TotalChildren],  
          [NumberChildrenAtHome],  
          [Education],  
          [Occupation],  
          [HouseOwnerFlag],  
          [NumberCarsOwned]  
        FROM  
          [dbo].[ProspectiveBuyer]  
        ') AS t  
    ON  
      [Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
      [Decision Tree].[Gender] = t.[Gender] AND  
      [Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
      [Decision Tree].[Total Children] = t.[TotalChildren] AND  
      [Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
      [Decision Tree].[Education] = t.[Education] AND  
      [Decision Tree].[Occupation] = t.[Occupation] AND  
      [Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
      [Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
    WHERE [Decision Tree].[Bike Buyer] =1  
    ORDER BY PredictProbability([Bike Buyer]) DESC  
    ```  
  
7.  在 **檔案**功能表上，按一下**另存 DMXQuery1.dmx 為**。  
  
8.  在 [**另存新檔**] 對話方塊中，瀏覽至適當的資料夾，並將檔案命名`Batch_Prediction.dmx`。  
  
9. 在工具列上，按一下**Execute**  按鈕。  
  
     查詢傳回一份資料表，其中包含客戶名稱、每一個客戶是否有可能購買自行車的預測及預測的機率。  
  
 這是 Bike Buyer 教學課程的最後步驟。 現在您已有採礦模型集合，可用來探索客戶之間的相似性，並預測潛在客戶是否會購買自行車。  
  
 若要了解如何在購物籃狀況中使用 DMX，請參閱[購物籃 DMX 教學課程](../../2014/tutorials/market-basket-dmx-tutorial.md)。  
  
  
