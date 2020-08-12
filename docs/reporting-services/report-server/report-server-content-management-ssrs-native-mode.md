---
title: 報表伺服器內容管理 (原生模式) | Microsoft Docs
description: 了解 Reporting Services 內容管理的入口網站和新入口網站體驗。 透過屬性和安全性設定來管理項目。
ms.date: 06/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- administering Reporting Services
- published reports [Reporting Services], managing
- report servers [Reporting Services], content management
- content management [Reporting Services]
ms.assetid: 641961ac-53a5-4997-9d42-cf4ecce1f892
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 12832f724da36f6359f34fd2fd950ba804619c45
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547244"
---
# <a name="report-server-content-management-ssrs-native-mode"></a>報表伺服器內容管理 (SSRS 原生模式)
在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中，內容管理是指管理報表伺服器項目。 所有項目都可以透過屬性和安全性設定單獨進行管理， 而任何一個項目都可以移至報表伺服器資料夾命名空間內的不同位置。 若要有效管理項目，您必須了解內容管理員所執行的工作。 從 SQL Server 2016 Reporting Services 或更新版本 (SSRS) CTP 3.2 開始，[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 入口網站可供使用。 本文會探討入口網站和新的入口網站體驗。  
  
> [!NOTE]  
> 內容管理與報表伺服器管理不同。 如需如何管理報表伺服器執行環境的詳細資訊，請參閱 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)。  
  
 內容管理包括下列工作：  
  
-   藉由套用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]所提供以角色為基礎的安全性，保護報表伺服器網站及項目的安全。  
  
-   藉由加入、修改和刪除資料夾，建立報表伺服器資料夾階層。  
  
-   設定套用至報表伺服器所管理之項目的預設值及屬性。 例如，您可以設定最大基準值，來決定報表記錄的儲存原則。  
  
-   建立可以用來取代報表特定資料來源連接的共用資料來源項目。 發行者或內容管理員可以選取和報表原始定義不同的資料來源；例如，以實際執行的資料庫的參考取代測試資料庫的參考。  
  
-   建立可用來取代報表特有和訂閱特有排程的共用排程，讓您更方便地隨著時間維護排程資訊。  
  
-   藉由從資料存放區擷取資料，建立可產生收件者清單的資料驅動訂閱。  
  
-   藉由建立報表處理排程，並指定何者可依需求執行以及何者要從快取載入，即可平衡伺服器的報表處理負荷。  
  
-   使用預先定義的角色提供權限以執行管理工作：**系統管理員**和**內容管理員**。 您必須被指派至這兩種角色，才能有效管理報表伺服器內容。  
  
用於管理報表伺服器內容的工具包括 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 與入口網站。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 可讓您設定預設值和啟用功能。 入口網站是用來將報表伺服器項目與作業的存取權授與使用者、檢視和使用報表與其他內容類型，以及檢視和使用所有共用項目與報表散發功能。 入口網站是更新的網站，允許使用大多數已過時的報表管理員功能。 如需詳細資訊，請參閱 [Reporting Services 工具](../../reporting-services/tools/reporting-services-tools.md)。  
  
##  <a name="report-server-items"></a><a name="bkmk_ReportServerItems"></a> 報表伺服器項目  
 報表伺服器項目包括報表、共用資料來源、共用資料集、報表組件、資源 (儲存在報表伺服器上但不由報表伺服器處理的項目) 及資料夾。 項目可能取決於其他項目，例如，報表可能取決於其參考的共用資料來源。 如果您移動相依項目，報表伺服器會自動更新參考資訊。  
  
 您可以將報表伺服器項目移至報表伺服器資料夾階層中不同的資料夾位置。 當您移動項目時，所有屬性 (包括安全性設定) 都會跟著項目移到新位置。 您移動資料夾時，資料夾內的所有項目都會隨著一起移動。  
  
> [!NOTE]  
>  針對 CTP 3.2，如果您想要移動某項目的位置，您需要在入口網站中執行該動作。  
  
 在入口網站中，資料夾階層中會指出可以移動的項目。 下列影像顯示每一個可移動項目的圖示。  
  
  ![可移動項目的報表伺服器圖示](media/report-server-content-management-ssrs-native-mode/report-server-content-icons.png)

 並非所有的項目都可以移動。 您無法移動與報表相關聯的項目，例如訂閱或報表記錄。 那些項目會隨著相關聯的報表移動。 同樣地，您無法移動存在於資料夾階層之外的項目 (例如共用排程)。 如果您沒有權限也無法移動項目。 在您的角色指派中為目標項目選取下列工作時，即涵蓋移動項目的權限：「管理報表」、「管理資料夾」，以及「管理資料來源」。  
  
