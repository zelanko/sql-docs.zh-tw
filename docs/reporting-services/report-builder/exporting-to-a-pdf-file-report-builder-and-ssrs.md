---
title: 匯出至 PDF 檔案 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 10/21/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-builder
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: f22497b7-f6c1-4c7b-b831-8c731e26ae37
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 940bdc4f76fcd171fbedc126cf7b651637ee5293
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43273662"
---
# <a name="exporting-to-a-pdf-file-report-builder-and-ssrs"></a>匯出至 PDF 檔案 (報表產生器及 SSRS)
  PDF 轉譯延伸模組會將 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表轉譯成可在 Adobe Acrobat 與支援 PDF 1.3 之其他協力廠商 PDF 檢視器中開啟的檔案。 雖然 PDF 1.3 與 Adobe Acrobat 4.0 和更新版本相容，但是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 只支援 Adobe Acrobat 11.0 或更新版本。 轉譯延伸模組不需要 Adobe 軟體就能轉譯報表。 但是，若要檢視或列印 PDF 格式的報表，則需要 PDF 檢視器 (例如 Adobe Acrobat)。  
  
 PDF 轉譯延伸模組支援 ANSI 字元，而且可以從日文、韓文、繁體中文、簡體中文、斯拉夫文、希伯來文和阿拉伯文，轉譯 Unicode 字元 (有特定限制)。 如需限制的詳細資訊，請參閱[匯出報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)。  
  
 PDF 轉譯器是一種實體頁面轉譯器，因此，其分頁行為與 HTML 和 Excel 之類的其他轉譯器不同。 本主題提供 PDF 轉譯器的特定資訊並描述規則的例外狀況。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="FontRequirements"></a> 字型內嵌  
 如果可以的話，PDF 轉譯延伸模組會內嵌在 PDF 檔中顯示報表所需之每個字型的子集。 報表中使用的字型必須安裝在報表伺服器上。 報表伺服器產生 PDF 格式的報表時，會使用以報表參考之字型儲存的資訊，來建立 PDF 檔案中的字元對應。 如果報表伺服器上未安裝參考字型，則產生的 PDF 檔案可能不會包含正確的對應，而且檢視時可能也無法正確地顯示。  
  
 當下列條件成立時，字型會內嵌在 PDF 檔案中：  
  
-   字型作者授與字型內嵌權限。 已安裝的字型包含表示字型作者是否想要讓字型內嵌在文件中的屬性。 如果屬性值為 EMBED_NOEMBEDDING，字型就不會內嵌在 PDF 檔案中。 如需詳細資訊，請參閱 msdn.microsoft.com 上的「TTGetEmbeddingType」。  
  
-   字型為 TrueType。  
  
-   字型由報表中的可見項目參考。 如果字型由 Hidden 屬性設定為 True 的項目所參考，則不需要字型來顯示轉譯的資料，而且字型將不會包含在檔案中。 只有在需要字型來顯示轉譯的報表資料時，才會內嵌字型。  
  
 如果字型符合所有的條件，就會內嵌在 PDF 檔案中。 如果其中有一或多個條件不符合，字型就不會內嵌在 PDF 檔案中。  
  
> [!NOTE]  
>  雖然符合這些條件，但是有一個情況不會在 PDF 檔案中內嵌字型。 如果使用的字型是 PDF 規格中一般稱為標準第一類字型或是基本十四種字型中的字型，則 ANSI 內容不會內嵌字型。  
  
  
### <a name="fonts-on-the-client-computer"></a>用戶端電腦上的字型  
 當字型內嵌在 PDF 檔案中時，用來檢視報表的電腦 (用戶端電腦) 不需要安裝字型，即可正確顯示報表。  
  
 當字型沒有內嵌在 PDF 檔案中時，用戶端電腦必須已安裝正確的字型，才能正確顯示報表。 如果字型未安裝在用戶端電腦上，PDF 檔案會針對不支援的字元顯示一個問號字元 (?)。  
  
