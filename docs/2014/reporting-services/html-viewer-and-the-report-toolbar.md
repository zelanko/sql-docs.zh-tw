---
title: HTML 檢視器和報表工具列 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- HTML Viewer [Reporting Services]
- report toolbar [Reporting Services]
ms.assetid: cd86b319-babd-45af-a6a4-f659fdcc40c3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 86ac5b6da861477bfd5b8e92feac97068ca5adc9
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59934054"
---
# <a name="html-viewer-and-the-report-toolbar"></a>HTML 檢視器和報表工具列
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 提供了 HTML 檢視器，可用來從報表伺服器要求報表時，視需要顯示這些報表。 HTML 檢視器提供以 HTML 檢視報表的架構。 其中包含報表工具列、參數區段、認證區段以及文件對應。 HTML 檢視器中的報表工具列含有可用來處理報表的功能，包括可以讓您以非 HTML 格式檢視報表的匯出選項。 只有在開啟設定為使用參數和文件引導模式控制項的報表時，才會顯示參數區段和文件引導模式。  
  
> [!NOTE]  
>  雖然您無法修改報表工具列，但是您可以設定報表 URL 上的參數，以在報表中隱藏此工具列。 如需隱藏報表工具列的詳細資訊，請參閱 [URL 存取參數參考](url-access-parameter-reference.md)。  
  
