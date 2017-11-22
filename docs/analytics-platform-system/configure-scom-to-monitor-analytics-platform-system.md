---
title: "設定 SCOM 監視 Analytics Platform System"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4dba9b50-1447-45fc-b219-b9fc99d47d8d
caps.latest.revision: "10"
ms.openlocfilehash: f9c8a778afad89abea9ad4fd092fefb15844a5ae
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="configure-scom-to-monitor-analytics-platform-system"></a>設定 SCOM 監視 Analytics Platform System
請遵循下列步驟來設定 Analytics Platform System for System Center Operations Manager (SCOM) 管理組件。 監視從 SCOM Analytics Platform System 所需的管理組件。  
  
## <a name="BeforeBegin"></a>開始之前  
**必要條件**  
  
System Center Operations Manager 2007 R2 必須已安裝且正在執行。  
  
必須安裝和設定管理組件。 請參閱[SCOM 管理組件 &#40; 安裝Analytics Platform System &#41;](install-the-scom-management-packs.md)和[匯入的 PDW &#40; SCOM 管理組件Analytics Platform System &#41;](import-the-scom-management-pack-for-pdw.md).  
  
## <a name="ConfigureRunAsProfile"></a>在 System Center 設定執行身分設定檔  
若要設定 System Center 中，您必須執行下列步驟：  
  
-   建立執行身分帳戶**AP 監看員**網域使用者並將它對應至**AP 監看員的 Microsoft 帳戶。**  
  
-   建立執行身分帳戶**monitoring_user** AP 使用者並將它對應至**Microsoft AP 動作帳戶**。  
  
以下是對此的詳細的指示：  
  
1.  建立**AP 監看員**執行身分帳戶與**Windows**帳戶類型的**AP 監看員**網域使用者。  
  
    1.  瀏覽至**管理** 窗格中，以滑鼠右鍵按一下**執行身分設定** -> **帳戶**選取**建立執行身分帳戶...**  
  
        ![ConfigureScomCreateRunAsAccount](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  **建立執行身分帳戶精靈**對話方塊將會開啟。 在**簡介**頁面上，按一下**下一步**。  
  
    3.  在**一般屬性**頁面上，選取**Windows**從**執行身分帳戶類型**並指定"APS 監看員 」 做為**顯示名稱**。  
  
        ![CreateRunAsAccountWizardGeneralProperties](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "CreateRunAsAccountWizardGeneralProperties")  
  
    4.  在**認證**頁面上，提供"APS 監看員 」 網域使用者認證。  
  
        ![CreateRunAsAccountWizardCredentials](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")  
  
    5.  在**散發安全性**頁面上，選取**較不安全**按一下**建立**按鈕，以完成。  
  
        ![CreateRunAsAccountWizardDistributionSecurity](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "CreateRunAsAccountWizardDistributionSecurity")  
  
        1.  如果您決定使用**更安全**選項，您必須手動指定電腦的認證會散發。 若要這樣做，建立執行身分帳戶之後，以滑鼠右鍵按一下它，然後選取**屬性**。  
  
        2.  瀏覽至**發佈** 索引標籤和**新增**預期的電腦。  
  
            ![RunAsAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  設定**AP 監看員的 Microsoft 帳戶**設定檔使用**AP 監看員**執行身分帳戶。  
  
    1.  瀏覽至**管理** -> **執行身分設定** -> **設定檔**。  
  
        ![AdministrationRunAsConfigurationProfiles](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  以滑鼠右鍵按一下**AP 監看員的 Microsoft 帳戶**清單並選取從**屬性**。  
  
        ![MicrosoftApsWatcherAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  **執行身分設定檔精靈**對話方塊將會開啟。 略過**簡介**頁面，即可**下一步**。  
  
    4.  在**一般屬性**頁面上，按一下**下一步**。  
  
    5.  在**執行身分帳戶**頁面上，按一下**新增...** 按鈕，然後選取先前建立**AP 監看員**執行身分帳戶。  
  
        ![RunAsProfileWizardAdd](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  按一下**儲存**完成指派設定檔。  
  
3.  請等候探索完成 AP 應用裝置。  
  
    1.  瀏覽至**監視**窗格並開啟**SQL Server 應用裝置** -> **Microsoft Analytics Platform System**  ->  **應用裝置**狀態檢視。  
  
        ![SqlServerApplianceMicrosoftApsAppliances](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  請等到應用裝置會出現在清單中。 應用裝置的名稱應該會等於所指定的登錄中。  
  
    探索完成之後應該會看到所有的裝置列出，但卻未受監視。 進行監視工作，請遵循下一個步驟。  
  
    > [!NOTE]  
    > 當您正在等候完成初始應用裝置探索時，可以完成接下來的步驟以平行方式。  
  
4.  建立另一個新的執行身分帳戶來擷取健全狀況資料的查詢 AP。  
  
    1.  開始建立新的執行身分帳戶，在步驟 1 中所述。  
  
    2.  在**一般屬性**頁面上，選取**基本驗證**帳戶類型。  
  
        ![CreateRunAsAccountWizardGeneralProperties2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  在**認證**頁面，請提供有效認證來存取 AP Dmv 的健全狀況狀態。  
  
        ![CreateRunAsAccountWizardCredentials2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  設定**Microsoft AP 動作帳戶**AP 執行個體所使用的新建立的執行身分帳戶設定檔。  
  
    1.  瀏覽至**Microsoft AP 動作帳戶**步驟 2 中所述的屬性。  
  
    2.  在**執行身分帳戶**頁面上，按一下**新增...** 然後選取新建立的執行身分帳戶。  
  
        ![RunAsProfileWizardAdd2](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>下一個步驟  
既然您已設定管理組件，您已準備好要開始監視應用裝置。 如需詳細資訊，請參閱[監視使用 System Center Operations Manager &#40; 應用裝置Analytics Platform System &#41;](monitor-the-appliance-by-using-system-center-operations-manager.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