##  <a name="folders"></a><a name="bkmk_Folders"></a> 資料夾  
 資料夾階層用於處理由報表伺服器所儲存及管理的項目。  根據預設，資料夾結構包含一個稱為 [主資料夾] 的根節點以及多個支援選擇性 [我的報表] 功能的保留資料夾。 其他為使用者定義的資料夾。 如果您要授與相同的存取層級給多個項目，報表伺服器資料夾相當實用。 您在資料夾上設定的權限可以由資料夾中的項目繼承，以及繼承至從該資料夾分支出去的其他資料夾。 例如，您可以在 [主資料夾] 下建立依組資料夾，指派小組權限給每個資料夾，然後讓小組成員視需要自訂小組資料夾底下的資料夾。  
  
 如果您使用瀏覽器直接連接到報表伺服器，則資料夾結構的根節點就是報表伺服器虛擬目錄的名稱。 您可以依需要從根節點建立、修改和刪除資料夾，以組織報表伺服器內容。 您可以將內容加入資料夾、在資料夾之間移動項目、修改資料夾名稱或位置，以及刪除不再需要的資料夾。  
  
 資料夾是已發行項目的虛擬容器，您可以透過入口網站或瀏覽器與報表伺服器的連接來存取。 資料夾與其內容實際上都不存在於檔案系統內。 而是儲存在報表伺服器資料庫中，而且可以透過報表伺服器 Web 服務端點存取。 報表伺服器資料夾命名空間是包含根節點、預先定義的資料夾與使用者自訂資料夾的階層。 命名空間會唯一識別儲存在報表伺服器上的項目。 它提供以 URL 指定項目的定址配置。 當您選取或尋找報表時，資料夾路徑會變成該報表之 URL 的一部分。  
  
 使用資料夾的方式，取決於屬於您角色指派的工作。 如果您要使用預設安全性，內容管理員和發行者可以建立和管理資料夾。 如果您使用自訂角色指派，角色指派就必須包括支援資料夾管理的工作。 如需角色指派和工作的詳細資訊，請參閱[在原生模式報表伺服器上授與權限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)[工作和權限](../../reporting-services/security/tasks-and-permissions.md)。  
  
 報表伺服器資料夾可以包含下列項目：  
  
-   報表  
  
-   共用資料來源  
  
-   共用資料集  
  
-   報表組件  
  
-   KPI  
  
-   行動報表  
  
-   資源 (儲存在報表伺服器上，但不是由報表伺服器處理的項目)  
  
-   其他資料夾  
  
### <a name="reserved-folders"></a>保留的資料夾  
 預先定義的資料夾在 Reporting Services 中是被保留的；不可以將它們移動、重新命名或刪除。 使用者自訂資料夾包含具有將項目加入資料夾之權限的使用者或報表伺服器管理員所建立的資料夾。  
  
 下表描述預先定義的資料夾，資料夾會錨定資料夾階層並提供數種功能的架構。  
  
|資料夾|目的|  
|------------|-------------|  
|Home|資料夾階層的根節點。|  
|使用者|啟用 [我的報表] 功能時，會出現此資料夾。 它包含使用 [我的報表] 功能之所有使用者的子資料夾，而且只有報表伺服器管理員能夠存取。 每個子資料夾名稱與使用者的名稱相符。|  
|我的報表|提供每個使用者的個人工作空間。|  
  
### <a name="creating-folders"></a>建立資料夾  
 您可以在階層中任何可用的資料夾內建立資料夾。  
  
 如果您要針對限制特定報表和模型之存取權的目的建立資料夾，就應該指定允許使用者瀏覽資料夾路徑中之父資料夾 (但無法檢視其內容) 的角色指派。  
  
### <a name="modifying-folder-properties"></a>修改資料夾屬性  
 在資料夾建立之後，您可以修改屬性以重新命名資料夾、新增或修改描述，或移動資料夾到其他位置。 這些屬性可從資料夾的 [一般] 屬性頁面存取。 如需設定授與資料夾存取權之屬性的詳細資訊，請參閱 [保護資料夾的安全](../../reporting-services/security/secure-folders.md)。  
  
