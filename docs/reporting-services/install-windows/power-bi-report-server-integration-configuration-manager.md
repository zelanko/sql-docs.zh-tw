---
description: Power BI 報表伺服器整合 (組態管理員)
title: Power BI 報表伺服器整合 (設定管理員) | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.date: 09/17/2017
ms.openlocfilehash: d0eb3bcdd62d7f78799f754b668544cfdd01fcd9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991864"
---
# <a name="power-bi-report-server-integration-configuration-manager"></a>Power BI 報表伺服器整合 (組態管理員)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員中的 [Power BI 整合]**** 頁面是用來向所需的 Azure Active Directory (AD) 受管理租用戶註冊報表伺服器，以允許報表伺服器的使用者將支援的報表項目釘選到 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 儀表板。 如需您可以釘選的支援項目清單，請參閱 [將 Reporting Services 項目釘選到 Power BI 儀表板](../../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)。

## <a name="requirements-for-power-bi-integration"></a><a name="bkmk_requirements"></a> Power BI 整合的需求

除了使用中的網際網路連線，您還可以瀏覽至 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 服務，以下是完成 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]整合的需求。

- **Azure Active Directory：** 貴組織必須使用 Azure Active Directory，為 Azure 服務和 Web 應用程式提供目錄和身分識別管理。 如需詳細資訊，請參閱[什麼是 Azure Active Directory？](https://azure.microsoft.com/documentation/articles/active-directory-whatis/)

- **受管理的租用戶︰** 您要在其中釘選報表項目的 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 儀表板必須是 Azure AD 受管理租用戶的一部分。  組織首次訂閱 Microsoft 365 和 Microsoft Intune 等 Azure 服務時，受管理的租用戶便會自動建立。   目前不支援病毒式租用戶。  如需詳細資訊，請參閱 [什麼是 Azure AD 目錄？](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant)中的＜什麼是 Azure AD 租用戶＞和＜如何取得 Azure AD 目錄＞二節。

- 執行 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 整合的使用者需為 Azure AD 租用戶的成員，該租用戶為 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 系統管理員以及 ReportServer 目錄資料庫的系統管理員。

- 執行 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 整合的使用者需要搭配用來安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的帳戶，或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服務正在其下執行的帳戶來啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員

- 您想要從中釘選的報表必須使用預存的認證。 這不是 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 整合本身的需求，而是已釘選項目重新整理程序的需求。  釘選報表項目這項動作會建立 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱來管理 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]中磚的重新整理排程。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱需要預存的認證。 若報表不會使用預存的認證，使用者還是可以釘選報表項目，但當相關聯的訂閱嘗試將資料重新整理至 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]時，您會在 [我的訂閱] **** 頁面看到類似下列的錯誤訊息。

    Power BI 傳遞錯誤︰儀表板︰IT 花費分析範例，視覺效果：Chart2，錯誤︰無法完成目前的動作。 使用者資料來源認證不符合需求，無法執行這份報表或執行共用資料集。 任一使用者資料來源認證。

如需如何儲存認證的詳細資訊，請參閱[在 Reporting Services 資料來源中儲存認證](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)中的＜為報表特定的資料來源設定預存認證＞一節。

系統管理員可以檢閱  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 記錄檔以取得詳細資訊。  其會看到與下列文字類似的訊息。 將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Power Query 用於檔案是檢閱及監視 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 記錄檔的好方法。  如需詳細資訊和短片，請參閱 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)。

- subscription!WindowsService_1!1458!09/24/2015-00:09:27:: e ERROR: PowerBI 傳遞錯誤︰儀表板︰IT 花費分析範例，視覺效果：Chart2，錯誤︰無法完成目前的動作。 使用者資料來源認證不符合需求，無法執行這份報表或執行共用資料集。 使用者資料來源認證未儲存在報表伺服器資料庫中，或使用者資料來源設定為不需要認證，但未指定自動的執行帳戶。

- notification!WindowsService_1!1458!09/24/2015-00:09:27:: e ERROR: Error occurred processing subscription fcdb8581-d763-4b3b-ba3e-8572360df4f9: PowerBI 傳遞錯誤︰儀表板︰IT 花費分析範例，視覺效果：Chart2，錯誤︰無法完成目前的動作。 使用者資料來源認證不符合需求，無法執行這份報表或執行共用資料集。 使用者資料來源認證未儲存在報表伺服器資料庫中，或使用者資料來源設定為不需要認證，但未指定自動的執行帳戶。

## <a name="to-integrate-and-register-the-report-server"></a><a name="bkmk_steps2integrate"></a> 整合並註冊報表伺服器

從 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 組態管理員完成下列步驟。 如需詳細資訊，請參閱 [Reporting Services 組態管理員](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)。

1. 選取 [ [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 整合] 頁面。

2. 選取 [向 Power BI 註冊]****。

    >[!Note]
    > 確定未封鎖連接埠 443。

3. 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 登入對話方塊中，輸入您用來登入 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]的認證。

4. 註冊完成之後，[Power BI 註冊詳細資料]**** 區段將記下 Azure 租用戶識別碼和重新導向 URL。  在 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 儀表板登入和通訊過程中會使用這些 URL，來向後與已註冊的報表伺服器通訊。

5. 在 [結果]**** 視窗中選取 [複製]**** 按鈕，將註冊詳細資料複製到 Windows 剪貼簿，以便您加以儲存供日後參考。

## <a name="unregister-with-power-bi"></a><a name="bkmk_unregister"></a> 取消註冊 Power BI

**取消註冊︰** 從報表伺服器取消註冊 Azure Active Directory 會導致下列情形：

- [我的設定]**** 連結將不再顯示於入口網站功能表列。

