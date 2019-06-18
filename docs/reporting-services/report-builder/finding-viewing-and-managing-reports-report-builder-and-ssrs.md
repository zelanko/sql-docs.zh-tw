---
title: 尋找、檢視和管理報表 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 05/20/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 5599300d-6bcd-4704-aba5-fa98e01c78a9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7a93f71f886484d38996a867bebbc6ef32c33c86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66175632"
---
# <a name="finding-viewing-and-managing-reports-report-builder-and-ssrs-"></a>尋找、檢視和管理報表 (報表產生器及 SSRS)
  在報表產生器中，您可以瀏覽報表伺服器或 SharePoint 網站上的資料夾，以便尋找報表、共用資料來源、模型，以及其他相關的報表項目，並瀏覽電腦以尋找本機報表。 為了更容易尋找報表，報表產生器會維護一份最近使用之伺服器及網站的清單，而且可以直接存取電腦檔案系統中的 [桌面]、[我的文件] 和 [我的電腦] 資料夾。  
  
 在報表設計師中，您也可以瀏覽電腦以尋找本機報表。 將報表部署至報表伺服器或 SharePoint 網站之後，您就可以透過使用 Web 入口網站來瀏覽報表伺服器，或搜尋 SharePoint 網站以尋找報表。 當您部署報表和相關的項目之後，它們會維持可在本機使用的狀態。  
  
> [!NOTE]  
> 您可以在本機模式下使用報表產生器，或連接到報表伺服器。 當您沒有與報表伺服器建立使用中的連接時，系統會套用特定的限制。  
  
 若要從報表產生器找出報表伺服器或 SharePoint 網站上的報表，您必須提供報表伺服器或 SharePoint 網站的 URL。 當您第一次安裝報表產生器時，可以指定要使用的 URL。 這是在您儲存或開啟報表時，報表產生器預設連接的伺服器或網站。  
  
 當您建立或更新報表時，可以在報表產生器和報表設計師中預覽報表，也可以使用 Web 入口網站在報表伺服器上檢視與管理，或在發行報表後使用內建的 SharePoint 工具和功能，在與 Reporting Services 整合的 SharePoint 網站上檢視與管理。 如需詳細資訊，請參閱 [在報表產生器中預覽報表](../../reporting-services/report-builder/previewing-reports-in-report-builder.md) 和 [預覽報表](../../reporting-services/reports/previewing-reports.md)。  
  
 當您在報表產生器和報表設計師中預覽報表，或在 Web 入口網站或 SharePoint 網站中檢視報表時，資料會重新整理，而且報表會從資料來源顯示報表使用的目前資料。 如果您想要檢視報表，而不重新整理其資料，您可以使用包含已發行之報表的報表記錄和快取資料。 在報表產生器和報表設計師中預覽報表時，您無法使用這些功能。  
  
