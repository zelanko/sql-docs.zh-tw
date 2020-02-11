---
title: 建立、修改和刪除標準訂閱（原生模式中的 Reporting Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- standard subscriptions [Reporting Services]
- subscriptions [Reporting Services], standard
ms.assetid: 5ab1c661-9bfa-434a-b315-faac34ed12b1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c929fd63cb886eaad301697d4eee245ffb30301c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66100985"
---
# <a name="create-modify-and-delete-standard-subscriptions-reporting-services-in-native-mode"></a>Create, Modify, and Delete Standard Subscriptions (Reporting Services in Native Mode)
  標準訂閱是希望能透過電子郵件傳遞報表，或傳遞到共用資料夾之個別使用者所建立的訂閱。 標準訂閱一律是透過它所依據的報表定義。  
  
 建立訂閱的使用者便擁有該訂閱。 每一個使用者都可以修改或刪除自己所擁有的訂閱。  
  
> [!NOTE]  
>  從 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 開始，您可以用程式設計的方式傳送訂閱的擁有權。 沒有任何使用者介面可以用來傳送訂閱的擁有權。 如需詳細資訊，請參閱 <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
 視**rsreportserver.config**的設定檔設定而定，使用者可能可以將更多使用者新增至訂用帳戶（例如，管理員會新增其直屬員工的電子郵件地址，讓他們各自收到一份報告）。 是否支援此功能取決於在定義個別訂閱時，[收件者:] 欄位是否為可見的。 如需詳細資訊，請參閱[為電子郵件傳遞設定報表伺服器 &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)。  
  
 此主題提供有關由個別使用者建立或管理的標準訂閱資訊。 資料驅動訂閱有不同的需求和步驟，且會在另一個主題中討論。 如需詳細資訊，請參閱[建立、修改和刪除資料驅動訂閱](data-driven-subscriptions.md)。  
  
 本主題內容：  
  
