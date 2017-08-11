---
title: "釘選到 Power BI 儀表板的 Reporting Services 項目 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 09/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pbi
- dashboard
- pin
- powerbi
- power bi integration
ms.assetid: 1d96c3f7-2fd4-40f7-8d1c-14a7f54cdb15
caps.latest.revision: 23
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ce952f1d25529948bbcc3dbae5f1707af9683b11
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="pin-reporting-services-items-to-power-bi-dashboards"></a>Power BI 儀表板的固定 Reporting Services 項目
  [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] 讓使用者能夠將 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表項目從報表檢視器工具列固定到 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 儀表板，當成新的圖格。   若要固定，您的系統管理員必須先整合報表伺服器和 Azure Active Directory 及 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]。  
  
 ![rs_powerbi_icon](../reporting-services/media/ssrs-powerbi-icon.png "rs_powerbi_icon")  
  
 [!INCLUDE[applies](../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 原生模式
  
##  <a name="bkmk_requirements_to_pin"></a> 固定需求  
  
-   針對 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 整合設定報表伺服器。 如需詳細資訊，請參閱 [Power BI 報表伺服器整合 &#40;組態管理員&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)。 如果尚未設定報表伺服器，工具列就不會看到 [釘選到 Power BI 儀表板]  按鈕。  
  
     ![ssRS_Report_PowerBI](../reporting-services/media/ssrs-report-powerbi.png)  
  
-   從您釘選[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]t 中的報表檢視器[!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]他範例`http://myserver/Reports`。  您無法從 [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion-md.md)]、從 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的報表設計師，或從報表伺服器 URL 固定。  例如`http://myserver/ReportServer`。  
  
-   您必須設定瀏覽器允許來自報表伺服器網站的快顯。  
  
-   如果您想要重新整理固定的項目，報表需有預存認證設定。  當您固定項目，就會自動建立 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 訂閱來管理儀表板的項目資料重新整理。  如果報表不使用預存認證，則當訂閱執行時，您會在 [我的訂閱]  頁面看到類似下列的錯誤訊息。  
  
        PowerBI Delivery error: dashboard: IT Spend Analysis Sample, visual: Chart2, error: The current action cannot be completed. The user data source credentials do not meet the requirements to run this report or shared dataset. Either the user data source credential.
 
    請參閱 [在 Reporting Services 資料來源中儲存認證](../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)中的＜為報表特定的資料來源設定預存認證 (原生模式)＞一節  
  
##  <a name="bkmk_supported_items"></a> 您可以固定的項目  
 下列報表項目可以固定到 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 儀表板。  您無法固定資料區域內部的巢狀項目。 例如，您無法釘選 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 資料表或清單內部的巢狀項目。  
  
-   圖表  
  
-   量測計面板  
  
-   地圖  
  
-   影像  
  
-   項目必須在報表主體中。  您無法固定頁首或頁尾的項目。  
  
-   您可以固定最上層矩形內部的個別項目，但無法將它們全部固定為單一群組。  
  
##  <a name="bkmk_to_pin"></a> 固定報表項目  
  
1. 確認您已登入 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]。 在[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]，選取功能表項目**我的設定**並登入。 如需詳細資訊，請參閱  [Power BI 整合的我的設定 &#40;入口網站&#41;](http://msdn.microsoft.com/en-us/85c2fac7-80bf-45b7-8654-764b5f5231f5) 。

    ![ssRS_WebPortal_MySettings](../reporting-services/media/ssrs-webportal-mysettings.png)  
  
2. 巡覽至包含報表的 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 資料夾，然後檢視報表。  
  
3. 檢視報表時，選取**釘選到 Power BI**按鈕工具列。  如果您還沒有登入，系統會提示您登入。  如果看不到 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 按鈕，表示報表伺服器尚未與 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]整合。 如需詳細資訊，請參閱 [Power BI 報表伺服器整合 &#40;組態管理員&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)。  
  
    ![ssRS_Report_PowerBI](../reporting-services/media/ssrs-report-powerbi.png)  
  
4. 選取您要釘選到 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]的報表項目。 一次只能固定一個項目。  報表檢視器會以陰影檢視顯示報表，反白顯示您可以固定的報表項目，以深色陰影顯示無法固定的項目。  
  
    **(1)** 選取包含您要釘選之目的地儀表板的群組， **(2)** 選取您也要釘選項目的儀表板，以及 **(3)** 選取您要在儀表板中更新磚的頻率。   ![請注意](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "注意")重新整理受[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]訂用帳戶已釘選的項目之後，您可以編輯訂用帳戶和設定不同的重新整理排程。  
  
    ![ssRS_Pin_to_PowerBI](../reporting-services/media/ssrs-pin-to-powerbi.png)  
  
5. 選取**Pin**  
  
    在**Pin 成功** 對話方塊中，您可以選取連結**在 Power BI 中查看**瀏覽至儀表板，並查看您剛才固定的項目。  
  
6. 選取 [關閉] 返回報表的標準模式。  
  
##  <a name="bkmk_in_the_dashboard"></a> 在儀表板中

在報表項目固定到儀表板之後，圖格看起來就和其他的儀表板圖格一樣，不會有任何視覺效果指示圖格來自 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]。 下列清單摘要說明如何從報表項目填入圖格屬性。  
  
從 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 儀表板中，固定的報表項目行為和其他圖格並無二致︰

