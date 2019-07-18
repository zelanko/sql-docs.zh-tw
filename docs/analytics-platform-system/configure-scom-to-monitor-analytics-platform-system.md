---
title: 設定 SCOM 以監視 Analytics Platform System |Microsoft Docs
description: 請遵循下列步驟來設定分析平台系統的 System Center Operations Manager (SCOM) 管理組件。 監視從 SCOM Analytics Platform System 所需的管理組件。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5ec495b3dd321f712aed54fb3b337efe85719be5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961230"
---
# <a name="configure-system-center-operations-manager-scom-to-monitor-analytics-platform-system"></a>設定 System Center Operations Manager (SCOM)，以監視 Analytics Platform System
請遵循下列步驟來設定分析平台系統的 System Center Operations Manager (SCOM) 管理組件。 監視從 SCOM Analytics Platform System 所需的管理組件。  
  
## <a name="BeforeBegin"></a>開始之前  
**必要條件**  
  
System Center Operations Manager 2007 R2 必須已安裝且正在執行。  
  
必須安裝並設定管理組件。 請參閱[安裝的 SCOM 管理組件&#40;Analytics Platform System&#41; ](install-the-scom-management-packs.md)並[匯入適用於 PDW 的 SCOM 管理組件&#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md)。  
  
## <a name="ConfigureRunAsProfile"></a>在 System Center 中設定執行身分設定檔  
若要設定 System Center，您必須執行下列步驟：  
  
-   建立執行身分帳戶**APS 監看員**網域使用者並將它對應至**AP 監看員的 Microsoft 帳戶。**  
  
-   建立執行身分帳戶**monitoring_user** APS 使用者並將它對應至**AP 動作的 Microsoft 帳戶**。  
  
以下是有關如何執行工作的詳細的指示：  
  
1.  建立**APS 監看員**具有執行身分帳戶**Windows**帳戶類型，如**AP 監看員**網域使用者。  
  
    1.  瀏覽至**Administration**  窗格中，以滑鼠右鍵按一下**執行身分設定** -> **帳戶**，然後選取**建立執行身分帳戶...**  
  
        ![ConfigureScomCreateRunAsAccount](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  **建立執行身分帳戶精靈**此時會開啟對話方塊。 在 [**簡介**頁面上，按一下**下一步]** 。  
  
    3.  在上**一般屬性**頁面上，選取**Windows**從**執行身分帳戶類型**，並指定為"AP 監看員 」**顯示名稱**。  
  
        ![CreateRunAsAccountWizardGeneralProperties](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "CreateRunAsAccountWizardGeneralProperties")  
  
    4.  在 **認證**頁面上， ![CreateRunAsAccountWizardCredentials](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")  
  
    5.  在 **散發安全性**頁面上，選取**較不安全**，按一下 **建立**按鈕來完成。  
  
        ![CreateRunAsAccountWizardDistributionSecurity](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "CreateRunAsAccountWizardDistributionSecurity")  
  
        1.  如果您決定要使用**更安全**選項時，您必須以手動方式指定的認證散發目的地的電腦。 若要這樣做，建立執行身分帳戶後，以滑鼠右鍵按一下它，然後選取**屬性**。  
  
        2.  瀏覽至**散發**索引標籤並**新增**所需的電腦。  
  
            ![RunAsAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  設定**APS 監看員的 Microsoft 帳戶**若要使用的設定檔**AP 監看員**執行身分帳戶。  
  
    1.  瀏覽至**Administration** -> **執行身分設定** -> **設定檔**。  
  
        ![AdministrationRunAsConfigurationProfiles](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  以滑鼠右鍵按一下**APS 監看員的 Microsoft 帳戶**從清單中選取**屬性**。  
  
        ![MicrosoftApsWatcherAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  **執行身分設定檔精靈**此時會開啟對話方塊。 略過**簡介**頁面上，依序按一下**下一步**。  
  
    4.  在 [**一般屬性**頁面上，按一下**下一步]** 。  
  
    5.  在 **執行身分帳戶**頁面上，按一下**加入...** 按鈕，然後選取先前建立**APS 監看員**執行身分帳戶。  
  
        ![RunAsProfileWizardAdd](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  按一下 **儲存**完成設定檔指派。  
  
3.  請等候探索完成 AP 設備。  
  
    1.  瀏覽至**監視**窗格，並開啟**SQL Server 應用裝置** -> **Microsoft Analytics Platform System**  ->  **設備**狀態檢視。  
  
        ![SqlServerApplianceMicrosoftApsAppliances](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  等到應用裝置出現在清單中。 設備名稱應該是等於指定的登錄中的其中一個。 探索完成之後，您應該會看到列出，但未受監視的所有設備。 若要啟用監視，請遵循接下來的步驟。  
  
    > [!NOTE]  
    > 可以以平行方式完成接下來的步驟，而您正在等候完成初始設備探索。  
  
4.  建立另一個新執行身分帳戶的健康情況資料擷取查詢 AP。  
  
    1.  開始建立新的執行身分帳戶，在步驟 1 中所述。  
  
    2.  在 **一般屬性**頁面上，選取**基本驗證**帳戶類型。  
  
        ![CreateRunAsAccountWizardGeneralProperties2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  在 **認證**頁面上，提供有效的認證來存取 AP Dmv 的健全狀況狀態。  
  
        ![CreateRunAsAccountWizardCredentials2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  設定**APS 動作的 Microsoft 帳戶**AP 執行個體所使用的新建立的執行身分帳戶設定檔。  
  
    1.  瀏覽至**APS 動作的 Microsoft 帳戶**步驟 2 中所述的屬性。  
  
    2.  在 **執行身分帳戶**頁面上，按一下**加入...** 和 
    3.  選取新建立的執行身分帳戶。  
  
        ![RunAsProfileWizardAdd2](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>下一個步驟  
既然您已設定管理組件，您已準備好要開始監視設備。 如需詳細資訊，請參閱 <<c0> [ 監視設備使用 System Center Operations manager &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)。</c0>  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
