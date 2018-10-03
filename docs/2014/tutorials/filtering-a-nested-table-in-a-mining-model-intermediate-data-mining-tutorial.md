---
title: 篩選巢狀的資料表中的採礦模型 （中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 0a3ae0e5-897b-4898-a60d-5455eec3d305
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2dcb1e84335100eda4155fa1f0a8a1cc9c65206e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48159972"
---
# <a name="filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial"></a>在採礦模型中篩選巢狀資料表 (中繼資料採礦教學課程)
  建立並探索模型之後，您決定要將焦點放在客戶資料子集上。 例如，您可能只要分析包含特定項目的購物籃，或是分析在特定期間未購買任何產品的客戶人口統計。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供了篩選採礦模型資料的功能。 此功能非常有用，因為您不需要設定新的資料來源檢視，以使用不同的資料。 在基本資料採礦教學課程中，您學會了如何對案例資料表套用條件，以篩選來自二維資料表的資料。 在這項工作中，您將建立套用至巢狀資料表的篩選。  
  
## <a name="filters-on-nested-vs-case-tables"></a>巢狀和案例資料表的篩選  
 如果您的資料來源檢視如同用於關聯模型的資料來源檢視，同樣包含一個案例資料表和一個巢狀資料表，您可以篩選來自案例資料表的值、巢狀資料表中存在或不存在的值，或是兩者的一些組合。  
  
 在這項工作中，您要先建立一份關聯模型副本，然後將 IncomeGroup 和 Region 屬性加入新的相關模型中，以便在案例資料表中篩選這些屬性。  
  
#### <a name="to-create-and-modify-a-copy-of-the-association-model"></a>建立並修改關聯模型副本  
  
1.  在 **採礦模型**索引標籤[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，以滑鼠右鍵按一下`Association`模型，然後選取**新的採礦模型**。  
  
2.  針對**模型名稱**，輸入`Association Filtered`。 針對**演算法名稱**，選取**Microsoft 關聯規則**。 按一下 [確定] 。  
  
3.  中的資料行篩選的關聯模型中，按一下 IncomeGroup 資料列，並將值從變更**略過**要**輸入**。  
  
 接下來，您將在新的關聯模型中的案例資料表上建立篩選。 篩選只會將目標區域的客戶或是具有目標收入等級的客戶傳往模型。 然後，您要加入第二組篩選條件，指定模型只使用購物籃至少包含一個項目的客戶。  
  
#### <a name="to-add-a-filter-to-a-mining-model"></a>將篩選加入採礦模型  
  
1.  在  **Mining Models**索引標籤，以滑鼠右鍵按一下 模型篩選的關聯，然後選取**設定模型篩選器**。  
  
2.  在 [模型篩選器] 對話方塊的 [採礦結構資料行] 文字方塊中，按一下方格中的上方資料列。  
  
3.  在 **採礦結構資料行** 文字方塊中，選取 IncomeGroup。  
  
     文字方塊左側的圖示會變更，指出選取的項目是資料行。  
  
4.  按一下 **運算子**文字方塊中，然後選取**=** 從清單中的運算子。  
  
5.  按一下 **值**文字方塊中，然後輸入`High`在方塊中。  
  
6.  在方格中，按下一個資料列。  
  
7.  按一下 **及/或**的方格，然後選取 下一步 列中的文字方塊**或**。  
  
8.  在 **採礦結構資料行** 文字方塊中，選取 IncomeGroup。 在 **值**文字方塊中，輸入`Moderate`。  
  
     您所建立的篩選條件會自動加入至**運算式** 文字方塊中，並應該看起來像這樣：  
  
     `[IncomeGroup] = 'High' OR [IncomeGroup] = 'Moderate'`  
  
9. 按一下 [下一步] 的資料列，在方格中，保留預設值，運算子**AND**。  
  
10. 針對**運算子**，保留預設值， **Contains**。 按一下 **值**文字方塊。  
  
11. 在 **篩選**對話方塊中，在底下的第一個資料列中**採礦結構資料行**，選取`Model`。  
  
12. 針對**運算子**，選取**IS NOT NULL**。 離開**值**空白的文字方塊。 按一下 [確定] 。  
  
     中的篩選條件**運算式**的文字方塊**模型篩選器**對話方塊會自動更新以包含巢狀資料表上新的條件。 完成的運算式如下：  
  
     `[IncomeGroup] = 'High' OR [IncomeGroup] = 'Moderate' AND EXISTS SELECT * FROM [vAssocSeqLineItems] WHERE [Model] <> NULL).`  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)] ``  
  
#### <a name="to-enable-drillthrough-and-to-process-the-filtered-model"></a>啟用鑽研並處理篩選模型  
  
1.  在  **Mining Models**索引標籤上，以滑鼠右鍵按一下`Association Filtered`模型，然後選取**屬性**。  
  
2.  變更**AllowDrillThrough**屬性設 **，則為 True**。  
  
3.  以滑鼠右鍵按一下`Association Filtered`採礦模型，然後選取**處理序模型**。  
  
4.  按一下  **[是]** 錯誤訊息，若要部署新的模型中[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]資料庫。  
  
5.  在 [**處理採礦結構**] 對話方塊中，按一下**執行**。  
  
6.  當處理完成時按一下**關閉**結束**處理進度** 對話方塊中，然後按一下 **關閉**以結束**處理採礦結構**  對話方塊。  
  
 您可以使用 Microsoft 一般內容樹狀檢視器進行確認，並且針對所包含案例少於原始模型的篩選模型，查看 NODE_SUPPORT 的值。  
  
## <a name="remarks"></a>備註  
 您剛建立的巢狀資料表篩選器只會檢查巢狀資料表中至少一個資料列的存在。不過，您也可以建立篩選條件，檢查特定產品的存在。  例如，您可以建立下列篩選：  
  
```  
[IncomeGroup] = 'High' AND  
 EXISTS (SELECT * FROM [<nested table name>] WHERE [Model] = 'Water Bottle' )   
```  
  
 這個陳述式代表您要將案例資料表上的客戶限制在已購買水壺 (Water Bottle) 的客戶。 不過，由於巢狀資料表屬性的數目基本上並無限制，所以 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不會提供可能值的清單以供選取。 因此，您必須輸入確實的值。  
  
 您可以按一下**編輯查詢**，手動變更篩選運算式。 不過，如果以手動方式變更了篩選運算式的任何部分，則該方格會停用，之後就只能在文字編輯模式中使用篩選運算式。 若要還原方格編輯模式，必須清除篩選運算式並重新開始。  
  
> [!WARNING]  
>  您無法在巢狀資料表篩選中使用 LIKE 運算子。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [預測關聯&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/predicting-associations-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [模型篩選語法和範例&#40;Analysis Services-資料採礦&#41;](../../2014/analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)   
 [採礦模型的篩選&#40;Analysis Services-資料採礦&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  
