---
title: "將篩選套用至模型測試資料 |Microsoft 文件"
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
- input row filtering [SQL Server]
- filtering input rows [Analysis Services]
- Mining Accuracy Chart [Analysis Services], filtering input rows
ms.assetid: 9ccc9a23-5597-4b35-a05f-2fc8eb885147
caps.latest.revision: "44"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 39d35b7421b9d3ddeff5cede6e1539b34b7012c2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="apply-filters-to-model-testing-data"></a>將篩選套用至模型測試資料
  當您指定要用於測試模型的外部資料來源時，可以選擇性地套用篩選，以限制輸入資料。 例如，您可能想要特別針對某個收入範圍的客戶進行預測來測試模型。  
  
 例如，在 Adventure Works 目標郵寄案例中，您可以對 ProspectiveBuyer (這是包含測試資料的資料表) 建立一個如下的篩選運算式，依收入範圍來限制測試案例：  
  
 `[YearlyIncome] = '50000'`  
  
 根據篩選的是模型定型資料還是測試資料集，篩選行為稍微不同：  
  
-   在測試資料集上定義篩選時，您要在內送資料上建立 WHERE 子句。 如果要篩選用於評估模型的輸入資料集，則篩選運算式會轉譯為 Transact-SQL 陳述式，並在建立圖表時套用至輸入資料表。 因此，測試案例數會大幅減少。  
  
-   將篩選套用至採礦模型時，您建立的篩選運算式會轉譯為「資料採礦延伸模組」(DMX) 陳述式，並套用至個別模型。 因此，將篩選套用至模型時，只會使用原始資料的子集來定型模型。 如果您使用一組準則來篩選定型模型，讓模型調整為某一組資料，然後使用另一組準則對模型進行測試，這可能會導致問題。  
  
-   如果在建立結構時定義了測試資料集，則用於定型的模型案例僅會包含採礦結構定型集中的案例**以及**符合篩選條件的案例。 因此，當您測試模型並選取 [使用採礦模型測試案例] 選項時，測試案例僅會包含採礦結構測試集中的案例以及符合篩選條件的案例。 不過，如果您未定義鑑效組資料集，則用於測試的模型案例會包含資料集中符合篩選條件的所有案例。  
  
-   模型上套用的篩選條件也會影響模型案例的鑽研查詢。  
  
 總之，在您測試多個模型時，即使所有模型都是根據相同的採礦結構，您也必須意識到模型可能會使用不同的資料子集來進行定型和測試。 這可能對精確度圖表具有下列影響：  
  
-   測試集中案例的總數在多個測試的模型中可能會不同。  
  
-   如果模型使用不同的定型資料或測試資料的子集，則每個模型的百分比在圖表中可能不會對齊。  
  
 若要判斷模型是否包含可能會影響結果的預先定義篩選，您可以在 [屬性] 窗格中尋找 [篩選] 屬性，或透過使用資料採礦結構描述資料列集來查詢模型。 例如，下列查詢會傳回指定之模型的篩選文字：  
  
 `SELECT [FILTER] FROM $system.DMSCHEMA_MINING_MODELS WHERE MODEL_NAME = 'name of model’`  
  
> [!WARNING]  
>  如果您要從現有的採礦模型中移除篩選，或者變更篩選條件，則必須重新處理採礦模型。  
  
 如需可套用的篩選類型以及如何評估篩選運算式的詳細資訊，請參閱[模型篩選語法和範例 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)。  
  
### <a name="create-a-filter-on-external-testing-data"></a>針對外部測試資料建立篩選  
  
1.  按兩下包含要測試模型的採礦結構，以開啟資料採礦設計師。  
  
2.  選取 **[採礦精確度圖表]** 索引標籤，然後選取 **[輸入選擇]** 索引標籤。  
  
3.  在 [輸入選擇] 索引標籤的 [選取要用於精確度圖表的資料集] 下，選取 [指定不同的資料集] 選項。  
  
4.  按一下瀏覽按鈕 **(...)** 開啟對話方塊，並選擇外部資料集。  
  
5.  選擇案例資料表，並視需要新增巢狀資料表。 視需要將模型中的資料行對應至外部資料集中的資料行。 關閉 [指定資料行對應] 對話方塊，以儲存來源資料表定義。  
  
6.  按一下 [開啟篩選編輯器] 定義資料集的篩選。  
  
     [資料集篩選器] 對話方塊隨即開啟。 如果結構包含巢狀資料表，您就可以分成兩個部分來建立篩選。 首先，請使用 [資料集篩選器] 對話方塊來設定案例資料表的條件，然後使用 [篩選] 對話方塊來設定巢狀資料列的條件。  
  
7.  在 [資料集篩選器] 對話方塊中，按一下方格中最上方的資料列 ([採礦結構資料行] 底下)，然後從清單中選取資料表或資料行。  
  
     如果資料來源檢視包含多份資料表或一份巢狀資料表，您就必須先選取資料表名稱。 否則，您可以直接從案例資料表中選取資料行。  
  
     針對您想要篩選的每個資料行，加入新的資料列。  
  
8.  您可以使用 [運算子] 和 [值] 資料行來定義資料行的篩選方式。  
  
     **注意**：當您輸入值時，請勿使用引號。  
  
9. 按一下 [及/或] 文字方塊並選取邏輯運算子來定義多項條件的組合方式。  
  
10. (選擇性) 按一下位於 [值] 文字方塊右側的瀏覽按鈕 **(…)**來開啟 [篩選] 對話方塊，並針對巢狀資料表或個別的案例資料表資料行設定條件。  
  
11. 檢視 [運算式] 窗格中的文字，藉以確認完成的篩選條件是否正確。  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     當您建立精確度圖表時，此篩選條件會套用至資料來源。  
  
## <a name="see-also"></a>請參閱＜  
 [選擇和對應模型測試資料](../../analysis-services/data-mining/choose-and-map-model-testing-data.md)   
 [使用巢狀資料表做為輸入用於精確度圖表](../../analysis-services/data-mining/using-nested-table-data-as-an-input-for-an-accuracy-chart.md)   
 [選擇精確度圖表類型及設定圖表選項](../../analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md)  
  
  
