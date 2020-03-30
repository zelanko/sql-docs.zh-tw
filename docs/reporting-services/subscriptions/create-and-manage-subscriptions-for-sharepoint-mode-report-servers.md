---
title: 建立及管理 SharePoint 模式報表伺服器的訂用帳戶 | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], creating
- subscriptions [Reporting Services], deleting
- subscriptions [Reporting Services], managing
ms.assetid: 44be7ee2-33ce-46e4-9d1a-a20aaf43a227
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5d4ffc3930003a4035211a4a63a54bc4f8196948
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "65578342"
---
# <a name="create-and-manage-subscriptions-for-sharepoint-mode-report-servers"></a>建立及管理 SharePoint 模式報表伺服器的訂閱
  您可以建立 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱，傳遞以 SharePoint 模式報表伺服器整合的 SharePoint Web 應用程式報表。 訂閱可以將報表傳遞至文件庫、檔案資料夾，或以電子郵件傳送。 本主題摘要說明建立 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱的需求與步驟。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式 &#124; SharePoint 2010 和 SharePoint 2013|  
  
 建立訂閱時，有三種方式可以指定其傳遞：  
  
-   **文件庫**：您可以建立訂閱，以便將以原始報表為基礎的文件傳遞至與原始報表位於相同 SharePoint 網站中的程式庫。 您無法將文件傳遞至相同網站集合中另一部伺服器或另一個網站上的程式庫。 若要傳遞文件，您必須在報表要傳遞至其中的程式庫上擁有「新增項目」權限。  
  
-   **檔案資料夾：** 您可以將以原始報表為基礎的文件傳遞至檔案系統上的共用資料夾。 您必須選取可透過網路連接存取的現有資料夾。  
  
-   **電子郵件：** 如果報表伺服器設定為使用報表伺服器電子郵件傳遞延伸模組，您就可以建立將報表或已匯出報表檔案 (以輸出格式儲存) 傳送至收件匣的訂閱。 若只要接收通知，但不接收報表或報表 URL，請清除 **[包含這個報表的連結]** 和 **[在訊息內顯示報表]** 核取方塊。  
  
 **本主題內容：**  
  
