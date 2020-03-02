---
title: 報表中的運算式用法 (報表產生器) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
helpviewer_keywords:
- expressions [Reporting Services], about expressions
ms.assetid: 76b9ed31-5aec-40fc-bb88-a1c1b0ab3fc3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e781df6f5ccbdbb427de7e8b68c9dbc06522be71
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "77080275"
---
# <a name="expression-uses-in-reports-report-builder-and-ssrs"></a>報表中的運算式用法 (報表產生器及 SSRS)
在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表中，整個報表定義中都會使用運算式來指定或計算參數、查詢、篩選、報表項目屬性、群組和排序定義、文字方塊屬性、書籤、文件引導模式、動態頁首和頁尾內容、影像及動態資料來源定義的值。 本主題提供的範例將說明您可以在許多地方使用運算式來將報表的內容或外觀差異化。 這份清單並不是完整的清單。 您可以在顯示運算式 (**fx**) 按鈕的對話方塊中或在顯示 **\<運算式...>** 的下拉式清單中，為任何屬性設定運算式。  
  
 運算式可能很簡單或很複雜。 *「簡單運算式」* (Simple Expression) 包含單一資料集欄位、參數或內建欄位的參考。 複雜運算式可包含多個內建參考、運算子和函數呼叫。 例如，複雜運算式可能會包含套用至 Sales 欄位的 Sum 函數。  
  
 運算式是以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 撰寫。 運算式的開頭是等號 (=)，後面緊接著內建集合 (如資料集欄位和參數、常數、函數及運算子) 之參考的組合。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Simple"></a> 使用簡單運算式  
 簡單運算式會出現在設計介面和對話方塊的方括號內，例如資料集欄位會以 `[ProductID]`形式出現。 當您從資料集將欄位拖曳到文字方塊上時，系統會自動為您建立簡單運算式。 便會建立預留位置，而且此運算式會定義基礎值。 您也可以將運算式直接輸入資料區資料格或文字方塊中，兩者都位於設計介面或對話方塊中 (例如 `[ProductID]`)。  
  
 下表列出您可以使用簡單運算式之方法的範例。 此表描述其功能、要設定的屬性、您通常用來設定它的對話方塊，以及屬性的值。 您可以在設計介面上、對話方塊中或 [屬性] 窗格內直接輸入簡單運算式，或者可以在 [運算式] 對話方塊中編輯它，就像是任何運算式一樣。  
  
|功能|屬性、內容和對話方塊|屬性值|  
|-------------------|---------------------------------------|--------------------|  
|指定要在文字方塊內顯示的資料集欄位。|文字方塊內的預留位置 Value 屬性。 使用 **[預留位置屬性對話方塊、一般]** 。|`[Sales]`|  
|彙總群組的值。|與 Tablix 群組相關聯的資料列內的預留位置 Value 屬性。 使用 **[文字方塊屬性對話方塊]** 。|`[Sum(Sales)]`|  
|包含頁碼。|放置在頁首之文字方塊內的預留位置 Value 屬性。 使用 **[文字方塊屬性對話方塊、一般]** 。|`[&PageNumber]`|  
|顯示選取的參數值。|設計介面之文字方塊內的預留位置 Value 屬性。 使用 **[文字方塊屬性對話方塊、一般]** 。|`[@SalesThreshold]`|  
|指定資料區的群組定義。|Tablix 群組上的群組運算式。 使用 **[Tablix 群組屬性對話方塊、一般]** 。|`[Category]`|  
|從資料表中排除特定的欄位值。|Tablix 上的篩選方程式。 使用 **[Tablix 屬性對話方塊、篩選]** 。|針對資料類型選取 **[整數]** 。<br /><br /> `[Quantity]`<br /><br /> `>`<br /><br /> `100`|  
|只包含群組篩選的特定值。|Tablix 群組上的篩選方程式。 使用 **[Tablix 群組屬性對話方塊、篩選]** 。|`[Category]`<br /><br /> `=`<br /><br /> `Clothing`|  
|從資料集中排除一個以上欄位的特定值。|Tablix 中群組的篩選方程式。 使用 **[Tablix 屬性對話方塊、篩選]** 。|`=[Color]`<br /><br /> `<>`<br /><br /> `Red`<br /><br /> `=[Color]`<br /><br /> `<>`<br /><br /> `Blue`|  
|根據資料表中的現有欄位指定排序次序。|Tablix 上的排序運算式。 使用 **[Tablix 屬性對話方塊、排序]** 。|`[SizeSortOrder]`|  
|將查詢參數連結到報表參數。|資料集上的參數集合。 使用 **[資料集屬性對話方塊、參數]** 。|`[@Category]`<br /><br /> `[@Category]`|  
|將參數從主報表傳遞到子報表。|子報表上的參數集合。 使用 **[子報表屬性對話方塊、參數]** 。|`[@Category]`<br /><br /> `[@Category]`|  
  
