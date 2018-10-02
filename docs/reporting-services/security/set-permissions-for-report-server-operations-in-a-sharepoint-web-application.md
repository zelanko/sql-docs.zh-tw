---
title: 在 SharePoint Web 應用程式中設定報表伺服器作業的權限 | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- SharePoint integration [Report Builder]
- security [Reporting Services], SharePoint integrated mode
- Report Builder 1.0, SharePoint integration
- model item security [Reporting Services]
ms.assetid: 9ea71f1a-ee9e-4337-95ff-d7cef79946e7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6ba1339184654094e1cd5d8ad249d43dcd645ca1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47699716"
---
# <a name="set-permissions-for-report-server-operations-in-a-sharepoint-web-application"></a>在 SharePoint Web 應用程式中設定報表伺服器作業的權限
  針對以 SharePoint 整合模式執行的報表伺服器，在 SharePoint 網站上定義的安全性設定可以決定您檢視與管理報表、報表模型與共用資料來源的方式。 如果您使用預設的 SharePoint 群組、權限等級以及權限指派，則可以使用目前的安全性設定處理報表和其他文件。  
  
 如果預設的安全性設定未提供您需要的存取等級，您可利用下面各章節中提供的資訊，了解特定作業所需的權限：  
  
-   [檢視和管理報表的權限](#permissionReports)  
  
-   [使用報表產生器建立報表的權限](#permissionReportBuilder)  
  
-   [建立和管理共用排程的權限](#permissionSharedSchedules)  
  
-   [建立和管理訂閱的權限](#permissionSubscriptions)  
  
-   [建立和管理共用資料來源以及報表模型的權限](#permissionDataSources)  
  
 您只需要少數重要權限便幾乎可在 SharePoint 網站上完成任何作業。 雖然這些權限並未列於下面的工作和權限表格中，但是如果您要建立自訂權限等級，就必須加入這些權限。  
  
-   瀏覽使用者資訊  
  
-   使用遠端介面  
  
-   開啟  
  
-   檢視應用程式頁面  
  
 如果您要使用預先定義的權限等級，則不需要進行任何動作，因為上述權限已經包括在完整控制、設計、參與、讀取和限制存取中。 但是，如果您要使用自訂權限等級或編輯權限指派給特定使用者或群組，則必須手動加入權限。  
  
 「瀏覽使用者資訊」權限可讓報表伺服器傳回項目建立者以及項目最後修改者的相關資訊。 沒有這個權限，報表伺服器將會傳回下列錯誤。 若是瀏覽作業，此錯誤為：「報表伺服器發生 SharePoint 錯誤。 ---> System.UnauthorizedAccessException: 存取遭到拒絕。」 若是發行作業，錯誤為「授與使用者 ‘\<網域>\\<使用者\>' 的權限不足，無法執行此作業」。  
  
##  <a name="permissionReports"></a> 檢視和管理報表的權限  
 報表定義權限是透過包含報表的文件庫上的「清單」權限定義，不過，如果您要限制存取，可以在個別報表上設定權限。 下表提供工作以及支援各項工作之權限的清單。  
  
|工作|權限|  
|----------|----------------|  
|檢視報表。|「檢視項目」 ，針對包含檔案的文件庫或個別的報表。|  
|檢視使用報表模型做為資料來源的點選連結報表。|「檢視項目」 ，針對包含報表和報表模型的文件庫，或個別的報表和模型。 如果您沒有檢視模型的權限，您仍可開啟報表，但是無法在資料上進行特定瀏覽。<br /><br /> 如果報表模型使用模型項目安全性，使用者也必須擁有報表模型的「列舉權限」  權限。|  
|檢視報表記錄中的快照集。|「編輯項目」 ，針對包含檔案的文件庫或個別的報表。 您可以針對特定報表檢視所有報表記錄，或不檢視任何報表記錄。 不過您無法在報表記錄中的個別快照集上設定權限。|  
|上傳或發行報表至程式庫。|「加入項目」 ，針對包含報表的文件庫。|  
|設定報表上的屬性，包括資料來源連接資訊、處理選項，以及參數屬性。|「編輯項目」 ，針對包含報表的文件庫或個別的報表。 您還需具備共用資料來源的檢視權限 (.rsds)，才能選取該來源搭配報表使用。|  
|排程報表處理。|若要選取共用排程，您必須擁有包含報表所在文件庫之網站的「開啟」  權限。 若要排程資料處理或快取過期，必須擁有包含報表的文件庫或個別報表上的「編輯項目」  權限。|  
|刪除報表。|「刪除項目」 ，針對包含報表的文件庫或個別的報表。|  
|將報表定義取代為較新的版本 (不影響屬性、權限、記錄或訂閱)。|「編輯項目」 ，針對包含報表的文件庫或個別的報表。|  
|建立報表記錄中的快照集。|「加入項目」 ，針對包含要建立其報表記錄之報表的文件庫。|  
|建立報表記錄中的快照集。|「加入項目」 ，針對包含要建立其報表記錄之報表的文件庫。|  
|刪除報表記錄中的快照集，以及刪除已簽出且修改一段時間的特定報表定義版本。|「刪除項目」 ，針對包含要刪除其報表記錄之報表的文件庫。|  
|檢視報表記錄中的快照集，以及檢視已簽出且修改一段時間的特定報表定義版本。|「檢視版本」 ，針對將包含報表的文件庫。|  
  
##  <a name="permissionReportBuilder"></a> 使用報表產生器建立報表的權限  
 報表產生器是可以用來建立特定報表的報表編輯工具。 報表產生器使用報表模型做為資料來源，以支援特定資料瀏覽。 您可以載入報表產生器中模型以建立報表、執行報表、瀏覽模型中的資料，以及選擇性地將報表儲存至程式庫。 具備足夠權限的使用者可以接著開啟相同的報表，還能執行特定資料瀏覽。  
  
> [!NOTE]  
>  報表產生器的存取可藉由權限以外的因素決定。 網站管理員可以設定伺服器屬性以停用隨選報表，或不加入報表產生器報表的內容類型，藉此限制使用報表產生器，如此可防止使用者從文件庫上的 **[新增]** 功能表建立新報表。 此外，報表伺服器管理員可以設定報表伺服器上的屬性，藉此停用報表產生器。 如果您的伺服器發生這些情況的任一種，則即使您擁有必要的權限，仍無法使用報表產生器。  
  
 下表提供建立報表和使用報表產生器的工作清單，以及支援各項工作的權限：  
  
|工作|權限|  
|----------|----------------|  
|啟動報表產生器。|沒有明確用來控制使用報表產生器的權限。 如果已設定報表伺服器整合，而且您具備將項目加入文件庫的權限，則可以使用報表產生器。 若要從文件庫中的 **[新增]** 功能表啟動報表產生器，則必須註冊報表產生器內容類型。 如需詳細資訊，請參閱 [將 Reporting Services 內容類型加入至 SharePoint 文件庫](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)。|  
|上傳模型或共用資料來源。|「加入項目」 ，針對包含檔案的文件庫。|  
|檢視模型或相依的共用資料來源。|「檢視項目」 ，針對將包含檔案的文件庫。<br /><br /> 如果模型包含模型項目安全性設定，使用者也必須擁有模型的「列舉權限」  權限。|  
|從共用資料來源產生模型。|「加入項目」 ，針對包含要從中產生模型之共用資料來源 (.rsds) 檔的文件庫。|  
|設定特定模型項目上模型內的權限。|「管理權限」 ，針對包含文件庫和報表模型 (.smdl) 檔的網站。|  
|載入報表產生器中模型。|「編輯項目」 ，針對報表模型 (.smdl) 檔。|  
|在報表產生器中建立報表定義，並將報表儲存至程式庫。|「加入項目」 ，將檔案儲存至文件庫。|  
|在報表產生器中編輯報表。|「編輯項目」 ，針對報表定義檔案。|  
  
 建立和使用訂閱、報表記錄，以及在報表產生器報表上設定報表或資料處理選項的權限，與在標準報表定義檔案上用來執行相同動作的權限相同。  
  
##  <a name="permissionSharedSchedules"></a> 建立和管理共用排程的權限  
 共用排程並非儲存在文件庫中的文件。 基於這個理由，建立和管理這些排程便需要網站權限。 您無法限制存取特定共用排程。 您建立的任何共用排程將會提供給任何具備整個網站的「開啟」權限的使用者。  
  
 下表提供建立、管理和使用共用排程的工作和權限清單：  
  
|工作|權限|  
|----------|----------------|  
|建立、編輯或刪除共用排程。|「管理網站」 ，針對網站。|  
|選取訂閱處理或資料擷取的共用排程。|「開啟」 ，針對包含文件庫的網站。|  
  
##  <a name="permissionSubscriptions"></a> 建立和管理訂閱的權限  
 SharePoint 會強制執行訂閱與檢視權限間的相依性。 您無法訂閱未具備檢視權限的報表。 如果您授與訂閱報表的權限，則會自動授與檢視權限。  
  
 下表提供建立、管理和使用訂閱的工作和權限清單：  
  
|工作|權限|  
|----------|----------------|  
|建立、編輯或刪除使用者擁有的特定報表訂閱。|程式庫 (包含該報表或位於該報表) 上的 [編輯項目] 。 「檢視項目」是相依權限，並且將會自動包含在權限等級中。 能夠建立訂閱的使用者，同樣能夠建立執行該訂閱的自訂排程。|  
|選取搭配訂閱使用的共用排程。|「開啟」 ，針對包含文件庫的網站。|  
|建立、編輯或刪除整個網站的任何訂閱。|「管理提醒」 ，針對網站。|  
  
##  <a name="permissionDataSources"></a> 建立和管理共用資料來源以及報表模型的權限  
 共用資料來源 (.rsds) 檔包含可供多個報表和模型使用的資料來源連接資訊。 若為標準報表，使用 .rsds 檔指定資料來源連接資訊則是選擇性的操作。 若為模型導向的報表，則必須使用 .rsds 檔。 報表模型會固定使用 .rsds 檔連接外部資料來源。  
  
 您可以設定共用資料來源上的屬性，以決定個別使用者是否可以檢視或管理共用資料來源。 檢視或管理共用資料來源的權限與報表檢視權限不同；您不需具備檢視 .rsds 檔本身的權限，也可以檢視使用 .rsds 檔的報表。  
  
|工作|權限|  
|-----------|----------------|  
|建立共用資料來源。|「加入項目」 ，針對包含共用資料來源的文件庫。 您可以從文件庫中的 [新增] 功能表建立新的共用資料來源。 若要這樣做，您必須在文件庫中註冊報表資料來源內容類型。 如需詳細資訊，請參閱 [將 Reporting Services 內容類型加入至 SharePoint 文件庫](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)。|  
|編輯共用資料來源。|「編輯項目」 ，針對包含共用資料來源的文件庫，或共用資料來源本身。|  
|刪除共用資料來源。|「刪除項目」 ，針對包含共用資料來源的文件庫，或共用資料來源本身。|  
|搭配報表使用共用資料來源 (.rsds)。|「編輯項目」 ，針對報表或包含報表的文件庫。 選取共用資料來源是設定報表上資料來源屬性的一部分。|  
|從共用資料來源產生報表模型。|「加入項目」 ，針對包含報表模型的文件庫。|  
|刪除報表模型。|「刪除項目」 ，針對包含報表模型的文件庫或報表模型本身。|  
|設定特定模型項目上模型內的權限。|「管理權限」 ，針對包含文件庫和報表模型 (.smdl) 檔的網站。|  
  
> [!NOTE]  
>  沒有編輯報表模型的權限。 即使您可以產生或刪除報表模型，仍無法在 SharePoint 網站內進行編輯。 編輯報表模型需要模型設計師，這是一個用戶端撰寫工具，不受您在 SharePoint 中設定的權限影響。  
  
## <a name="see-also"></a>另請參閱  
 [授與 SharePoint 網站上報表伺服器項目的權限](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [將 Reporting Services 中的角色和工作與 SharePoint 群組和權限做比較](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [授與 SharePoint 網站上報表伺服器項目的權限](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [在 Windows SharePoint Services 中使用報表伺服器項目的內建安全性](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)  
  
  