- 已釘選的報表項目仍會釘選在儀表板上，不過儀表板上的磚將不再更新。

- 正在更新磚的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱仍會在報表伺服器上，但當其依據設定的排程執行時，會顯示類似下面的錯誤訊息。

    **無法載入此訂閱的傳遞延伸模組**

從組態管理員的 [Power BI]**** 頁面，選取 [向 Power BI 取消註冊]**** 按鈕。

##  <a name="update-registration"></a><a name="bkmk_updateregistration"></a> 更新註冊

若報表伺服器的組態已變更，則使用 [更新註冊] **** 。 例如，若您想要新增或移除使用者用來瀏覽至 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]的 URL。

- 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 設定管理員中，選取 [入口網站 URL]****

     選取 [進階]  。

- 選取 [新增]**** 為 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 新增新的 HTTP 識別，然後選取 [確定]****。

     [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 圖示會變更，指出已變更伺服器設定。  ![ssrs_powebi_icon_warning](../../reporting-services/install-windows/media/ssrs-powebi-icon-warning.png "ssrs_powebi_icon_warning")

- 在 [Power BI 整合]**** 頁面上，選取 [更新註冊]****。

     系統會提示您登入 Azure AD。 頁面會重新整理，您會看到 [重新導向 URL] **** 中所列的新 URL。

##  <a name="summary-of-the-power-bi-integration-and-pin-process"></a><a name="bkmk_integration_process"></a> Power BI 整合和釘選程序的摘要

本節摘要了當您整合報表伺服器與 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] ，並將報表項目釘選到儀表板時，所需的基本步驟和涉及的相關技術。

 **整合︰**

1. 在組態管理員中，當您選取 [向 Power BI 註冊]**** 按鈕時，系統將會提示您登入 Azure Active Directory。

2. [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 用戶端應用程式已向您受管理的租用戶註冊。

3. Azure Active Directory 內的受管理租用戶是 Power BI 用戶端應用程式的建立位置。

4. 註冊包含使用者從報表伺服器登入時會使用的重新導向 URL。  應用程式識別碼和 URL 會儲存至 ReportServer 資料庫。 在對 Azure 進行驗證呼叫期間會使用重新導向 URL，以便呼叫可傳回至報表伺服器。 例如，使用者登入或將項目釘選到儀表板時。

5. 在設定管理員中會顯示應用程式識別碼和 URL。

 ![ssrs_pbiflow_integration](../../reporting-services/install-windows/media/ssrs-pbiflow-integration.png "ssrs_pbiflow_integration")

 **當使用者將報表項目釘選到儀表板︰**

1. 使用者在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 中預覽報表，並首次按一下以從 [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] 釘選報表項目。

2. 系統會將他們重新導向至 Azure AD 的登入頁面。 使用者也可以從 [我的設定][!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] **** 頁面登入。 當使用者登入 Azure 受管理的租用戶時，其 Azure 帳戶與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 權限之間會建立關聯性。  如需詳細資訊，請參閱 [Power BI 整合的我的設定 &#40;入口網站&#41;](../my-settings-for-power-bi-integration-web-portal.md)。

3. 使用者安全性權杖會傳回到報表伺服器。

4. 使用者安全性權杖儲存在 ReportServer 資料庫中。

5. 使用者可存取的群組和儀表板清單擷取自 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 服務。  使用者選取目的地群組和儀表板，並設定 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)] 磚上資料重新整理的頻率。

6. 報表項目會釘選到儀表板。

7. 建立 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂用帳戶，以管理儀表板磚上報表項目排定的重新整理。 訂閱會採用使用者登入時所建立的安全性權杖。

     權杖的期限為 **90 天**，使用者需在該期限過後再次登入以建立新的使用者權杖。 權杖到期時，已釘選的磚仍會顯示在儀表板上，但資料不會再重新整理。  為釘選的項目所使用的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱會發生錯誤，直到建立新的使用者權杖為止。 請參閱 [Power BI 整合的我的設定 &#40;入口網站&#41;](../my-settings-for-power-bi-integration-web-portal.md)。 以取得詳細資訊。

使用者再次釘選項目時，會略過步驟 1-4，改為從 ReportServer 資料庫中擷取應用程式識別碼與 URL，然後接續執行步驟 5。

![ssRS-pin-to-powerbi-flow](../../reporting-services/install-windows/media/ssrs-pin-to-powerbi-flow.png)

 **當訂閱引發進而重新整理儀表板磚時︰**

1. 報表會在提出 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂用帳戶時轉譯。

2. 使用者權杖擷取自 ReportServer 資料庫。

3. 報表項目狀態和資料會連同權杖傳送至 [!INCLUDE[sspowerbi](../../includes/sspowerbi-md.md)]服務。

4. 權杖會傳送至 Azure AD 進行驗證。 若權杖有效，報表項目資料會傳送至儀表板磚，並更新磚的日期屬性。

5. 若權杖無效，系統會傳回錯誤並使用報表伺服器記錄。  無狀態或其他資訊會傳送至儀表板。

![ssRS-subscription-to-powerbi-flow](../../reporting-services/install-windows/media/ssrs-subscription-to-powerbi-flow.png)

   <iframe width="560" height="315" src="https://www.youtube.com/embed/QhPQObqmMPc" frameborder="0" allowfullscreen></iframe>

## <a name="considerations-and-limitations"></a>考量與限制

* 不支援網路和政府機關租用戶。

## <a name="next-steps"></a>後續步驟

[Power BI 整合的我的設定 &#40;入口網站&#41;](../my-settings-for-power-bi-integration-web-portal.md)  
[將 Reporting Services 項目釘選到 Power BI 儀表板](../../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md)
[Power BI 中的儀表板](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
