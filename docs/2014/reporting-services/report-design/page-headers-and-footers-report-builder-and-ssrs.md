---
title: 頁首和頁尾 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.pagefooter.fill.f1
- "10125"
- "10121"
- "10120"
- "10122"
- "10123"
- sql12.rtp.rptdesigner.pageheader.border.f1
- sql12.rtp.rptdesigner.pageheader.general.f1
- sql12.rtp.rptdesigner.pagefooter.border.f1
- sql12.rtp.rptdesigner.pageheader.fill.f1
- sql12.rtp.rptdesigner.pagefooter.general.f1
- "10124"
ms.assetid: 4fb9faac-511e-404a-b8d7-1f2e3cb47b11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7b746f27653f5e8d1c24a584ac19c8fbac05a57c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105525"
---
# <a name="page-headers-and-footers-report-builder-and-ssrs"></a>頁首和頁尾 (報表產生器及 SSRS)
  報表可以包含分別在每個頁面的頂端和底端邊緣處的頁首和頁尾。 頁首和頁尾可以包含靜態文字、影像、線條、矩形、框線、背景色彩、背景影像和運算式。 運算式包含剛好具有一個資料集之報表的資料集欄位參考，以及包含該資料集做為範圍的彙總函式呼叫。  
  
> [!NOTE]  
>  每個轉譯延伸模組處理頁面的方式不同。 如需報表分頁和轉譯延伸模組的詳細資訊，請參閱 [Reporting Services 中的分頁 &#40;報表產生器及 SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md)。  
  
 根據預設，報表具有頁尾，但沒有頁首。 如需如何將其新增或移除的詳細資訊，請參閱[新增或移除頁首或頁尾 &#40;報表產生器及 SSRS&#41;](add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md)。  
  
 頁首和頁尾通常包含頁碼、報表標題和其他報表屬性。 如需如何將這些項目新增至報表頁首或頁尾的詳細資訊，請參閱[顯示頁碼或其他報表屬性 &#40;報表產生器及 SSRS&#41;](display-page-numbers-or-other-report-properties-report-builder-and-ssrs.md)。  
  
 頁首或頁尾在建立之後，就會顯示在每個報表頁面上。 如需如何在第一頁和最後一頁上隱藏頁首和頁尾的詳細資訊，請參閱[隱藏第一頁或最後一頁的頁首或頁尾 &#40;報表產生器及 SSRS&#41;](hide-a-page-header-or-footer-on-the-first-or-last-page-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-headers-and-footers"></a>報表頁首和頁尾  
 頁首和頁尾與報表首及報表尾並不相同。 報表並不具有特殊的報表首或報表尾區域。 報表首是由報表設計介面上放置於報表主體頂端的報表項目所組成。 這些項目是報表最前面的內容，只會出現一次。 報表尾則是由放置於報表主體底端的報表項目所組成。 這些項目是報表的最後內容，只會出現一次。  
  
## <a name="displaying-variable-data-in-a-page-header-or-footer"></a>在頁首或頁尾中顯示變數資料  
 頁首和頁尾可以包含靜態內容，但它們通常用來顯示會改變的內容，如頁碼或頁面內容的相關資訊。 若要顯示每個頁面各不相同的變數資料，必須使用運算式。  
  
 如果報表中只有定義一個資料集，則您可以在頁首或頁尾中加入 `[FieldName]` 之類的簡單運算式。 將欄位從 [報表資料] 窗格的資料集欄位集合或 [內建欄位] 集合拖曳到頁首或頁尾。 系統會自動為您加入具有適當運算式的文字方塊。  
  
 若要計算頁面上值的總和或其他彙總，可以使用指定 ReportItems 或資料集名稱的彙總運算式。 ReportItems 集合是在報表轉譯發生之後，每個頁面上的文字方塊集合。 資料集名稱必須存在於報表定義中， 下表顯示每種彙總運算式類型所支援的項目：  
  
|運算式提供支援|ReportItems 彙總|資料集彙總 (範圍必須是資料集的名稱)|  
|-----------------------------|----------------------------|----------------------------------------------------------|  
|報表主體中的文字方塊|是|否|  
|&PageNumber|是|否|  
|&TotalPages|是|否|  
|彙總函式|是的。 例如，<br /><br /> `=First(ReportItems!TXT_LastName.Value)`|是的。 例如，<br /><br /> `=Max(Quantity.Value,"DataSet1")`|  
|頁面上項目的欄位集合|間接。 例如，<br /><br /> `=Sum(ReportItems!Textbox1.Value)`|是的。 例如，<br /><br /> `=Sum(Fields!Quantity.Value,"DataSet1")`|  
|資料繫結影像|間接。 例如， `=ReportItems!TXT_Photo.Value`|是的。 例如，<br /><br /> `=First(Fields!Photo.Value,"DataSet1")`|  
  
 這個主題的下列各節顯示立即可用的運算式，它們會取得頁首和頁尾中常用的變數資料。 另外，還有一節會說明 Excel 轉譯延伸模組如何處理頁首和頁尾。 如需運算式的詳細資訊，請參閱[運算式 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)。  
  
### <a name="adding-calculated-page-totals-to-a-header-or-footer"></a>在頁首或頁尾中加入計算頁面總計  
 對於某些報表而言，在每份報表的頁首或頁尾中併入計算的值，可能會很有用 (例如，當頁面包括數值時的個別頁面總計)。 由於您無法直接參考欄位，因此您放在頁首或頁尾的運算式必須參考報表項目 (如文字方塊) 的名稱，而不是資料欄位的名稱：  
  
 `=Sum(ReportItems!Textbox1.Value)`  
  
 如果文字方塊所在的資料表或清單包含重複的資料列，頁首或頁尾在執行階段所顯示的值，便是目前頁面的資料表或清單中的所有 `TextBox1` 執行個體資料所有值的總和。  
  
 當計算頁面總計時，您可以預期在利用不同轉譯延伸模組來檢視報表時，總計會不同。 每個轉譯延伸模組的分頁輸出計算方式各不相同。 如果將您以 HTML 所檢視的相同頁面以 PDF 來檢視，且 PDF 頁面中的資料量不同，則可能會顯示不同的總計。 如需詳細資訊，請參閱[轉譯行為 &#40;報表產生器及 SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md)。  
  
### <a name="for-reports-with-multiple-datasets"></a>具有多個資料集的報表  
 對於具有一個以上資料集的報表，您不能將欄位或資料繫結影像直接加入至頁首和頁尾。 不過，您可以撰寫運算式來間接參考頁首和頁尾所要使用的欄位或資料繫結影像。  
  
 若要將變數資料放在頁首或頁尾中，請執行下列動作：  
  
-   將文字方塊加入頁首和頁尾中。  
  
-   在文字方塊中，撰寫一個運算式來產生所需要的變數資料。  
  
-   在運算式中，包含對頁面報表項目的參考 (例如，您可以參考包含特定欄位之資料的文字方塊)。 請勿包含對資料集欄位的直接參考。 例如，您不能使用 `[LastName]`運算式。 您可以使用下列運算式來顯示名為 `TXT_LastName`的文字方塊第一個執行個體的內容：  
  
     `=First(ReportItems!TXT_LastName.Value)`  
  
 您不能在頁首或頁尾的欄位中，使用彙總函式。 您可以只在報表主體中的報表項目上使用彙總函式。 如需頁首和頁尾中的常見運算式，請參閱[運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)。  
  
#### <a name="adding-a-data-bound-image-to-a-header-or-footer"></a>在頁首或頁尾中加入資料繫結影像  
 您可以在頁首或頁尾中，使用資料庫所儲存的影像資料。 不過，您不能直接從影像報表項目參考資料庫欄位。 相反地，您必須將文字方塊加入報表主體中，再將文字方塊設成包含影像的資料欄位 (請注意，這個值必須是 base64 編碼)。 您可以將文字方塊隱藏在報表主體中，以避免顯示 base64 編碼的影像。 之後，您便可以從頁首或頁尾中的影像報表項目參考隱藏文字方塊的值。  
  
 例如，假設您有一份產品資訊頁面所組成的報表。 每個頁面的頁首都要顯示產品的照片。 若要在報表首中列印儲存影像，請在報表主體中定義名為 `TXT_Photo` 的隱藏文字方塊，以用來從資料庫擷取影像，並利用運算式為其提供值：  
  
 `=Convert.ToBase64String(Fields!Photo.Value)`  
  
 在頁首中，加入一個影像報表項目來使用 `TXT_Photo` 文字方塊，以便解碼顯示影像：  
  
 `=Convert.FromBase64String(ReportItems!TXT_Photo.Value)`  
  
## <a name="using-headers-and-footers-to-position-text"></a>利用頁首或頁尾來定位文字  
 您可以利用頁首和頁尾來將文字定位在頁面中。 例如，假設您正在建立一份要利用郵件送交客戶的報表。 您可以利用頁首或頁尾來放置客戶地址，以便在摺疊之後，它可以出現在封套視窗之中。  
  
 如果您只使用文字方塊來擴展頁首或頁尾，可以在報表主體中隱藏文字方塊。 文字方塊在報表主體中的位置，會影響值是否在報表第一頁或最後一頁的頁首或頁尾出現。 例如，如果您有會使報表跨越多個頁面的資料表、矩陣或清單，隱藏的文字方塊值會出現在最後一頁中。 如果您要它出現在第一頁，請將隱藏的文字方塊放在報表主體的頂端。  
  
## <a name="designing-reports-with-page-headers-and-footers-for-specific-renderers"></a>設計具有特定轉譯器之頁首和頁尾的報表  
 在處理報表時，系統會結合資料和配置資訊。 當您檢視報表時，結合的資訊會傳遞至轉譯器，這個轉譯器則會判斷可在每個報表頁面上納入多少報表資料。  
  
 如果您使用瀏覽器來檢視報表伺服器上的報表，則 HTML 轉譯器會控制您所查看的報表頁面上的內容。 如果您計畫以不同於檢視所用的格式來傳遞報表，或者要以特定的格式列印報表，則可以針對將用於報表最終格式的轉譯器，進行報表配置的最佳化。 如需報表分頁的詳細資訊，請參閱 [Reporting Services 中的分頁 &#40;報表產生器及 SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md)。  
  
### <a name="working-with-page-headers-and-footers-in-excel"></a>在 Excel 中使用頁首和頁尾  
 當定義以 Excel 轉譯延伸模組為目標的報表之頁首和頁尾時，請遵循下列準則來得到最佳結果：  
  
-   利用頁尾來顯示頁碼。  
  
-   利用頁首來顯示影像、標題或其他文字。 請勿將頁碼放在頁首。  
  
 在 Excel 中，頁尾的配置會受到限制。 如果您在頁尾定義了包括複雜報表項目的報表，當在 Excel 中檢視報表時，頁尾不會依照您預期的方式來處理。  
  
 Excel 轉譯延伸模組可以接受簡單或複雜報表項目在頁首中的影像和絕對定位。 支援複雜頁首配置的副作用是，會減弱對在頁首中計算頁碼的支援。 在 Excel 轉譯延伸模組中，預設值會根據工作表數目來計算頁碼。 隨著您定義報表的方式而不同，這有可能產生錯誤的頁碼。 例如，假設您有一份轉譯成分四頁列印之單一大型工作表的報表。 如果您在頁首併入頁碼資訊，每個列印頁面的頁首都會顯示「第 1 頁，共 1 頁」。  
  
 較精確的頁面計數是以關聯於列印頁面尺寸的邏輯頁面為基礎。 在 Excel 中，頁尾會自動使用邏輯頁碼。 若要將邏輯頁面計數放在頁首中，您必須將裝置資訊設定設成使用簡單頁首。 請注意，使用簡單頁首時，您會移除在頁首區域中處理複雜報表配置的功能。  
  
 如需詳細資訊，請參閱 [匯出至 Microsoft Excel &#40;報表產生器及 SSRS&#41;](../report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)中使用這項資料。  
  
## <a name="see-also"></a>另請參閱  
 [在報表中內嵌影像 &#40;報表產生器及 SSRS&#41;](embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [矩形和線條 &#40;報表產生器及 SSRS&#41;](rectangles-and-lines-report-builder-and-ssrs.md)  
  
  
