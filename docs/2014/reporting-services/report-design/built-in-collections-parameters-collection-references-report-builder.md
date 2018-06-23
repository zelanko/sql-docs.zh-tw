---
title: 參數集合參考 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c4b47e15-0484-4c13-9182-898db825f01f
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: a036b16073f19c106b507653921185fcb8df0bbd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145780"
---
# <a name="parameters-collection-references-report-builder-and-ssrs"></a>參數集合參考 (報表產生器及 SSRS)
  報表參數是您可以從運算式參考的其中一個內建集合。 您可以在運算式中包含參數，以根據使用者所做的選擇來自訂報表資料及外觀。 可以針對提供 (*Fx*) 或 \<**運算式**> 選項的任何報表項目屬性或文字方塊屬性使用運算式。 您也可以用其他方法來使用運算式控制報表的內容及外觀。 如需詳細資訊，請參閱[運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)。  
  
 在執行階段比較參數值與資料集欄位值時，所比較的兩個項目的資料類型必須相同。 報表參數可以是以下其中一個類型：布林、日期時間、整數、浮點數或文字 (代表基礎資料類型「字串」)。 如有必要，也可以將參數值的資料類型轉換成符合資料集值。 如需詳細資訊，請參閱[Data Types in Expressions&#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)。  
  
 若要在運算式中包含參數參考，您必須了解如何指定參數參考的正確語法，此語法會根據參數是單一值或多重值參數而改變。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Single"></a> 在運算式中使用單一值參數  
 下表顯示當您在運算式中加入任何資料類型之單一值參數的參考時，所要使用的語法範例。  
  
|範例|描述|  
|-------------|-----------------|  
|`=Parameters!` \<參數名稱> `.IsMultiValue`|傳回`False`。<br /><br /> 檢查參數是否為多重值。 如果`True`參數為多重值，它是物件的集合。 如果為 `False`，表示參數為單一值，且為單一物件。|  
|`=Parameters!` \<參數名稱> `.Count`|傳回整數值 1。 如果是單一值參數，此計數一定會是 1。|  
|`=Parameters!` \<參數名稱> `.Label`|會傳回參數標籤，經常當做可用值下拉式清單中的顯示名稱。|  
|`=Parameters!` \<參數名稱> `.Value`|會傳回參數值。 如果尚未設定 Label 屬性，這個值會出現在可用值下拉式清單中。|  
|`=CStr(Parameters!` \<參數名稱> `.Value)`|會傳回字串形式的參數值。|  
|`=Fields(Parameters!` \<參數名稱> `.Value).Value`|會傳回與參數同名之欄位的值。|  
  
 如需在篩選中使用參數的詳細資訊，請參閱[新增資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)。  
  
##  <a name="Multi"></a> 在運算式中使用多重值參數  
 下表顯示當您在運算式中加入任何資料類型之多重值參數的參考時，所要使用的語法範例。  
  
|範例|描述|  
|-------------|-----------------|  
|`=Parameters!` \<多值參數名稱> `.IsMultiValue`|傳回 `True` 或 `False`。<br /><br /> 檢查參數是否為多重值。 如果為 `True`，表示參數為多重值，且為物件的集合。 如果為 `False`，表示參數為單一值，且為單一物件。|  
|`=Parameters!` \<多值參數名稱> `.Count`|傳回整數值。<br /><br /> 參考值的數目。 如果是單一值參數，此計數一定會是 1。 如果是多重值參數，此計數是 0 或以上。|  
|`=Parameters!` \<多值參數名稱> `.Value(0)`|傳回多重值參數中的第一個值。|  
|`=Parameters!` \<多值參數名稱> `.Value(Parameters!` \<多值參數名稱> `.Count-1)`|傳回多重值參數中的最後一個值。|  
|`=Split("Value1,Value2,Value3",",")`|傳回數值的陣列。<br /><br /> 針對多重值的 `String` 參數建立數值陣列。 您可以在第二個參數中使用任何分隔符號來分隔。 這個運算式可用來設定多重值參數的預設值或是建立多重值參數，以傳送至子報表或鑽研報表。|  
|`=Join(Parameters!` \<多值參數名稱> `.Value,", ")`|傳回`String`，包含以逗號分隔清單中多重值參數的值。 您可以在第二個參數中使用任何分隔符號來聯結。|  
  
 如需在篩選中使用參數的詳細資訊，請參閱[報表參數 &#40;報表產生器和報表設計師&#41;](report-parameters-report-builder-and-report-designer.md)。  
  
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [常用的篩選 &#40;報表產生器及 SSRS&#41;](commonly-used-filters-report-builder-and-ssrs.md)   
 [加入、 變更或刪除報表參數&#40;報表產生器和 SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [教學課程：將參數新增至報表 &#40;報表產生器&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [教學課程&#40;報表產生器&#41;](../report-builder-tutorials.md)   
 [Built-in Collections in Expressions&#40;報表產生器和 SSRS&#41;](built-in-collections-in-expressions-report-builder.md)  
  
  