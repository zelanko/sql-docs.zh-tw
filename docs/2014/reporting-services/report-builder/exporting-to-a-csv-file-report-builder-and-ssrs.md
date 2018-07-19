---
title: 匯出至 CSV 檔案 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 68ec746e-8c82-47f5-8c3d-dbe403a441e5
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 2c6bcbf4ce4a3bb3121bd55b8df95070de817f93
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37232688"
---
# <a name="exporting-to-a-csv-file-report-builder-and-ssrs"></a>匯出至 CSV 檔案 (報表產生器及 SSRS)
  逗號分隔值 (CSV) 轉譯延伸模組會將報表從多數應用程式都可輕易讀取與交換的標準化純文字格式報表，轉譯為扁平化表示的資料。  
  
 CSV 轉譯延伸模組使用字串字元分隔符號來分隔欄位和資料列，可將此字串字元分隔符號設定為非逗號字元。 所產生的檔案可以使用試算表程式 (例如 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] ) 開啟，或當做其他程式的匯入格式使用。 匯出的報表會變成.csv 檔案，並傳回 MIME 類型的`text/csv`。  
  
 如果您要使用與 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)]中的圖表、資料橫條、走勢圖、量測計和指標相關的資料，請將報表匯出為 CSV 檔，然後在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 中開啟檔案。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="CSVRendering"></a> CSV 轉譯  
 使用預設值轉譯時，CSV 報表會具有下列特性：  
  
-   預設的欄位分隔符號字串是逗號 (,)。  
  
    > [!NOTE]  
    >  您可以藉由變更裝置資訊設定的方式，將欄位分隔符號變更為所需的任何字元，包括 TAB。 如需詳細資訊，請參閱 [CSV Device Information Settings](../csv-device-information-settings.md)。  
  
-   記錄分隔符號字串是歸位字元和換行字元 (\<cr>\<lf>)。  
  
-   文字限定詞字串是引號 (")。  
  
     CSV 轉譯器不會在所有文字字串周圍加上限定詞。 只有在值包含分隔符號字元時，或值擁有分行符號時，才會加上文字限定詞。  
  
-   如果文字包含內嵌的分隔符號字串或限定詞字串，則文字限定詞是放置於該文字周圍，且內嵌的限定詞字串是重複的。  
  
-   忽略格式和配置。  
  
 下列項目會在轉譯過程中忽略：  
  
-   頁首  
  
-   頁尾  
  
-   自訂報表項目  
  
-   線條  
  
-   image  
  
-   矩形  
  
-   自動小計  
  
 剩餘的報表項目會先由上至下，再由左至右排序。 接著，每個項目會轉譯成資料行。 如果報表有巢狀資料項目 (例如，清單或資料表)，則父項目會在每一筆記錄中重複。  
  
 下表指出報表項目轉譯時的外觀：  
  
|項目|轉譯行為|  
|----------|------------------------|  
|文字方塊|轉譯文字方塊的內容。 在預設模式下，系統會根據項目的格式化屬性來設定項目的格式。 在相容模式下，格式可以依據裝置資訊設定來變更。 如需有關 CSV 轉譯模式的詳細資訊，請參閱以下。|  
|Table|藉由展開資料表，並為每個資料列與資料行以最低層級的詳細資料建立資料列與資料行，來進行轉譯。 小計資料列和資料行沒有資料行或資料列標題。 不支援鑽研報表。|  
|矩陣|藉由展開矩陣，並為每個資料列與資料行以最低層級的詳細資料建立資料列與資料行，來進行轉譯。 小計資料列和資料行沒有資料行或資料列標題。|  
|清單|轉譯每個詳細資料列或清單中執行個體的記錄。|  
|子報表|內容的每個執行個體都會重複父項目。|  
|圖表|針對每個圖表值和成員標籤建立資料列以進行轉譯。 階層中數列和類別目錄的標籤會扁平化，並且包含在圖表值的資料列中。|  
|資料橫條|像圖表一樣轉譯。 資料橫條通常不包含階層或標籤。|  
|走勢圖|像圖表一樣轉譯。 走勢圖通常不包含階層或標籤。|  
|量測計|轉譯為包含線性標尺的最小與最大值、範圍的開始與結束值，以及指標值的單一記錄。|  
|指標|以作用中的狀態名稱、可用的狀態以及資料值轉譯成單一記錄。|  
|對應|轉譯資料列，其中包含地圖圖層之每一個地圖成員的標籤和值。<br /><br /> 如果地圖有多個圖層，則資料列中的值會根據地圖圖層是使用相同或不同的地圖資料區域而有所不同。 如果多個地圖圖層使用相同的資料區域，則資料列會包含所有圖層中的資料。|  
  
### <a name="hierarchical-and-grouped-data"></a>階層與群組資料  
 階層與群組資料必須扁平化，才能以 CSV 格式表示。  
  
 轉譯延伸模組會將報表扁平化為樹狀結構，可表示資料區域內的巢狀群組。 若要將報表扁平化：  
  
-   資料列階層要在資料行階層之前扁平化。  
  
-   資料行的排列順序如下：文字方塊在主體順序中為由左至右、由上至下，後面接著以由左至右、由上至下排列的資料區域。  
  
-   在資料區域中，資料行的排列順序如下：邊角成員、資料列階層成員、資料行階層成員，然後是資料格。  
  
-   對等資料區域是一種資料區域或動態群組，可以共用一般資料區域或動態上階。 對等資料會以扁平化樹狀結構的分支識別。  
  
 如需詳細資訊，請參閱 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)。  
  
 
  
