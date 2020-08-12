---
title: 設定報表產生器的存取 | Microsoft Docs
description: 設定報表產生器，這是與 SQL Server Reporting Services 報表產生器一起安裝的報表工具。 其使用原生模式或 SharePoint 整合模式。
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.date: 06/06/2019
ms.openlocfilehash: 168e8897743e113ae1a40df5ad8d35c66289fde0
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84548080"
---
# <a name="configure-report-builder-access"></a>設定報表產生器的存取
報表產生器是一個隨選報表工具，此工具會與設定原生模式或 SharePoint 整合模式的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器一起安裝。  

報表產生器的存取權會因下列因素而異：  

- 決定是否可以在報表伺服器上使用報表產生器的伺服器屬性。  

- 可將報表產生器提供給個別使用者或群組使用的角色指派或權限。  

- 驗證設定，可判斷使用者認證是否可以傳遞給報表伺服器，或是在應用程式檔案上設定匿名存取。

## <a name="prerequisites"></a>必要條件

並非每個 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中都可使用報表產生器。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本支援的功能清單，請參閱 [SQL Server 2017 版本支援的功能](../../sql-server/editions-and-components-of-sql-server-2017.md)。  

用戶端電腦必須針對 SSRS 2016 和 2017 分別安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6 或 4.6.1。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 提供了執行 [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 應用程式的基礎結構。  

您必須使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 11 或更新版本，或使用其他新式瀏覽器。  

報表產生器一定會在完全信任模式中執行；您不能設定它在部分信任模式中執行。 在舊版中，報表產生器可以在部分信任模式中執行，但是在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本中則不支援這個選項。  

## <a name="enabling-and-disabling-report-builder"></a>啟用及停用報表產生器  

預設會啟用報表產生器。 報表伺服器管理員可以選擇將報表伺服器系統屬性 **ShowDownloadMenu** 設定為 **false**，以停用報表產生器功能。 設定這個屬性將會停用該報表伺服器的報表產生器、行動報表發行工具和 Power BI 行動版下載功能。  

 若要設定報表伺服器系統屬性，您可以使用 Management Studio 或指令碼：   

 - 若要使用 Management Studio，請連線到報表伺服器，並使用 [進階伺服器屬性] 頁面將 **ShowDownloadMenu** 設定為 **false**。 如需如何開啟此頁面的詳細資訊，請參閱[設定報表伺服器屬性 &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)。      

 - 若要檢視設定報表伺服器屬性的範例指令碼，請參閱 [編寫部署和管理工作的指令碼](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)。  

## <a name="role-assignments-granting-report-builder-access-on-a-native-mode-report-server"></a>原生模式報表伺服器上授與報表產生器存取的角色指派  

在原生模式報表伺服器上，建立使用者角色指派來包含使用報表產生器的工作。 您必須是內容管理員和系統管理員，才能建立或修改項目和網站層級的角色定義與角色指派。  

下列指示假設您使用預先定義的角色。 如果您已修改角色定義或是從 SQL Server 2000 升級，請檢查這些角色，以確認它們有包含所需的工作。 如需建立角色指派的詳細資訊，請參閱[將報表伺服器的存取權授與使用者](../../reporting-services/security/grant-user-access-to-a-report-server.md)。

在建立角色指派之後，使用者將有權執行以下作業：  

- 指派給「系統使用者」和「瀏覽者」角色的使用者可以檢視報表伺服器上的已發行報表產生器報表，而不需啟動報表產生器。  

- 指派給「系統使用者」和「報表產生器」角色的使用者可以產生模型、啟動報表產生器及建立報表，並將報表儲存到報表伺服器。  

- 指派給「系統使用者」和「發行者」角色的使用者可以從模型設計師將模型發行到報表伺服器。 模型會在報表產生器中當做資料來源使用。  

- 指派給「系統管理員」和「內容管理員」角色的使用者具有建立、檢視及管理報表產生器報表的完整權限。  

### <a name="to-verify-required-tasks-are-in-the-role-definitions"></a>確認必要工作位於角色定義中  

1. 啟動 Management Studio，然後連接到報表伺服器。  

2. 開啟 [安全性] 資料夾。  

3. 開啟 [系統角色] 資料夾。  

4. 以滑鼠右鍵按一下 [系統管理員]，然後選取 [屬性]。  

5. 選取 [執行報表定義]  ，然後按一下 [確定]  。  

6. 以滑鼠右鍵按一下 [系統使用者]，然後選取 [屬性]。  

7. 選取 [執行報表定義]，然後按一下 [確定]。  

8. 開啟 [角色] 資料夾。  

9. 以滑鼠右鍵按一下 [瀏覽器]，然後選取 [屬性]。  

10. 選取 [檢視模型]，然後按一下 [確定]。  

11. 以滑鼠右鍵按一下 [內容管理員]，然後選取 [屬性]。  

12. 選取 [檢視模型]、[管理模型]、[取用報表]，然後按一下 [確定]。  

13. 以滑鼠右鍵按一下 [發行者]，然後選取 [屬性]。  

14. 選取 [管理模型]，然後按一下 [確定]。  

15. 如果報表產生器角色不存在，請建立該角色：  

    1. 開啟 [安全性] 資料夾。  

    2. 以滑鼠右鍵按一下 [角色]，並選取 [新增角色]。  

    3. 在 [名稱] 中，輸入 **報表產生器**。  

    4. 在 [描述] 中，輸入角色的描述，好讓入口網站中的使用者知道這個角色的目的。  

    5. 新增下列工作：[取用報表]、[檢視報表]、[檢視模型]、[檢視資源]、[檢視資料夾] 及 [管理個別訂閱]。  

    6. 按一下 [確定]，儲存角色。  

#### <a name="to-create-role-assignments-that-grant-access-to-report-builder"></a>建立角色指派來授與報表產生器的存取權  

1. 啟動入口網站。  

2. 按一下入口網站首頁右上方的齒輪圖示，然後從下拉式功能表中選取 [網站設定]。  
![入口網站齒輪圖示和功能表](../../reporting-services/report-builder/media/configure-report-builder-access/ssrswebportal-site-settings-gear-icon-and-menu.png)

3. 按一下 **[安全性]** 。  

4. 如果您想要設定報表產生器存取的使用者或群組已經有角色指派，請按一下 [編輯]。  
否則請按一下 [新增角色指派]。 在群組或使用者中，使用下列格式來輸入 Windows 網域使用者或群組帳戶：\<domain>\\<帳戶\>。 如果您要使用表單驗證或自訂安全性，請使用適用於部署的正確格式來指定使用者或群組帳戶。  

5. 選取 [系統使用者]，然後按一下 [確定]。  

6. 按一下 [首頁]。  

7. 按一下 [資料夾設定] 索引標籤。  

8. 按一下 [安全性] 索引標籤。  

9. 如果您想要設定報表產生器存取的使用者或群組已經有角色指派，請按一下 [編輯]。  

    否則請按一下 [新增角色指派]。 在群組或使用者中，使用下列格式來輸入 Windows 網域使用者或群組帳戶：\<domain>\\<帳戶\>。 如果您要使用表單驗證或自訂安全性，請使用適用於部署的正確格式來指定使用者或群組帳戶。  

10. 選取 [報表產生器]，然後按一下 [套用]。  

11. 重複上述步驟，以便建立或修改其他使用者或群組的角色指派。  

## <a name="permissions-granting-report-builder-access-on-a-sharepoint-integrated-mode-report-server"></a>授與 SharePoint 整合模式報表伺服器上之報表產生器存取的權限  

在 SharePoint 整合模式報表伺服器上，報表產生器的存取會授與給具有「參與」或「完全控制」權限等級的 SharePoint 使用者。  

如果您要使用自訂權限等級，您必須在此權限等級中包括「加入項目」和「編輯項目」。 如需透過內建權限層級存取報表產生器的詳細資訊，請參閱 [在 Windows SharePoint Services 中使用報表伺服器項目的內建安全性](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md)。 如需自訂權限層級的權限需求詳細資訊，請參閱 [在 SharePoint Web 應用程式中設定報表伺服器作業的權限](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)。  

## <a name="authentication-considerations-and-credential-reuse"></a>驗證考量與認證重複使用  

- 報表產生器會開啟它自己與報表伺服器的連接。 如果您未搭配單一登入來使用 Windows 整合式安全性，使用者必須針對與報表伺服器的報表產生器連接重新輸入認證。  

下表說明報表伺服器所支援的驗證類型，以及是否需要其他組態才能存取報表產生器。  

## <a name="see-also"></a>另請參閱  

- [報表伺服器的驗證](../../reporting-services/security/authentication-with-the-report-server.md)
- [Reporting Services 和 Power View 的瀏覽器支援](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)
- [啟動報表產生器](../../reporting-services/report-builder/start-report-builder.md)
- [報表伺服器的入口網站 (SSRS 原生模式)](../web-portal-ssrs-native-mode.md)
- [連接至 Management Studio 中的報表伺服器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)
- [報表伺服器系統屬性](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)
