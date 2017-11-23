---
title: "建立預測查詢使用預測查詢產生器 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- prediction queries [Analysis Services]
- Mining Model Prediction [Analysis Services], prediction queries
ms.assetid: e02836e5-dd8c-4c97-a078-840ae79d3660
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e788f53ac41de8cdecdfbc88f61afacc0bfbad16
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="create-a-prediction-query-using-the-prediction-query-builder"></a>使用預測查詢產生器來建立預測查詢
  您可以建立預測查詢，方法是當您在 BI Development Studio 中建立資料採礦方案時，或是在 SQL Server Management Studio 中以滑鼠右鍵按一下現有的採礦模型，然後選擇 [建立預測查詢] 選項。  
  
 [預測查詢產生器] 有以下三個設計模式，您可以按一下左上角的圖示切換模式。  
  
-   **設計**  
  
-   **查詢**  
  
-   **結果**  
  
 **[設計]** 模式可讓您建立預測查詢，方式是選擇輸入資料、將資料對應到模型，然後將預測函數加入至使用方格所建立的陳述式中。 設計方格包含以下建置組塊：  
  
 **Source**  
 選擇新資料行的來源。 您可以使用採礦模型中的資料行、資料來源檢視中包含的輸入資料表、預測函數或自訂運算式。  
  
 **欄位**  
 決定與 [來源] 資料行中之選取範圍相關聯的特定資料行或函數。  
  
 **別名**  
 決定如何在結果集內命名資料行。  
  
 **顯示**  
 決定 [來源] 資料行中的選取範圍是否顯示在結果中。  
  
 **群組**  
 使用 [及/或] 資料行，以括號將運算式群組在一起。 例如，(expr1 或 expr2) 及 expr3。  
  
 **及/或**  
 在查詢中建立邏輯。 例如，(expr1 或 expr2) 及 expr3。  
  
 **準則/引數**  
 指定適用於資料行的條件或使用者運算式。 您可以將資料行從資料表拖曳至資料格。  
  
 [查詢] 模式提供一個文字編輯器，可讓您直接存取資料採礦延伸模組 (DMX) 語言，連同輸入資料和模型資料行的檢視。 當您選取 **[查詢]** 模式時，基本文字編輯器會取代您用來定義查詢的方格。 您可以使用此編輯器來複製和儲存您所撰寫的查詢，或是從剪貼簿貼入現有 DMX 查詢中，並加以執行。  
  
 **[結果]** 檢視會執行目前的查詢，並將結果顯示在方格中。 如果基礎資料已變更而且您想要重新執行查詢，請按一下狀態上的 [執行] 按鈕。  
  
 您可以使用視覺工具與文字編輯器的組合來設計資料採礦查詢。 如果在文字編輯器中輸入查詢的變更，然後切換回 **[設計]** 檢視，則所有變更都會遺失，且查詢會還原為預測查詢產生器所建立的原始查詢。本主題會逐步引導您使用圖形化查詢產生器。  
  
### <a name="to-create-a-prediction-query"></a>若要建立預測查詢  
  
1.  按一下資料採礦設計師中的 **[採礦模型預測]** 索引標籤。  
  
2.  按一下 **[採礦模型]** 資料表上的 **[選取模型]** 。  
  
     **[選取採礦模型]** 對話方塊就會開啟，以顯示存在於目前專案中的所有採礦結構。  
  
3.  選取您要建立預測的模型，然後按一下 **[確定]**。  
  
4.  在 [選取輸入資料表] 資料表中，按一下 [選取案例資料表]。  
  
     此時會開啟 **[選取資料表]** 對話方塊。  
  
5.  在 **[資料來源]** 清單中，選取包含要建立預測之資料的資料來源。  
  
6.  在 [資料表/檢視表名稱] 方塊中，選取包含要建立預測之資料的資料表，然後按一下 [確定]。  
  
     選好輸入資料表之後，「預測查詢產生器」會根據資料行的名稱，在採礦模型和輸入資料表之間建立預設的對應。 若要刪除對應，請按一下以選取將 [採礦模型] 資料表中的資料行連結到 [選取輸入資料表] 資料表中之對應資料行的線條，然後按下 DELETE 鍵。 您也可以手動建立對應，方式是按一下 [選取輸入資料表] 資料表中的資料行，然後將它拖曳至 [採礦模型] 資料表中的對應資料行。  
  
7.  將下列三種類型資訊的任何結合加入至 [預測查詢產生器] 方格：  
  
    -   **[採礦模型]** 方塊中的可預測資料行。  
  
    -   [選取輸入資料表] 方塊中輸入資料行的任何組合。  
  
    -   預測函數  
  
8.  按一下 **[採礦模型預測]** 索引標籤之工具列上的第一個按鈕，然後選取 **[結果]**來執行查詢。  
  
## <a name="see-also"></a>請參閱＜  
 [在資料採礦設計師中建立單一查詢](../../analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer.md)   
 [資料採礦查詢](../../analysis-services/data-mining/data-mining-queries.md)  
  
  