##  <a name="RenderingModes"></a> 轉譯器模式  
 CSV 轉譯延伸模組可以在兩種模式下操作：一種會針對 Excel 最佳化，而另一種則會針對需要 CSV 嚴格遵循 RFC 4180 中 CSV 合規性的協力廠商應用程式最佳化。 根據所使用的模式，對等資料區域的處理方式也會不同。  
  
### <a name="default-mode"></a>預設模式  
 預設模式會針對 Excel 最佳化。 以預設模式進行轉譯時，報表會轉譯為包含多個 CSV 轉譯資料區塊的 CSV 檔。 每個對等區域都會以一個空行分隔。 報表主體內的對等資料區域在 CSV 檔中，會轉譯為個別的資料區塊。 結果是 CSV 檔，而其中：  
  
-   報表主體內的各個文字方塊在 CSV 檔中會轉譯一次，而且會轉譯為第一個資料區塊。  
  
-   報表主體中的每個最上層對等資料區域都會在自己的資料區塊中進行轉譯。  
  
-   巢狀資料區域會以對角方式轉譯為相同的資料區塊。  
  
#### <a name="formatting"></a>格式化  
 數值會利用其格式化的狀態進行轉譯。 Excel 可以識別格式化的數值，例如，貨幣、百分比與日期，並在匯入 CSV 檔時，適當地格式化資料格。  
  
### <a name="compliant-mode"></a>相容模式  
 相容模式會針對協力廠商應用程式最佳化。  
  
#### <a name="data-regions"></a>資料區域  
 只有檔案的第一個資料列包含資料行標頭，而且每個資料列都有相同數目的資料行。  
  
#### <a name="formatting"></a>格式化  
 這些值沒有格式化。  
  
##  <a name="Interactivity"></a> 互動性  
 此轉譯器產生的任一種 CSV 格式都不支援互動性。 系統不會轉譯下列互動項目：  
  
-   超連結  
  
-   顯示或隱藏  
  
-   文件引導模式  
  
-   鑽研或點選連結的連結  
  
-   使用者排序  
  
-   固定頁首  
  
-   書籤  
  

  
##  <a name="DeviceInfo"></a> 裝置資訊設定  
 您可以變更此轉譯器的某些預設值，包括要在哪個模式下進行轉譯、要使用哪些字元當做分隔符號，以及要使用哪些字元當做文字限定詞的預設字串，只要變更裝置資訊設定即可。 如需詳細資訊，請參閱 [CSV Device Information Settings](../csv-device-information-settings.md)。  
  
  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 中的分頁 &#40;報表產生器及 SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [轉譯行為 &#40;報表產生器及 SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [不同報表轉譯延伸模組的互動式功能&#40;報表產生器及 SSRS&#41;](interactive-functionality-different-report-rendering-extensions.md)   
 [轉譯報表項目 &#40;報表產生器及 SSRS&#41;](../report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  