##  <a name="Complex"></a> 使用複雜運算式  
 複雜運算式可包含多個內建參考、運算子和函數呼叫，而且會以 `<<Expr>>`形式出現在設計介面上。 若要查看或變更運算式文字，您必須開啟 **[運算式]** 對話方塊或是直接在 [屬性] 窗格內輸入。 下表列出您可以使用複雜運算式來顯示或組織資料或是變更報表外觀的典型方法，包括所要設定的屬性、通常用來設定它的對話方塊及屬性的值。 您可以在對話方塊中、設計介面上或 [屬性] 窗格內直接輸入運算式。  
  
|功能|屬性、內容和對話方塊|屬性值|  
|-------------------|---------------------------------------|--------------------|  
|計算資料集的彙總值。|文字方塊內的預留位置 Value 屬性。 使用 **[預留位置屬性對話方塊、一般]** 。|`=First(Fields!Sales.Value,"DataSet1")`|  
|串連相同文字方塊內的文字和運算式。|放置在頁首或頁尾之文字方塊內的預留位置值。 使用 **[預留位置屬性對話方塊、一般]** 。|`="This report began processing at " & Globals!ExecutionTime`|  
|計算不同範圍內資料集的彙總值。|放置在 Tablix 群組之文字方塊內的預留位置值。 使用 **[預留位置屬性對話方塊、一般]** 。|`=Max(Fields!Total.Value,"DataSet2")`|  
|根據值格式化文字方塊內的資料。|Tablix 的詳細資料資料列中，文字方塊內的預留位置色彩。 使用 **[文字方塊屬性對話方塊、字型]** 。|`=IIF(Fields!TotalDue.Value < 10000,"Red","Black")`|  
|計算值一次，以便在整個報表中參考。|報表變數的值。 使用 **[報表屬性對話方塊、變數]** 。|`=Variables!MyCalculation.Value`|  
|從資料集中併入一個以上欄位的特定值。|Tablix 中群組的篩選方程式。 使用 **[Tablix 屬性對話方塊、篩選]** 。|選取 **[布林值]** 做為資料類型。<br /><br /> `=IIF(InStr(Fields!Subcat.Value,"Shorts")=0 AND (Fields!Size.Value="M" OR Fields!Size.Value="S"),TRUE, FALSE)`<br /><br /> `=`<br /><br /> `TRUE`|  
|隱藏設計介面上的文字方塊，使用者可以使用名為 *Show*的布林參數進行切換。|文字方塊上的 Hidden 屬性。 使用 **[文字方塊屬性對話方塊、可見性]** 。|`=Not Parameters!` Show\<布林參數>  `.Value`|  
|指定動態頁首或頁尾內容。|放置在頁首或頁尾之文字方塊內的預留位置值。|`="Page " & Globals!PageNumber & " of "  & Globals!TotalPages`|  
|使用參數動態指定資料來源。|資料來源上的連接字串。 使用 **[資料來源屬性對話方塊、一般]** 。|`="Data Source=" & Parameters!ServerName.Value & ";initial catalog=AdventureWorks2012"`|  
|識別使用者選擇之多值參數的所有值。|文字方塊內的預留位置值。 使用 **[Tablix 屬性對話方塊、篩選]** 。|`=Join(Parameters!MyMultivalueParameter.Value,", ")`|  
|在沒有其他群組的 Tablix 內，每 20 個資料列指定分頁符號。|Tablix 內群組的群組運算式。 使用 **[群組屬性對話方塊、分頁符號]** 。 選取 **[在群組的每個執行個體之間]** 選項。|`=Ceiling(RowNumber(Nothing)/20)`|  
|根據參數指定條件式可見性。|Tablix 的 Hidden 屬性。 使用 **[Tablix 屬性對話方塊、可見性]** 。|`=Not Parameters!<` 布林參數  `>.Value`|  
|指定針對特定文化特性格式化的日期。|資料區中文字方塊內的預留位置值。 使用 **[文字方塊屬性對話方塊、一般]** 。|`=Fields!OrderDate.Value.ToString(System.Globalization.CultureInfo.CreateSpecificCulture("de-DE"))`|  
|串連字串及數字 (該數字格式化成兩個小數位數的百分比)。|資料區中文字方塊內的預留位置值。 使用 **[文字方塊屬性對話方塊、一般]** 。|`="Growth Percent: " & Format(Fields!Growth.Value,"p2")`|  
  
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [報表參數 &#40;報表產生器和報表設計師&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [篩選方程式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)   
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [頁首和頁尾 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [格式化文字和預留位置 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [隱藏項目 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/hide-an-item-report-builder-and-ssrs.md)  
  
  
