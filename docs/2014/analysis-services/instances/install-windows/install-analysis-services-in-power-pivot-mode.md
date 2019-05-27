---
title: PowerPivot for SharePoint 2013 安裝 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: d3310562-82c1-454f-9c48-33a241749238
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f89ba75ab8d13960b3c86193862f5061f6727bb6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079935"
---
# <a name="powerpivot-for-sharepoint-2013-installation"></a>PowerPivot for SharePoint 2013 安裝
  本主題中的程序會引導您完成 SharePoint 部署模式之 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器的單一伺服器安裝。 這些步驟包含執行 [SQL Server 安裝精靈]，以及使用 SharePoint 2013 管理中心的設定工作。  
  
 **[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 201  
  
 **本主題內容：**  
  
 [背景](#bkmk_background)  
  
 [必要條件](#bkmk_prereq)  
  
 [步驟 1：安裝 PowerPivot for SharePoint](#InstallSQL)  
  
 [步驟 2：設定基本 Analysis Services SharePoint 整合](#bkmk_config)  
  
 [步驟 3：確認整合](#bkmk_verify)  
  
 [設定 Windows 防火牆以允許 Analysis Services 存取](#bkmk_firewall)  
  
 [升級活頁簿和排程的資料重新整理](#bkmk_upgrade_workbook)  
  
 [超越單一伺服器安裝 PowerPivot for Microsoft SharePoint](#bkmk_multiple_servers)  
  
##  <a name="bkmk_background"></a> 背景  
 PowerPivot for SharePoint 是中間層及後端服務的集合，可以在 SharePoint 2013 伺服器陣列中提供 PowerPivot 資料存取功能。  
  
-   **後端服務：** 如果您使用 PowerPivot for Excel 建立包含分析資料的活頁簿時，您必須具有 PowerPivot for SharePoint，才可存取該伺服器環境中的資料。 您可以在已安裝 SharePoint Server 2013 的電腦或在沒有 SharePoint 軟體的另一部電腦上執行 SQL Server 安裝程式。 Analysis Services 沒有 SharePoint 的相依性。  
  
     **注意：** 本主題說明如何安裝[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]伺服器和後端服務。  
  
-   **中介層：** 包括 PowerPivot 圖庫、 排程資料重新整理、 管理儀表板和資料提供者的 SharePoint 中 PowerPivot 體驗的增強功能。 如需有關安裝及設定中介層的詳細資訊，請參閱以下主題：  
  
    -   [安裝或解除安裝 PowerPivot for SharePoint 增益集&#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
    -   [設定 PowerPivot 及部署解決方案&#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)  
  
##  <a name="bkmk_prereq"></a> 必要條件  
  
1.  您必須是本機系統管理員，才能執行 SQL Server 安裝程式。  
  
2.  PowerPivot for SharePoint 需要 SharePoint Server 2013 Enterprise 版。 您也可以使用 Evaluation Enterprise 版。  
  
3.  電腦必須與 Excel Services 加入相同 Active Directory 樹系中的網域。  
  
4.  必須提供 PowerPivot 執行個體名稱。 正在安裝 Analysis Services SharePoint 模式的電腦上，不能有現存的 PowerPivot 具名執行個體。  
  
5.  檢閱[硬體和軟體需求，以 SharePoint 模式的 Analysis Services 伺服器&#40;SQL Server 2014&#41;](../../../sql-server/install/hardware-software-requirements-analysis-services-server-sharepoint-mode.md)。  
  
6.  檢閱版本資訊[SQL Server 2012 Service Pack 1 版本資訊](https://go.microsoft.com/fwlink/?LinkID=248389)(https://go.microsoft.com/fwlink/?LinkID=248389)。  
  
###  <a name="bkmk_sqleditions"></a> SQL Server Edition 需求  
 並非在所有版本的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]中都提供商業智慧功能。 如需詳細資訊，請參閱 <<c0> [ 支援的 SQL Server 2012 版本的功能 (https://go.microsoft.com/fwlink/?linkid=232473) ](https://go.microsoft.com/fwlink/?linkid=232473)並[版本和 SQL Server 2014 元件](../../../sql-server/editions-and-components-of-sql-server-2016.md)。  
  
 目前的版本資訊，請參閱[SQL Server 2012 SP1 版本的資訊](ttp://go.microsoft.com/fwlink/?LinkID=248389)(https://go.microsoft.com/fwlink/?LinkID=248389)。  
  
 [Microsoft SQL Server 2012 版本資訊 (https://go.microsoft.com/fwlink/?LinkId=236893)](https://go.microsoft.com/fwlink/?LinkId=236893)。  
  
##  <a name="InstallSQL"></a> 步驟 1：安裝 PowerPivot for SharePoint  
 在此步驟中，您會執行 SQL Server 安裝程式，安裝 SharePoint 模式的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 伺服器。 在後續步驟中，您針對活頁簿資料模型設定 Excel Services 使用此伺服器。  
  
1.  執行 [SQL Server 安裝精靈] \(Setup.exe)。  
  
2.  按一下左邊功能窗格中的 **[安裝]** 。  
  
3.  按一下 **[新增 SQL Server 獨立安裝或將功能加入至現有安裝]**。  
  
4.  如果看到 **[產品金鑰]** 頁面，請指定 Evaluation Edition 或是輸入 Enterprise Edition 授權複本的產品金鑰。 按一下 [下一步] 。 如需版本的詳細資訊，請參閱＜ [Editions and Components of SQL Server 2014](../../../sql-server/editions-and-components-of-sql-server-2016.md)＞。  
  
5.  檢閱並接受 Microsoft 軟體授權條款的條款，然後按 **[下一步]**。  
  
6.  如果您看到 **[全域規則]** 頁面，請檢閱安裝精靈顯示的所有規則資訊。  
  
7.  在 **[Microsoft Update]** 頁面上，建議您使用 Microsoft Update 來檢查更新，然後按 **[下一步]**。  
  
8.  **[安裝安裝檔案]** 頁面會執行數分鐘。 檢閱任何規則警告或失敗規則，然後按 **[下一步]**。  
  
9. 如果您看到另一個 **[安裝程式支援規則]**，請檢閱任何警告，然後按 **[下一步]**。  
  
     **注意：** 因為已啟用 Windows 防火牆，您會看到開放通訊埠來啟用遠端存取的警告。  
  
10. 在 **[安裝程式角色]** 頁面上，選取 **[SQL Server PowerPivot for SharePoint]**。 此選項會安裝 SharePoint 模式的 Analysis Services。  
  
     您可選擇性地在安裝中加入一項 Database Engine 的執行個體。 您可能會加入 Database Engine，設定新的伺服器陣列時，且需要資料庫伺服器以執行伺服器陣列的組態和內容資料庫。 此選項也會安裝 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]。  
  
     如果您加入 Database Engine，則會安裝為 **PowerPivot** 具名執行個體。 每當您指定此執行個體的連接時，請用此格式輸入資料庫名稱：[`servername`]\PowerPivot。  
  
     按一下 [下一步] 。  
  
     ![安裝程式角色](../../../sql-server/install/media/gmni-setupui-featurerole-sql2012sp1.gif "安裝程式角色")  
  
11. [特徵選取] 會顯示各項功能的唯讀清單，以供使用者參考。 您無法加入或移除預先為這個角色選取的項目。 按一下 [下一步] 。  
  
12. 在 **[執行個體組態]** 頁面上，顯示 'PowerPivot' 的唯讀執行個體名稱是為了給使用者參考。 此執行個體名稱是必要的，而且無法修改。 但是，您可以輸入唯一的執行個體識別碼來指定描述性目錄名稱和登錄機碼。 按一下 [下一步] 。  
  
13. 在 **[伺服器組態]** 頁面上，將所有服務的 **[啟動類型]** 設定為 [自動]。 指定 **SQL Server Analysis Services**的所需網域帳戶和密碼，即下圖中的 **(1)** 。  
  
    -   針對 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，您可以使用 **網域使用者** 帳戶或 **NetworkService** 帳戶。 請勿使用 LocalSystem 或 LocalService 帳戶。  
  
    -   若已新增 SQL Server Database Engine 與 SQL Server Agent，您可以將服務設定為利用網域使用者帳戶或預設虛擬帳戶加以執行。  
  
    -   絕不要使用您自己的網域使用者帳戶來提供服務帳戶。 這麼做會授與伺服器您對網路中的資源所擁有的相同權限。 如果惡意使用者入侵伺服器，該使用者就會使用您的網域認證登入。 該使用者將有權下載或使用您有權下載或使用的相同資料和應用程式。  
  
     按一下 [下一步] 。  
  
     ![SSAS Server 組態](../../../sql-server/install/media/ssas-powerpivotsetupsql2012sp1-serverconfiguration.gif "SSAS Server 組態")  
  
14. 若您正安裝 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]，則隨即會出現 **[資料庫引擎組態]** 頁面。 在 [資料庫引擎組態] 中按一下 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] [加入目前使用者] **，為您的使用者帳戶授與** 執行個體的管理員權限。  
  
     按一下 [下一步] 。  
  
15. 在 **[Analysis Services 組態]** 頁面上，按一下 **[加入目前使用者]** ，為您的使用者帳戶授與管理權限。 在完成安裝程式之後，您將會需要管理權限來設定伺服器。  
  
    -   在相同的頁面上，加入也需要管理權限之任何人的 Windows 使用者帳戶。 例如，想要在 [!INCLUDE[ssGeminiSrv](../../../includes/ssgeminisrv-md.md)] 中連接至 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 執行個體以疑難排解資料庫連接問題的所有使用者，都必須擁有系統管理員權限。 請加入可能需要立即針對伺服器進行疑難排解或管理之任何人的使用者帳戶。  
  
    -   > [!NOTE]  
        >  需要存取 Analysis Services 伺服器執行個體的所有服務應用程式都必須具有 Analysis Services 管理權限。 例如，加入 Excel Services、Power View 及 Performance Point 服務的服務帳戶。 此外，請加入 SharePoint 伺服器陣列帳戶，做為裝載管理中心的 Web 應用程式的識別。  
  
     按 [下一步] 。  
  
16. 在 **[錯誤報告]** 頁面上，按 **[下一步]**。  
  
17. 在 **[準備安裝]** 頁面上，按一下 **[安裝]**。  
  
18. 如果您看見 **[需要重新啟動電腦]** 對話方塊，請按一下 **[確定]**。  
  
19. 安裝完成時，按一下 **[關閉]**。  
  
20. 重新啟動電腦。  
  
21. 如果您的環境有防火牆，請檢閱《SQL Server 線上叢書》主題＜ [Configure the Windows Firewall to Allow Analysis Services Access](../configure-the-windows-firewall-to-allow-analysis-services-access.md)＞。  
  
### <a name="verify-the-sql-server-installation"></a>確認 SQL Server 安裝  
 確認 Analysis Services 服務正在執行。  
  
1.  在 Microsoft Windows 按一下 **[開始]**，按一下 **[所有程式]**，然後按一下 **[Microsoft SQL Server 2012]** 群組。  
  
2.  按一下 **[SQL Server Management Studio]**。  
  
3.  連接至 Analysis Services 執行個體，例如 **[您的伺服器名稱]\POWERPIVOT**。 如果您可以連接到執行個體，表示已確認服務正在執行。  
  
##  <a name="bkmk_config"></a> 步驟 2：設定基本 Analysis Services SharePoint 整合  
 下列步驟描述必要的組態變更，讓您可以與 SharePoint 文件庫中的 Excel 進階資料模型互動。 在您安裝 SharePoint Server 2013 和 SQL Server Analysis Services 之後，完成這些步驟。  
  
### <a name="grant-excel-services-server-administration-rights-on-analysis-services"></a>將 Analysis Services 的伺服器管理權限授與 Excel Services  
 如果在 Analysis Services 安裝期間，便不需要完成本節；您已加入 Excel Services 應用程式服務帳戶做為 Analysis Services 管理員。  
  
1.  在 Analysis Services 伺服器上，啟動 SQL Server Management Studio 並連接至 Analysis Services 執行個體，例如 `[MyServer]\POWERPIVOT`.  
  
2.  在 [物件總管] 中，以滑鼠右鍵按一下執行個體名稱，然後按一下 **[屬性]**。  
  
     ![檢視 SSAS 伺服器的內容](../../../sql-server/install/media/as-ssms-proeprties.gif "SSAS 伺服器的檢視內容")  
  
3.  按一下左窗格中的 **[安全性]**。 加入您在步驟 1 中為 Excel Services 應用程式設定的網域登入。  
  
     ![SSAS 伺服器的安全性設定](../../../sql-server/install/media/as-ssms-security.gif "SSAS 伺服器的安全性設定")  
  
### <a name="configure-excel-services-for-analysis-services-integration"></a>針對 Analysis Services 整合設定 Excel Services  
  
1.  在 [SharePoint 管理中心] 的 [應用程式管理] 群組中，按一下 **[管理服務應用程式]**。  
  
2.  按一下您的服務應用程式名稱，預設為 **[Excel Services 應用程式]**。  
  
3.  在 **[管理 Excel Services 應用程式]** 頁面上，按一下 **[資料模型設定]**。  
  
4.  按一下 **[加入伺服器]**。  
  
5.  在 **[伺服器名稱]** 中，輸入 Analysis Services 伺服器名稱和 PowerPivot 執行個體名稱。 例如 `MyServer\POWERPIVOT`。 PowerPivot 執行個體名稱是必要項。  
  
     輸入描述。  
  
6.  按一下 **[確定]**。  
  
7.  變更在數分鐘內就會生效，您也可以 **[停止]** 和 **[啟動]** **[Excel Calculation Services]** 服務。 若要  
  
     另一個選項是使用系統管理權限來開啟命令提示字元，並輸入 `iisreset /noforce`。  
  
     您可以檢閱 ULS 記錄檔中的項目，驗證 Excel Services 已辨識伺服器。 您會看到與下列文字類似的項目：  
  
    ```  
    Excel Services Application            Data Model        27           Medium                Check Administrator Access ([ServerName]\POWERPIVOT): Pass.        f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Server Version ([ServerName]\POWERPIVOT): Pass (11.0.2809.24 >= 11.0.2800.0).         f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
    Excel Services Application            Data Model        27           Medium                Check Deployment Mode ([ServerName]\POWERPIVOT): Pass.            f127bd9b-bae3-e0e0-9b48-3f7b5ad1eae6  
  
    ```  
  
##  <a name="bkmk_verify"></a> 步驟 3：確認整合  
 下列步驟會逐步引導您建立和上傳新的活頁簿，以確認 Analysis Services 整合。 您將需要使用 SQL Server 資料庫才能完成這些步驟。  
  
1.  **注意：** 如果您已經使用交叉分析篩選器或篩選的進階活頁簿，您可以將它上傳至 SharePoint 文件庫，並確認您能夠與交叉分析篩選器和篩選互動從文件庫檢視。  
  
2.  在 Excel 中啟動新的活頁簿。  
  
3.  在 [資料] 索引標籤上，按一下功能區上 **[取得外部資料]** 中的 **[從其他來源]**。  
  
4.  選取 **[從 SQL Server]**。  
  
5.  在 **[資料連線精靈]**，輸入具有您要使用的資料庫的 SQL Server 執行個體名稱。  
  
6.  或登入認證，確認已選取 **[使用 Windows 驗證]** ，然後按 **[下一步]**。  
  
7.  選取您要使用的資料庫。  
  
8.  確認已選取 **[連接至指定的表格]** 核取方塊。  
  
9. 按一下 **[啟用選取多個資料表並將資料表加入至 Excel 資料模型]** 核取方塊。  
  
10. 選取要匯入的資料表。  
  
11. 按一下 **[匯入選定資料表之間的關聯性]** 核取方塊，然後按 **[下一步]**。 從關聯式資料庫匯入多個資料表，可讓您使用已經相關的資料表。 這個方式可以免除一些步驟，因為您不需要手動建立關聯性。  
  
12. 在精靈的 **[儲存資料連線檔案和完成]** 頁面上，輸入您的連接名稱，然後按一下 **[完成]**。  
  
13. **[匯入資料]** 對話方塊將會出現。 選擇 **[樞紐分析表]**，然後按一下 **[確定]**。  
  
14. [樞紐分析表欄位清單] 會出現在活頁簿中。   
    在欄位清單中，按一下 **[全部]** 索引標籤。  
  
15. 在欄位清單中的資料列、資料行和值區域，新增欄位。  
  
16. 將篩選或交叉分析篩選器加入至樞紐分析表。 **請勿略過這個步驟**。 篩選或交叉分析篩選器是協助您確認 Analysis Services 安裝的元素。  
  
17. 將活頁簿儲存至已設定 Excel Services 的 SharePoint Server 2013 文件庫。 您也可以將活頁簿儲存至檔案共用，然後將它上傳至 SharePoint Server 2013 文件庫。  
  
18. 按一下您的活頁簿名稱，在 SharePoint 中檢視它，然後按一下交叉分析篩選器或變更您先前加入的篩選。 如果發生資料更新，您就會知道 Analysis Services 已安裝，可供 Excel Services 使用。 如果您在 Excel 中開啟活頁簿，將會使用快取副本，而不是 Analysis Services 伺服器。  
  
##  <a name="bkmk_firewall"></a> 設定 Windows 防火牆以允許 Analysis Services 存取  
 請使用＜ [Configure the Windows Firewall to Allow Analysis Services Access](../configure-the-windows-firewall-to-allow-analysis-services-access.md) ＞主題中的資訊來判斷是否需要在防火牆中解除封鎖通訊埠，以允許存取 Analysis Services 或 PowerPivot for SharePoint。 您可以遵循此主題所提供的步驟，設定通訊埠以及防火牆。 實際上，您必須執行這些步驟，才能允許存取 Analysis Services 伺服器。  
  
##  <a name="bkmk_upgrade_workbook"></a> 升級活頁簿和排程的資料重新整理  
 升級在舊版 PowerPivot 中建立之活頁簿所需的步驟主要取決於建立活頁簿的 PowerPivot 版本。 如需詳細資訊，請參閱 [升級活頁簿和排程的資料重新整理 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)。  
  
##  <a name="bkmk_multiple_servers"></a> 超越單一伺服器安裝 PowerPivot for Microsoft SharePoint  
 **Web 前端 (WFE)** 或是**中介層：**:若要使用[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]較大的 SharePoint 伺服器陣列中，以及其他的 PowerPivot 功能安裝至伺服器陣列中，執行安裝程式套件的 SharePoint 模式伺服器**spPowerPivot.msi**每部 SharePoint 伺服器上。 spPowerPivot.msi 會安裝必要的資料提供者以及 PowerPivot for SharePoint 2013 組態工具。  
  
 如需有關安裝及設定中介層的詳細資訊，請參閱以下主題：  
  
-   [安裝或解除安裝 PowerPivot for SharePoint 增益集&#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)  
  
-   若要下載 .msi，請參閱＜ [Microsoft SQL Server 2014 PowerPivot for Microsoft SharePoint 2013](https://go.microsoft.com/fwlink/?LinkID=324854)＞  
  
-   [設定 PowerPivot 及部署解決方案&#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/configure-power-pivot-and-deploy-solutions-sharepoint-2013.md)  
  
 **備援性和伺服器負載：** 安裝第二個，或其他[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]SharePoint 模式的伺服器可提供備援性[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]伺服器功能。 其他伺服器也會分散伺服器的負載。 如需詳細資訊，請參閱下列內容：  
  
-   [設定 Analysis Services 以便處理 Excel Services 中的資料模型](https://technet.microsoft.com/library/jj614437\(v=office.15\))(https://technet.microsoft.com/library/jj614437(v=office.15))。  
  
-   [管理 Excel Services 資料模型設定 (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780\(v=office.15\)) (https://technet.microsoft.com/library/jj219780(v=office.15))。  
  
 ![SharePoint 設定](../../../analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 設定")[透過 Microsoft SQL Server Connect 提交意見與連絡資訊](https://connect.microsoft.com/SQLServer/Feedback)(https://connect.microsoft.com/SQLServer/Feedback)。  
  
## <a name="see-also"></a>另請參閱  
 [將 PowerPivot 移轉至 SharePoint 2013](../../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)   
 [安裝或解除安裝 PowerPivot for SharePoint 增益集&#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)   
 [升級活頁簿和排程的資料重新整理 &#40;SharePoint 2013&#41;](../../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  