-   [若要建立訂閱](#bkmk_create_subscription)  
  
-   [若要建立檔案共用訂閱](#bkmk_create_fileshare_subscription)  
  
-   [若要建立電子郵件訂閱](#bkmk_create_email_subscription)  
  
-   [若要修改訂用帳戶](#bkmk_modify_subscription)  
  
-   [若要刪除訂用帳戶](#bkmk_delete_subscription)  
  
##  <a name="bkmk_create_subscription"></a>若要建立訂用帳戶  
 若要建立訂閱，請選擇適用於報表伺服器部署的工具和方法：  
  
-   本主題的內容描述如何使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表管理員在原生模式報表伺服器上建立訂閱。 定義了訂閱之後，您可以在報表管理員中，透過特定報表的 [我的訂閱] 頁面或 **[訂閱]** 索引標籤存取訂閱。  
  
-   [建立及管理 Sharepoint 模式報表伺服器的訂閱](create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)說明如何使用 sharepoint 網站中的應用程式頁面，訂閱以 sharepoint 整合模式執行之報表伺服器上的報表。  
  
 此主題提供建立電子郵件訂閱與檔案共用傳遞訂閱的指示。  
  
-   若要使用電子郵件傳遞，您必須先針對 SMTP 伺服器或閘道連接設定報表伺服器，才可以建立訂閱。  
  
-   若要使用檔案共用傳遞，您必須已經定義目標資料夾。 如需詳細資訊，請參閱[為電子郵件傳遞設定報表伺服器 &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)。  
  
 報表資料來源必須設定為使用預存認證或不使用認證，然後才能訂閱報表。 如需詳細資訊，請參閱 [在 Reporting Services 資料來源中儲存認證](../report-data/store-credentials-in-a-reporting-services-data-source.md)。 否則的話， **[新增訂閱]** 按鈕便無法使用。  
  
 本主題並未說明如何建立資料驅動訂閱。 如需如何建立資料驅動訂閱的指示，請參閱[建立資料驅動訂閱 &#40;SSRS 教學課程&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md) 或報表管理員中 [建立資料驅動訂閱] 頁面的線上說明。  
  
###  <a name="bkmk_create_fileshare_subscription"></a>若要建立檔案共用訂閱  
  
1.  啟動 [報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)。  
  
2.  在報表管理員的 **[內容]** 頁面上，瀏覽至您要訂閱的報表。 按一下報表以開啟它。  
  
3.  按一下 **[訂閱]** 索引標籤，然後按一下 **[新增訂閱]**。  
  
4.  在 **[傳遞者]** 中，選取 **[Windows 檔案共用]**。  
  
5.  在 **[檔案名稱]** 中，輸入報表的檔案名稱。  
  
6.  選取 **[建立檔案時加入副檔名]**。 這個選項會將三個字元的副檔名加入至檔案名稱。 副檔名是由您選取的報表輸出格式所決定。  
  
7.  在 [**路徑**] 文字方塊中，輸入您要傳遞報表之現有資料夾的通用命名慣例（UNC）路徑（ \\ \\例如，<servername\> \\<myreports 都\>）。 在路徑的開頭包含雙反斜線字元。 請勿在尾端指定反斜線。  
  
8.  在 [轉譯格式] 中，選取檔案傳遞的報表輸出格式。 選擇對應至將用於開啟報表之桌面應用程式的格式。 請避免使用無法在單一資料流完成報表轉譯的格式，或者會導入靜態檔案無法支援之互動性的格式 (例如 HTML 4.0)。  
  
9. 在 [**使用者名稱**] 和 [**密碼**] 文字方塊中，使用使用者名稱的 [ * \<網域>* \\ * \<使用者名稱>* 格式，指定存取檔案共用所需的認證。  
  
10. 指定覆寫選項。 如果您按一下 **[如果舊版存在，不要覆寫檔案]**，則若是偵測到現有的檔案，將不會傳遞。 如果您按一下 **[加入較新版本時，遞增檔案名稱]**，報表伺服器就會在檔案名稱後面附加一個數字，以便與相同名稱的現有檔案區別。  
  
11. 指定您要傳遞報表的時機：  
  
    -   若要排程傳遞時間，請按一下 **[排程報表執行完成時]** ，然後按一下 **[選取排程]** 按鈕。 就會開啟排程頁面。  
  
    -   若要選取預先定義的共用排程，其中已經具有您想要使用的日期、時間和循環資訊，請按一下 **[在共用排程上]**，然後選取要用的排程。  
  
    -   若要在以更新的版本更新報表快照集時傳遞報表，請按一下 [重新整理報表內容時]****。 如果您要訂閱以排程間隔擷取資料的報表，用來重新整理資料的排程就會決定處理訂閱的時間。  
  
        > [!NOTE]  
        >  只有當快照集已經和更新排程相關聯時可使用此選項。  
  
12. 如果是參數化報表，請指定要用於此訂閱之報表的參數。 參數可以與視需要執行報表或依其他排程作業執行報表所用的參數不同。  
  
 報表會以靜態檔案傳遞。 如果報表包括互動式功能 (例如，連結到其他資料列或資料行)，則那些功能無法使用。  
  
###  <a name="bkmk_create_email_subscription"></a>若要建立電子郵件訂閱  
  
1.  在報表管理員的 **[內容]** 頁面上，瀏覽至您要訂閱的報表。 按一下報表以開啟它。  
  
2.  按一下 **[訂閱]** 索引標籤，然後按一下 **[新增訂閱]**。  
  
3.  在 [**傳遞者**] 中，選取 [**電子郵件**]。 如果這種傳遞類型無法使用，表示您的報表伺服器尚未針對電子郵件訂閱進行設定。  
  
4.  **在 [收**件者] 文字方塊中，會使用您的網域使用者帳戶來自我定址 [收件者：] 欄位中的收件者名稱。 報表伺服器組態設定會決定系統是否會使用您的使用者帳戶來自行處理 [收件者]**** 欄位。 如需變更設定電子郵件地址的詳細資訊，請參閱[為電子郵件傳遞設定報表伺服器 &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)。  
  
    > [!NOTE]  
    >  根據您的權限，可能可以輸入想要傳遞報表的目標電子郵件地址。 若要指定多個電子郵件地址，請使用分號 (;) 隔開。 您也可以在 [副本]****、[密件副本]**** 和 [回覆至]**** 文字方塊中，鍵入其他電子郵件地址。 這需要您具有管理所有訂閱的權限。  
  
5.  選取傳遞選項，如下所示：  
  
    -   若要內嵌或附加報表的副本，請選取 **[包含報表]**。 報表的格式是由您選取的轉譯格式所決定。 如果您認為報表大小將超出您為電子郵件系統所定義的限制，請勿選擇此選項。  
  
    -   若要在電子郵件訊息主體中包含報表的 URL 連結，請選取 [**包含連結**]。  
  
    > [!NOTE]  
    >  如果您清除這兩個選項，就只會傳送主旨行中的通知文字。  
  
6.  從 **[轉譯格式]** 清單方塊中選擇轉譯格式。 如果選取 **[包含報表]** 以內嵌或附加報表的副本，就可以使用此選項。  
  
    -   若要將報表內嵌於電子郵件訊息的主體，請選取 [網頁封存]****。  
  
    -   若要將報表當成附加檔案傳送，請選擇其他任一種轉譯格式。  
  
7.  從 **[優先權]** 清單方塊中，選取優先權。 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange 中，此設定會設定電子郵件訊息重要性層級的旗標。  
  
8.  指定您要傳遞報表的時機：  
  
    -   若要排程傳遞時間，請按一下 **[排程報表執行完成時]** ，然後按一下 **[選取排程]**。 就會為您開啟排程頁面。  
  
    -   若要選取預先定義的共用排程，其中已經具有您想要使用的日期、時間和循環資訊，請按一下 **[在共用排程上]**，然後選取要用的排程。  
  
    -   若要在以更新的版本更新報表快照集時傳遞報表，請按一下 [重新整理報表內容時]****。 如果您要訂閱以排程間隔擷取資料的報表，用來重新整理資料的排程就會決定處理訂閱的時間。  
  
    > [!NOTE]  
    >  只有當快照集已經和更新排程相關聯時可使用此選項。  
  
9. 如果是參數化報表，請指定要用於此訂閱之報表的參數。 您指定的參數，可以與視需要執行報表或依其他排程作業執行報表所用的參數不同。  
  
##  <a name="bkmk_modify_subscription"></a>若要修改訂用帳戶  
 您可以在任何時間修改訂閱。 如果您在處理訂閱時修改訂閱，當更新的設定在傳遞延伸模組接收到訂閱資料之前，儲存到報表伺服器資料庫中時，就會使用更新的設定。 否則，會使用現有的設定。  
  
 若要找出訂閱，請使用 **[我的訂閱]** 頁面，或檢視與報表相關聯的訂閱定義。 您無法直接搜尋訂閱，也無法依擁有者名稱、觸發程序資訊、狀態資訊等等搜尋訂閱。  
  
 訂閱也可以由報表伺服器管理員修改或刪除。  
  
> [!NOTE]  
>  報表伺服器管理員無法從一個位置，管理在給定報表伺服器上使用的所有個別訂閱。 然而，報表伺服器管理員可以存取個別訂閱以修改或刪除。  
  
##  <a name="bkmk_delete_subscription"></a>若要刪除訂用帳戶  
 刪除訂閱：  
  
1.  啟動 [報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)。  
  
2.  在報表管理員中，按一下全域工具列上的 **[我的訂閱]** ，然後導覽至您要修改或刪除的訂閱。  
  
3.  或者，在開啟之報表的 **[訂閱]** 索引標籤上，找到您要修改或刪除的訂閱。 執行下列其中一項：  
  
    1.  若要修改訂閱，請按一下 **[編輯]**。  
  
    2.  若要刪除訂閱，請選取訂閱旁的核取方塊，然後按一下 **[刪除]**。  
  
 本主題並未說明如何取消目前正在報表伺服器上處理的訂閱。 如需取消訂閱的詳細資訊，請參閱[管理執行中的進程](manage-a-running-process.md)  
  
 如果您想要結束訂閱但無法輕易的找到該訂閱，請在所收到的報表上註明，然後依名稱搜尋。 存取到報表之後，您就可以將自己從訂閱中移除。 如果您找不到訂閱，則該訂閱可能是資料驅動訂閱。 如需詳細資訊，請洽詢您的報表伺服器管理員。  
  
 如果基礎報表被刪除，則會自動刪除訂閱。 如果您在處理訂閱時刪除訂閱，當刪除作業在傳遞延伸模組接收到訂閱資料之前發生，訂閱就會停止。 否則，訂閱會繼續處理。  
  
## <a name="see-also"></a>另請參閱  
 [工作和權限](../security/tasks-and-permissions.md)   
 [建立及管理 SharePoint 模式報表伺服器的訂閱](create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)   
 [建立和管理原生模式報表伺服器的訂閱](../create-manage-subscriptions-native-mode-report-servers.md)   
 [Data-Driven Subscriptions](data-driven-subscriptions.md)   
 [訂閱與傳遞 &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)   
 [使用我的訂閱](use-my-subscriptions-native-mode-report-server.md)  
  
  
