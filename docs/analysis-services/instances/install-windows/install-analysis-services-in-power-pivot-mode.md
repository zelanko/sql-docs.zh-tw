---
title: "以 Power Pivot 模式安裝 Analysis Services |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d3310562-82c1-454f-9c48-33a241749238
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: ffad3e8daf95263a5c0ce8ee6607c2715defe43b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="install-analysis-services-in-power-pivot-mode"></a>以 Power Pivot 模式安裝 Analysis Services
  本主題中的程序會引導您完成 SharePoint 部署 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 模式之 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 伺服器的單一伺服器安裝。 這些步驟包含執行 [SQL Server 安裝精靈]，以及使用 SharePoint 管理中心的設定工作。  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2016 &#124; SharePoint 2013|  
  
 **本主題內容：**  
  
 [背景](#bkmk_background)  
  
 [必要條件](#bkmk_prereq)  
  
 [步驟 1：安裝 Power Pivot for SharePoint](#InstallSQL)  
  
 [步驟 2：設定基本 Analysis Services SharePoint 整合](#bkmk_config)  
  
 [步驟 3：確認整合](#bkmk_verify)  
  
 [設定 Windows 防火牆以允許 Analysis Services 存取](#bkmk_firewall)  
  
 [升級活頁簿和排程的資料重新整理](#bkmk_upgrade_workbook)  
  
 [超越單一伺服器安裝 – PowerPivot for Microsoft SharePoint](#bkmk_multiple_servers)  
  
##  <a name="bkmk_background"></a> 背景  
 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 是中間層及後端服務的集合物件，可以在 SharePoint 2016 或 SharePoint 2013 伺服器陣列中提供 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 資料存取功能。  
  
-   **後端服務** ：如果您使用 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for Excel 建立包含分析資料的活頁簿，伺服器環境必須具有 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint，才可存取該資料。 您可在已安裝 SharePoint Server 的電腦，或是在沒有 SharePoint 軟體的另一部電腦上，執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 沒有 SharePoint 的相依性。  
  
     **注意** ：本主題將描述 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器和後端服務的安裝。  
  
-   **中介層：** SharePoint 中 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 體驗的增強功能，包括 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 圖庫、排程資料重新整理、管理儀表板和資料提供者。 如需有關安裝及設定中介層的詳細資訊，請參閱以下主題：  
  
    -   [安裝或解除安裝 Power Pivot for SharePoint 增益集 (SharePoint 2016)](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2016.md)  
  
    -   [安裝或解除安裝 PowerPivot for SharePoint 增益集 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
    -   [設定 Power Pivot 及部署方案 &#40;SharePoint 2016&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2016.md)  
  
    -   [設定 Power Pivot 及部署方案 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)  
  
##  <a name="bkmk_prereq"></a> 必要條件  
  
1.  您必須是本機系統管理員，才能執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式。  
  
2.  [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 需要 SharePoint Server Enterprise 版。 您也可以使用 Evaluation Enterprise 版。  
  
3.  電腦必須與 Office Online Server (SharePoint 2016) 或 Excel Services (SharePoint 2013) 加入相同 Active Directory 樹系中的網域。  
  
4.  必須要有 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 執行個體名稱。 正在以 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]模式安裝 Analysis Services 的電腦上，不得具有現存的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 具名執行個體。  
  
     **附註：** 執行個體名稱必須為 POWERPIVOT。  
  
5.  請參閱 [Analysis Services SharePoint 模式伺服器的硬體和軟體需求 (SQL Server 2014)](http://msdn.microsoft.com/library/fb86ca0a-518c-4c61-ae78-7680c57fae1f)。  
  
6.  檢閱位於 [SQL Server 2016 Release Notes](../../../sql-server/sql-server-2016-release-notes.md)的版本資訊。  
  
###  <a name="bkmk_sqleditions"></a> SQL Server Edition 需求  
 並非在所有版本的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]中都提供商業智慧功能。 如需詳細資訊，請參閱[Analysis Services 的 SQL Server 2016 的版本支援的功能](../../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)和[and Components of SQL Server 2016](../../../sql-server/editions-and-components-of-sql-server-2016.md)。  
  
##  <a name="InstallSQL"></a> 步驟 1：安裝 Power Pivot for SharePoint  
 在此步驟中，您會執行 SQL Server 安裝程式，以在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 模式中安裝 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 伺服器。 在後續步驟中，您針對活頁簿資料模型設定 Excel Services 使用此伺服器。  
  
1.  執行 [SQL Server 安裝精靈] (Setup.exe)。  
  
2.  選取位於左邊功能窗格的 [安裝]  。  
  
3.  選取 [新增 SQL Server 獨立安裝或將功能加入至現有安裝]。  
  
4.  如果看到 **[產品金鑰]** 頁面，請指定 Evaluation Edition 或是輸入 Enterprise Edition 授權複本的產品金鑰。 select **[下一步]**。 如需版本的詳細資訊，請參閱＜ [Editions and Components of SQL Server 2016](../../../sql-server/editions-and-components-of-sql-server-2016.md)＞。  
  
5.  檢閱並接受 Microsoft 軟體授權條款的條款，然後選取 [下一步] 。  
  
6.  如果您看到 **[全域規則]** 頁面，請檢閱安裝精靈顯示的所有規則資訊。  
  
7.  在 [Microsoft Update]  頁面上，建議您使用 Microsoft Update 來檢查更新，然後選取 [下一步] 。  
  
8.  **[安裝安裝檔案]** 頁面會執行數分鐘。 檢閱所有規則警告或失敗規則，然後選取 [下一步] 。  
  
9. 若您看到另一個 [安裝程式支援規則] ，請檢閱任何警告，然後選取 [下一步] 。  
  
     **注意：** 由於已啟用 Windows 防火牆，因此您會看到開放通訊埠才可啟用遠端存取的警告。  
  
10. 在 [安裝程式角色]  頁面上，選取 [SQL Server 功能安裝] 。  
  
     選取 **[下一步]**。  
  
11. 在 [特徵選取] 頁面上，選取 [Analysis Services] 。 此選項可讓您安裝三種 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 模式之一。 您將在稍後步驟中選取模式。 選取 **[下一步]**。  
  
12. 在 [執行個體設定]  頁面上，選取 [具名執行個體]  ，然後針對執行個體名稱輸入 **POWERPIVOT** ，接著再按一下 [下一步] 。  
  
     ![SQL 安裝程式-登陸頁面的執行個體組態](../../../analysis-services/instances/install-windows/media/sql2016-pp-instance-config-landing-page.png "SQL 安裝程式-登陸頁面的執行個體組態")  
  
13. 在 **[伺服器組態]** 頁面上，將所有服務的 **[啟動類型]**設定為 [自動]。 指定 **SQL Server Analysis Services**的所需網域帳戶和密碼，即下圖中的 **(1)** 。  
  
    -   針對 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，您可以使用 **網域使用者** 帳戶或 **NetworkService** 帳戶。 請勿使用 LocalSystem 或 LocalService 帳戶。  
  
    -   若已新增 SQL Server Database Engine 與 SQL Server Agent，您可以將服務設定為利用網域使用者帳戶或預設虛擬帳戶加以執行。  
  
    -   絕不要使用您自己的網域使用者帳戶來提供服務帳戶。 這麼做會授與伺服器您對網路中的資源所擁有的相同權限。 如果惡意使用者入侵伺服器，該使用者就會使用您的網域認證登入。 該使用者將有權下載或使用您有權下載或使用的相同資料和應用程式。  
  
     選取 **[下一步]**。  
  
     ![SQL 安裝程式-伺服器組態 登陸頁面](../../../analysis-services/instances/install-windows/media/sql2016-pp-server-config-landing-page.png "SQL 安裝程式-伺服器組態 登陸頁面")  
  
14. 若您正安裝 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]，則隨即會出現 **[資料庫引擎組態]** 頁面。 在 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 設定中，選取 [加入目前使用者]  ，以針對資料庫引擎執行個體授與使用者帳戶管理員權限。  
  
     選取 **[下一步]**。  
  
15. 在 [Analysis Services 設定]  頁面的 [伺服器模式]  下方，選取 [PowerPivot 模式]   
  
     ![SQL 安裝程式-Analysis Services 組態登陸頁面](../../../analysis-services/instances/install-windows/media/sql2016-pp-as-config-landing-page.png "SQL 安裝程式-登陸頁面的 Analysis Services 組態")  
  
16. 在 [Analysis Services 設定]  頁面上，選取 [加入目前使用者]  ，為您的使用者帳戶授與管理權限。 在完成安裝程式之後，您將會需要管理權限來設定伺服器。  
  
    -   在相同的頁面上，加入也需要管理權限之任何人的 Windows 使用者帳戶。 例如，想要在 [!INCLUDE[ssGeminiSrv](../../../includes/ssgeminisrv-md.md)] 中連接至 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 執行個體以疑難排解資料庫連接問題的所有使用者，都必須擁有系統管理員權限。 請加入可能需要立即針對伺服器進行疑難排解或管理之任何人的使用者帳戶。  
  
    -   > [!NOTE]  
        >  需要存取 Analysis Services 伺服器執行個體的所有服務應用程式都必須具有 Analysis Services 管理權限。 例如，加入 Excel Services、Power View 及 Performance Point 服務的服務帳戶。 此外，請加入 SharePoint 伺服器陣列帳戶，做為裝載管理中心的 Web 應用程式的識別。  
  
     選取 **[下一步]**。  
  
17. 在 [錯誤報告]  頁面上，選取 [下一步] 。  
  
18. 在 [已可安裝]  頁面上，選取 [安裝] 。  
  
19. 若您看見 [需要重新啟動電腦] 對話方塊，請選取 [確定] 。  
  
20. 安裝完成時，選取 [關閉] 。  
  
21. 重新啟動電腦。  
  
22. 如果您的環境有防火牆，請檢閱《SQL Server 線上叢書》主題＜ [Configure the Windows Firewall to Allow Analysis Services Access](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)＞。  
  
### <a name="verify-the-sql-server-installation"></a>確認 SQL Server 安裝  
 確認 Analysis Services 服務正在執行。  
  
1.  在 Microsoft Windows 中，按一下 [開始] ，選取[所有程式] ，然後選取 [Microsoft SQL Server 2016]  群組。  
  
2.  選取 [SQL Server Management Studio] 。  
  
3.  連接至 Analysis Services 執行個體，例如 **[您的伺服器名稱]\POWERPIVOT**。 如果您可以連接到執行個體，表示已確認服務正在執行。  
  
##  <a name="bkmk_config"></a> 步驟 2：設定基本 Analysis Services SharePoint 整合  
 下列步驟描述必要的組態變更，讓您可以與 SharePoint 文件庫中的 Excel 進階資料模型互動。 在您安裝 SharePoint 和 SQL Server Analysis Services 之後，完成這些步驟。  
  
### <a name="sharepoint-2016"></a>SharePoint 2016  
 Excel Services 已自 SharePoint 2016 移除，而改為使用 Office Online Server 來裝載 Excel。  
  
#### <a name="grant-office-online-server-machine-account-administration-rights-on-analysis-services"></a>針對 Analysis Services 授與 Office Online Server 機器帳戶管理權限  
 若在 Analysis Services 安裝期間則無須完成本節；您已加入 Office Online Server 機器帳戶做為 Analysis Services 管理員。  
  
1.  在 Analysis Services 伺服器上，啟動 SQL Server Management Studio 並連接至 Analysis Services 執行個體，例如 `[MyServer]\POWERPIVOT`.  
  
2.  在 [物件總管] 中，以滑鼠右鍵按一下執行個體名稱，然後選取 [屬性]。  
  
     ![檢視 SSAS 伺服器的內容](../../../analysis-services/instances/install-windows/media/as-ssms-proeprties.gif "SSAS 伺服器的檢視內容")  
  
3.  在左窗格中選取 [安全性] 。 新增已安裝 Office Online Server 的機器帳戶。  
  
     ![SSAS 伺服器的安全性設定](../../../analysis-services/instances/install-windows/media/as-ssms-security.gif "SSAS 伺服器的安全性設定")  
  
#### <a name="register-analysis-services-server-with-office-online-server"></a>使用 Office Online Server 登錄 Analysis Services 伺服器  
 您將會在 Office Online Server 上執行這些步驟。  
  
-   以系統管理員身分開啟 PowerShell 命令提示字元視窗。  
  
-   載入 `OfficeWebApps` PowerShell 模組。  
  
     `Import-Module OfficeWebApps`  
  
-   新增 Analysis Services 伺服器，例如 `[MyServer]\POWERPIVOT`。  
  
     `New-OfficeWebAppsExcelBIServer -ServerId [MyServer]\POWERPIVOT]`  
  
### <a name="sharepoint-2013"></a>SharePoint 2013  
  
#### <a name="grant-excel-services-server-administration-rights-on-analysis-services"></a>將 Analysis Services 的伺服器管理權限授與 Excel Services  
 如果在 Analysis Services 安裝期間，便不需要完成本節；您已加入 Excel Services 應用程式服務帳戶做為 Analysis Services 管理員。  
  
1.  在 Analysis Services 伺服器上，啟動 SQL Server Management Studio 並連接至 Analysis Services 執行個體，例如 `[MyServer]\POWERPIVOT`.  
  
2.  在 [物件總管] 中，以滑鼠右鍵按一下執行個體名稱，然後選取 [屬性]。  
  
     ![檢視 SSAS 伺服器的內容](../../../analysis-services/instances/install-windows/media/as-ssms-proeprties.gif "SSAS 伺服器的檢視內容")  
  
3.  在左窗格中選取 [安全性] 。 加入您在步驟 1 中為 Excel Services 應用程式設定的網域登入。  
  
     ![SSAS 伺服器的安全性設定](../../../analysis-services/instances/install-windows/media/as-ssms-security.gif "SSAS 伺服器的安全性設定")  
  
#### <a name="configure-excel-services-for-analysis-services-integration"></a>針對 Analysis Services 整合設定 Excel Services  
  
1.  在 [SharePoint 管理中心] 的 [應用程式管理] 群組中，按一下 **[管理服務應用程式]**。  
  
2.  按一下您的服務應用程式名稱，預設為 **[Excel Services 應用程式]**。  
  
3.  在 **[管理 Excel Services 應用程式]**頁面上，按一下 **[資料模型設定]**。  
  
4.  按一下 **[加入伺服器]**。  
  
5.  在 [伺服器名稱] 中，輸入 Analysis Services 伺服器名稱和 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 執行個體名稱。 例如 `MyServer\POWERPIVOT`。 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 執行個體名稱為必填。  
  
     輸入描述。  
  
6.  按一下 **[確定]**。  
  
7.  變更在數分鐘內就會生效，您也可以 **[停止]** 和 **[啟動]** **[Excel Calculation Services]**服務。 若要  
  
     另一個選項是使用系統管理權限來開啟命令提示字元，並輸入 `iisreset /noforce`。  
  
     您可以檢閱 ULS 記錄檔中的項目，驗證 Excel Services 已辨識伺服器。 您會看到與下列文字類似的項目：  
  
    ```  
    Excel Services Application            Data Model        27           Medium                Check Administrator Access ([ServerName]\POWERPIVOT): Pass.        f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Server Version ([ServerName]\POWERPIVOT): Pass (11.0.2809.24 >= 11.0.2800.0).         f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Deployment Mode ([ServerName]\POWERPIVOT): Pass.            f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
  
    ```  
  
##  <a name="bkmk_verify"></a> 步驟 3：確認整合  
 下列步驟會逐步引導您建立和上傳新的活頁簿，以確認 Analysis Services 整合。 您將需要使用 SQL Server 資料庫才能完成這些步驟。  
  
1.  **注意** ：如果您已經有含交叉分析篩選器或篩選的進階活頁簿，可以將它上傳至 SharePoint 文件庫，然後確認您可以從文件庫檢視中與交叉分析篩選器和篩選互動。  
  
2.  在 Excel 中啟動新的活頁簿。  
  
3.  在 [資料] 索引標籤上，選取位於 [取得外部資料]  功能區的 [從其他來源] 。  
  
4.  選取 **[從 SQL Server]**。  
  
5.  在 **[資料連線精靈]**，輸入具有您要使用的資料庫的 SQL Server 執行個體名稱。  
  
6.  在登入認證下方，確認已選取 [使用 Windows 驗證]  ，然後選取 [下一步] 。  
  
7.  選取您要使用的資料庫。  
  
8.  確認已選取 **[連接至指定的表格]** 核取方塊。  
  
9. 選取 [啟用選取多個資料表並將資料表加入至 Excel 資料模型]  核取方塊。  
  
10. 選取要匯入的資料表。  
  
11. 選取 [匯入選定資料表之間的關聯性] 核取方塊，然後選取 [下一步] 。 從關聯式資料庫匯入多個資料表，可讓您使用已經相關的資料表。 這個方式可以免除一些步驟，因為您不需要手動建立關聯性。  
  
12. 在精靈的 [儲存資料連線檔案和完成]  頁面上，輸入您的連接名稱，然後選取 [完成] 。  
  
13. **[匯入資料]** 對話方塊將會出現。 選擇 [樞紐分析表] ，然後選取 [確定] 。  
  
14. [樞紐分析表欄位清單] 會出現在活頁簿中。   
    在欄位清單中，選取 [全部]  索引標籤  
  
15. 在欄位清單中的資料列、資料行和值區域，新增欄位。  
  
16. 將篩選或交叉分析篩選器加入至樞紐分析表。 **請勿略過這個步驟**。 篩選或交叉分析篩選器是協助您確認 Analysis Services 安裝的元素。  
  
17. 將活頁簿儲存至您 SharePoint 伺服器陣列中的文件庫。 您也可以將活頁簿儲存至檔案共用，然後將其上傳至 SharePoint 文件庫。  
  
18. 選取您的活頁簿名稱並在 Excel Online 中檢視，然後按一下交叉分析篩選器或變更您先前加入的篩選。 若發生資料更新，您就會知道 Analysis Services 已安裝並可供 Excel 使用。 如果您在 Excel 中開啟活頁簿，將會使用快取副本，而不是 Analysis Services 伺服器。  
  
##  <a name="bkmk_firewall"></a> 設定 Windows 防火牆以允許 Analysis Services 存取  
 請使用＜ [設定 Windows 防火牆以允許 Analysis Services 存取](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) ＞主題中的資訊來判斷是否需要在防火牆中解除封鎖通訊埠，以允許存取 Analysis Services 或 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 需要 SharePoint Server Enterprise 版。 您可以遵循此主題所提供的步驟，設定通訊埠以及防火牆。 實際上，您必須執行這些步驟，才能允許存取 Analysis Services 伺服器。  
  
##  <a name="bkmk_upgrade_workbook"></a> 升級活頁簿和排程的資料重新整理  
 升級在舊版 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 中建立之活頁簿所需的步驟，主要取決於建立活頁簿的 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 版本。 如需詳細資訊，請參閱 [升級活頁簿和排程的資料重新整理 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)。  
  
##  <a name="bkmk_multiple_servers"></a> 超越單一伺服器安裝 – PowerPivot for Microsoft SharePoint  
 **Web 前端 (WFE)** 或 **中介層**：若要在較大的 SharePoint 伺服器陣列中使用 SharePoint 模式的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器，並且將其他 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 功能安裝至伺服器陣列中，請在每部 SharePoint 伺服器上執行安裝程式封裝 **spPowerPivot16.msi (SharePoint 2016) 或 spPowerPivot.msi (SharePoint 2013)** 。 spPowerPivot16.msi 或 spPowerPivot.msi 會安裝必要的資料提供者以及 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] for SharePoint 2016 或 2013 設定工具。  
  
 如需有關安裝及設定中介層的詳細資訊，請參閱以下主題：  
  
-   [安裝或解除安裝 PowerPivot for SharePoint 增益集 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
-   [安裝或解除安裝 PowerPivot for SharePoint 增益集 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
-   若要下載 .msi，請參閱＜ [Microsoft SQL Server 2016 PowerPivot for Microsoft SharePoint 2016](http://go.microsoft.com/fwlink/?LinkID=324854)＞  
  
-   [設定 Power Pivot 及部署方案 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)  
  
 **備援性和伺服器負載** ：在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 模式下安裝第二部或其他 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 伺服器，可提供 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器功能的備援性。 其他伺服器也會分散伺服器的負載。 如需詳細資訊，請參閱下列內容：  
  
-   [在 Excel Services 中設定 Analysis Services 以處理資料模型](http://technet.microsoft.com/library/jj614437\(v=office.15\)) (http://technet.microsoft.com/library/jj614437(v=office.15))。  
  
-   [Manage Excel Services data model settings (SharePoint Server 2013)](http://technet.microsoft.com/library/jj219780\(v=office.15\)) (http://technet.microsoft.com/library/jj219780(v=office.15)) (管理 Excel Services 資料模型設定 (SharePoint Server 2013)).  
  
 ![SharePoint 設定](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 設定")[透過 Microsoft SQL Server Connect 提交意見和連絡資訊](https://connect.microsoft.com/SQLServer/Feedback)(https://connect.microsoft.com/SQLServer/Feedback)。  
  
## <a name="see-also"></a>請參閱＜  
 [將 Power Pivot 移轉至 SharePoint 2013](../../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)   
 [安裝或解除安裝 PowerPivot for SharePoint 增益集 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)   
 [升級活頁簿和排程的資料重新整理 &#40;SharePoint 2013 &#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  
