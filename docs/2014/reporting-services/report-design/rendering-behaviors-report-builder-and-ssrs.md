---
title: 轉譯行為 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8f873ef9-27a3-40e5-b58b-6774f8027a58
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: f99447693a466e016e84c29cb254bbddd4a75b05
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030722"
---
# <a name="rendering-behaviors-report-builder--and-ssrs"></a>轉譯行為 (報表產生器及 SSRS)
  根據所選取的轉譯器，當轉譯報表時，系統會將某些規則套用到報表主體及其內容。 將報表項目全部容納在一頁的方式，取決於下列因素的組合：  
  
-   轉譯規則。  
  
-   報表項目的寬度和高度。  
  
-   報表主體的大小。  
  
-   頁面的寬度和高度。  
  
-   用於分頁的轉譯器特定支援。  
  
 本主題討論 Reporting Services 所應用的一般規則。 如需詳細資訊，請參閱[轉譯報表項目 &#40;報表產生器及 SSRS&#41;](rendering-report-items-report-builder-and-ssrs.md)、[轉譯資料區 &#40;報表產生器及 SSRS&#41;](rendering-data-regions-report-builder-and-ssrs.md) 和[轉譯資料 &#40;報表產生器及 SSRS&#41;](rendering-data-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="general-behaviors-for-html-mhtml-word-and-excel-soft-page-break-renderers"></a>適用於 HTML、MHTML、Word 與 Excel (軟分頁轉譯器) 的一般行為  
 使用 HTML 和 MHTML 格式匯出的報表會針對各種長度的頁面，提供最佳的電腦螢幕檢視效果。 分頁符號只會以垂直方式插入到報表主體內的約略位置。 這些約略位置取決於 [屬性] 窗格中的互動式高度設定。 例如，假設互動式高度設定為 5 英吋。 轉譯報表時，頁面高度的長度大約是 5 英吋。 Word 和 Excel 會根據邏輯分頁符號分頁，並忽略互動式高度設定。  
  
> [!NOTE]  
>  若要判定報表出現在軟分頁符號轉譯器的方式，請使用 [報表預覽]。 報表會 HTML、MHTML、Word 或 Excel 格式出現。  
  
 將報表匯出為 HTML、MHTML、Word 或 Excel 時，會遵循下列一般規則進行：  
  
-   系統會將您明確插入的分頁符號，也就是邏輯分頁符號，套用到報表項目中。 例如，如果您在每個群組之間插入分頁符號，則會在轉譯報表時套用這些分頁符號。  
  
-   系統會使用報表項目上顯示的頁面高度與次數來建立約略的版面配置。 例如，如果文字方塊的高度為 .5 英吋，而且會在報表中重複 5 次，就會保留 2.5 英吋。  
  
-   系統會根據互動式高度設定，插入多個軟分頁符號。 若要在 HTML 和 ReportViewer 控制項中隱藏分頁符號，而且僅控制具有明確分頁符號的分頁，請將 [互動高度] 值設定為 0 或非常大的數字。  
  
    > [!NOTE]  
    >  在軟分頁符號轉譯器中不會使用互動式寬度設定。  
  
-   報表頁面可以擴展以配合需要保持在一起的視窗、孤立項目以及報表項目。 也就是說，報表可以擴展到超出畫面寬度，而且可以使用滑動軸檢視。  
  
-   分頁只會以垂直方式套用到報表中。  
  
-   系統不會套用頁面邊界。  
  
## <a name="general-behaviors-for-pdf-image-and-print-hard-page-break-renderers"></a>適用於 PDF、影像與列印 (手動分頁符號轉譯器) 的一般行為  
 使用 PDF 和影像匯出的報表會針對大小一致的頁面，提供最佳的書籍或列印效果。 分頁符號會以垂直和水平的方式插入到報表主體內的特定位置。 這些特定位置取決於頁面寬度與頁面高度設定。  
  
> [!NOTE]  
>  若要判定報表出現在手動分頁符號轉譯器的方式，請使用 [預覽列印]。 報表會 PDF 或影像格式出現。  
  
-   頁面會先由左至右，再由上至下循序編號。  
  
-   系統會將您明確插入的分頁符號，也就是邏輯分頁符號，套用到報表項目中。 這些分頁符號可能會使報表項目將其他項目推移到下一頁。  
  
-   如果實體分頁符號穿過必須保持在一起的報表項目，必須保持在一起的項目就會移到下一頁。  
  
-   由於頁面大小的限制，可能無法將所有項目保持在一起，也可能無法重複項目。 如果發生這個情況，轉譯器可能會忽略某些與其他項目重複的規則，才能讓報表項目容納在該頁面上。  
  
-   如果有項目無法保持在一起 (例如，因為擴展到太大而無法容納在垂直之可用頁面區域內的文字方塊)，則該項目將會在實體頁面界限遭到裁剪，而且繼續留到下一頁。  
  
-   分頁會以垂直和水平的方式套用到報表中。  
  
    > [!NOTE]  
    >  在手動分頁符號轉譯器中不會使用互動式寬度設定。  
  
## <a name="minimum-spacing-between-report-items"></a>報表項目間的最小間距  
 報表項目會在報表主體內擴展以容納其內容。 例如，轉譯報表時，矩陣資料區域在頁面中通常會以橫向往下擴展，而且文字方塊的高度為隨著運算式所傳回的資料而調整。  
  
 轉譯器會在報表配置中定義的報表項目之間維持最小的空間。 當您在報表配置上，將某個報表項目放置在另一個報表項目旁邊時，報表項目間的距離會變成報表項目水平或垂直擴展時所必須維持的最小距離。 例如，如果您在報表中加入矩陣資料區域，然後在矩陣右側加入矩形 .25 英吋，該空間就會隨著矩陣的擴展來維持。 每一個項目都會往右移動，以維持其本身與其左邊結束之項目之間的最小空間。  
  
## <a name="page-headers-and-footers"></a>頁首和頁尾  
 頁首和頁尾會出現在每個轉譯頁面的頂端和底部。 您可以設定頁首和頁尾的格式，讓其包含框線色彩、框線樣式，以及框線寬度。 您也可以加入背景色彩或背景影像。 這些格式選項全部都會根據您選擇的格式進行轉譯。  
  
 以 HTML 或 MHTML 轉譯格式進行轉譯時，下列規則會套用到頁首和頁尾：  
  
> [!NOTE]  
>  如需 Excel 如何轉譯頁首和頁尾的資訊，請參閱[匯出至 Microsoft Excel &#40;報表產生器及 SSRS&#41;](../report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)。 如需 Word 如何轉譯頁首和頁尾的資訊，請參閱[匯出至 Microsoft Word &#40;報表產生器及 SSRS&#41;](../report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md)。  
  
-   頁面出現時，在每頁頂端和底部的可用頁面區域內，會轉譯頁首和頁尾。  
  
-   在隱藏頁首或頁尾的頁面上，即使沒有轉譯頁首或頁尾，仍然會在可用的頁面區域內保留頁首或頁尾的高度。  
  
-   如果頁首或頁尾的內容擴展到超出頁首或頁尾的界限，頁首或頁尾的大小會增加來容納這些內容。  
  
 以 PDF 或影像轉譯格式進行轉譯時，下列規則會套用到頁首和頁尾：  
  
-   在每頁頂端和底部的可用頁面區域內，會轉譯頁首或頁尾。  
  
-   在隱藏頁首或頁尾的頁面上，即使沒有轉譯頁首或頁尾，仍然會在可用的頁面區域內保留頁首或頁尾的高度。  
  
-   頁首和頁尾不會擴展，也不會縮減。 當您建立頁首或頁尾時，會以指定的高度，在每一頁上進行轉譯。  
  
-   不管報表內的資料行數目有多少，每頁都只有一個頁首和頁尾。  
  
-   如果頁首或頁尾的內容擴展到超出頁首或頁尾的界限，這些內容會遭到裁剪。  
  
-   將報表轉譯為子報表時，不會轉譯在原始 RDL 檔案中所定義的頁首和頁尾。  
  
## <a name="logical-page-breaks"></a>邏輯分頁符號  
 邏輯分頁符號是您在報表項目或群組前後插入的分頁符號。 轉譯或匯出報表時，分頁符號有助於決定如何將內容納入報表頁面，以獲得最佳的檢視效果。  
  
 轉譯邏輯分頁符號時，適用下列規則：  
  
-   對於持續隱藏的報表項目，以及透過按一下其他報表項目來控制可見性的報表項目，系統會忽略邏輯分頁符號。  
  
-   如果目前在轉譯報表時可以看到邏輯分頁符號，就會有條件地在可見的項目上套用邏輯分頁符號。  
  
-   系統會保留含有邏輯分頁符號之報表項目與其對等報表項目之間的空間。  
  
-   在報表項目之前插入的邏輯分頁符號會將報表項目向下推送到下一頁。 系統會在下一頁的頂端轉譯報表項目。  
  
-   系統不會保留在資料表或矩陣資料格之項目上定義的邏輯分頁符號。 這不適用於清單中的項目。  
  
## <a name="see-also"></a>另請參閱  
 [不同報表轉譯延伸模組的互動式功能&#40;報表產生器和 SSRS&#41;](../report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [轉譯為 HTML &#40;報表產生器及 SSRS&#41;](../report-builder/rendering-to-html-report-builder-and-ssrs.md)   
 [頁面配置和轉譯&#40;報表產生器和 SSRS&#41;](page-layout-and-rendering-report-builder-and-ssrs.md)  
  
  