---
title: "建立及管理原生模式報表伺服器的訂用帳戶 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: subscriptions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- standard subscriptions [Reporting Services]
- subscriptions [Reporting Services], standard
ms.assetid: 5ab1c661-9bfa-434a-b315-faac34ed12b1
caps.latest.revision: "52"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 77666065993e86cbee7fa90beb4865a1562580c2
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="create-and-manage-subscriptions-for-native-mode-report-servers"></a>建立及管理原生模式報表伺服器的訂閱
  標準訂閱是希望能透過電子郵件傳遞報表，或傳遞到共用資料夾之個別使用者所建立的訂閱。 此主題提供有關由個別使用者建立或管理的標準訂閱資訊。 資料驅動訂閱有不同的需求和步驟，且會在另一個主題中討論。 如需詳細資訊，請參閱 [建立、修改和刪除資料驅動訂閱](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)  
  
 **本主題內容：**  
  
-   [訂閱的一般需求](#bkmk_create_subscription)  
  
-   [若要建立檔案共用訂閱](#bkmk_create_fileshare_subscription)  
  
-   [若要建立電子郵件訂閱](#bkmk_create_email_subscription)  
  
-   [修改訂閱](#bkmk_modify_subscription)  
  
-   [若要刪除訂閱](#bkmk_delete_subscription)  
  
##  <a name="bkmk_create_subscription"></a> 訂閱的一般需求  
 本主題的內容描述如何使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表管理員在原生模式報表伺服器上建立訂閱。 定義了訂閱之後，您可以在報表管理員中，透過特定報表的 [我的訂閱] 頁面或 **[訂閱]** 索引標籤存取訂閱。  
  
 [建立及管理 SharePoint 模式報表伺服器的訂閱](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md) 說明如何使用 SharePoint 網站中的應用程式頁面來訂閱 SharePoint 模式報表伺服器上的報表。  
  
-   若要使用電子郵件傳遞，您必須先針對 SMTP 伺服器或閘道連接設定報表伺服器，才可以建立訂閱。  
  
-   若要使用檔案共用傳遞，您必須已經定義目標資料夾。 如需詳細資訊，請參閱 [為電子郵件傳遞設定報表伺服器 (SSRS 組態管理員)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83)。  
  
 報表資料來源必須設定為使用預存認證或不使用認證，然後才能訂閱報表。 如需詳細資訊，請參閱 [在 Reporting Services 資料來源中儲存認證](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)。 否則的話， **[新增訂閱]** 按鈕便無法使用。  
  
 本主題並未說明如何建立資料驅動訂閱。 如需如何建立資料驅動訂閱的指示，請參閱[建立資料驅動訂閱 &#40;SSRS 教學課程&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md) 或報表管理員中 [建立資料驅動訂閱] 頁面的線上說明。  
  
###  <a name="bkmk_create_fileshare_subscription"></a> 若要建立檔案共用訂閱  
  
1.  啟動 [報表管理員 &#40;SSRS 原生模式&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)。  
  
2.  瀏覽至您想要訂閱的報表。 按一下 [報表] 功能表及 [訂閱] 。  
  
     ![報表功能表](../../reporting-services/subscriptions/media/ssrs-report-menu-report-manager.png "報表功能表")  
  
3.  **描述**：輸入報表的描述，最多 512 個字元。  
  
4.  **擁有者**︰擁有者欄位預設為目前的使用者，且在您建立訂閱時無法編輯。 不過，在儲存訂閱之後，您可以變更訂閱屬性，包括擁有者與描述。  
  
5.  **傳遞者**：選取 [Windows 檔案共用] 。  
  
6.  **檔案名稱**：輸入報表的檔案名稱。  
  
7.  **建立檔案時加入副檔名**︰這個選項會將三個字元的副檔名加入檔案名稱。 副檔名是由您選取的報表輸出格式所決定。  
  
8.  **路徑**：鍵入您要傳遞報表之現有資料夾的通用命名慣例 (UNC) 路徑 (例如，\\\\<伺服器名稱\>\\<我的報表\>)。 在路徑的開頭包含雙反斜線字元。 請勿在尾端指定反斜線。  
  
     ![檔案共用訂用帳戶](../../reporting-services/subscriptions/media/ssrs-file-share-subscription.png "檔案共用訂用帳戶")  
  
9. **轉譯格式**：選取檔案傳遞的報表輸出格式。 選擇對應至將用於開啟報表之桌面應用程式的格式。 請避免使用無法在單一資料流完成報表轉譯的格式，或者會導入靜態檔案無法支援之互動性的格式 (例如 HTML 4.0)。  
  
10. **認證**︰選取以使用檔案共用帳戶或特定的 Windows 使用者認證。 若報表管理員未設定檔案共用帳戶，則會停用 [使用檔案共用帳戶]  。 如需詳細資訊，請參閱[訂閱設定與檔案共用帳戶 &#40;組態管理員&#41;](../../reporting-services/install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md)。 在 [使用者名稱] 及 [密碼] 文字方塊中，指定存取檔案共用所需的認證，使用者名稱請使用 \<網域>\\\<使用者名稱>。  
  
11. **覆寫選項**：  
  
    -   **如果舊版存在，不要覆寫檔案**：若是偵測到現有的檔案，將不會傳遞。  
  
    -   **加入較新版本時，遞增檔案名稱**：報表伺服器會在檔案名稱後面附加一個數字，以便與相同名稱的現有檔案區別。  
  
12. **排程**：指定您要傳遞報表的時機：  
  
    -   若要排程傳遞時間，請按一下 **[排程報表執行完成時]** ，然後按一下 **[選取排程]** 按鈕。 就會開啟排程頁面。  
  
    -   若要選取預先定義的共用排程，其中已經具有您想要使用的日期、時間和循環資訊，請按一下 **[在共用排程上]**，然後選取要用的排程。  
  
    -   若要在以更新的版本更新報表快照集時傳遞報表，請按一下 [重新整理報表內容時]。 如果您要訂閱以排程間隔擷取資料的報表，用來重新整理資料的排程就會決定處理訂閱的時間。  
  
        > [!NOTE]  
        >  只有當快照集已經和更新排程相關聯時可使用此選項。  
  
13. 如果是參數化報表，請指定要用於此訂閱之報表的參數。 參數可以與視需要執行報表或依其他排程作業執行報表所用的參數不同。  
  
 報表會以靜態檔案傳遞。 如果報表包括互動式功能 (例如，連結到其他資料列或資料行)，則那些功能無法使用。  
  
###  <a name="bkmk_create_email_subscription"></a> 若要建立電子郵件訂閱  
  
1.  啟動 [報表管理員 &#40;SSRS 原生模式&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)。  
  
2.  瀏覽至您想要訂閱的報表。 按一下 [報表] 功能表及 [訂閱] 。  
  
     ![報表功能表](../../reporting-services/subscriptions/media/ssrs-report-menu-report-manager.png "報表功能表")  
  
3.  **描述**：輸入報表的描述，最多 512 個字元。  
  
4.  **擁有者**︰擁有者欄位預設為目前的使用者，且在您建立訂閱時無法編輯。 不過，在儲存訂閱之後，您可以變更訂閱屬性，包括擁有者與描述。  
  
5.  **傳遞者**：選取 [電子郵件]。 如果無法使用 [電子郵件]，表示您的報表伺服器尚未針對電子郵件訂用帳戶進行設定。 請參閱 [為電子郵件傳遞設定報表伺服器 (SSRS 組態管理員)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83)  
  
6.  **收件者**：系統會使用您的網域使用者帳戶，自行處理 [收件者:] 欄位中的收件者名稱。 驗證格式為 [使用者名稱]@[網域.com] 報表伺服器組態設定會決定系統是否會使用您的使用者帳戶來自行處理 [收件者] 欄位。 如需如何變更電子郵件地址組態設定的詳細資訊，請參閱 [為電子郵件傳遞設定報表伺服器 (SSRS 組態管理員)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83)。  
  
    > [!NOTE]  
    >  根據您的權限，可能可以輸入想要傳遞報表的目標電子郵件地址。 若要指定多個電子郵件地址，請使用分號 (;) 隔開。 您也可以在 [副本]、[密件副本] 和 [回覆至] 文字方塊中，鍵入其他電子郵件地址。 這需要您具有管理所有訂閱的權限。  
  
7.  **主旨**：預設為 “@ReportName 已在 @ExecutionTime” 執行。 您可以編輯主旨，但請注意，@ReportName 和 @ExecutionTime 是 [主旨] 欄位中唯一支援的全域變數。  
  
8.  選取傳遞選項，如下所示：  
  
    -   **包含報表**：選取此選項可內嵌或附加報表的複本。 報表的格式是由您選取的轉譯格式所決定。 如果您認為報表大小將超出您為電子郵件系統所定義的限制，請勿選擇此選項。  
  
    -   **包含連結**：選取此選項可在電子郵件訊息主體中包含報表的 URL 連結。  
  
    > [!NOTE]  
    >  如果您清除這兩個選項，就只會傳送主旨行中的通知文字。  
  
9. 從 **[轉譯格式]** 清單方塊中選擇轉譯格式。 如果選取 **[包含報表]** 以內嵌或附加報表的副本，就可以使用此選項。  
  
    -   若要將報表內嵌於電子郵件訊息的主體，請選取 [網頁封存]。  
  
    -   若要將報表當成附加檔案傳送，請選擇其他任一種轉譯格式。  
  
10. 從 **[優先權]** 清單方塊中，選取優先權。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange 中，此設定會設定電子郵件訊息重要性層級的旗標。  
  
11. 指定您要傳遞報表的時機：  
  
    -   若要排程傳遞時間，請按一下 **[排程報表執行完成時]** ，然後按一下 **[選取排程]**。 就會為您開啟排程頁面。  
  
    -   若要選取預先定義的共用排程，其中已經具有您想要使用的日期、時間和循環資訊，請按一下 **[在共用排程上]**，然後選取要用的排程。  
  
    -   若要在以更新的版本更新報表快照集時傳遞報表，請按一下 [重新整理報表內容時]。 如果您要訂閱以排程間隔擷取資料的報表，用來重新整理資料的排程就會決定處理訂閱的時間。  
  
    > [!NOTE]  
    >  只有當快照集已經和更新排程相關聯時可使用此選項。  
  
12. 如果是參數化報表，請指定要用於此訂閱之報表的參數。 您指定的參數，可以與視需要執行報表或依其他排程作業執行報表所用的參數不同。  
  
##  <a name="bkmk_modify_subscription"></a> 修改訂閱  
 您可以在任何時間修改訂閱。 如果您在處理訂閱時修改訂閱，當更新的設定在傳遞延伸模組接收到訂閱資料之前儲存到報表伺服器中時，就會使用更新的設定。 否則，會使用現有的設定。  
  
 建立訂閱的使用者便擁有該訂閱。 每一個使用者都可以修改或刪除自己所擁有的訂閱。 您可以從訂閱屬性頁面中變更報表的擁有者，或者可以透過程式設計方式變更擁有權。 如需詳細資訊，請參閱下列內容：  
  
-   [使用 PowerShell 變更及列出 Reporting Services 訂閱擁有者並執行訂閱](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
  
-   <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
 若要找出訂閱，請使用 **[我的訂閱]** 頁面，或檢視與報表相關聯的訂閱定義。 您無法直接搜尋訂閱，也無法依擁有者名稱、觸發程序資訊、狀態資訊等等搜尋訂閱。  
  
 訂閱也可以由報表伺服器管理員修改或刪除。  
  
> [!NOTE]  
>  報表伺服器管理員無法從一個位置，管理在給定報表伺服器上使用的所有個別訂閱。 然而，報表伺服器管理員可以存取個別訂閱以修改或刪除。  
  
##  <a name="bkmk_delete_subscription"></a> 若要刪除訂閱  
 若要刪除訂閱  
  
1.  啟動 [報表管理員 &#40;SSRS 原生模式&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)。  
  
2.  在報表管理員中，按一下工具列上的 [我的訂閱]  ，然後瀏覽至您要修改或刪除的訂閱。  
  
3.  開啟 [報表] 功能表，然後按一下 [刪除]   
  
     ![報表功能表](../../reporting-services/subscriptions/media/ssrs-report-menu-report-manager.png "報表功能表")  
  
 若要取消目前正在報表伺服器上處理的訂閱，請參閱 [管理執行中的處理序](../../reporting-services/subscriptions/manage-a-running-process.md)。  
  
 如果您想要結束訂閱但找不到該訂閱，請記下所收到的報表，然後依名稱搜尋。 存取到報表之後，您就可以將自己從訂閱中移除。 如果您找不到訂閱，則該訂閱可能是資料驅動訂閱。 如需詳細資訊，請洽詢您的報表伺服器管理員。  
  
 如果基礎報表被刪除，則會自動刪除訂閱。 如果您在處理訂閱時刪除訂閱，當刪除作業在傳遞延伸模組接收到訂閱資料之前發生，訂閱就會停止。 否則，訂閱會繼續處理。  
  
## <a name="see-also"></a>另請參閱  
 [建立及管理 SharePoint 模式報表伺服器的訂閱](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)   
 [Use PowerShell to Change and List Reporting Services Subscription Owners and Run a Subscription](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)   
 [資料驅動訂閱](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [訂閱與傳遞 &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [使用我的訂用帳戶 &#40;原生模式報表伺服器&#41;](../../reporting-services/subscriptions/use-my-subscriptions-native-mode-report-server.md)  
  
  
