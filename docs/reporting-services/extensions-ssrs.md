---
title: 延伸模組
author: markingmyname
ms.author: maghan
manager: kfile
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 59a716d08047c69655f775f7553e2d80d5ff396f
ms.sourcegitcommit: 2f5773f4bc02bfff4f2924226ac5651eb0c00924
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/18/2018
ms.locfileid: "53553150"
---
# <a name="extensions-for-sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS) 的延伸模組

  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中的報表伺服器會使用延伸模組，以模塊化其接受用於驗證、資料處理、報表轉譯及報表傳遞的輸入或輸出類型。 這可讓現有的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 安裝輕鬆地利用產業中的新軟體標準，例如新驗證結構，或是自訂資料來源類型。 報表伺服器支援自訂驗證延伸模組、資料處理延伸模組、報表處理延伸模組、轉譯延伸模組和傳遞延伸模組，以及在 RSReportServer.config 組態檔中適用於使用者的可設定延伸模組。 例如，您可以限制報表檢視器允許使用的匯出格式。 報表伺服器至少需要一個驗證延伸模組、資料處理延伸模組和轉譯延伸模組。 傳遞與報表處理延伸模組是選擇性的，但是您若要支援報表散發或自訂控制項，則是必要的。  
  
 此主題描述 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中便於使用的延伸模組。  
  
## <a name="security-extensions"></a>安全性延伸模組

 安全性延伸模組用於驗證和授權使用者與群組至報表伺服器。 預設的安全性延伸模組會以 Windows 驗證為基礎。 如果您的部署模型需要其他驗證方法 (例如，您的網際網路或外部網路部署若是需要以表單為基礎的驗證)，也可以建立自訂安全性延伸模組以取代預設的安全性。 在單一 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 安裝中，只能使用一個安全性延伸模組。 您可以取代預設的 Windows 驗證安全性延伸模組，但是不能和自訂安全性延伸模組一起使用。  
  
## <a name="data-processing-extensions"></a>資料處理延伸模組

 資料處理延伸模組可用於查詢資料來源，並傳回扁平化的資料列集。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 會使用不同的延伸模組與不同的資料來源類型互動。 您可以使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]內含的延伸模組，或者開發自己的延伸模組。 目前提供了 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、Oracle、 [!INCLUDE[SAP_DPE_BW_1](../includes/sap-dpe-bw-1-md.md)]、Hyperion Essbase、Teradata、OLE DB 和 ODBC 資料來源的資料處理延伸模組。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 也可以使用任何 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 資料提供者。 資料處理延伸模組會藉由執行下列工作來處理報表處理器元件的查詢要求：  
  
- 開啟資料來源的連接。  
  
- 分析查詢並傳回欄位名稱清單。  
  
- 針對資料來源執行查詢並傳回資料列集。  
  
- 如果需要的話，將參數傳遞給查詢。  
  
- 反覆運算資料列集並擷取資料。  
  
有些延伸模組也可以執行下列工作：  
  
- 分析查詢並傳回查詢所使用的參數名稱清單。  
  
- 分析查詢並傳回群組所使用的欄位清單。  
  
- 分析查詢並傳回排序所使用的欄位清單。  
  
- 提供使用者名稱與密碼以連接到資料來源。  
  
- 傳遞具有多個值的參數給查詢。  
  
- 反覆運算資料列並擷取輔助中繼資料。  
  
## <a name="rendering-extensions"></a>轉譯延伸模組

 轉譯延伸模組會將報表處理器的資料與配置資訊轉換成裝置特定格式。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 包含七個轉譯延伸模組：HTML、Excel、CSV、XML、Image、PDF 和 [!INCLUDE[msCoName](../includes/msconame-md.md)] Word。  
  
- **HTML 轉譯延伸模組** ：當您透過網頁瀏覽器向報表伺服器要求報表時，報表伺服器就會使用 HTML 轉譯延伸模組來轉譯報表。 HTML 轉譯延伸模組會使用 UTF-8 編碼來產生所有 HTML。 如需詳細資訊，請參閱[轉譯為 HTML &#40;報表產生器及 SSRS&#41;](../reporting-services/report-builder/rendering-to-html-report-builder-and-ssrs.md) 和 [Reporting Services 和 Power View 的瀏覽器支援](../reporting-services/browser-support-for-reporting-services-and-power-view.md)。  
  
- **Excel 轉譯延伸模組** ：Excel 轉譯延伸模組會轉譯可在 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 97 或更新版本中檢視和修改的報表。 這個轉譯延伸模組會以二進位交換檔案格式 (BIFF) 建立檔案。 BIFF 是 Excel 資料的原生檔案格式。 在 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 中轉譯的報表支援任何試算表的所有可用功能。 如需詳細資訊，請參閱 [匯出至 Microsoft Excel &#40;報表產生器及 SSRS&#41;](../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)中使用這項資料。  
  
- **CSV 轉譯延伸模組** ：逗號分隔值 (CSV) 轉譯延伸模組會將報表轉譯成逗號分隔的純文字檔案，沒有任何格式。 使用者可以使用 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)]之類的試算表應用程式或是任何可讀取文字檔的其他程式來開啟這些檔案。 如需詳細資訊，請參閱 [匯出至 CSV 檔案 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md)中使用這項資料。  
  
