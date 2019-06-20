---
title: 第 3 課：定義資料驅動訂閱 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 89197b9b-7502-4fe2-bea3-ed7943eebf3b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ee51a19d1dc169d2ae784d8a44403e021ff8b665
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108511"
---
# <a name="lesson-3-defining-a-data-driven-subscription"></a>第 3 課：定義資料驅動訂閱
  在這個課程中，您將利用資料驅動訂閱頁面來連接訂閱資料來源、建立擷取訂閱資料的查詢，以及將結果集對應至報表和傳遞選項。  
  
> [!NOTE]  
>  開始之前，請確認 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 服務正在執行。 若未執行，您就無法儲存訂閱。  
  
 這一課會假設您已完成第 1 課和第 2 課，而且報表資料來源使用預存認證。  如需詳細資訊，請參閱[第 2 課：修改報表資料來源屬性](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md)  
  
 本主題內容：  
  
-   [啟動資料驅動訂閱精靈](#bkmk_startwizard)  
  
-   [步驟 1-定義描述](#bkmk_definesubscription)  
  
-   [步驟 2-定義訂閱者資料來源的連接](#bkmk_defineconnectiontosubscriber)  
  
-   [步驟 3-定義擷取訂閱者資料的查詢](#bkmk_definequery)  
  
-   [步驟 4-設定傳遞選項](#bkmk_set_deliveryoptions)  
  
-   [步驟 5-設定參數值以改變報表輸出](#bkmk_configure_parameter)  
  
-   [步驟 6-為訂閱建立排程](#bkmk_schedule_subscription)  
  
##  <a name="bkmk_startwizard"></a> 啟動資料驅動訂閱精靈  
  
1.  在報表管理員中，按一下 **[首頁]** ，然後導覽至包含 **Sales Orders** 報表的資料夾。  
  
2.  在報表的內容功能表中，按一下 **[管理]** ，然後按一下 **[訂閱]** 索引標籤。  
  
3.  按一下 **新的資料驅動訂閱**。 如果您沒有看見這個按鈕，表示您沒有「內容管理員」權限。  
  
##  <a name="bkmk_definesubscription"></a> 步驟 1-定義描述  
  
1.  在 [描述] 中，輸入 **銷售訂單傳遞** 。  
  
2.  在 **[指定通知收件者的方式]** 中，選取 **[Windows FileShare]** 。  
  
3.  選取 **[僅為此訂閱指定]** ，然後按 **[下一步]** 。  
  
##  <a name="bkmk_defineconnectiontosubscriber"></a> 步驟 2-定義訂閱者資料來源的連接  
  
1.  選取 **[Microsoft SQL Server]** 做為資料來源類型。  
  
2.  在 [連接字串] 中，輸入下列連接字串：  
  
    ```  
    data source=localhost; initial catalog=Subscribers  
    ```  
  
    > [!NOTE]  
    >  訂閱者是您在第 1 課所建立的資料庫。  
  
3.  按一下 **[安全地儲存在報表伺服器中的認證]** 。  
  
4.  在 **[使用者名稱]** 和 **[密碼]** 中，輸入網域使用者名稱和密碼。 指定 **[使用者名稱]** 時，請同時包括網域和使用者帳戶。  
  
    > [!NOTE]  
    >  用於連接至訂閱者資料來源的認證不會傳回給 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。 如果您稍後修改了訂閱，就必須重新輸入用於連接到資料來源的密碼。  
  
5.  選取 **[連接到資料來源時做為 Windows 認證]** ，再按 **[下一步]** 。  
  
##  <a name="bkmk_definequery"></a> 步驟 3-定義擷取訂閱者資料的查詢  
  
1.  在查詢方塊中，輸入下列查詢：  
  
    ```  
    Select * from OrderInfo  
    ```  
  
2.  將逾時指定為 30 秒。  
  
3.  按一下 **[驗證]** ，再按 **[下一步]** 。  
  
##  <a name="bkmk_set_deliveryoptions"></a> 步驟 4-設定傳遞選項  
  
1.  針對 **[檔案名稱]** ，選取 **[從資料庫取值]** 。 選取 **[Order]** 欄位。  
  
2.  針對 **[路徑]** ，選取 **[指定靜態值]** 。 在 [設定值] 中，輸入您擁有寫入權限之公用檔案共用的名稱 (例如 `\\mycomputer\public\myreports`)。  
  
3.  針對 **[轉譯格式]** ，選取 **[從資料庫取值]** 。 選取 **[格式]** 。  
  
4.  針對 **[寫入模式]** ，選取 **[指定靜態值]** 並選取 **[自動遞增]** 。  
  
5.  針對 **[副檔名]** ，選取 **[指定靜態值]** 並選取 **[True]** 。  
  
6.  針對 **[使用者名稱]** ，選取 **[指定靜態值]** 。 輸入網域使用者帳戶。 請使用下列格式輸入： `<domain>\<account>`。 使用者帳戶必須擁有您在上述步驟中設定之路徑的權限。  
  
7.  針對 **[密碼]** ，選取 **[指定靜態值]** 。 輸入密碼。 請務必小心輸入密碼。 精靈不會驗證密碼。  
  
8.  按 **[下一步]** 。  
  
##  <a name="bkmk_configure_parameter"></a> 步驟 5-設定參數值以改變報表輸出  
  
1.  針對 **[OrderNumber]** ，選取 **[從資料庫取值]** 。 在 [值] 中，選取 **[Order]** 。 按 **[下一步]** 。  
  
##  <a name="bkmk_schedule_subscription"></a> 步驟 6-為訂閱建立排程  
  
1.  按一下 **[在為此訂閱建立的排程上]** ，然後按 **[下一步]** 。  
  
2.  在 **[排程詳細資料]** 中，按一下 **[一次]** 。  
  
3.  請指定現在以後的幾分鐘做為開始時間。  
  
4.  按一下 **[完成]** 。  
  
## <a name="next-steps"></a>後續步驟  
 當訂閱執行時，會將四個報表檔傳遞至您指定的檔案共用，「訂閱者」  資料來源中的每筆訂單各一個。 在資料 (資料應該隨著訂單而不同)、轉譯格式及檔案格式等方面，每項傳遞都應該是唯一的。 您可以開啟共用資料夾中的每一份報表，確認每個版本都是根據您定義的訂閱選項來自訂的。  
  
 ![訂閱建立的檔案清單](../../2014/tutorials/media/ssrs-tutorial-datadriven-subscription-filelist.gif "訂閱建立的檔案清單")  
  
 報表管理員中的訂閱頁面將包含訂閱的 **[上次執行]** 日期和 **[狀態]** 。  
  
> [!NOTE]  
>  請在訂閱執行之後重新整理頁面，以便查看更新的資訊。  
  
 ![報表管理員中的訂閱結果](../../2014/tutorials/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.gif "報表管理員中的訂閱結果")  
  
 此步驟是＜定義資料驅動訂閱＞教學課程的總結。 若要深入了解其他[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]教學課程，請參閱[Reporting Services 教學課程&#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立資料驅動訂閱 &#40;SSRS 教學課程&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [訂閱與傳遞 &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Data-Driven Subscriptions](subscriptions/data-driven-subscriptions.md)   
 [建立、 修改及刪除資料驅動訂閱](subscriptions/create-modify-and-delete-data-driven-subscriptions.md)   
 [使用外部資料來源以取得訂閱者資料 &#40;資料驅動訂閱&#41;](subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)  
  
  
