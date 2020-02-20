---
title: 將編頁報表項目釘選到 Power BI 儀表板 - Reporting Services | Microsoft Docs
ms.date: 01/14/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
description: 您可以將內部部署 Reporting Services 編頁報表項目釘選到 Power BI 服務中的儀表板，作為新的磚。
ms.topic: conceptual
helpviewer_keywords:
- pbi
- dashboard
- pin
- powerbi
- power bi integration
ms.assetid: 1d96c3f7-2fd4-40f7-8d1c-14a7f54cdb15
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: da984efa4e0b4d964cf947929094ee7b392063f2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75952474"
---
# <a name="pin-reporting-services-paginated-report-items-to-dashboards-in-power-bi"></a>將 Reporting Services 編頁報表項目釘選到 Power BI 中的儀表板

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

您可以將內部部署 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 編頁報表項目釘選到 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 服務中的儀表板，作為新的磚。   若要固定，您的系統管理員必須先整合報表伺服器和 Azure Active Directory 及 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]。  
  
##  <a name="bkmk_requirements_to_pin"></a> 固定需求  
  
-   針對 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 整合設定報表伺服器。 如需詳細資訊，請參閱 [Power BI 報表伺服器整合 &#40;組態管理員&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)。 如果尚未設定報表伺服器，您將不會在報表檢視器工具列上看到 [釘選到 Power BI 儀表板]  按鈕。  
  
     ![報表檢視器工具列](../reporting-services/media/ssrs-report-powerbi.png)  
  
-   您會從[!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表檢視器釘選，例如 `https://myserver/Reports`。  您無法從[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)]、[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的報表設計師或報表伺服器 URL 釘選。  例如，`https://myserver/ReportServer`。  
  
-   您必須設定瀏覽器允許來自報表伺服器網站的快顯。  
  
-   如果您想要重新整理釘選的項目，您需要設定報表使用預存認證。  當您固定項目，就會自動建立 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 訂閱來管理儀表板的項目資料重新整理。  如果報表不使用預存認證，則當訂閱執行時，您會在 [我的訂閱]  頁面看到類似下面的訊息。  
  
    「Power BI 傳遞錯誤：儀表板：IT 支出分析範例，視覺效果：Chart2，錯誤：無法完成目前的動作。 使用者資料來源認證不符合需求，無法執行這份報表或執行共用資料集。 任一使用者資料來源認證。」
 
    請參閱 [在 Reporting Services 資料來源中儲存認證](../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)中的＜為報表特定的資料來源設定預存認證 (原生模式)＞一節  
  
##  <a name="bkmk_supported_items"></a> 您可以固定的項目  
 下列報表項目可以固定到 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 儀表板。  您無法釘選資料區域內部的巢狀項目。 例如，您無法釘選 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 資料表或清單內部的巢狀項目。  
  
-   圖表  
-   量測計面板  
-   地圖  
-   影像  
-   項目必須在報表主體中。  您無法釘選頁首或頁尾的項目。  
-   您可以釘選最上層矩形內部的個別項目，但無法將它們全部釘選為單一群組。  
  
##  <a name="bkmk_to_pin"></a> 固定報表項目  
  
1. 確認您已登入 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]。 在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]中，選取 [我的設定]  功能表項目並登入。 如需詳細資訊，請參閱 [Power BI 整合的我的設定 &#40;入口網站&#41;](my-settings-for-power-bi-integration-web-portal.md)。

    ![ssRS_WebPortal_MySettings](../reporting-services/media/ssrs-webportal-mysettings.png)  
  
2. 巡覽至包含報表的 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 資料夾，然後檢視報表。  
  
3. 檢視報表時，選取工具列的 [釘選到 Power BI]  按鈕。  如果您還沒有登入，系統會提示您登入。  如果看不到 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 按鈕，表示報表伺服器尚未與 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]整合。 如需詳細資訊，請參閱 [Power BI 報表伺服器整合 &#40;組態管理員&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)。  
  
    ![ssRS_Report_PowerBI](../reporting-services/media/ssrs-report-powerbi.png)  
  
4. 選取您要釘選到 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]的報表項目。 一次只能固定一個項目。  報表檢視器會以陰影檢視顯示報表，醒目提示您可以釘選的報表項目，並以深色陰影顯示無法釘選的項目。  
  
    **(1)** 選取包含您要釘選之目的地儀表板的群組， **(2)** 選取您也要釘選項目的儀表板，以及 **(3)** 選取您要在儀表板中更新磚的頻率。   ![注意](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/ssrs-fyi-note.png "注意") 重新整理由 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 訂用帳戶管理，而釘選項目之後，您可以編輯訂用帳戶及設定不同的重新整理排程。  
  
    ![ssRS_Pin_to_PowerBI](../reporting-services/media/ssrs-pin-to-powerbi.png)  
  
5. 選取 [釘選]   
  
    在 [釘選成功]  對話方塊中，您可以選取 [在 Power BI 中查看]  連結以巡覽至儀表板，並查看您剛才釘選的項目。  
  
6. 選取 [關閉]  返回報表的標準模式。  
  
##  <a name="bkmk_in_the_dashboard"></a> 在儀表板中

在報表項目固定到儀表板之後，圖格看起來就和其他的儀表板圖格一樣，不會有任何視覺效果指示圖格來自 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]。 下列清單摘要說明如何從報表項目填入圖格屬性。  
  
從 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 儀表板中，固定的報表項目行為和其他圖格並無二致︰

**(1)** 您可以將磚釘選到其他儀表板。