### <a name="deleting-folders-and-folder-contents"></a>刪除資料夾與資料夾內容  
 當您刪除資料夾時，同時會刪除其包含的所有項目。 在刪除資料夾前，應該檢查其內容，以判斷是否包含資料夾階層其他部分的項目可能會參考或使用的項目。 參考的項目包括支援連結報表、共用資料來源，以及資源的報表定義。  
  
 如果您刪除有一或多個連結報表參考到的報表，則刪除報表之後連結報表就變成無效。 因為報表並不保留以其做為基礎之連結報表的相關資訊，所以您無法在事先判斷哪些連結報表會受到影響。 然而，您可以檢閱連結報表的屬性，來了解它以哪些報表做為基礎。 相對地，共用資料來源項目會列出目前使用該項目的所有報表，如此您可以輕易地判斷連接資訊是否正在使用。 如需詳細資訊，請參閱[建立、修改和刪除共用資料來源 &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)。 最後，報表所使用的資源，並不會識別這些報表。  
  
 在刪除資料夾之前，請考慮是否需要保留任何即將刪除之報表的報表記錄，或屬於報表的報表特定建構 (例如，資料驅動訂閱)。 如果您可能需要其中任何資訊，請在刪除資料夾之前將項目移出該資料夾。  
  
 資料夾中之項目的可見性，會依角色指派 (亦即，檢視某個項目的權限) 和資料夾適用的檢視選項而定。 在入口網站中，您可以將 [內容] 頁面設定為清單檢視或詳細資料檢視。 在某些情況下，報表或項目可能會在清單檢視中隱藏。 刪除資料夾內容之前，務必要在詳細資料檢視中檢視資料夾。  
  
##  <a name="resources"></a><a name="bkmk_Resources"></a> 資源  
 資源是指儲存在報表伺服器上，但並非由報表伺服器所處理的 Managed 項目。 一般而言，資源會提供外部內容給報表使用者。 範例包括 .jpg 檔、包含空間資料的 ESRI 形狀檔，或 HTML 檔中描述報表所使用之商務規則的影像。 雖然此 JPG、SHP 或 HTML 檔會儲存在報表伺服器上，但是報表伺服器會直接將此檔案傳遞至瀏覽器而非先處理它。 如需詳細資訊，請參閱[影像 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md) 和[地圖 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md) 的＜將資料新增至地圖＞一節。  
  
### <a name="adding-and-viewing-a-resource"></a>加入和檢視資源  
 若要將資源加入至報表伺服器，您可以上傳或發行檔案：  
  
