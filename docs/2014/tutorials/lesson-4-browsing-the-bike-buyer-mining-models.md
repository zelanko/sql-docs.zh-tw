---
title: 第 4 課：瀏覽 Bike Buyer 採礦模型 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 8de3c500-f881-42da-a096-b6c03300d58d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 709df371d840d4b24e420b4fcd08750fd31e8075
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63070876"
---
# <a name="lesson-4-browsing-the-bike-buyer-mining-models"></a>第 4 課：瀏覽自行車買主採礦模型
  在這一課，您將使用[SELECT (DMX)](/sql/dmx/select-dmx)陳述式來探索決策樹和群集採礦的內容模型中建立您[第 2 課：將採礦模型加入預測採礦結構](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md)。  
  
 包含在採礦模型中的資料行不是採礦結構所定義的資料行，而是描述該演算法所發現的趨勢和模式的一組特定資料行。 這些採礦模型資料行所述[DMSCHEMA_MINING_MODEL_CONTENT 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset)結構描述資料列。 例如，內容結構描述資料列集的 MODEL_NAME 資料行包含採礦模型的名稱。 若為群集採礦模型，NODE_CAPTION 資料行包含每一個群集的名稱，NODE_DESCRIPTION 資料行包含每一個群集之特性的描述。 您可以利用 SELECT FROM 瀏覽這些資料行\<模型 >。在 DMX 中的陳述式內容。 您也可以使用此陳述式來探索用來建立採礦模型的資料。 您必須在採礦結構中啟用鑽研，才能使用此陳述式。 如需有關此陳述式的詳細資訊，請參閱[FROM&#60;模型&#62;。案例&#40;DMX&#41;](/sql/dmx/select-from-model-content-dmx)。  
  
 您也可以使用 SELECT DISTINCT 陳述式來傳回分隔資料行的所有狀態。 例如，如果您在性別資料行執行此作業，該查詢將傳回 `male` 和 `female`。  
  
## <a name="lesson-tasks"></a>課程工作  
 您將在這一課執行下列工作：  
  
-   探索採礦模型所包含的內容  
  
-   從用來培訓採礦模型的來源資料中傳回案例  
  
-   探索特定分隔資料行可用的不同狀態  
  
## <a name="returning-the-content-of-a-mining-model"></a>傳回採礦模型的內容  
 在這一課，您可以使用[FROM&#60;模型&#62;。內容&#40;DMX&#41; ](/sql/dmx/select-from-model-dimension-content-dmx)陳述式來傳回群集模型的內容。  
  
 以下是 SELECT FROM 的一般範例\<模型 >。內容的陳述式：  
  
```  
SELECT <select list> FROM [<mining model>].CONTENT  
WHERE <where clause>  
```  
  
 程式碼的第一行定義要從採礦模型內容中傳回的資料行，及其相關聯的採礦模型：  
  
```  
SELECT <select list> FROM [<mining model].CONTENT  
```  
  
 採礦模型名稱旁邊的 .CONTENT 子句指定您要從採礦模型傳回內容。 如需有關採礦模型中包含的資料行的詳細資訊，請參閱[DMSCHEMA_MINING_MODEL_CONTENT 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset)。  
  
 您可以選擇性地使用程式碼的最後一行來篩選陳述式傳回的結果：  
  
```  
WHERE <where clause>  
```  
  
 例如，如果您想要將查詢的結果限制為只有包含大量案例的群集，您可以將下列 WHERE 子句加入 SELECT 陳述式中：  
  
```  
WHERE NODE_SUPPORT > 100  
```  
  
 如需使用 WHERE 陳述式的詳細資訊，請參閱 <<c0> [ 選取&#40;DMX&#41;](/sql/dmx/select-dmx)。</c0>  
  
#### <a name="to-return-the-content-of-the-clustering-mining-model"></a>若要傳回群集採礦模型的內容  
  
1.  中**物件總管**，以滑鼠右鍵按一下執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向**新查詢**，然後按一下**DMX**。  
  
     此時會開啟 [查詢編輯器] 且包含新的空白查詢。  
  
2.  將 SELECT FROM 的一般範例複製\<模型 >。內容到空白查詢的陳述式。  
  
3.  取代下列項目：  
  
    ```  
    <select list>   
    ```  
  
     成為：  
  
    ```  
    *  
    ```  
  
     您也可以取代 * 任何資料行中包含一份[DMSCHEMA_MINING_MODEL_CONTENT 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset)。  
  
4.  取代下列項目：  
  
    ```  
    [<mining model>]   
    ```  
  
     成為：  
  
    ```  
    [Clustering]  
    ```  
  
     現在，完整的陳述式應該如下所示：  
  
    ```  
    SELECT * FROM [Clustering].CONTENT  
    ```  
  
5.  在 **檔案**功能表上，按一下**另存 DMXQuery1.dmx 為**。  
  
6.  在 [**另存新檔**] 對話方塊中，瀏覽至適當的資料夾，並將檔案命名`SELECT_CONTENT.dmx`。  
  
7.  在工具列上，按一下**Execute**  按鈕。  
  
     此查詢會傳回採礦模型的內容。  
  
## <a name="use-drillthrough"></a>使用鑽研  
 下一步是使用鑽研陳述式來傳回用來培訓決策樹採礦模型的案例取樣。 在這一課，您可以使用[FROM&#60;模型&#62;。案例&#40;DMX&#41; ](/sql/dmx/select-from-model-content-dmx)陳述式來傳回決策樹模型的內容。  
  
 以下是 SELECT FROM 的一般範例\<模型 >。CASES 陳述式：  
  
```  
SELECT <select list>   
FROM [<mining model>].CASES  
WHERE IsInNode('<node id>')  
```  
  
 程式碼的第一行定義要從來源資料中傳回的資料行，及其包含的採礦模型：  
  
```  
SELECT <select list> FROM [<mining model>].CASES  
```  
  
 .CASES 子句會指定您執行鑽研查詢。 若要使用鑽研，則當您建立採礦模型時必須啟用鑽研。  
  
 程式碼的最後一行是選用的，它指定採礦模型中您要求案例的節點：  
  
```  
WHERE IsInNode('<node id>')  
```  
  
 如需有關搭配 IsInNode 使用 WHERE 陳述式的詳細資訊，請[FROM&#60;模型&#62;。案例&#40;DMX&#41;](/sql/dmx/select-from-model-content-dmx)。  
  
#### <a name="to-return-the-cases-that-were-used-to-train-the-mining-model"></a>若要傳回用來培訓採礦模型的案例  
  
1.  中**物件總管**，以滑鼠右鍵按一下執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向**新查詢**，然後按一下**DMX**。  
  
     此時會開啟 [查詢編輯器] 且包含新的空白查詢。  
  
2.  將 SELECT FROM 的一般範例複製\<模型 >。到空白查詢的情況下陳述式。  
  
3.  取代下列項目：  
  
    ```  
    <select list>   
    ```  
  
     成為：  
  
    ```  
    *  
    ```  
  
     您也可以將 * 取代成來源資料 (例如 [Bike Buyer]) 所包含的任何資料行清單。  
  
4.  取代下列項目：  
  
    ```  
    [<mining model>]   
    ```  
  
     成為：  
  
    ```  
    [Decision Tree]  
    ```  
  
     現在，完整的陳述式應該如下所示：  
  
    ```  
    SELECT *   
    FROM [Decision Tree].CASES  
    ```  
  
5.  在 **檔案**功能表上，按一下**另存 DMXQuery1.dmx 為**。  
  
6.  在 [**另存新檔**] 對話方塊中，瀏覽至適當的資料夾，並將檔案命名`SELECT_DRILLTHROUGH.dmx`。  
  
7.  在工具列上，按一下**Execute**  按鈕。  
  
     該查詢會傳回用來培訓決策樹採礦模型的來源資料。  
  
## <a name="return-the-states-of-a-discrete-mining-model-column"></a>傳回分隔採礦模型資料行的狀態  
 下一步是使用 SELECT DISTINCT 陳述式來傳回指定的採礦模型資料行中不同的可能狀態。  
  
 以下是 SELECT DISTINCT 陳述式的一般範例：  
  
```  
SELECT DISTINCT [<column>]   
FROM [<mining model>]  
```  
  
 程式碼的第一行定義傳回其狀態的採礦模型資料行：  
  
```  
SELECT DISTINCT [<column>]   
```  
  
 您必須包括 DISTINCT 才能傳回資料行的所有狀態。 如果您排除 DISTINCT，則完整陳述式將成為預測的捷徑，並傳回所指定資料行最可能的狀態。 如需詳細資訊，請參閱 [SELECT &#40;DMX&#41;](/sql/dmx/select-dmx)。  
  
#### <a name="to-return-the-states-of-a-discrete-column"></a>若要傳回分隔資料行的狀態  
  
1.  中**物件總管**，以滑鼠右鍵按一下執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向**新查詢**，然後按一下**DMX**。  
  
     此時會開啟 [查詢編輯器] 且包含新的空白查詢。  
  
2.  將 SELECT Distinct 陳述式的一般範例複製到空白查詢中。  
  
3.  取代下列項目：  
  
    ```  
    [<column,name>   
    ```  
  
     成為：  
  
    ```  
    [Bike Buyer]  
    ```  
  
4.  取代下列項目：  
  
    ```  
    [<mining model>]   
    ```  
  
     成為：  
  
    ```  
    [Decision Tree]  
    ```  
  
     現在，完整的陳述式應該如下所示：  
  
    ```  
    SELECT DISTINCT [Bike Buyer]   
    FROM [Decision Tree]  
    ```  
  
5.  在 **檔案**功能表上，按一下**另存 DMXQuery1.dmx 為**。  
  
6.  在 [**另存新檔**] 對話方塊中，瀏覽至適當的資料夾，並將檔案命名`SELECT_DISCRETE.dmx`。  
  
7.  在工具列上，按一下**Execute**  按鈕。  
  
     該查詢會傳回 Bike Buyer 資料行的可能狀態。  
  
 在下一課，您將使用決策樹採礦模型來預測潛在客戶是否會成為自行車買主。  
  
## <a name="next-lesson"></a>下一課  
 [第 5 課：執行預測查詢](../../2014/tutorials/lesson-5-executing-prediction-queries.md)  
  
  