**(2)** 在 [磚詳細資料]  中您會發現，磚的預設標題使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 的報表標題。

**(3)** 磚副標題是根據磚釘選的日期和時間，或根據 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]上次重新整理資料的日期和時間。 重新整理排程由 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 訂閱管理，這個訂閱是在您固定報表項目時自動建立的。

**(5)** 如果您選取磚本身，[!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 會使用 **(4) 自訂連結**巡覽至已註冊報表伺服器的 [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] 頁面。 從 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]固定項目時，即設定連結。 如果報表伺服器沒有網際網路連線，您會在瀏覽器中看到錯誤。  

![ssrs_pinned_tile_details](../reporting-services/media/ssrs-pinned-tile-details.png "ssrs_pinned_tile_details")  
  
##  <a name="bkmk-troubleshoot"></a> 疑難排解問題  
  
-   **報表檢視器工具列上沒有 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 按鈕：** 此訊息表示報表伺服器尚未與 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 整合。 如需詳細資訊，請參閱 [Power BI 報表伺服器整合 &#40;組態管理員&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)。  
  
- **無法釘選**：當您嘗試釘選項目時，會看到下列錯誤訊息：請參閱[您可以釘選的項目](#bkmk_supported_items)一節。  
  
    「無法釘選：這個頁面上沒有任何報表項目可以固定到 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]。」  
  
-   **儀表板中** 的項目顯示過時資料 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] ，但它確實已更新了一段時間。  使用者認證 Token 已過期，您需要再次登入。  向 Azure 註冊的使用者認證， [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 的有效期為 90 天。 在[!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]中，按一下 [我的設定]  。 如需詳細資訊，請參閱 [Power BI 整合的我的設定 &#40;入口網站&#41;](my-settings-for-power-bi-integration-web-portal.md)。  
  
-   **儀表板中** 固定的項目顯示過時資料 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] ，它根本沒有重新整理過。  問題在於報表未設定使用預存認證。 報表必須使用預存認證，因為釘選報表項目的動作會建立 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 訂閱來管理磚的重新整理排程。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 訂閱需要預存的認證。 如果您檢閱 [我的訂閱]  頁面，會看到類似下面的錯誤訊息：  
  
    「Power BI 傳遞錯誤：儀表板：SSRS 專案，視覺效果：Image3，錯誤：無法完成目前的動作。 使用者資料來源認證不符合需求，無法執行這份報表或執行共用資料集。 使用者資料來源認證未儲存在報表伺服器資料庫中，或使用者資料來源設定為不需要認證，但未指定自動的執行帳戶。 (rsInvalidDataSourceCredentialSetting)」
  
-   **過期的 Power BI 認證：** 您嘗試釘選項目，但看到下列錯誤訊息。 在[!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]中，按一下 [我的設定]  ，然後按一下 [我的設定] 頁面上的 [登入]  。 如需詳細資訊，請參閱 [Power BI 整合的我的設定 &#40;入口網站&#41;](my-settings-for-power-bi-integration-web-portal.md)。  
  
    「無法釘選：未預期的伺服器錯誤：Power BI 認證遺失、無效或已過期。」  
  
-   **無法釘選**：如果您嘗試將項目釘選到唯讀狀態的儀表板，您會看到類似下面的錯誤訊息：  
  
    「伺服器錯誤：找不到『儀表板已刪除 015cf022-8e2f-462e-88e5-75ab0a04c4d0』項目。 (rsItemNotFound)」  

-   **Power BI 應用程式中的磚會顯示過時資料：** 如果您將 Reporting Services 報表項目釘選到儀表板，然後在應用程式中散發該儀表板，則該儀表板中的釘選報表項目將不會更新。 

##  <a name="bkmk_subscription_management"></a> 訂閱管理  
 除了＜疑難排解＞一節描述的訂閱相關問題，下列資訊也會協助您維護 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 的相關訂閱。
  
-   **項目名稱變更：** 如果重新命名或刪除釘選的報表項目，則 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 磚就不再更新，而您會看到類似下面的錯誤訊息。  如果您將項目重新命名回原來的名稱，訂閱就會再次開始工作，而圖格會按照訂閱排程重新整理。  
  
    「Power BI 傳遞錯誤：儀表板：SSRS 專案，視覺效果：Image1，錯誤：錯誤：找不到 "Image1" 報表項目。」  
  
    您也可以編輯訂閱內容，並將 [報表視覺效果名稱]  變更為適當的報表項目名稱。 ![變更用於 Power BI 重新整理的視覺效果](../reporting-services/media/ssrs-powerbi-subscription-visual.png "變更用於 Power BI 重新整理的視覺效果")  
  
-   **刪除圖格**。 如果您在 [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] 中刪除磚，就不會在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中刪除相關聯的訂閱，而在 [我的訂閱]  頁面上會看到類似下面的錯誤。 您可以刪除訂閱。  
  
    「Power BI 傳遞錯誤：儀表板：SSRS 專案，視覺效果：Image3，錯誤：找不到『磚已刪除 af7131d9-5eaf-480f-ba45-943a07d19c9f』項目。」  

## <a name="video"></a>影片

<iframe width="560" height="315" src="https://www.youtube.com/embed/QhPQObqmMPc" frameborder="0" allowfullscreen></iframe>

## <a name="see-also"></a>另請參閱  
 [Power BI 報表伺服器整合 &#40;組態管理員&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
 [Power BI 整合的我的設定 &#40;入口網站&#41;](my-settings-for-power-bi-integration-web-portal.md)  
 [Power BI 的儀表板](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]