|作業|檔案類型|  
|---------------|---------------|  
|上傳|若要上傳資源，您必須使用入口網站 (如果報表伺服器以原生模式執行的話) 或 SharePoint 網站上的應用程式頁面 (如果伺服器以 SharePoint 整合模式執行的話)。 如需詳細資訊，請參閱[在報表伺服器中上傳檔案或報表](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)或[將文件上傳到 SharePoint 文件庫 &#40;SharePoint 模式的 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)。|  
|發佈|專案中不是報表、報表組件、資料來源或資料集的所有檔案都會當做資源上傳。 若要發行資源，請在報表設計師中，將現有的項目加入至專案，然後將此專案發行至報表伺服器。|  
  
 所有資源都會先在檔案系統上以檔案的形式產生，然後再上傳至報表伺服器。 除了 ASP.NET 所加諸的 4 MB 預設檔案大小限制以外，您可以上傳的檔案類型沒有任何限制。 不過，以資源發行至報表伺服器時，具有對等 MIME 類型之檔案類型的效能會優於其他類型。 例如，當使用者按一下資源時，以 HTML 和 JPG 檔為基礎的資源將在瀏覽器視窗中開啟，HTML 將轉譯成網頁，JPG 將轉譯成影像，供使用者檢視。 反之，沒有對等 MIME 類型的資源 (例如桌上型電腦應用程式檔案) 可能就無法在瀏覽器視窗中轉譯。  
  
 資源是否可供報表使用者檢視，要看瀏覽器的檢視功能而定。 由於報表伺服器不會處理資源，因此瀏覽器可能會提供檢視功能來轉譯特定 MIME 類型。 如果瀏覽器無法轉譯內容，檢視資源的使用者就只能看到資源的一般屬性。  
  
### <a name="securing-and-managing-a-resource"></a>保護和管理資源  
 資源會連同報表、共用資料來源、共用排程和資料夾一起當做具名項目存在報表伺服器資料夾階層中。 您可以搜尋、檢視、保護和設定資源的屬性，就像處理報表伺服器上所儲存的任何項目一樣。 若要檢視或管理資源，您的角色指派中必須具有檢視資源或管理員資源的工作。  
  
### <a name="referencing-an-image-resource-from-a-report"></a>從報表參考影像資源  
 資源可以包含您在報表中參考的影像。 如果報表需求包括使用外部影像，請考慮下列將影像儲存成資源的優點：  
  
-   報表伺服器資料庫中的集中式儲存。 如果您將報表伺服器資料庫及其內容移至另一部電腦，外部影像會與報表一起移動。 您不需要追蹤儲存在不同電腦之磁碟上的影像檔。  
  
-   透過角色指派而非檔案系統安全性進行保護。 用來檢視報表的相同權限可以套用至資源。 反之，如果您將影像儲存在磁碟上，就必須確保匿名使用者帳戶或自動執行帳戶擁有存取此檔案的權限。  
  
 若要在報表中使用影像資源，請將影像檔加入至專案，然後將它與報表一起發行。 發行影像之後，您可以更新報表中的影像參考，讓它指向報表伺服器上的資源，然後單獨重新發行該報表，以便儲存您的變更。 之後，您就可以透過重新發行資源，更新影像 (與報表分開處理)。 報表會使用報表伺服器上可用的最新影像版本。  
  
 如需詳細資訊，請參閱[更新資源 (入口網站)](../../reporting-services/report-server/update-a-resource-report-manager.md)。  
  
##  <a name="my-reports"></a><a name="bkmk_MyReports"></a> 我的報表  
 [我的報表] 資料夾是以有效網域帳戶登入報表伺服器的使用者之個人工作空間。 此特定用途資料夾提供儲存區給處理中的報表、不要進行全區散發的報表，或針對特定需求而修改的報表。 您無法限制儲存在 [我的報表] 資料夾中的項目數量或大小，也無法設定 [我的報表] 資料夾在使用者之間共用。  
  
 技術上來說，[我的報表] 會將每一位使用者看到的虛擬資料夾名稱 (我的報表)，對應到主要 [使用者資料夾] 資料夾之下、以使用者名稱為名的唯一子資料夾。 當使用者存取他/她自己的 [我的報表] 資料夾時，實際上是將使用者重新導向到 [使用者資料夾] 中、他/她本身的子資料夾。 每一個子資料夾都提供儲存區，以儲存使用者加入到其 [我的報表] 資料夾中的報表和項目。 在入口網站中，根層級不會顯示 [我的報表]。 您必須向下切入至 [使用者] 資料夾。  
  
 安裝報表伺服器時，就會建立 [使用者資料夾] 資料夾。 使用者第一次開啟 [我的報表] \(例如在入口網站中按一下 [我的報表]\) 時，就會陸陸續續建立以使用者為基礎的子資料夾。 每一個資料夾名稱都會採用下列格式：  
  
```  
/Users Folders/<username>/My Reports  
```  
  
 使用者的系統帳戶必須為有效的，才會配置資料夾。 如果使用者名稱包含特殊字元，就會以對等的逸出字元建立。 對等的逸出字元列於下表中。  
  
|字元|逸出值|範例|  
|---------------|------------------|-------------|  
|(空格)|[ ]|*Firstname Lastname* 會變成 *Firstname[ ]Lastname*|  
|\ (反斜線)|會以單一空格字元取代|*DomainName\Username* 會變成 *DomainName Username*|  
|@ (at 符號)|[at]|*username*@hotmail.com 會變成 *username*[at]hotmail.com|  
|& (連字號)|[amp]|*username*@*company*&*company.com* 會變成 *username*[at]*company*[amp]*company.com*|  
|$ (貨幣符號)|[dollar]|*User* $*Name* 會變成 *User*[ ][dollar]*Name*|  
  
 [我的報表] 功能是選擇性的。 安裝報表伺服器時，[我的報表] 預設為停用。 如需啟用此功能的詳細資訊，請參閱 [啟用與停用我的報表](../../reporting-services/report-server/enable-and-disable-my-reports.md)。 如需詳細資訊，請參閱 [保護我的報表](../../reporting-services/security/secure-my-reports.md)。  
  
## <a name="tasks"></a>工作  
 [上傳檔案到資料夾](../../reporting-services/report-server/upload-files-to-a-folder.md)  
 [建立、刪除或修改資料夾 (入口網站)](../../reporting-services/report-server/create-delete-or-modify-a-folder-web-portal.md)  
 [更新資源 (入口網站)](../../reporting-services/report-server/update-a-resource-report-manager.md)  
 [上傳檔案到資料夾](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 工具](../../reporting-services/tools/reporting-services-tools.md)   
 [角色與權限 &#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md)   
 [Reporting Services 報表 &#40;SSRS&#41;](../../reporting-services/reports/reporting-services-reports-ssrs.md)  
  