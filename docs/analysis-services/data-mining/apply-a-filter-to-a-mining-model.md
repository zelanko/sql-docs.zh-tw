---
title: "將篩選套用至採礦模型 |Microsoft 文件"
ms.custom: 
ms.date: 03/19/2017
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
- model filter [data mining]
- filters [data mining]
- filtering input rows [Analysis Services]
- filtering data [Analysis Services]
ms.assetid: 4d0abeb5-e939-46d3-9097-6e0358244300
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b3beab78045a254a30e398928cd262785703df4c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="apply-a-filter-to-a-mining-model"></a>將篩選套用至採礦模型
  如果採礦結構包含巢狀資料表，則篩選可以套用至案例資料表、巢狀資料表或兩者。  
  
 下列程序會示範如何建立兩種篩選：案例篩選及巢狀資料表資料列上的篩選。  
  
 案例資料表的條件將客戶限制為收入在 30000 和 40000 之間。 巢狀資料表的條件則將客戶限制為未購買特定項目的對象。  
  
 在此範例中建立的完整篩選條件如下：  
  
```  
[Income] > '30000'   
AND  [Income] < '40000'   
AND EXISTS (SELECT * FROM [<nested table name>]   
WHERE [Model] <> 'Water Bottle' )   
```  
  
### <a name="to-create-a-case-filter-on-a-mining-model"></a>若要建立採礦模型的案例篩選  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的 [方案總管] 中，按一下包含要篩選的採礦模型的採礦結構。  
  
2.  按一下 **[採礦模型]** 索引標籤。  
  
3.  選擇模型，然後以滑鼠右鍵按一下，開啟快速鍵功能表。  
  
     -或-  
  
     選取此模型。 然後在 [採礦模型] 功能表上，選取 [設定模組篩選器]。  
  
4.  在 [模型篩選器] 對話方塊的 [採礦結構資料行] 文字方塊中，按一下方格中的上方資料列。  
  
5.  如果資料來源包含單一的一般資料表，則下拉式清單僅會顯示該資料表中的資料行名稱。  
  
     如果採礦結構包含多個資料表，則清單會顯示來源資料表的名稱。 在選取資料表之前，不會顯示資料行名稱。  
  
     如果採礦結構包含案例資料表和巢狀資料表，則下拉式清單會顯示案例資料表的資料行以及巢狀資料表的名稱。  
  
6.  從下拉式清單中選取資料行。  
  
     文字方塊左側的圖示會變更，指出選取的項目是資料表或資料行。  
  
7.  按一下 [運算子] 文字方塊，然後從清單選取運算子。 有效運算子會根據所選取資料行的資料類型而變更。  
  
8.  按一下 [值] 文字方塊，然後在方塊中輸入值。  
  
     例如，選取 **Income** 作為資料行，然後選取大於運算子 (>)，再輸入 **30000**。  
  
9. 在方格中，按下一個資料列。  
  
     您所建立的篩選條件會自動加入 [運算式] 文字方塊。 例如，使用 IPv4 位址的 `[Income] > '30000'`  
  
10. 在方格的下一個資料列中，按一下 [AND/OR] 文字方塊以加入條件。  
  
     例如，若要建立 BETWEEN 條件，請從邏輯運算元的下拉式清單選取 [AND]。  
  
11. 選取運算子並輸入值，如步驟 7 和 8 所述。  
  
     例如，再次選取 **Income** 作為資料行，然後選取小於運算子 (<)，再輸入 **40000**。  
  
12. 在方格中，按下一個資料列。  
  
13. 在 [運算式] 文字方塊中的篩選條件會自動更新，以包含新的條件。 完成的運算式如下： `[Income] > '30000'AND [Income] < '40000'`  
  
### <a name="to-add-a-filter-on-the-nested-table-in-a-mining-model"></a>若要在採礦模型中的巢狀資料表加入篩選  
  
1.  在**\<名稱 > 模組篩選器**對話方塊方塊中，按一下空白資料列在底下的方格**採礦結構資料行**。  
  
2.  從下拉式清單選取巢狀資料表的名稱。  
  
     文字方塊左側的圖示會變更，指出選取的項目是資料表的名稱。  
  
3.  按一下 [運算子] 文字方塊，然後選取 [包含] 或 [不包含]。  
  
     這是 [模組篩選器] 對話方塊中，唯一可用於巢狀資料表的條件，因為您將案例資料表限制為僅在巢狀資料表中包含特定值的案例。 下一個步驟將設定巢狀資料表的條件值。  
  
4.  按一下 [值] 方塊，然後按一下 **(…)** 按鈕建置運算式。  
  
     **\<名稱 > 篩選**對話方塊隨即開啟。 這個對話方塊只能在目前的資料表上設定條件，在此例中為巢狀資料表。  
  
5.  按一下 [採礦結構資料列] 方塊，然後從巢狀資料表資料行的下拉式清單選取資料行名稱。  
  
6.  按一下 [運算子]，然後從資料行的有效運算子清單選取運算子。  
  
7.  按一下 [值]，然後輸入值。  
  
     例如，如果是 [採礦結構資料行]，請選取 **Model**。 如果是 [運算子]，則請選取 **<>**，然後輸入 **Water Bottle** 值。 這種情況會建立下列篩選運算式：  
  
```  
EXISTS (SELECT * FROM [<nested table name>] WHERE [Model] <> 'Water Bottle' )   
```  
  
> [!NOTE]  
>  由於巢狀資料表屬性的數目基本上並無限制，所以 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 不會提供可能值的清單以供選取。 您必須輸入確實的值。 此外，您也不能在巢狀資料表中使用 LIKE 運算子。  
  
1.  視需要加入更多條件，在 [條件] 方格左側的 [AND/OR] 方塊中選取 [AND] 或 [OR] 來組合條件。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
2.  在 [模型篩選器] 對話方塊中，檢閱您使用 [篩選器] 對話方塊建立的條件。 巢狀資料表的條件會附加至案例資料表的條件，完整的篩選條件集合會在 [運算式] 文字方塊中顯示。  
  
3.  或者，您可以按一下 [編輯查詢]，手動變更篩選運算式。  
  
    > [!NOTE]  
    >  如果您以手動方式變更篩選運算式的任何部分，則該方格會停用，之後就只能在文字編輯模式中使用篩選運算式。 若要還原方格編輯模式，必須清除篩選運算式並重新開始。  
  
## <a name="see-also"></a>請參閱＜  
 [採礦模型的篩選 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)   
 [採礦模型工作和使用說明](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [從採礦模型中刪除篩選](../../analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)  
  
  