### <a name="verifying-fonts-in-a-pdf-file"></a>確認 PDF 檔案中的字型  
 當在報表中使用不支援非拉丁字元的字型，然後將非拉丁字元加入至報表中時，PDF 的輸出中最常發生差異的情形。 您應該在報表伺服器和用戶端電腦上皆測試 PDF 轉譯輸出，以確認報表正確轉譯。  
  
 請勿依賴在預覽中檢視報表，或匯出至 HTML，因為報表會由於圖形設計介面或 Microsoft Internet Explorer 個別所執行的字型自動替換，而使其外觀看起來是正確的。 如果伺服器上有缺少 Unicode 圖像，您會看到這些字元會以問號 (?) 取代。 如果用戶端上有缺少字型，您會看到這些字元以方塊 (□) 取代。  
  
 內嵌在 PDF 檔案中的字型包含在 Fonts 屬性中，而此屬性則以中繼資料的形式和檔案一起儲存。  
  
##  <a name="Metadata"></a> 中繼資料  
 除了報表配置之外，PDF 轉譯延伸模組也會將下列中繼資料寫入 PDF 文件資訊字典。  
  
|PDF 屬性|來源|  
|------------------|------------------|  
|**Title**|**Name** RDL 元素的 **Report** 屬性。|  
|**作者**|**Author** RDL 元素。|  
|**主旨**|**Description** RDL 元素。|  
|**建立者**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 產品名稱和版本。|  
|**產生器 (producer)**|轉譯延伸模組名稱與版本。|  
|**CreationDate**|PDF **datetime** 格式的報表執行時間。|  
  
  
##  <a name="Interactivity"></a> 互動性  
 在 PDF 中支援某些互動項目。 下列是特定行為的描述。  
  
### <a name="show-and-hide"></a>顯示與隱藏  
 在 PDF 中不支援動態顯示與隱藏元素。 系統會轉譯 PDF 文件以符合報表中任何項目的目前狀態。 例如，如果項目在一開始執行報表時顯示，則會轉譯該項目。 如果在匯出報表時，可以切換的影像是隱藏的，就不會轉譯這些影像。  
  
### <a name="document-map"></a>文件引導模式  
 如果報表中有任何文件引導模式標籤，就會在 PDF 檔案中加入文件大綱。 每個文件引導模式標籤都會以該標籤在報表中出現的順序，顯示為文件大綱中的一個項目。 在 Acrobat 中，只有在轉譯目標書籤所在頁面時，才會將該書籤加入到文件大綱中。  
  
 如果只轉譯單一頁面，則不會加入任何文件大綱。 系統會以階層的方式排列文件引導模式，來反映報表中的巢狀層級。 您可以在 Acrobat 的 [書籤] 索引標籤下存取文件大綱。按一下文件大綱內的項目時，會讓文件移至加上書籤的位置。  
  
### <a name="bookmarks"></a>書籤  
 在 PDF 轉譯中不支援書籤。  
  
### <a name="drillthrough-links"></a>鑽研連結  
 在 PDF 轉譯中不支援鑽研連結。 鑽研連結不會轉譯為可點按的連結，而且鑽研報表無法連接到鑽研的目標。  
  
### <a name="hyperlinks"></a>超連結  
 報表中的超連結會轉譯為 PDF 檔案中可點按的連結。 當您按一下超連結時，Acrobat 會開啟預設的用戶端瀏覽器，並導覽至超連結 URL。  
  
  
##  <a name="Compression"></a> 壓縮  
 影像壓縮會以影像的原始檔案類型為基礎。 PDF 轉譯延伸模組預設會壓縮 PDF 檔案。  
  
 若要盡可能保留 PDF 檔案隨附的任何壓縮影像，JPEG 影像會儲存為 JPEG，而其他所有影像類型則會儲存為 BMP。  
  
> [!NOTE]  
>  PDF 檔案不支援內嵌 PNG 影像。  
  
  
##  <a name="DeviceInfo"></a> 裝置資訊設定  
 您可以透過變更裝置資訊設定，變更此轉譯器的某些預設設定。 如需詳細資訊，請參閱 [PDF Device Information Settings](../../reporting-services/pdf-device-information-settings.md)。  
  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 中的分頁 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [轉譯行為 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [不同報表轉譯延伸模組的互動式功能 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [轉譯報表項目 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
