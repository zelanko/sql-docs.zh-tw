---
title: 以 SharePoint 模式 (SSRS) 報表伺服器上的已發行的報表項目的 URL 範例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 54cb861a-8cec-445c-875d-599fb9bd1973
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 9138f2b27518a3b271bd14628b753ba5f729b3f6
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56026529"
---
# <a name="url-examples-for-published-report-items-on-a-report-server-in-sharepoint-mode-ssrs"></a>SharePoint 模式 (SSRS) 在報表伺服器上已發行報表項目的 URL 範例
  若要將報表和相關項目發行至 SharePoint 文件庫，您可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 撰寫工具 (例如報表設計師) 來發行內容，也可以使用 SharePoint 網站動作來上傳內容。  
  
 SharePoint 網站在原生模式下，會使用不同於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器的 Web 位址。 SharePoint 網站的 Web 階層包含 SharePoint Web 應用程式、一個頂層網站、選用的子網站，以及文件庫。 您必須知道如何建立 URL 位址，該位址會指定 SharePoint 伺服器以及在 SharePoint 網站階層中的位址，讓您可以在其中發行報表或相關項目。  
  
 與報表相關的項目包括共用資料來源、子報表、鑽研報表和資源 (如網路架構影像檔)。 已發行至 SharePoint 文件庫的報表，必須在 SharePoint 文件庫中指定這些相關項目的位置。  
  
 請使用本主題中的範例，協助您建立報表方案中報表及相關項目的 URL。  
  
## <a name="site-hierarchy"></a>網站階層  
 當您將報表伺服器設定為以 SharePoint 整合模式執行時，會使用 SharePoint Web 階層，替在報表伺服器上處理與管理的項目定址。  
  
 您可以使用以下的 Web 階層元素來存取報表伺服器的內容並保護其安全性。 其他諸如清單與頁面等物件則不會用來存取報表伺服器的內容，因此不會在下表中說明。  
  
|Object|描述|  
|------------|-----------------|  
|SharePoint Web 應用程式|SharePoint Web 應用程式可以當做獨立的伺服器安裝，或安裝在包含虛擬伺服器集合的伺服器陣列下。 Web 應用程式具有一個 URL (例如， http://伺服器名稱)，而且可以包含多個網站。|  
|網站|網站可能是 Web 應用程式的上層網站或子網站。|  
|SharePoint 文件庫|文件庫包含文件或資料夾。 文件庫或文件庫中的資料夾是可以儲存報表、報表模型、共用資料來源與外部影像的唯一站台物件。|  
|項目|您可以在 URL 中參考的報表伺服器項目包括報表或子報表的報表定義、報表模型、共用資料來源或外部影像。|  
  
## <a name="url-syntax-and-rules"></a>URL 語法與規則  
 在文件庫中的每個報表伺服器項目可由完整的 URL 識別，完整的 URL 包含通訊協定前置詞、伺服器名稱、站台、文件庫、檔案名稱，以及檔案類型的副檔名。  
  
### <a name="url-for-a-sharepoint-server"></a>SharePoint 伺服器的 URL  
 當您將「報表伺服器」或「報表模型」專案從 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 部署至報表伺服器時，您必須使用指向 SharePoint 伺服器的 URL。  
  
 若要尋找欲使用之伺服器的名稱，開啟瀏覽器，然後找出您要發行報表的 SharePoint 文件庫。 伺服器名稱會出現在通訊協定前置詞的後面，例如， http://伺服器名稱。  
  
 不支援使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL Proxy 端點。 Proxy 端點包含通訊埠編號，例如， http://伺服器名稱:8080/reportserver。  
  
### <a name="url-for-a-sharepoint-server-site-or-subsite"></a>SharePoint 伺服器網站或子網站的 URL  
 當您部署報表或報表資料來源時，您必須使用指向 SharePoint 網站或子網站的 URL (如果有的話)。 在 URL 中，網站名稱會出現在伺服器名稱後面，例如， http://伺服器名稱/網站 或 http://伺服器名稱/網站/子網站。  
  
 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007 或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] Web 應用程式上，網站和子網站通常會對應到主要網站上的索引標籤。 若要尋找網站名稱或子網站名稱，按一下 [主資料夾]，然後按一下 [所有網站內容]。 捲動至底部，然後尋找 [網站與工作區]。 網站清單便會出現在此區段中。  
  