> [!NOTE]  
> [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="FindingAndViewingReportsRB30"></a> 在報表產生器中尋找及檢視報表  
 若要尋找您要使用的報表，或選取要在報表中使用的共用資料來源、影像或子報表，請瀏覽您的電腦，報表伺服器上的資料夾，或與 Reporting Services 整合的 SharePoint 網站。  
  
 若要尋找報表伺服器上的報表，您必須指定報表伺服器的 URL，並具備資料夾的適當權限，以讓您讀取和儲存報表項目。 請向報表伺服器的系統管理員要求適當的 URL 和權限。  
  
 在報表產生器中尋找並開啟報表之後，您可以預覽並進行變更。 預覽時，您會看到目前的資料。 如需詳細資訊，請參閱 [Previewing Reports in Report Builder](../../reporting-services/report-builder/previewing-reports-in-report-builder.md)。  
  
 報表產生器可協助您進行下列工作：  
  
-   **尋找報表** ：當您瀏覽報表時，可以使用熟悉的 Microsoft Office 樣式的 **[開啟檔案]** 對話方塊，此對話方塊已針對報表產生器進行自訂。 您可以瀏覽報表伺服器或檔案系統上的資料夾，包括 [我的報表]、[站台和伺服器]、[桌面]、[我的文件] 和 [我的電腦]。 [站台和伺服器] 提供最近使用過的伺服器清單。  
  
-   **尋找共用的資料來源** ：當您瀏覽共用資料來源時，可以從最近使用過的清單挑選，或瀏覽到與報表位置相同之報表伺服器上的其他資料夾。  
  
-   **檢視報表** ：建立或更新報表時，可以在報表產生器中進行預覽。 當報表產生器連接至報表伺服器時，報表伺服器會載入並處理報表；否則，報表會在本機進行處理。 報表產生器中的報表檢視器會顯示轉譯的報表。  
  
 
##  <a name="ViewingAndManagingReportServer"></a> 檢視和管理報表伺服器上的報表  
 您可以使用 Web 入口網站來檢視和管理報表伺服器上的報表。 瀏覽伺服器上的資料夾以找出報表、執行報表以便在瀏覽器中檢視這些報表，然後執行管理工作。  
  
 Web 入口網站可以協助您進行下列管理工作：  
  
-   檢視及更新報表的屬性、共用資料來源，以及其他報表項目。  
  
-   上傳報表並建立報表的新共用資料來源。  
  
-   建立排程以便在指定的時間和間隔執行報表。  
  
-   建立、變更或刪除報表的訂閱。  
  
-   建立報表記錄，並指定要保留在報表記錄中的報表快照集數目。  
  
-   在伺服器上建立新的資料夾，以便使用您想要的方式組織您的報表。  
  
 報表伺服器的系統管理員可能會為您完成以上某些工作。 若要深入了解報表伺服器上執行的工作，請參閱 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)。  
  
Web 入口網站通常包含資料夾、報表、資料來源及 [我的報表] 資料夾。 [我的報表] 是個人的工作空間，可以用來儲存和使用您擁有的報表。 其他報表伺服器資料夾都是公開的，通常使用者必須具備進階權限才可以加入或修改資料夾內容。 您可以在 [我的報表] 中建立子資料夾，以進一步組織您的報表。  
  
 Web 入口網站會使用 Reporting Services HTML 檢視器中顯示報表。 HTML 檢視器會提供架構，以便使用 HTML 檢視報表，而且包含報表工具列、參數區段、認證區段及文件引導模式。 報表工具列會提供頁面巡覽，縮放、重新整理、搜尋、匯出、列印及資料摘要功能。 透過 URL 存取報表時，報表工具列也會顯示在報表上方的瀏覽器視窗中。 列印功能是選擇性的，而且必須由您的系統管理員開啟。 可用時，印表機圖示就會顯示在報表工具列中。 下列圖例會顯示 Web 入口網站中報表工具列的特寫。  
  
 ![Web 入口網站中的報表工具列](../../reporting-services/report-builder/media/finding-viewing-and-managing-reports-report-builder-and-ssrs/report-toolbar-in-the-web-portal.png)  
  
當您執行報表時，您可以將報表匯出成其他格式，例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 或 PDF。 您也可以使用資料轉譯延伸模組 (例如，逗號分隔值 (CSV) 轉譯延伸模組) 來匯出報表，然後使用 CSV 資料檔做為其他應用程式的輸入。 如需有關如何匯出報表的詳細資訊，請參閱[匯出報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)。
  
 選取和執行報表最簡單的方法，是開啟 Web 入口網站，然後搜尋或瀏覽至您要檢視的報表。 如需有關如何開啟報表的逐步指示，請參閱[開啟及關閉報表](../../reporting-services/reports/open-and-close-a-report-report-manager.md)。  
  
 執行報表後，您可以進行重新整理以查看新的資料。  
  
