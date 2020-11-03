---
title: 設定 System Center Operations Manager 以監視 AP
description: 遵循下列步驟來設定適用于 Analytics Platform System 的 System Center Operations Manager (SCOM) 管理套件。 需要有管理元件，才能從 SCOM 監視 Analytics Platform System。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2840ba401c0b7f3df5b0b27726cbdaa05390f952
ms.sourcegitcommit: 442fbe1655d629ecef273b02fae1beb2455a762e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93235265"
---
# <a name="configure-system-center-operations-manager-scom-to-monitor-analytics-platform-system"></a>設定 System Center Operations Manager (SCOM) 以監視 Analytics Platform System
遵循下列步驟來設定適用于 Analytics Platform System 的 System Center Operations Manager (SCOM) 管理套件。 需要有管理元件，才能從 SCOM 監視 Analytics Platform System。  
  
## <a name="before-you-begin"></a><a name="BeforeBegin"></a>開始之前  
**先決條件**  
  
必須安裝並執行 System Center Operations Manager 2007 R2。  
  
必須安裝和設定管理元件。 請參閱 [安裝 Scom 管理元件 &#40;Analytics Platform system&#41;](install-the-scom-management-packs.md) 並匯 [入適用于 PDW 的 scom 管理元件 &#40;analytics platform system&#41;](import-the-scom-management-pack-for-pdw.md)。  
  
## <a name="configure-run-as-profile-in-system-center"></a><a name="ConfigureRunAsProfile"></a>在 System Center 中設定 Run-As 設定檔  
若要設定 System Center，您必須執行下列步驟：  
  
-   為 **ap** 監看員網域使用者建立執行帳戶，並將其對應至 Microsoft ap 監看員 **帳戶。**  
  
-   為 **monitoring_user** ap 使用者建立執行帳戶，並將其對應至 **Microsoft ap 動作帳戶** 。  
  
以下是如何執行工作的詳細指示：  
  
1.  使用適用于 **ap** 監看員網域使用者的 **Windows** 帳戶類型來建立 **Ap** 監看員執行身份帳戶。  
  
    1.  流覽至 [系統 **管理** ] 窗格，以滑鼠右鍵按一下 [ **執行身份** 設定  ->  **帳戶** ]，然後選取 [ **建立執行帳戶** ]。  
  
        ![顯示 [建立執行帳戶] 選項的螢幕擷取畫面。](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  [ **建立執行身份帳戶嚮導** ] 對話方塊隨即開啟。 在 [簡介]  頁面上，按一下 [下一步]  。  
  
    3.  在 [ **一般** 內容] 頁面上，從 **[執行身份帳戶類型** ] 選取 [ **Windows** ]，並指定 [Ap 監看員] 作為 **顯示名稱** 。  
  
        ![螢幕擷取畫面，顯示 [建立執行身份帳戶] 嚮導的 [一般] 屬性頁面。](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "CreateRunAsAccountWizardGeneralProperties")  
  
    4.  在 [ **認證** ] 頁面上， ![顯示 [建立執行身分帳戶] 嚮導之 [認證] 頁面的螢幕擷取畫面。](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")  
  
    5.  在 [ **散發安全性** ] 頁面上，選取 [ **不安全** ]，然後按一下 [ **建立** ] 按鈕來完成。  
  
        ![螢幕擷取畫面，顯示 [建立執行身份帳戶] 嚮導的 [散發安全性] 頁面。](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "CreateRunAsAccountWizardDistributionSecurity")  
  
        1.  如果您決定使用 **更安全** 的選項，則必須手動指定將發佈認證的電腦。 若要這樣做，請在建立執行身份帳戶之後，以滑鼠右鍵按一下它，然後選取 [ **屬性** ]。  
  
        2.  流覽至 [ **散發** ] 索引標籤，並 **新增** 所需的電腦。  
  
            ![顯示 [執行身份帳戶屬性] 對話方塊的螢幕擷取畫面。](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  將 **MICROSOFT ap** 監看員帳戶設定檔設定為使用 **ap** 監看員執行身份帳戶。  
  
    1.  流覽至 [ **管理**  ->  **執行身份配置**  ->  **檔** ]。  
  
        ![顯示 [設定檔] 選項的螢幕擷取畫面。](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  以滑鼠右鍵按一下清單中的 [ **MICROSOFT ap** 監看員帳戶]，然後選取 [ **屬性** ]。  
  
        ![顯示 [屬性] 選項的螢幕擷取畫面。](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  [ **執行身份設定檔 Wizard** ] 對話方塊隨即開啟。 按一下 **[下一步]** 略過 [ **簡介** ] 頁面。  
  
    4.  在 [一般內容]  頁面上，按一下 [下一步]  。  
  
    5.  在 [ **執行身份帳戶** ] 頁面上，按一下 [ **新增** ] 按鈕，然後選取先前建立的 **Ap** 監看員執行身份帳戶。  
  
        ![顯示 [新增執行帳戶] 對話方塊的螢幕擷取畫面。](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  按一下 [ **儲存** ] 以完成設定檔指派。  
  
3.  等候 AP 設備探索完成。  
  
    1.  流覽至 [ **監視** 中] 窗格，然後開啟 **SQL Server 設備**  ->  **Microsoft Analytics Platform System**  ->  **設備** 狀態視圖。  
  
        ![顯示裝置選項的螢幕擷取畫面。](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  等候設備出現在清單中。 設備的名稱應該等於登錄中指定的名稱。 探索完成之後，您應該會看到所有已列出但未受監視的設備。 若要啟用監視，請遵循後續步驟。  
  
    > [!NOTE]  
    > 當您等待初始設備探索完成時，可以平行完成後續步驟。  
  
4.  建立另一個新的執行身份帳戶來查詢 AP 以進行健康狀態資料抓取。  
  
    1.  開始建立新的執行身份帳戶，如步驟1所述。  
  
    2.  在 [ **一般屬性** ] 頁面上，選取 [ **基本驗證** 帳戶類型]。  
  
        ![螢幕擷取畫面，顯示 [執行帳戶類型] 下拉式清單中選取 [基本驗證] 的 [建立執行身份帳戶] 頁面的 [一般] 屬性頁面。](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  在 [ **認證** ] 頁面上，提供有效的認證以存取「ap 健全狀況狀態 dmv」。  
  
        ![顯示 [建立執行身分帳戶] 頁面的 [認證] 頁面的螢幕擷取畫面，其中包含有效的認證 wo 存取 AP 健全狀況狀態 Dmv。](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  設定 **MICROSOFT Ap 動作帳戶** 設定檔，以使用新建立的「執行身份」帳戶做為「ap」實例。  
  
    1.  流覽至 **MICROSOFT Ap 動作帳戶** 內容，如步驟2中所述。  
  
    2.  在 [ **執行身份帳戶** ] 頁面上，按一下 [ **新增]。** 
    3.  選取新建立的執行身份帳戶。  
  
        ![顯示 [新增執行帳戶] 對話方塊的螢幕擷取畫面，其中已從 [執行身份帳戶] 下拉式清單選取 AP 動作。](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>後續步驟  
現在您已設定管理元件，您已準備好開始監視設備。 如需詳細資訊，請參閱 [使用 System Center Operations Manager &#40;Analytics Platform System&#41;來監視設備 ](monitor-the-appliance-by-using-system-center-operations-manager.md)。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