-   [訂閱的一般需求](#bkmk_subscription_requirements)  
  
-   [若要建立傳遞報表至 SharePoint 文件庫的訂閱](#bkmk_tosharepoint_library)  
  
-   [若要建立傳遞報表至 SharePoint 文件庫的訂閱](#bkmk_tosharepoint_library)  
  
-   [建立報表伺服器電子郵件傳遞的訂閱](#bkmk_subscription_for_email)  
  
-   [檢視或修改訂閱](#bkmk_to_modify_subscription)  
  
-   [刪除訂閱](#bkmk_to_delete_subscription)  
  
##  <a name="general-requirements-for-subscriptions"></a><a name="bkmk_subscription_requirements"></a> 訂閱的一般需求  
 若要建立訂閱，報表必須使用預存認證，而且您必須具有檢視報表和建立警示的權限。  
  
 當您建立訂閱時，可以選取輸出檔案格式。 並非每份報表都適用於每種格式。 在您選取訂閱的格式之前，請開啟報表並將它匯出成不同的格式，以便確認它是否如預期方式顯示。  
  
 若要能夠建立 **訂閱，使用者需要 SharePoint 中的** [編輯項目] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 清單權限。 如需相關資訊，請參閱 [報表伺服器項目的 SharePoint 網站和清單權限參考](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)  
  
> [!IMPORTANT]  
>  將報表傳遞至文件庫或共用資料夾的訂閱會建立以原始報表為基礎的新靜態檔案，但是此檔案並非在報表檢視器 Web 組件中執行的真正報表定義。 如果原始報表具有互動式功能 (例如，鑽研連結) 或動態內容，這些功能將無法在傳遞至目標位置的靜態檔案中使用。 如果您選取「網頁」，就可以保留某些互動性，但是因為文件不是在報表檢視器中執行的 .rdl 檔，所以按一下連結報表將會在瀏覽器工作階段中建立新頁面，導致您必須捲動才能回到網站。  
  
 您無法將匯出之報表的副檔名重新命名為 .rdl，並讓它在報表檢視器 Web 組件中執行。 如果您想要建立可提供實際報表的訂閱，請使用報表伺服器電子郵件傳遞延伸模組並將選項設定為包含報表的連結。  
  
 包含傳遞文件之文件庫的版本設定會決定每次傳遞該文件時是否會建立新的版本。 依預設，每個文件庫都會啟用版本設定。 除非您明確選擇 **[無版本設定]** ，否則只要一傳遞就會建立文件新的主要版本。 訂閱傳遞的結果只會建立文件的主要版本，絕不會建立次要版本，即使所選取的版本設定選項允許次要版本。 如果限制要保留的主要版本數目，則在達到上限時，新傳遞項目將會取代舊傳遞項目。  
  
 您針對訂閱所選取的輸出格式會以報表伺服器上安裝的轉譯延伸模組為基礎。 您只能選取報表伺服器之轉譯延伸模組所支援的輸出格式。  
  
###  <a name="to-create-a-subscription-to-deliver-a-report-to-a-sharepoint-library"></a><a name="bkmk_tosharepoint_library"></a> 若要建立傳遞報表至 SharePoint 文件庫的訂閱  
  
1.  瀏覽至包含報表的 SharePoint 文件庫。  
  
2.  按一下報表旁的向下箭頭，然後選取 **[管理訂閱]** 。  
  
3.  按一下 [ **加入訂閱**]。  
  
4.  在 **[傳遞延伸模組]** 中，選取 **[SharePoint 文件庫]** 。  
  
5.  在 **[文件庫]** 中，選取相同網站內的文件庫。  
  
6.  在 **[檔案選項]** 中，指定訂閱將建立之文件的檔案名稱和標題。  
  
7.  在 **[輸出格式]** 中，選取應用程式格式。  
  
     網頁封存 (MHTML) 是預設值，因為它會產生獨立的 HTML 檔案，但是它將不會保留原始報表中可能存在的互動式報表功能。  
  
8.  在 **[覆寫選項]** 中，指定可決定後續傳遞項目是否會覆寫檔案的選項。 如果您要保留之前的傳遞項目，可以選取 **[使用唯一的名稱建立檔案]** 。 如此就會將數字附加至新的檔案，以便建立唯一的檔案名稱。  
  
9. 在 **[傳遞事件]** 中，指定導致訂閱執行的排程或事件。 每當使用快照集資料執行之報表的資料重新整理時，您就可以建立自訂排程、選取共用排程 (如果可用的話) 或執行訂閱。 如需排程和資料處理的詳細資訊，請參閱[設定處理選項 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)。  
  
10. 在 **[參數]** 中，如果您要建立參數化報表的訂閱，請指定您想要在處理訂閱時搭配報表使用的值。 如果您選取的報表不包含參數，表示在此頁面上看不到報表區段。 如需參數的詳細資訊，請參閱[在已發行的報表上設定參數 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)。  
  
###  <a name="to-create-a-subscription-for-shared-folder-delivery"></a><a name="bkmk_subscription_for_sharedfolder"></a> 若要建立共用資料夾傳遞的訂閱  
  
1.  瀏覽至包含報表的 SharePoint 文件庫。  
  
2.  按一下報表旁的向下箭頭，然後選取 **[管理訂閱]** 。  
  
3.  按一下 [ **加入訂閱**]。  
  
4.  在 **[傳遞延伸模組]** 中，選取 **[Windows 檔案共用]** 。  
  
5.  在 **[檔案名稱]** 中，輸入將在共用資料夾中建立之檔案的名稱。  
  
6.  在 [路徑]  中，以統一命名慣例 (UNC) 格式輸入包含電腦網路名稱的資料夾路徑。 資料夾路徑中不要包含尾端的反斜線。 範例路徑可能是 `\\ComputerName01\Public\MyReports`，其中 Public 和 MyReports 都是共用資料夾。  
  
7.  在 **[轉譯格式]** 中，選取報表的應用程式格式。  
  
8.  在 **[寫入模式]** 中，選擇 **[無]** 、 **[自動遞增]** 或 **[覆寫]** 。 這些選項會決定後續傳遞項目是否會覆寫檔案。 如果要保留之前的傳遞項目，可以選擇 **[自動遞增]** 。 如此就會將數字附加至新的檔案，以便建立唯一的檔案名稱。 如果選擇 **[無]** ，而且目標位置中已存在相同名稱的檔案，就不會進行任何傳遞。  
  
9. 在 **[副檔名]** 中，選擇 **[True]** 加入對應至應用程式檔案格式的副檔名，或 [False] 建立不含副檔名的檔案。  
  
10. 在 **[使用者名稱]** 和 **[密碼]** 中，輸入在共用資料夾上具有寫入權限的認證。  
  
11. 在 **[傳遞事件]** 中，指定導致訂閱執行的排程或事件。 每當使用快照集資料執行之報表的資料重新整理時，您就可以建立自訂排程、選取共用排程 (如果可用的話) 或執行訂閱。 如需排程和資料處理的詳細資訊，請參閱[設定處理選項 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)。  
  
12. 在 **[參數]** 中，如果您要建立參數化報表的訂閱，請指定您想要在處理訂閱時搭配報表使用的值。 如需參數的詳細資訊，請參閱[在已發行的報表上設定參數 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)。  
  
###  <a name="to-create-a-subscription-for-report-server-e-mail-delivery"></a><a name="bkmk_subscription_for_email"></a> 建立報表伺服器電子郵件傳遞的訂閱  
  
1.  瀏覽至包含報表的 SharePoint 文件庫。  
  
2.  按一下報表旁的向下箭頭，然後選取 **[管理訂閱]** 。  
  
3.  按一下 [ **加入訂閱**]。  
  
4.  在 [傳遞延伸模組]  中，選取 [電子郵件]  。  
  
5.  在 [傳遞選項]  中，指定要將報表傳送至其中的電子郵件地址。  
  
6.  或者，您可以修改 [主旨] 行。 [主旨] 行會使用內建參數，以便擷取報表名稱和處理報表的時間。 這些參數是唯一可用的內建參數。 雖然這些參數是可自訂 [主旨] 行中顯示之文字的預留位置，但是您可以將它取代成靜態文字。  
  
7.  如果要在訊息主體中內嵌報表 URL，請選擇 **[包含這個報表的連結]** 。  
  
8.  在 **[報表內容]** 中，指定您是否想要在訊息主體中內嵌實際的報表。  
  
     轉譯格式和瀏覽器會決定是否要內嵌或附加報表。 如果您的瀏覽器支援 HTML 4.0 與 MHTML，而且您選取網頁封存轉譯格式，則報表會內嵌為訊息的一部分。 所有其他轉譯格式 (CSV、PDF 等等) 均以附加檔案傳遞報表。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 在傳送報表之前，不會檢查附加檔案或訊息的大小。 如果附加檔案或訊息超過郵件伺服器所允許的上限，將不會傳遞報表。 如果是大型報表，請選擇其中一個傳遞選項 (例如 URL 或通知)。  
  
9. 在 **[傳遞事件]** 中，指定導致訂閱執行的排程或事件。 每當使用快照集資料執行之報表的資料重新整理時，您就可以建立自訂排程、選取共用排程 (如果可用的話) 或執行訂閱。 如需排程和資料處理的詳細資訊，請參閱[設定處理選項 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)。  
  
10. 在 **[參數]** 中，如果您要建立參數化報表的訂閱，請指定您想要在處理訂閱時搭配報表使用的值。 如需參數的詳細資訊，請參閱[在已發行的報表上設定參數 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)。  
  
###  <a name="to-view-or-modify-a-subscription"></a><a name="bkmk_to_modify_subscription"></a> 檢視或修改訂閱  
  
1.  瀏覽至包含報表的 SharePoint 文件庫。  
  
2.  按一下報表旁的向下箭頭，然後按一下 **[管理訂閱]** 。  
  
3.  每個訂閱都可由傳遞類型加以識別。 按一下訂閱類型，即可檢視並變更現有的屬性。  
  
###  <a name="to-delete-a-subscription"></a><a name="bkmk_to_delete_subscription"></a> 刪除訂閱  
  
1.  瀏覽至包含報表的 SharePoint 文件庫。  
  
2.  按一下報表旁的向下箭頭，然後按一下 **[管理訂閱]** 。  
  
3.  按一下訂閱旁的核取方塊，然後按一下 **[刪除]** 。  
  
## <a name="see-also"></a>另請參閱  
 [訂閱與傳遞 &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Reporting Services 中的電子郵件傳遞](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)   
 [Reporting Services 中的檔案共用傳遞](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)   
 [Reporting Services 中的 SharePoint 文件庫傳遞](../../reporting-services/subscriptions/sharepoint-library-delivery-in-reporting-services.md)   
 [為電子郵件傳遞設定報表伺服器 (SSRS 設定管理員)](https://msdn.microsoft.com/b838f970-d11a-4239-b164-8d11f4581d83)  
  
  