### <a name="url-for-a-sharepoint-library"></a>SharePoint 文件庫的 URL  
 當您將報表或相關項目部署至 SharePoint 文件庫時，您必須使用指向 SharePoint 文件庫的 URL。 要用於文件庫的 URL 會視您所使用的 SharePoint 版本而有所不同。  
  
 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 或 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]上，文件庫會出現在伺服器名稱後面，例如， http://*伺服器名稱/* Shared Documents。  
  
 在 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007 或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 上，文件庫會出現在網站和子網站後面。 例如， http://伺服器名稱/網站/Documents。  
  
 若要尋找新 SharePoint 文件庫或不熟悉之網站的路徑資訊，開啟瀏覽器，然後找出您要發行報表的 SharePoint 文件庫。 如果文件庫是空的，上傳任何檔案。 以滑鼠右鍵按一下檔案，然後選取 [屬性]，以開啟 [屬性] 視窗。 檔案的位址包含發行作業所需的 URL 值。  
  
### <a name="fully-qualified-urls-for-items-on-a-sharepoint-site"></a>SharePoint 網站上之項目的完整 URL  
 儲存在 SharePoint 文件庫中的項目一定會透過完整的 URL 定址，該 URL 會以 Web 應用程式開始 (http://伺服器)，當作根節點，然後以您要參考之檔案的名稱結尾。  
  
 在 URL 中的檔案名稱包含副檔名。  
  
 您無法將相對 URL 用於報表中發行至 SharePoint 網站的相依項目。 例如，您無法使用相對 URL 來參考共用資料來源、報表模型或子報表。 您永遠必須針對每個項目，指定指向 SharePoint 文件庫的完整 URL。 您無法預測相依檔案的可能位置，因為您可以用於剖析 URL 格式的網站沒有預先定義的階層。  
  
 當您發行或上傳包含相依項目的報表時，您必須在發行報表後，設定相依項目的參考。 可以在報表設計師的預覽模式中正確運作的參考不保證在發行報表後仍有效。 如需詳細資訊，請參閱本主題中的 [從撰寫工具發行到 SharePoint 文件庫](#publishingToDocLib) 。  
  
### <a name="urls-for-external-images"></a>外部影像的 URL  
 報表定義可以包含當做外部檔案儲存的影像檔。 您可以設定指向影像檔的完整 URL，在報表定義中參考該檔案。 它可以儲存在 SharePoint 網站或遠端電腦上。  
  
> [!IMPORTANT]  
>  如果外部 URL 代表 SharePoint 網站上的影像，則當您在報表產生器中預覽報表時，會出現不完整的影像圖示。 當您將報表上傳至 SharePoint 網站，並且以連線模式轉譯報表時，如果您僅具有 `View Items` 權限，則會出現不完整的影像圖示。  
  
 不管報表伺服器的模式為何，在報表中的外部影像檔參考必須是完整的 URL。 同時，參考外部影像檔通常需要您設定自動報表處理帳戶。  
  
### <a name="specifying-subreports-and-drillthrough-reports"></a>指定子報表和鑽研報表  
 子報表必須與主要報表位於相同的資料夾。 您不能指定相對資料夾。  
  
 若要指定鑽研報表，請在運算式中加入 URL。 例如，若要指定名為 SalesDetails 的報表做為鑽研報表，請在文字方塊或預留位置文字的 [動作] 中，將 ReportName 設到下列運算式：  
  
```  
="http://site/subsite/documentlibrary/SalesDetails.rdl"  
```  
  
### <a name="reserved-names-on-sharepoint-sites"></a>在 SharePoint 網站上的保留名稱  
 如果您要建立或建構指向位於 SharePoint 網站之項目的 URL，必須知道 **Personal** 和 **Sites** 這兩個字都是預設網站下的保留名稱。  
  
## <a name="examples-of-urls"></a>URL 的範例  
 將項目發行到 SharePoint 文件庫時，您必須指定指向目標文件庫的完整 URL。 完整的 SharePoint URL 包括 SharePoint Web 應用程式、站台、文件庫、資料夾 (選擇性)、檔案和副檔名。 下列範例提供數個應使用之語法的說明。  
  
|目標|範例 URL|  
|------------|-----------------|  
|SharePoint 伺服器。|http://TestServer|  
|SharePoint 伺服器網站或子網站。|http://TestServer/toplevelsite/subsite|  
|在 **或** 部署上， [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] Shared Documents [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 中的 Company Sales 範例報表。|http://TestServer/TestSite/Shared%20Documents/Company%20Sales.rdl|  
|在 **或** 執行個體上， [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] Documents/Doc [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 資料夾中的 Company Sales 範例報表。|http://TestServer/TestSite/Documents/Doc/Company%20Sales.rdl|  
|在 [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 執行個體上，[報告中心] 中的 Company Sales 範例報表。|http://TestServer/TestSite/Reports/Doc/Company%20Sales.rdl|  
  
##  <a name="publishingToDocLib"></a> 從撰寫工具發行到 SharePoint 文件庫  
 當您使用報表撰寫工具將報表和相關的檔案發行至文件庫時，加入這些檔案之前會先進行驗證。 如果您在 SharePoint 文件庫上使用 [上傳] 動作來上傳報表與相關檔案，則不會進行任何驗證檢查。 因此，在您藉由管理、編輯或執行檔案來存取報表前，將不會知道檔案是否有效。  
  
> [!NOTE]  
>  為了將報表從 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]發行到 SharePoint 網站，您可能需要將 SharePoint 網站加入您 Internet Explorer 瀏覽器的信任位置清單。  
  
### <a name="shared-data-sources"></a>共用資料來源  
 `TargetDataSourceFolder`當您從報表撰寫工具發行共用資料來源時，您可以設定專案屬性  目標資料來源資料夾必須是指向 SharePoint 文件庫的 URL。 不像在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式下，您無法指定相對資料夾，因為相對路徑無效。 如果在 Document Library 路徑下沒有資料夾存在，則會建立一個。  
  
 當您將共用資料來源 (.rds) 檔發行到 SharePoint 網站時，這會將資料來源檔的副檔名變更為 .rsds。 .rsds 檔無法從 SharePoint 網站儲存到本機，也無法匯入到現有的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 專案中。 副檔名為 .rds 和 .rsds 的共用資料來源不可互換。  
  
#### <a name="shared-data-sources-from-report-designer"></a>來自報表設計師的共用資料來源  
 如果您要從報表設計師專案發行共用資料來源，您可以使用指定目標文件庫的 URL，或者您可以將屬性留空。 不像在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式下，您無法指定相對資料夾，因為相對路徑無效。 如果在 Document Library 路徑下沒有資料夾存在，則會建立一個。 如果您將目標資料來源資料夾留空，則會在目標報表資料夾中發行資料來源。  
  
### <a name="file-names"></a>檔案名稱  
 在 URL 中的報表項目檔案名稱必須包含副檔名。 副檔名會決定檔案類型。 當您從報表撰寫工具發行報表項目時，會自動包含副檔名。 如果您要將報表項目上傳至 SharePoint 文件庫，您必須包含副檔名。  
  
 如果沒有為您要上傳到 SharePoint 網站的項目指定副檔名，則會發生 `rsInvalidDataSourceReference` 錯誤。 檔案名稱不得包含 SharePoint 應用程式不視為有效檔案名稱字元的字元。 不包含下列字元: # %& *: \< > 嗎？ / { | }。  
  
## <a name="differences-between-uploading-and-publishing"></a>上傳與發行之間的差異  
 當您使用報表設計師或報表產生器，將報表和相關的檔案發行至文件庫時，加入這些檔案之前會先進行驗證。 如果您在 SharePoint 文件庫上使用 [上傳] 動作來上傳報表與相關檔案，則不會進行任何驗證檢查。 因此，在您藉由管理、編輯或執行檔案來存取報表前，將不會知道檔案是否有效。  
  
## <a name="updating-a-published-item"></a>上傳已發行的項目  
 在您已經將項目發行或上傳到 SharePoint 文件庫後，您應該先將該項目從文件庫中簽出，然後再更新它。 如果報表簽出給您，則您將是具有變更報表權限的唯一使用者。 當您完成時，請將其簽入。  
  
 如果您在上傳或發行報表前沒有先簽出文件 (例如，藉由上傳與現有項目具有相同名稱的項目)，報表伺服器會為您簽出該文件、加入更新的報表做為現有項目的新版本，然後再將該文件簽入。  
  
## <a name="external-images-as-resources"></a>當做資源的外部影像  
 以原生模式執行的報表伺服器支援資源的概念，這個概念的定義為，在報表伺服器上儲存並保護其安全性，但不由報表伺服器所處理的任何檔案。 在原生模式下，這可能是任何類型的檔案。  
  
 當報表伺服器以 SharePoint 整合模式執行時，資源概念的定義則比較窄化。 報表伺服器會保留資源的概念，以儲存參考外部影像的報表。 如果報表是快照集或保留給內部使用的副本，則也適用這個概念。  
  
## <a name="see-also"></a>另請參閱  
 [將報表發行到 SharePoint 文件庫](../reports/publish-a-report-to-a-sharepoint-library.md)   
 [將共用資料來源發行至 SharePoint 文件庫](../reports/publish-a-shared-data-source-to-a-sharepoint-library.md)   
 [專案屬性頁對話方塊](project-property-pages-dialog-box.md)  
  
  
