---
title: "參數集合參考 （報表產生器及 SSRS） |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c4b47e15-0484-4c13-9182-898db825f01f
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 17698a3c268e824d2f638042b71b3ec21f994e86
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="built-in-collections---parameters-collection-references-report-builder"></a>內建集合的參數集合參考 （報表產生器）
  報表參數是您可以從運算式參考的其中一個內建集合。 您可以在運算式中包含參數，以根據使用者所做的選擇來自訂報表資料及外觀。 運算式可以用於任何報表項目屬性或文字方塊屬性提供 (*Fx*) 或\<**運算式**> 選項。 您也可以用其他方法來使用運算式控制報表的內容及外觀。 如需詳細資訊，請參閱[組運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)。  
  
 在執行階段比較參數值與資料集欄位值時，所比較的兩個項目的資料類型必須相同。 報表參數可以是以下其中一個類型：布林、日期時間、整數、浮點數或文字 (代表基礎資料類型「字串」)。 如有必要，也可以將參數值的資料類型轉換成符合資料集值。 如需詳細資訊，請參閱[運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)。  
  
 若要在運算式中包含參數參考，您必須了解如何指定參數參考的正確語法，此語法會根據參數是單一值或多重值參數而改變。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Single"></a> 在運算式中使用單一值參數  
 下表顯示當您在運算式中加入任何資料類型之單一值參數的參考時，所要使用的語法範例。  
  
|範例|Description|  
|-------------|-----------------|  
|`=Parameters!`*\<參數名稱 >*`.IsMultiValue`|傳回 **False**。<br /><br /> 檢查參數是否為多重值。 如果為 **True**，表示參數為多值，且為物件的集合。 如果為 **False**，表示參數為單一值，且為單一物件。|  
|`=Parameters!`*\<參數名稱 >*`.Count`|傳回整數值 1。 如果是單一值參數，此計數一定會是 1。|  
|`=Parameters!`*\<參數名稱 >*`.Label`|會傳回參數標籤，經常當做可用值下拉式清單中的顯示名稱。|  
|`=Parameters!`*\<參數名稱 >*`.Value`|會傳回參數值。 如果尚未設定 Label 屬性，這個值會出現在可用值下拉式清單中。|  
|`=CStr(Parameters!`  *\<參數名稱 >*`.Value)`|會傳回字串形式的參數值。|  
|`=Fields(Parameters!`*\<參數名稱 >*`.Value).Value`|會傳回與參數同名之欄位的值。|  
  
 如需在篩選中使用參數的詳細資訊，請參閱[新增資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)。  
  
##  <a name="Multi"></a> 在運算式中使用多重值參數  
 下表顯示當您在運算式中加入任何資料類型之多重值參數的參考時，所要使用的語法範例。  
  
|範例|Description|  
|-------------|-----------------|  
|`=Parameters!` *\<MultivalueParameterName >*`.IsMultiValue`|傳回 **True** 或 **False**。<br /><br /> 檢查參數是否為多重值。 如果為 **True**，表示參數為多值，且為物件的集合。 如果為 **False**，表示參數為單一值，且為單一物件。|  
|`=Parameters!` *\<MultivalueParameterName >*`.Count`|傳回整數值。<br /><br /> 參考值的數目。 如果是單一值參數，此計數一定會是 1。 如果是多重值參數，此計數是 0 或以上。|  
|`=Parameters!` *\<MultivalueParameterName >*`.Value(0)`|傳回多重值參數中的第一個值。|  
|`=Parameters!` *\<MultivalueParameterName >* `.Value(Parameters!` * \<MultivalueParameterName >*`.Count-1)`|傳回多重值參數中的最後一個值。|  
|`=Split("Value1,Value2,Value3",",")`|傳回數值的陣列。<br /><br /> 針對多值的 **String** 參數建立數值陣列。 您可以在第二個參數中使用任何分隔符號來分隔。 這個運算式可用來設定多重值參數的預設值或是建立多重值參數，以傳送至子報表或鑽研報表。|  
|`=Join(Parameters!` *\<MultivalueParameterName >*`.Value,", ")`|傳回 **String** ，此值是由多值參數中以逗號分隔的值清單所組成。 您可以在第二個參數中使用任何分隔符號來聯結。|  
  
 如需在篩選中使用參數的詳細資訊，請參閱[報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)。  
  
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [常用的篩選 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/commonly-used-filters-report-builder-and-ssrs.md)   
 [加入、變更或刪除報表參數 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [教學課程：將參數加入至報表 &#40;報表產生器&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [報表產生器教學課程](../../reporting-services/report-builder-tutorials.md)   
 [運算式中的內建集合 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)  
  
  
