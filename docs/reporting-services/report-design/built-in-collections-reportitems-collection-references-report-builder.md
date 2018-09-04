---
title: ReportItems 集合參考 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: edc0c75f-0530-4e6d-85aa-3385301bfd00
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6dd790d1e739933df2246764cf7d337ea3d2574a
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43280571"
---
# <a name="built-in-collections---reportitems-collection-references-report-builder"></a>內建集合 - ReportItems 集合參考 (報表產生器)
  **ReportItems** 內建集合是報表項目的文字方塊集合，例如，報表設計介面上的資料區或文字方塊列。 **ReportItems** 集合包含在頁首、頁尾或報表主體目前範圍中的文字方塊。 這個集合是在執行階段由報表處理器和報表轉譯器而決定。 隨著報表處理器連續地將報表資料和報表項目配置元素結合為報表的使用者檢視頁面，目前的範圍也會變更。 您可以使用 **ReportItems** 內建集合來產生字典樣式的頁首，以在每個頁面上顯示第一個及最後一個項目。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-the-reportitems-value-property"></a>使用 ReportItems 值屬性  
 **ReportItems** 集合內的項目只有一個屬性：Value。 **ReportItems** 項目的值可用來顯示或計算報表中其他欄位的資料。 若要存取目前文字方塊的值，您可以使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 內建全域 Me.Value，或是只使用 Value。 在報表函數 (例如，First 和彙總函式) 中，請使用完整的語法。  
  
 例如：  
  
-   這個置於文字方塊中的運算式會顯示名為 **之** ReportItem `Textbox1`文字方塊的值：  
  
     `=ReportItems!Textbox1.Value`  
  
-   這個放在 **ReportItem** 文字方塊 Color 屬性中的運算式，會在值 > 0 時以黑色顯示文字，否則會以紅色文字顯示值：  
  
     `=IIF(Me.Value > 0,"Black","Red")`  
  
-   這個放在頁首或頁尾之文字方塊中的運算式，會為名為 `LastName`的文字方塊顯示已轉譯報表之每一頁的第一個值：  
  
     `=First(ReportItems("LastName").Value)`  
  
## <a name="dictionary-style-page-header-expressions"></a>字典樣式頁首運算式  
 您可以建立頁首來顯示頁面上的第一個客戶，以及頁面上的最後一個客戶。 因為頁首中的文字方塊在運算式中只能參考 **ReportItems** 內建集合一次，所以您需要將兩個文字方塊加入到頁首：一個是第一個客戶的名稱 (`=First(ReportItems!textboxLastName.Value`)，另一個則是最後一個客戶的名稱 (`=Last(ReportItems!textboxLastName.Value`)。  
  
 在頁首或頁尾區段中，只有目前頁面上的文字方塊才能作為 **ReportItems** 集合的成員。 例如，如果 `ReportItems!textboxLastName.Value` 參考的文字方塊只會顯示在多頁面資料區域的第一個頁面上，則您會看到第一頁的值，但所有其他的頁面都會顯示 **#Error** ，表示運算式無法評估為已寫入。  
  
## <a name="scope-for-the-reportitems-collection"></a>ReportItems 集合的範圍  
 在系統處理報表時，每個報表主體或資料區域中的文字方塊都會在其資料集、資料區域和群組關聯的內容中進行評估。 **ReportItems** 集合參考的範圍是目前的範圍或高於目前範圍的任何點。  
  
 例如，在父群組的資料列內的文字方塊所包含的運算式，不得參考子群組資料列中的文字方塊的名稱。 此類運算式不會解析為報表中的值，因為子資料列文字方塊超出範圍。 如需詳細資訊，請參閱 [彙總函式參考 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)。  
  
## <a name="see-also"></a>另請參閱  
 [運算式中的內建集合 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Reporting Services 中的分頁 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
