---
title: 第 3 課：定義資料驅動訂閱 | Microsoft Docs
ms.date: 05/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 89197b9b-7502-4fe2-bea3-ed7943eebf3b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ad6781d27078053a67d236c6a96b21fd67e355df
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47703476"
---
# <a name="lesson-3-defining-a-data-driven-subscription"></a>Lesson 3: Defining a Data-Driven Subscription
在這個 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 教學課程中，您將利用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 入口網站資料驅動訂閱頁面來連接訂閱資料來源、建立擷取訂閱資料的查詢，以及將結果集對應至報表和傳遞選項。  
  
> [!NOTE]  
> 開始之前，請確認 **[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent** 服務正在執行。 若未執行，您就無法儲存訂閱。  驗證的其中一個方法是開啟 [SQL Server 組態管理員](../relational-databases/sql-server-configuration-manager.md)。
這一課會假設您已完成第 1 課和第 2 課，而且報表資料來源使用預存認證。  如需詳細資訊，請參閱 [第 2 課：修改報表資料來源屬性](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md)  
  
## <a name="bkmk_startwizard"></a>啟動資料驅動訂閱精靈  
  
1.  在 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 入口網站中，按一下 [首頁]，然後巡覽至包含 **Sales Orders** 報表的資料夾。  
  
2.  在報表的操作功能表 ![ssrs_tutorial_datadriven_reportmenu](../reporting-services/media/ssrs-tutorial-datadriven-reportmenu.png) 中，按一下 [管理]，然後按一下左窗格中的 [訂閱]。  
  
3.  按一下 [+ 新增訂閱]。 如果您沒有看見這個按鈕，表示您沒有「內容管理員」權限。 
  
## <a name="define-a-description"></a>定義描述  
1.  在 [描述] 中，輸入 **銷售訂單傳遞** 。
## <a name="type"></a>類型
1.  按一下 [資料驅動訂閱]。  
## <a name="schedule"></a>[排程]
1. 在 [排程] 區段中，按一下 [報表特定排程]。
2. 按一下 [編輯排程]。
3.  在 **[排程詳細資料]** 中，按一下 **[一次]**。  
4.  請指定現在以後的幾分鐘做為開始時間。  
5.  按一下 **[套用]**。
## <a name="destination"></a>目的地  
1.  在 [目的地] 區段中，選取 [Windows 檔案共用] 傳遞方法。  

## <a name="dataset"></a>資料集
1. 按一下 [編輯資料集]。
2. 選取 **[自訂資料來源]**。
3. 選取 [Microsoft SQL Server] 作為資料來源 [連線] 類型。
4. 在 [連接字串] 中，輸入下列連接字串。 「訂閱者」是您在第 1 課所建立的資料庫。 
  
    ```  
    data source=localhost; initial catalog=Subscribers
    ```
    
 ## <a name="credentials"></a>認證
 1. 選取 [使用以下認證]。
 2. 選取 [Windows 使用者名稱與密碼]。
 3.  在 **[使用者名稱]** 和 **[密碼]** 中，輸入網域使用者名稱和密碼。 指定 **[使用者名稱]** 時，請同時包括網域和使用者帳戶。
     > [!NOTE]  
    > 用於連接至訂閱者資料來源的認證不會傳回給 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。 如果您稍後修改了訂閱，就必須重新輸入用於連接到資料來源的密碼。
## <a name="query"></a>查詢      
1.  在查詢方塊中，輸入下列查詢：  
  
    ```  
    Select * from OrderInfo  
    ```  
  
2.  將逾時指定為 30 秒。  
  
3.  按一下 [驗證查詢]，然後按一下 [套用]。
## <a name="delivery-options"></a>傳遞選項
填入下列值：

參數  |值的來源  | 值/欄位  
---------|---------|---------
**檔案名稱**     |從資料集取得值 | 單     
**路徑**     | 輸入值  | 在 [值] 中，輸入您擁有寫入權限之公用檔案共用的名稱 (例如 `\\mycomputer\public\myreports`)。 
**轉譯格式** | 從資料集取得值 | [格式]
**寫入模式**| 輸入值| 自動遞增    
**副檔名** |輸入值 |True
**[使用者名稱]** | 輸入值 | 輸入網域使用者帳戶。 請以此格式來輸入：\<網域>\\\<帳戶>。 使用者帳戶必須擁有您設定之路徑的權限。 
**密碼** | 輸入值 | 輸入密碼

## <a name="report-parameters"></a>報表參數
 1. 在 [OrderNumber] 欄位中，選取 [從資料集取得值]。 在 [值] 中，選取 **[Order]**。 
 2. 按一下 [建立訂閱]。
   
## <a name="next-steps"></a>Next Steps  
當訂閱執行時，會將四個報表檔傳遞至您指定的檔案共用，「訂閱者」  資料來源中的每筆訂單各一個。 在資料 (資料應該隨著訂單而不同)、轉譯格式及檔案格式等方面，每項傳遞都應該是唯一的。 您可以開啟共用資料夾中的每一份報表，確認每個版本都是根據您定義的訂閱選項來自訂的。  
  
![訂閱建立的檔案清單](../reporting-services/media/ssrs-tutorial-datadriven-subscription-filelist.gif "訂閱建立的檔案清單")  
  
入口網站中的訂閱頁面將包含訂閱的 [上次執行] 日期和 [狀態]。 
**注意：** 請在訂閱執行之後重新整理頁面，以便查看更新的資訊。  
    
![報表管理員中的訂閱結果](../reporting-services/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.png "報表管理員中的訂閱結果")  
  
此步驟是＜定義資料驅動訂閱＞教學課程的總結。   
  
## <a name="see-also"></a>另請參閱  
[訂閱與傳遞 &#40;Reporting Services&#41;](../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
[資料驅動訂閱](../reporting-services/subscriptions/data-driven-subscriptions.md)  
[建立、修改和刪除資料驅動訂閱](../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)  
[使用外部資料來源以取得訂閱者資料 &#40;資料驅動訂閱&#41;](../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)  
  
  
  

