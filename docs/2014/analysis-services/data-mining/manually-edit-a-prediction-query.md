---
title: 手動編輯預測查詢 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- modifying prediction queries
- Mining Model Prediction [Analysis Services], modifying prediction queries
- manual prediction query modification [Analysis Services]
ms.assetid: 9f6a9298-49d5-4675-ad49-977a47dff5a6
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8809e025a60a47acb2db5dae312702ee2e3effd3
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84522067"
---
# <a name="manually-edit-a-prediction-query"></a>手動編輯預測查詢
  在使用預測查詢產生器設計查詢之後，您可以切換到資料採礦設計師的 [採礦模型預測]**** 索引標籤上的 [查詢文字] 檢視來修改查詢。 文字編輯器會出現在畫面底端，以顯示查詢產生器建立的查詢。  
  
 切換到 [查詢文字] 檢視對於在查詢中添加內容很實用。 例如，您可以加入 WHERE 子句或 ORDER BY 子句。  
  
 使用預測查詢產生器中的方格來插入物件和資料行的名稱，並為個別預測函數設定語法，然後切換到手動編輯模式來變更參數值。  
  
> [!NOTE]  
>  如果您從 [查詢文字]**** 檢視切回到 [設計]**** 檢視，則會失去您在 [查詢文字]**** 檢視中所做的任何變更。  
  
### <a name="modify-a-query"></a>修改查詢  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，於資料採礦設計師的 [採礦模型預測]**** 索引標籤上，按一下 [SQL]****。  
  
     畫面底端的方格會由包含查詢的文字編輯器所取代。 您可以在此編輯器中輸入對查詢的變更。  
  
2.  若要執行查詢，請在 [採礦模型]**** 功能表上選取 [結果]****，或按一下按鈕切換到查詢結果。  
  
    > [!NOTE]  
    >  如果您建立的查詢無效，則 [結果] 視窗不會顯示錯誤，也不會顯示任何結果。 按一下 [設計]**** 按鈕或從 [採礦模型]**** 功能表選取 [設計]**** 或 [查詢]**** 以修正問題，並再次執行查詢。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦查詢](data-mining-queries.md)   
 [預測查詢產生器 &#40;資料採礦&#41;](../prediction-query-builder-data-mining.md)   
 [第 6 課：建立及處理預測 &#40;基本資料採礦教學課程&#41;](../../tutorials/lesson-6-creating-and-working-with-predictions-basic-data-mining-tutorial.md)  
  
  
