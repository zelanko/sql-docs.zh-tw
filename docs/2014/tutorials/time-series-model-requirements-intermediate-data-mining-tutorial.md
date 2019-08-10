---
title: 瞭解時間序列模型的需求 (元資料採礦教學課程) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1ce2b3e3-108a-4f7e-985f-a20b816d0da7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8e46d7fc8a0c214501841de448a94d1211b95fa1
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892967"
---
# <a name="understanding-the-requirements-for-a-time-series-model-intermediate-data-mining-tutorial"></a>了解時間序列模型的需求 (中繼資料採礦教學課程)
  當您準備要用於預測模型的資料時，必須確認該資料包含可用於識別時間序列步驟的資料行。 該資料行將指定為 `Key Time` 資料行。 此資料行是索引鍵，因此必須包含唯一的數值。  
  
 選擇 `Key Time` 資料行的正確單位是分析中重要的一環。 例如，假設銷售資料每分鐘重新整理一次。 您不一定要將分鐘當做時間序列單位使用；您可能會發現，依日、週或甚至月來積存銷售資料可能更有意義。 如果您不確定要使用哪個時間單位，可以為每個彙總建立一個新的資料來源檢視，並建立相關的模型，看看是否在每個彙總層級出現不同的趨勢。  
  
 在本教學課程中，每天於交易式銷售資料庫中收集銷售資料，但對於資料採礦，則使用檢視，依月預先彙總資料。  
  
 此外，對於分析，資料的間距愈少愈好。 如果您計劃分析多個資料數列，所有數列的開始和結束時間最好應該在同一天。 如果資料有間距，但間距不在數列開頭或結尾處，您可以使用 MISSING_VALUE_SUBSTITUTION 參數來填滿數列。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 也提供數個選項，讓您以值 (例如平均值或常數) 取代遺漏資料。  
  
> [!WARNING]  
>  我們不再提供舊版資料來源檢視設計工具隨附的樞紐分析圖和樞紐分析表工具。 建議您使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 隨附的資料分析工具等工具，事先識別時間序列資料的間距。  
  
### <a name="to-identify-the-time-key-for-the-forecasting-model"></a>識別預測模型的時間索引鍵  
  
1.  在窗格中, **salesbyregion.dsv [Design]** , 以滑鼠右鍵按一下資料表 vTimeSeries, 然後選取 [**流覽資料**]。  
  
     新索引標籤隨即開啟, 標題為 [**流覽 VTimeSeries 資料表**]。  
  
2.  在 [**資料表**] 索引標籤上, 檢查 [TimeIndex] 和 [報告日期] 資料行中所使用的資料。  
  
     這兩個資料行都是具有唯一值的序列，都可以做為時間序列索引鍵；不過，資料行的資料類型不同。 Microsoft 時間序列演算法不要求使用 `datetime` 資料類型，只要求使用的值必須相異且經過排序。 因此，您可以使用任何一個資料行做為預測模型的時間索引鍵。  
  
3.  在 [資料來源] 視圖設計介面中, 選取 [報表日期] 資料行, 然後選取 [**屬性**]。 接下來, 按一下 [TimeIndex] 資料行, 然後選取 [**屬性**]。  
  
     欄位 TimeIndex 的資料類型為 System.object, 而欄位報告日期的資料類型為 system.string。 許多資料倉儲都會將日期/時間值轉換為整數，並將整數資料行做為索引鍵，以改進索引效能。 不過，如果您使用此資料行，Microsoft 時間序列演算法會使用未來值 (例如 201014、201014 等) 做預測。 因為您想要使用行事曆日期來表示銷售資料預測, 所以您將使用 [報表日期] 資料行做為唯一的數列識別碼。  
  
### <a name="to-set-the-key-in-the-data-source-view"></a>若要設定資料來源檢視中的索引鍵  
  
1.  在 [ **salesbyregion.dsv**] 窗格中, 選取 [vTimeSeries] 資料表。  
  
2.  以滑鼠右鍵按一下資料行 [報表日期], 然後選取 [**設定邏輯主鍵**]。  
  
## <a name="handling-missing-data-optional"></a>處理遺漏資料 (選擇性)  
 如果有任何序列遺漏資料，當您嘗試處理模型時，可能會收到錯誤訊息。 解決遺漏資料的方法有好幾種：  
  
-   您可以讓 Analysis Services 計算平均值或使用上一個值，藉此填滿遺漏值。 方法是，在採礦模型上設定 MISSING_VALUE_SUBSTITUTION 參數。 如需此參數的詳細資訊, 請參閱[Microsoft 時間序列演算法技術參考](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)。 如需如何變更現有的採礦模型參數的詳細資訊, 請參閱[View Or Change 演算法 parameters](../../2014/analysis-services/data-mining/view-or-change-algorithm-parameters.md)。  
  
-   您可以改變資料來源或是篩選基礎檢視，以便刪除不完全的數列或取代值。 您可以在關聯式資料來源中進行此動作，或是建立自訂具名查詢或具名計算以修改資料來源檢視。 如需詳細資訊，請參閱 [多維度模型中的資料來源檢視](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models)。 此課程稍後的一項工作提供了如何建立具名查詢與自訂計算的範例。  
  
 在這個案例中，有一個數列開頭處缺少某些資料：亦即，直到 2007 年 7 月才有 T1000 產品線的資料。 除此之外，所有數列都是在同一天結束，沒有遺漏值。  
  
 Microsoft 時間序列演算法的需求是您包含在單一模型中的任何數列都應該具有相同的**結束**點。 由於 T1000 自行車模型從 2007 年引進，這個序列的資料比其他自行車模型開始時間晚，但是結束日期相同，因此這個序列的資料可以使用。  
  
#### <a name="to-close-the-data-source-view-designer"></a>關閉資料來源檢視設計師  
  
-   以滑鼠右鍵按一下 [**流覽 VTimeSeries 資料表**] 索引標籤, 然後選取 [**關閉**]。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [建立預測結構和模型&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 時間序列演算法](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
