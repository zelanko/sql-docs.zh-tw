---
title: 建立、修改和刪除資料驅動訂閱 | Microsoft Docs
ms.date: 06/12/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- query-based subscriptions [Reporting Services]
- queries [Reporting Services], data-driven subscriptions
- subscriptions [Reporting Services], data-driven
- data-driven subscriptions
ms.assetid: 0ba2093e-9393-4eb6-af06-9da10988cfaf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b385e04cf2efa103dba4a66d4e794a7984814fb4
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67140272"
---
# <a name="create-modify-and-delete-data-driven-subscriptions"></a>建立、修改和刪除資料驅動訂閱
  資料驅動訂閱是查詢式訂閱，會在執行階段取得用於處理訂閱的資料值。 觸發訂閱時，會處理查詢以取得有關收件者、報表傳遞選項、轉譯格式，以及參數設定的最新資訊。 查詢結果會與訂閱定義結合，以建立動態訂閱，該動態訂閱會使用您已在員工資料庫、客戶資料庫，或包含可做為訂閱者資料之資訊的其他任何資料庫中維護的資料。  
  
 若要建立新的資料驅動訂閱或修改現有訂閱，請使用入口網站中的 [管理]   > [訂閱]  頁面。 [訂閱]  頁面會引導您逐步建立或修改訂閱。 若要在訂閱建立之後存取，請使用 [我的訂閱]  頁面或 [訂閱] 清單。 若要了解如何建立資料驅動訂閱，請參閱[建立資料驅動訂閱 &#40;SSRS 教學課程&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)。  
  
 本文內容：  
  
-   [管理和刪除資料驅動訂閱](#bkmk_manage_and_delete)  
  
-   [建立和修改資料驅動訂閱](#bkmk_create_and_modify)  
  
-   [定義查詢來擷取訂閱資訊](#bkmk_define_query)  
  
-   [執行訂閱](#bkmk_run_subscription)  
  
##  <a name="managing-and-deleting-a-data-driven-subscription"></a><a name="bkmk_manage_and_delete"></a> 管理和刪除資料驅動訂閱  
 您無法透過入口網站停止或刪除正在進行中的資料驅動訂閱。 因此，建議您使用共用排程來觸發資料驅動訂閱。 這樣一來，如果您想要暫時防止訂閱處理，就可以暫停觸發訂閱的排程。 如需詳細資訊，請參閱 [建立和管理原生模式報表伺服器的訂閱](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)。  
  
 若要刪除資料驅動訂閱，請選取 [訂閱]  頁面上報表旁的核取方塊，然後選取 [刪除]  。  
  
 如需如何取消資料驅動訂閱的指示，請參閱 [管理執行中的處理序](../../reporting-services/subscriptions/manage-a-running-process.md)。  
  
##  <a name="creating-and-modifying-a-data-driven-subscription"></a><a name="bkmk_create_and_modify"></a> 建立和修改資料驅動訂閱  
 若要建立資料驅動訂閱，請選取使用預存認證或無認證的報表。 當您建立資料驅動訂閱時，請考慮使用 [描述] 欄位的命名慣例，如此就能輕鬆區分標準訂閱與資料驅動訂閱。  
  
### <a name="to-create-a-data-driven-subscription-native-mode"></a>若要建立資料驅動訂閱 (原生模式)  
  
1. 在入口網站中，巡覽至包含報表的資料夾，以滑鼠右鍵按一下該報表，然後從下拉式功能表中選取 [管理]  。  
  
2. 選取 **[訂閱]** 索引標籤。  
  
3. 在 [訂閱]  頁面上選取 [+ 新增訂閱]  。  
  
### <a name="to-create-a-data-driven-subscription-sharepoint-mode"></a>若要建立資料驅動訂閱 (SharePoint 模式)  
  
1. 在 SharePoint 文件庫中，將滑鼠停留在報告上方，接著開啟 [選項] 功能表，然後按一下 **[管理訂閱]** 。  
  
2. 按一下 **[加入資料驅動訂閱]** 。  
  
### <a name="to-modify-an-existing-data-driven-subscription-native-mode"></a>若要修改現有的資料驅動訂閱 (原生模式)  
  
1. 在入口網站中，巡覽至包含報表的資料夾，以滑鼠右鍵按一下該報表，然後從下拉式功能表中選取 [管理]  。  
  
2. 選取 **[訂閱]** 索引標籤。  
  
3. 選取所要修改訂閱旁的核取方塊，然後選取 [編輯]  。 資料驅動訂閱在 [類型]  資料行中的值為「資料驅動」。  
  
### <a name="to-modify-an-existing-data-driven-subscription-sharepoint-mode"></a>若要修改現有的資料驅動訂閱 (SharePoint 模式)  
  
1.  在 SharePoint 文件庫中，將滑鼠停留在報告上方，接著開啟 [選項] 功能表，然後按一下 **[管理訂閱]** 。  
  
2.  選取您要修改的訂閱。  
  
    > [!NOTE]  
    > 您可以修改任何已經指定的值。 所有值均以第一次建立時的方式呈現，除了用來存取訂閱者資料存放區的密碼。 每次修改值的時候，都必須在第二頁或任何後續頁面重新輸入密碼。  
  
  在可以建立資料驅動訂閱之前，請先確定有滿足以下需求：  
  
-   **報表需求**。 報表必須使用預存認證或不使用認證，才能在執行階段擷取資料。 如果報表是使用模擬或委派的認證來連接外部資料來源，您便無法訂閱此報表；當處理此訂閱時，將無法使用建立或擁有此訂閱之使用者的認證。 預存認證可以是 Windows 帳戶或資料庫使用者帳戶。 如需詳細資訊，請參閱 [指定報表資料來源的認證及連接資訊](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)。  
  
     如果「報表產生器」報表是使用模型當做資料來源，而該模型包含模型項目安全性設定，您便無法訂閱此報表。 這項限制中只包含使用模型項目安全性的報表。  
  
     您不能在包含 `User!UserID` 運算式的報表上建立資料驅動訂閱。  
  
-   **資料需求**。 您必須有一個包含訂閱者資料的可存取外部資料來源。  
  
-   **使用者需求**。 此訂閱的作者必須具有「管理報表」和「管理所有訂閱」的權限。 如需項目層級工作權限的詳細資訊，請參閱 [工作和權限](../../reporting-services/security/tasks-and-permissions.md)。 此作者也必須具有適當的認證，才能存取包含訂閱者資料的外部資料來源。  
  
##  <a name="defining-a-query-that-retrieves-subscription-information"></a><a name="bkmk_define_query"></a> 定義查詢來擷取訂閱資訊  
 資料驅動訂閱必須指定查詢或命令來擷取訂閱者資料， 查詢應該針對每一個訂閱者產生一個資料列。 如果您是使用電子郵件傳遞延伸模組，則查詢應傳回每一個訂閱者的有效電子郵件別名。 傳遞的數目會依據查詢所傳回的資料列數目而定。 如果資料列集包括 10,000 個資料列，則訂閱會傳遞 10,000 個報表。  
  
 如果執行查詢很花時間，您可以增加逾時值以容納更多的處理。  
  
 針對此步驟，您必須在繼續之前先驗證查詢。 驗證並不會處理查詢，但會傳回在資料列集內的所有資料行清單，讓您可以在後續選取範圍中參考資料行。 如果查詢未通過驗證，您就無法繼續。 如果查詢語法不正確或資料來源的連接無效，查詢就無法通過驗證。 使用 **[上一步]** 按鈕，以更正資料來源。  
  
##  <a name="running-the-subscription"></a><a name="bkmk_run_subscription"></a> 執行訂閱  
 您必須指定處理訂閱的條件。 您可以指定排程，或觸發訂閱，讓更新與報表執行快照集一致。 資料驅動訂閱的處理和標準訂閱的處理相同。  
  
## <a name="see-also"></a>另請參閱  
 [建立及管理原生模式報表伺服器的訂閱](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [訂閱與傳遞 &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [報表伺服器的入口網站 (SSRS 原生模式)](../../reporting-services/web-portal-ssrs-native-mode.md)   
 [建立及管理原生模式報表伺服器的訂閱](create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [使用訂閱 (入口網站)](../../reporting-services/working-with-subscriptions-web-portal.md) [使用我的訂閱 (原生模式報表伺服器)](../../reporting-services/subscriptions/use-my-subscriptions-native-mode-report-server.md)  
 