- **XML 轉譯延伸模組** ：XML 轉譯延伸模組將報表轉譯成 XML 檔案。 然後，這些 XML 檔案就可以供其他程式儲存或讀取。 您也可以使用 XSLT 轉換，將報表變成可供其他應用程式使用的另一種 XML 結構描述。 由 XML 轉譯延伸模組所產生的 XML 是以 UTF-8 編碼。 如需詳細資訊，請參閱 [匯出至 XML &#40;報表產生器及 SSRS&#41;](../reporting-services/report-builder/exporting-to-xml-report-builder-and-ssrs.md)中使用這項資料。  
  
- **影像轉譯延伸模組** ：影像轉譯延伸模組會將報表轉譯成點陣圖或中繼檔。 這個延伸模組可將報表轉譯成下列格式：BMP、EMF、GIF、JPEG、PNG、TIFF 和 WMF。 依預設，影像會轉譯成 TIFF 格式，可使用作業系統預設的影像檢視器來顯示 (例如，Windows 圖片和傳真檢視器)。 您可以從檢視器將影像傳送到印表機。 使用影像轉譯延伸模組來轉譯報表，以確保報表在每一個用戶端看起來皆一致。 (當使用者以 HTML 格式檢視報表時，報表的外觀會因使用者所用的瀏覽器版本、使用者的瀏覽器設定，以及可使用的字型而有所不同)。影像轉譯延伸模組會在伺服器上轉譯報表，因此所有的使用者皆會看到相同的影像。 因為報表是在伺服器上轉譯，報表中所使用的所有字型都必須安裝在伺服器上。 如需詳細資訊，請參閱 [匯出至影像檔 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-builder/exporting-to-an-image-file-report-builder-and-ssrs.md)中使用這項資料。  
  
- **PDF 轉譯延伸模組** ：PDF 轉譯延伸模組會將報表轉譯成可在 Adobe Acrobat 6.0 或更新版本中開啟和檢視的 PDF 檔案。 如需詳細資訊，請參閱 [匯出至 PDF 檔案 &#40;報表產生器及 SSRS&#41;](../reporting-services/report-builder/exporting-to-a-pdf-file-report-builder-and-ssrs.md)中使用這項資料。  
  
- **Microsoft Word 轉譯延伸模組** ： [!INCLUDE[msCoName](../includes/msconame-md.md)] Word 轉譯延伸模組會將報表轉譯成與 [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Word 2000 或更新版本相容的 Word 文件。 如需詳細資訊，請參閱 [匯出至 Microsoft Word &#40;報表產生器及 SSRS&#41;](../reporting-services/report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md)中使用這項資料。  
  
## <a name="report-processing-extensions"></a>報表處理延伸模組

 您可以加入報表處理延伸模組，以便提供 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中未包含之報表項目的自訂報表處理。 根據預設，報表伺服器可以處理資料表、圖表、矩陣、清單、文字方塊、影像和其他所有報表項目。 如果您想要將特殊功能加入在報表執行過程中需要自訂處理的報表 (例如，想要內嵌 [!INCLUDE[msCoName](../includes/msconame-md.md)] MapPoint 對應)，則可以建立報表處理延伸模組來執行。  
  
## <a name="delivery-extensions"></a>傳遞延伸模組
 背景處理應用程式會使用傳遞延伸模組，將報表傳遞至各個位置。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 包括電子郵件傳遞延伸模組以及檔案共用傳遞延伸模組。 電子郵件傳遞延伸模組會透過 Simple Mail Transport Protocol (SMTP)，傳送包含報表本身或連至報表之 URL 連結的電子郵件訊息。 也可以將沒有 URL 連結或報表的短訊傳送到呼叫器、電話或其他裝置。 檔案共用傳遞延伸模組會將報表儲存到您網路上的共用資料夾。 您可以為所建立的檔案指定位置、轉譯格式、檔案名稱和覆寫選項。 您可以使用檔案共用傳遞封存轉譯的報表，並當成處理非常大型報表之策略的一部分。 傳遞延伸模組配合訂閱使用。 使用者建立訂閱時，選擇可用的傳遞延伸模組之一，以決定如何傳遞報表。