**(1)** 您可以將磚釘選到其他儀表板。

**(2)**中**圖格詳細資料**您會注意到[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]報表標題用於磚的預設標題。

**(3)** 磚副標題是根據磚釘選的日期和時間，或根據 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]上次重新整理資料的日期和時間。 重新整理排程由 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 訂閱管理，這個訂閱是在您固定報表項目時自動建立的。

**(4)** 如果您按一下磚本身， [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 會使用 **(3) 自訂連結** 巡覽至已註冊報表伺服器的 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 頁面。 從 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]固定項目時，即設定連結。 如果報表伺服器沒有網際網路連線，您會在瀏覽器中看到錯誤。  

![ssrs_pinned_tile_details](../reporting-services/media/ssrs-pinned-tile-details.png "ssrs_pinned_tile_details")  
  
##  <a name="bkmk-troubleshoot"></a> 疑難排解問題  
  
-   **報表檢視器工具列上沒有 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 按鈕**︰這表示報表伺服器尚未與 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 整合。 如需詳細資訊，請參閱 [Power BI 報表伺服器整合 &#40;組態管理員&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)。  
  
- **無法釘選**︰當您嘗試釘選項目時，會看到下列錯誤訊息︰請參閱 [您可以釘選的項目](#bkmk_supported_items)一節。  
  
      Cannot Pin: There are no report items on this page that you can pin to [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].  
  
-   **儀表板中** 的項目顯示過時資料 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] ，但它確實已更新了一段時間。  使用者認證 Token 已過期，您需要再次登入。  向 Azure 註冊的使用者認證， [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 的有效期為 90 天。 在 t[!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]他按一下**我的設定**。 如需詳細資訊，請參閱 [Power BI 整合的我的設定 &#40;入口網站&#41;](http://msdn.microsoft.com/en-us/85c2fac7-80bf-45b7-8654-764b5f5231f5)。  
  
-   **儀表板中** 固定的項目顯示過時資料 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] ，它根本沒有重新整理過。  問題在於報表未設定使用預存認證。 報表必須使用預存認證，因為固定報表項目的動作會建立 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 訂閱來管理圖格的重新整理排程。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 訂閱需要預存的認證。 如果您檢閱 [我的訂閱]  頁面，會看到類似下面的錯誤訊息：  
  
        PowerBI Delivery error: dashboard: SSRS items, visual: Image3, error: The current action cannot be completed. The user data source credentials do not meet the requirements to run this report or shared dataset. Either the user data source credentials are not stored in the report server database, or the user data source is configured not to require credentials but the unattended execution account is not specified. (rsInvalidDataSourceCredentialSetting)
  
-   **過期的 Power BI 認證︰**  您嘗試固定項目，但看到下列錯誤訊息。 在[!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]，按一下 **我的設定**在我的設定] 頁面上，按一下 [**登入**。 如需詳細資訊，請參閱  [Power BI 整合的我的設定 &#40;入口網站&#41;](http://msdn.microsoft.com/en-us/85c2fac7-80bf-45b7-8654-764b5f5231f5) 。  
  
        Cannot Pin : Unexpected Server Error: Missing, invalid or expired Power BI credentials.  
  
-   **無法釘選**︰如果您嘗試將項目釘選到唯讀狀態的儀表板，您會看到類似下面的錯誤訊息：  
  
        Server Error : The item 'Dashboard deleted 015cf022-8e2f-462e-88e5-75ab0a04c4d0' cannot be found. (rsItemNotFound)  
  
##  <a name="bkmk_subscription_management"></a> 訂閱管理  
 除了＜疑難排解＞一節描述的訂閱相關問題，下列資訊也會協助您維護 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 的相關訂閱。
  
-   **項目名稱變更︰** 如果重新命名或刪除固定的報表項目，則 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 圖格就不再更新，而您會看到類似下面的錯誤訊息。  如果您將項目重新命名回原來的名稱，訂閱就會再次開始工作，而圖格會按照訂閱排程重新整理。  
  
        PowerBI Delivery error: dashboard: SSRS items, visual: Image1, error: Error: Report item 'Image1' cannot be found.  
  
     您也可以編輯訂閱內容，並將 [報表視覺效果名稱]  變更為適當的報表項目名稱。 ![變更用於 power bi 重新整理視覺效果](../reporting-services/media/ssrs-powerbi-subscription-visual.png "變更用於 power bi 重新整理視覺效果")  
  
-   **刪除圖格**。 如果您刪除在圖格[!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]，相關聯的訂用帳戶不會刪除中[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]以及**我的訂閱** 頁面上，您會看到類似下列的錯誤。 您可以刪除訂閱。  
  
        PowerBI Delivery error: dashboard: SSRS items, visual: Image3, error: The item 'Tile deleted af7131d9-5eaf-480f-ba45-943a07d19c9f' cannot be found.  

## <a name="video"></a>視訊

<iframe width="560" height="315" src="https://www.youtube.com/embed/QhPQObqmMPc" frameborder="0" allowfullscreen></iframe>

## <a name="see-also"></a>請參閱＜  
 [Power BI 報表伺服器整合 &#40;組態管理員&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
 [Power BI 整合的我的設定 &#40;入口網站&#41;](http://msdn.microsoft.com/en-us/85c2fac7-80bf-45b7-8654-764b5f5231f5)  
 [Power BI 的儀表板](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]