### <a name="refreshing-reports"></a>重新整理報表  
 報表資料經常變更，因此，您可以重新整理報表以檢視最新的資料。 您可以使用三種不同的方法來重新整理報表。  
  
|選項|結果|  
|------------|------------|  
|瀏覽器視窗上的 **[重新整理]** 按鈕。|顯示儲存在工作階段快取中的報表。 使用者開啟報表時，便會建立工作階段快取。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會使用瀏覽器工作階段，在報表開啟時維持一致的檢視方式。|  
|![報表工具列上的瀏覽器重新整理按鈕](../../reporting-services/report-builder/media/finding-viewing-and-managing-reports-report-builder-and-ssrs/browser-refresh-button-on-report-toolbar.png)|當您按一下報表工具列的 **[重新整理]** 按鈕時，報表伺服器會重新執行查詢，如果報表為視需要執行，還會更新報表資料。 如果報表已快取或為快照集， **[重新整理]** 會顯示儲存在報表伺服器資料庫中的報表。|  
|CTRL+F5 組合鍵|與按一下報表工具列的 **[重新整理]** 按鈕的結果相同。|  
  
  
##  <a name="ViewingAndManagingSharePointSite"></a> 從 SharePoint 網站檢視和管理報表伺服器項目  
 當系統管理員將報表伺服器設定為以 SharePoint 整合模式執行時，您就可以從 SharePoint 網站檢視和管理報表及其他報表伺服器項目。  
  
 SharePoint 網站包含用於設定資料來源屬性、報表記錄、報表處理選項、排程、訂閱、報表參數和建立共用排程的頁面。 您可以在 SharePoint 網站上管理報表伺服器項目，方法就像使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的其他工具來建立和管理這些項目一樣。  
  
 若要存取應用程式頁面，請從報表的下拉式功能表選取項目專屬的動作，或選取您先前加入到 SharePoint 文件庫的其他報表伺服器項目。 根據項目和權限，您也可能可以在報表產生器中建立報表、產生模型和設定模型項目安全性。  
  
 如需 Reporting Services 和 SharePoint 技術的詳細資訊，請參閱[設定和管理報表伺服器 &#40;Reporting Services SharePoint 模式&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md)。
  
### <a name="finding-report-server-items-on-a-sharepoint-site"></a>在 SharePoint 網站上尋找報表伺服器項目  
 您必須要先能找到項目，才能設定屬性。 報表伺服器項目一律儲存在程式庫或程式庫內的資料夾中。  
  
 存取 SharePoint 網站時，您會看到 [瀏覽] 頁面和 [程式庫工具] 索引標籤。[瀏覽] 頁面會列出程式庫以及所選程式庫的內容。 您可以檢視文件庫中的報表與其他項目、瀏覽資料夾，以及搜尋網站來尋找項目。  
  
 若要在 SharePoint 網站上區分報表伺服器項目和其他項目，可以使用圖示以視覺方式識別項目，或將滑鼠游標置於類型上，然後檢視副檔名。 下列影像顯示**報表**文件庫中的資料夾與報表定義：  
  
 ![具有報表伺服器項目的 SharePoint 文件庫](../../reporting-services/report-builder/media/rs-sharepointlibrary.gif "具有報表伺服器項目的 SharePoint 文件庫")  
  
### <a name="viewing-reports"></a>檢視報表  
 您上傳到 SharePoint 文件庫的報表定義 (.rdl 檔案) 是透過由 Reporting Services 增益集安裝的報表檢視器 Web 組件來檢視。 當您安裝增益集時，會自動定義 .rdl 檔案關聯。 當您選取報表時，會自動在 Web 組件中開啟。 在報表開啟後，就可以使用 Web 組件中所含的報表工具列來導覽頁面、搜尋、縮放和列印報表。 這個工具列包含 [匯出至資料摘要] 選項和 **[動作]** 功能表，前者可將報表匯出至 Atom 資料摘要，後者則具有列印、訂閱及將報表匯出成不同格式 (例如 PDF、Word 和 Excel) 的選項。 您也可以從 **[動作]** 功能表，在報表產生器中開啟報表。 下列影像顯示一份報表，以及 **[動作]** 功能表中 [匯出] 選項的選項。  
  
 ![rs_SharePointRunReport](../../reporting-services/report-builder/media/rs-sharepointrunreport.gif "rs_SharePointRunReport")  
  
### <a name="managing-items-through-actions"></a>透過動作管理項目  
 下拉式功能表上的動作可支援每個項目的管理工作。 根據您的權限，每個項目都具有通用的動作，對於儲存在 SharePoint 程式庫中的項目而言，這些都是標準動作。 **[檢視屬性]** 和 **[編輯屬性]** 是通用動作的範例。 自訂動作可提供項目特定的管理功能。 下列影像顯示報表定義的動作。 報表定義的自訂動作範例包括 **[管理訂閱]** 和 **[管理處理選項]** ：  
  
 ![報表伺服器項目的功能表命令](../../reporting-services/report-builder/media/rs-ecbforrsitems.gif "報表伺服器項目的功能表命令")  
  
  
##  <a name="DeskTop"></a> 在桌面應用程式中檢視報表  
 您可以完全略過瀏覽器檢視，改用桌面應用程式 (例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel) 作為報表檢視器。 若要這樣做，請定義指定桌面應用程式格式和共用資料夾目的地的訂閱。 報表伺服器會將報表建立成應用程式檔案，加上副檔名，然後將報表儲存成硬碟中的檔案。 之後，您便可以改用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel (或其他應用程式) 取代瀏覽器來檢視報表。  
  
  
##  <a name="AboutUserSessions"></a> 關於使用者工作階段  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會使用瀏覽器工作階段來維持檢視報表時的一致性。 工作階段是以瀏覽器連接為基礎，並非以驗證的使用者為基礎。 每次使用者在新的瀏覽器視窗中開啟報表時，就會建立新的工作階段。 建立瀏覽器工作階段之後，您就可以繼續使用工作階段開始時所開啟的報表版本，即使該報表後來已經在報表伺服器上修改過也一樣。 例如，若您在下午 11:00 開啟報表，且報表作者在下午 11:01 重新發行相同的報表，則您的工作階段期間將會繼續使用您所開啟的版本。  
  
 如果您在相同工作階段內使用 **[重新整理]** 按鈕重新整理報表，則會顯示報表的原始工作階段版本。 如果您使用報表工具列上的 **[重新整理]** 按鈕來重新整理視需要執行的報表，則會重新執行報表並顯示新資料 (如果有的話)。  
  
 工作階段資訊會儲存在報表伺服器的暫存資料庫中。 報表伺服器不會使用 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 工作階段管理。 如果您重新啟動伺服器或執行資料庫復原作業，並不會還原工作階段狀態。 如需工作階段管理的詳細資訊，請參閱 [識別執行狀態](../../reporting-services/report-server-web-service-net-framework-soap-headers/identifying-execution-state.md)。  
  
 
##  <a name="InThisSection"></a> 本節內容  
 下列文章提供有關檢視與管理報表的其他資訊。  
  
 [尋找、檢視和管理報表](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)
  
 [使用瀏覽器尋找及檢視報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/finding-and-viewing-reports-with-a-browser-report-builder-and-ssrs.md)  
 描述如何使用 URL 尋找和檢視報表。  
  
 [在報表產生器中預覽報表](../../reporting-services/report-builder/previewing-reports-in-report-builder.md)  
 描述如何在您建立或更新報表時預覽報表。  
  
## <a name="see-also"></a>另請參閱  
 [儲存報表 &#40;報表產生器&#41;](../../reporting-services/report-builder/saving-reports-report-builder.md)   
 [SQL Server 的報表產生器](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
 