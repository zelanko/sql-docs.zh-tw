---
title: "轉譯為 HTML （報表產生器及 SSRS） |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf559b0a-499a-4d74-b520-b382b87e0b17
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: a431b5b8c988b981f217353c366bbbe1f1f68699
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="rendering-to-html-report-builder-and-ssrs"></a>轉譯為 HTML (報表產生器及 SSRS)
  HTML 轉譯延伸模組會轉譯 HTML 格式的分頁報表。 轉譯延伸模組也可產生完整的 HTML 頁面，或內嵌在其他 HTML 頁面中的 HTML 片段。 所有 HTML 均以 UTF-8 編碼產生。  
  
 HTML 轉譯延伸模組是在瀏覽器中檢視之報表的預設轉譯延伸模組，包括在 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 入口網站中執行時。  
  
 HTML 轉譯延伸模組是在瀏覽器中檢視之報表的預設轉譯延伸模組，包括在 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 入口網站中執行時。 HTML 轉譯延伸模組可以將 HTML 轉譯成片段，或完整的 HTML 文件。 如果 HTML 是片段，則會移除 HTML 文件的 **HEAD**、 **HTML**和 **BODY** 標記。 系統只會轉譯 **BODY** 標記的內容。 這很適合用於將 HTML 內嵌於其他應用程式所產生的 HTML 中。  
  
 在某些情況下，當報表轉譯為 HTML 時，報表參數可能會被用來發動指令碼資料隱碼攻擊。 如需保護報表安全的詳細資訊，請參閱 [保護報表和資源的安全](../../reporting-services/security/secure-reports-and-resources.md)。  
  
 如需瀏覽器的詳細資訊，請參閱 [Reporting Services 和 Power View 的瀏覽器支援](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RenderingMHTML"></a> 在 MHTML 中轉譯  
 HTML 轉譯延伸模組也可以在 MHTML (彙總 HTML 文件的 MIME 封裝) 中轉譯報表。 MHTML 擴充了 HTML，可以在 HTML 文件中內嵌編碼的物件，例如影像。 使用 MHTML 轉譯延伸模組時，您可以利用 MIME 結構，將影像、文件或其他二進位檔案等資源內嵌在單一檔案的報表 HTML 中。 MHTML 報表也適合用於內嵌在電子郵件訊息中，因為所有的資源都包含在報表中。 雖然實際上是 HTML 轉譯延伸模組轉譯 MHTML，此功能也可視為 MHTML 轉譯延伸模組。  
  
  
##  <a name="BrowserSupport"></a> 瀏覽器支援  
 此轉譯延伸模組支援下列瀏覽器版本：  
  
-   Internet Explorer 5.5 及更新版本  
  
-   Firefox 1.5 及更新版本  
  
-   Safari 3.0 及更新版本  
  
 由於跨瀏覽器的考量，轉譯的報表在不同的瀏覽器中可能略有不同。 例如，文字方塊包含稱為 WritingMode 的屬性。 Firefox 中不支援此屬性。  
  
  
##  <a name="HTMLSpecificRenderingRules"></a> HTML 特定的轉譯規則  
 下列 HTML 特定規則會在轉譯時套用：  
  
-   轉譯器會建立一個 HTML 資料表結構，以便在每個 **ReportItems** 集合 (如果有一個以上) 中包含所有項目。  
  
-   資料表結構中的每個項目都會佔用一個單一的資料格。  
  
-   空的資料格會盡量摺疊在一起以減少 HTML 的大小。  
  
-   系統會將空白資料格的資料列加入到上邊緣，並將另一個資料行加入到左邊緣，就可以增進瀏覽器轉譯資料表的速度。  
  
-   不包含任何項目，只包含項目間之間距的資料表資料列或資料行，其寬度和高度是固定的。  
  
-   其他所有資料列和資料行都可以根據每個報表項目的大小成長。  
  
-   所有座標和報表項目大小都會轉換為公釐。 包括樣式屬性在內的其他所有大小則會保留其原始單位。 大小和位置的差異小於 .2 公釐時，則會視為 0 公釐。  
  
  
##  <a name="Interactivity"></a> 互動性  
 HTML 中支援某些互動元素。 下列是特定行為的描述。  
  
### <a name="show-and-hide"></a>顯示與隱藏  
 可以切換其可見性的報表項目會以 +/- 切換影像轉譯，而且可以點按。 按一下項目時，系統會回呼伺服器，才能利用已變更的顯示或隱藏狀態重新轉譯輸出。  
  
### <a name="document-map"></a>文件引導模式  
 文件引導模式標籤可以轉譯，而且可以使用檢視器控制項中的文件引導模式來導覽。 若是省略的資料區域標頭，就會在第一個子資料格上轉譯標籤。 如果沒有顯示任何子資料格，則會在第一個子資料格前的子系上轉譯標籤。  
  
### <a name="bookmarks"></a>書籤  
 系統會轉譯書籤連結並顯示為超連結。 同時，系統會轉譯書籤目標，而且按一下書籤連結就可以導覽。 按一下書籤連結時，報表會移到第一個出現的目標書籤標籤，而且，如果可能，瀏覽器會捲動，讓書籤連結位於視窗最上方。 HTML 錨定 (\<>) 標記用於標示書籤目標。  
  
### <a name="interactive-sorting"></a>互動式排序  
 如果文字方塊中已定義使用者排序，HTML 轉譯延伸模組會將文字方塊中的排序圖示轉譯到其內容的右側。 如果報表內含其中已定義使用者排序的任何文字方塊，按一下排序影像時，會轉譯導致回傳至伺服器的 JavaScript。  
  
### <a name="hyperlinks-and-drillthrough"></a>超連結與鑽研  
 超連結與鑽研連結會轉譯為超連結的報表項目使用 HTML 錨定 (\<>) 標記定義所在的項目周圍。  
  
### <a name="search"></a>搜尋  
 [搜尋] 功能可讓使用者在報表內搜尋文字的字串。  
  
 其他搜尋和尋找功能是由 ReportViewer Web 表單控制項提供。  
  
  
##  <a name="DeviceInfo"></a> 裝置資訊設定  
 您可以變更此轉譯器的某些預設值，包括要在哪個模式下轉譯，方法是，變更裝置資訊設定。 如需相關資訊，請參閱 [HTML Device Information Settings](../../reporting-services/html-device-information-settings.md)。  
  
  
## <a name="see-also"></a>請參閱＜  
 [Reporting Services 中的分頁 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [轉譯行為 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [不同報表轉譯延伸模組的互動式功能 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [轉譯報表項目 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