## <a name="report-toolbar"></a>報表工具列  
 報表工具列會針對以 HTML 轉譯延伸模組轉譯的報表，提供頁面導覽、顯示比例、重新整理、搜尋、匯出、列印和資料摘要功能。  
  
 列印功能是選擇性的。 可用時，印表機圖示就會顯示在報表工具列中。 首次使用時，按一下印表機圖示會下載您必須安裝的 ActiveX 控制項。 控制項安裝完成之後，按一下 [印表機] 圖示就會開啟 [列印] 對話方塊，讓您選取電腦已設定的印表機。 列印可用性會由伺服器設定與瀏覽器設定來決定。 如需詳細資訊，請參閱[使用列印控制項從瀏覽器列印報表 &#40;報表產生器及 SSRS&#41;](report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md) 和[啟用和停用 Reporting Services 的用戶端列印](report-server/enable-and-disable-client-side-printing-for-reporting-services.md)。  
  
 報表工具列會與下列圖例所顯示的工具列相似。 您看到的報表工具列可能會與此圖例有所不同，依可用的報表功能或轉譯選項而定。  
  
 ![Report toolbar](media/htmlviewer-toolbar.gif "Report toolbar")  
  
 下表描述報表工具列的常用功能。 每一項功能都可以透過存取該功能的控制項來識別。  
  
|使用這個圖示或控制項||若要|  
|------------------------------|-|--------|  
|![頁面導覽控制項](media/htmlviewer-pagenav.gif "頁面導覽控制項")|**頁面導覽控制項**|開啟報表的第一頁或最後一頁、逐頁捲動報表和開啟報表中的特定頁面。 若要檢視特定頁面，請輸入頁碼然後按 ENTER。|  
|![頁面顯示控制項](media/htmlviewer-pagesize.gif "頁面顯示控制項")|**頁面顯示控制項**|放大或縮小報表頁面的尺寸。 除了百分比架構的變更之外，您還可以選取 [頁寬] 使其符合瀏覽器視窗中報表頁面的水平長度，或選取 [整頁] 使其符合瀏覽器視窗中報表的垂直長度。 [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 5.5 和更新的版本可以支援 [顯示比例] 選項。|  
|![搜尋欄位](media/htmlviewer-search.gif "搜尋欄位")|**搜尋欄位**|輸入想要尋找的單字或片語 (最大長度為 256 個字元)，即可搜尋報表中的內容。 搜尋不區分大小寫，從目前所選取的頁面或區段開始。 只有可見的內容會包含在搜尋作業中。 若要搜尋相同值的下一個出現位置，請按 **[下一個]**。|  
|![匯出格式](media/htmlviewer-export.GIF "匯出格式")|**匯出格式**|開啟新的瀏覽器視窗，並以選取的格式來轉譯報表。 可用的格式會由報表伺服器上安裝的轉譯延伸模組決定。 建議使用 TIFF 來列印。 按一下 [匯出] 就能夠以所選取格式檢視報表。|  
|![文件引導模式圖示](media/htmlviewer-docmap.GIF "文件引導模式圖示")|**文件引導模式圖示**|在含有文件引導模式的報表中，顯示或隱藏文件引導模式。 文件引導模式是一種報表瀏覽控制項，類似於網站的導覽窗格。 按一下文件引導模式中的項目，即可導覽至特定群組、頁面或子報表。|  
|![印表機圖示](media/printer-icon.gif "印表機圖示")|**印表機圖示**|開啟 [列印] 對話方塊，使您可以指定列印選項和列印報表。 首次使用時，按一下此圖示會提示您下載列印控制項。|  
||**顯示與隱藏圖示**|顯示或隱藏包含參數之報表中的參數值欄位和 [檢視報表] 按鈕。|  
|![報表工具列上的瀏覽器重新整理按鈕](media/htmlviewer-refresh.GIF "報表工具列上的瀏覽器重新整理按鈕")|**報表重新整理圖示**|重新整理報表。 會重新整理使用中報表的資料。 會從儲存快取報表的位置重新載入報表。|  
|![htmlviewer_datafeed](media/htmlviewer-datafeed.gif "htmlviewer_datafeed")|**資料摘要圖示**|從報表產生資料摘要。|  
  
### <a name="about-export-formats"></a>關於匯出格式  
 您可從報表工具列中選取以各種格式來檢視報表。 可用的格式會由報表伺服器上安裝的轉譯延伸模組決定。 當您選取另一種格式時，系統會使用第二個瀏覽器視窗來顯示報表，並使用與您所選取之匯出格式相關聯的檢視器。 如果所選取的格式沒有可用的檢視器，您可以選取其他格式。  
  
 預設的報表伺服器安裝中，有包含下列匯出格式。 您可用的匯出格式清單，可能會與此處所列的清單有所不同。  
  
|匯出格式|描述|  
|-------------------|-----------------|  
|XML|以 XML 語法檢視報表。 在新的瀏覽器視窗中，以 XML 檢視報表。|  
|CSV|以逗號分隔格式來檢視報表。 報表會在與 CSV 檔案類型相關聯的應用程式中開啟。|  
|Acrobat (PDF) 檔案|使用用戶端 PDF 檢視器來檢視報表。 您必須擁有協力廠商 PDF 檢視器 (例如 Adobe Acrobat Reader)，才能使用此格式。|  
|[匯出]|在 [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 中檢視報表。|  
|網頁封存|以 MIME 編碼的 HTML 格式檢視報表，在報表中保留影像和連結的內容。|  
|TIFF 檔案|以預設的 TIFF 檢視器檢視報表。 對於某些 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 用戶端來說，這會是 Windows 圖片和傳真檢視器。 選取此格式就能夠以頁面導向的配置來檢視報表。|  
  
## <a name="parameters"></a>參數  
 參數是用來選取特定資料的值 (亦即，它們是用來完成選取報表資料或篩選結果集的查詢)。 報表中常用的參數包括日期、名稱和 ID。 指定參數的值時，報表只會包含符合該值的資料；例如，以「員工識別碼」參數為基礎的員工資料。 參數會對應至報表的欄位。 指定參數之後，請按一下 [檢視報表] 以取得資料。  
  
 報表作者會定義每一份報表的有效參數值。 報表管理員也可以設定參數值。 若要找出報表的有效參數值，請洽詢報表設計師或管理員。  
  
## <a name="credentials"></a>認證  
 認證是授權存取資料來源的使用者名稱和密碼值。 指定認證之後，請按一下 [檢視報表] 以取得資料。 如果報表要求您登入，則您獲准查看的資料可能會與另一位使用者所見的資料不同。 因此，兩位使用者可以執行相同報表而取得不同結果。 此外，有些報表會包含隱藏的區域，顯示與否將根據使用者登入認證或在報表中所做的選擇而定。 報表中的隱藏區域會排除在搜尋作業之外，與報表各部分都可見時得到不同的搜尋結果。  
  
## <a name="see-also"></a>另請參閱  
 [指定報表資料來源的認證及連接資訊](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [匯出報表&#40;報表產生器及 SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
