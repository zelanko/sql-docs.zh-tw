---
title: 使用 SCOM 監視
description: 請遵循下列步驟來設定 Analytics Platform System 的 System Center Operations Manager （SCOM）管理元件。 需要管理元件，才能從 SCOM 監視分析平臺系統。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 67029d235a1bc65b5ee0ab6f01f51dea42ebcc8b
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401304"
---
# <a name="configure-system-center-operations-manager-scom-to-monitor-analytics-platform-system"></a>設定 System Center Operations Manager （SCOM）以監視分析平臺系統
請遵循下列步驟來設定 Analytics Platform System 的 System Center Operations Manager （SCOM）管理元件。 需要管理元件，才能從 SCOM 監視分析平臺系統。  
  
## <a name="BeforeBegin"></a>開始之前  
**必要條件**  
  
System Center Operations Manager 2007 R2 必須已安裝且正在執行。  
  
必須安裝並設定管理元件。 請參閱[&#40;分析平臺系統安裝 Scom 管理元件&#41;](install-the-scom-management-packs.md)並匯[入適用于 PDW 的 scom 管理元件 &#40;分析平臺系統&#41;](import-the-scom-management-pack-for-pdw.md)。  
  
## <a name="ConfigureRunAsProfile"></a>在 System Center 中設定執行身分設定檔  
若要設定 System Center，您必須執行下列步驟：  
  
-   為「 **ap**監看員」網域使用者建立執行身分帳戶，並將它對應到 Microsoft ap 監看員**帳戶。**  
  
-   為**monitoring_user**的 ap 使用者建立執行身分帳戶，並將其對應至**Microsoft ap 動作帳戶**。  
  
以下是如何執行工作的詳細指示：  
  
1.  為「 **ap**監看員」網域使用者建立具有**Windows**帳戶類型的「 **ap**監看員」執行身分帳戶。  
  
    1.  流覽至 [系統**管理**] 窗格，在 [**執行** -> 身分設定**帳戶**] 上按一下滑鼠右鍵，然後選取 [**建立執行身分帳戶**]。  
  
        ![ConfigureScomCreateRunAsAccount](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  [**建立執行身分帳戶嚮導**] 對話方塊隨即開啟。 在 [簡介] **** 頁面上，按一下 [下一步] ****。  
  
    3.  在 [**一般**內容] 頁面上，從 [**執行身分帳戶類型**] 選取 [ **Windows** ]，並指定 [ap 監看員] 做為**顯示名稱**。  
  
        ![CreateRunAsAccountWizardGeneralProperties](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "CreateRunAsAccountWizardGeneralProperties")  
  
    4.  在 [**認證**] 頁面上， ![CreateRunAsAccountWizardCredentials](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")  
  
    5.  在 [**散發安全性**] 頁面上，選取 [**較不安全**]，然後按一下 [**建立**] 按鈕以完成。  
  
        ![CreateRunAsAccountWizardDistributionSecurity](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "CreateRunAsAccountWizardDistributionSecurity")  
  
        1.  如果您決定使用**更安全**的選項，您必須手動指定將發佈認證的電腦。 若要這麼做，請在建立執行身分帳戶之後，以滑鼠右鍵按一下它，然後選取 [**屬性**]。  
  
        2.  流覽至 [**發佈**] 索引標籤，然後**新增**所需的電腦。  
  
            ![RunAsAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  將**MICROSOFT ap**監看員帳戶設定檔設定為使用**ap**監看員的執行身分帳戶。  
  
    1.  流覽至 [系統**管理** -> ] [**執行** -> 身分設定配置**檔**]。  
  
        ![AdministrationRunAsConfigurationProfiles](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  以滑鼠右鍵按一下清單中的 [ **MICROSOFT ap**監看員帳戶]，然後選取 [**屬性**]。  
  
        ![MicrosoftApsWatcherAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  [**執行身分設定檔嚮導**] 對話方塊隨即開啟。 按一下 **[下一步]**，略過 [**簡介**] 頁面。  
  
    4.  在 [**一般屬性**] 頁面上，按 **[下一步]**。  
  
    5.  在 [**執行身分帳戶**] 頁面上，按一下 [**新增 ...** ] 按鈕，然後選取先前建立的「 **ap**監看員」執行身分帳戶。  
  
        ![RunAsProfileWizardAdd](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  按一下 [**儲存**] 完成設定檔指派。  
  
3.  等待 [AP 設備探索] 完成。  
  
    1.  流覽至 [**監視**中] 窗格，然後開啟 [ **SQL Server 設備** -> ] [**Microsoft Analytics Platform System** -> **設備**] 狀態 view。  
  
        ![SqlServerApplianceMicrosoftApsAppliances](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  等待應用裝置出現在清單中。 設備的名稱應該與登錄中指定的相同。 探索完成之後，您應該會看到所有已列出但未受監視的設備。 若要啟用監視，請遵循後續步驟。  
  
    > [!NOTE]  
    > 當您在等候初始設備探索完成時，可以平行完成後續步驟。  
  
4.  建立另一個新的執行身分帳戶，以查詢用於健康情況資料抓取的 AP。  
  
    1.  開始建立新的執行身分帳戶，如步驟1所述。  
  
    2.  在 [**一般屬性**] 頁面上，選取 [**基本驗證**帳戶類型]。  
  
        ![CreateRunAsAccountWizardGeneralProperties2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  在 [**認證**] 頁面上，提供有效的認證以存取 ap 健全狀況狀態 dmv。  
  
        ![CreateRunAsAccountWizardCredentials2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  設定**MICROSOFT Ap 動作帳戶**設定檔，為 ap 實例使用新建立的執行身分帳戶。  
  
    1.  流覽至**MICROSOFT Ap 動作帳戶**屬性，如步驟2中所述。  
  
    2.  在 [**執行身分帳戶**] 頁面上，按一下 [**新增**]，然後 
    3.  選取新建立的執行身分帳戶。  
  
        ![RunAsProfileWizardAdd2](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>後續步驟  
現在您已設定管理元件，您已準備好開始監視設備。 如需詳細資訊，請參閱[使用 System Center Operations Manager &#40;分析平臺系統&#41;來監視設備](monitor-the-appliance-by-using-system-center-operations-manager.md)。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
