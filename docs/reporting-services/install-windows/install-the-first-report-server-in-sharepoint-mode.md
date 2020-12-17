---
description: 以 SharePoint 模式安裝第一部報表伺服器
title: 以 SharePoint 模式安裝第一部報表伺服器 | Microsoft Docs
ms.date: 10/05/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016'
ms.openlocfilehash: 36b68809377492e3643ebc7c60e0b2111d52f638
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484240"
---
# <a name="install-the-first-report-server-in-sharepoint-mode"></a>以 SharePoint 模式安裝第一部報表伺服器

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

  本主題中的程序會引導您完成 SharePoint 模式之 Reporting Services 的單一伺服器安裝。 這些步驟包含執行 [SQL Server 安裝精靈]，以及使用 SharePoint 管理中心的設定工作。 本主題也可以用於更新現有安裝的個別程序，例如建立 Reporting Services 服務應用程式。  
  
> [!NOTE]
> SQL Server 2016 後即不再提供 Reporting Services 與 SharePoint 的整合。
  
 如需將其他 Reporting Services 伺服器新增至現有伺服器陣列的資訊，請參閱下列主題：  
  
-   [將其他報表伺服器加入至伺服器陣列 &#40;SSRS 向外延展&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
-   [將其他 Reporting Services Web 前端加入至伺服器陣列](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 單一伺服器安裝對開發和測試案例很實用，但是不建議在實際執行環境中使用。  
  
##  <a name="example-single-server-deployment"></a><a name="bkmk_singleserver"></a> 單一伺服器部署範例

 單一伺服器安裝對開發和測試案例很實用，但是不建議在實際執行環境中使用單一伺服器。 單一伺服器環境是指在同一部電腦上安裝 SharePoint 和 Reporting Services 元件的單一電腦。 本主題並未涵蓋具有多部 Reporting Services 伺服器的向外延展。  
  
 下圖說明單一伺服器 Reporting Services 部署之一部分的元件。  
 
 > [!NOTE]
 > 對於 SharePoint 2016，Excel Services 已移至 Office Online Server，而且不能用於單一伺服器部署中。 Office Online Server 必須部署至不同的伺服器。 如需詳細資訊，請參閱 [Office Online Server 概觀](https://technet.microsoft.com/library/jj219437\(v=office.16\).aspx) 和 [設定 Excel Online 系統管理設定](https://technet.microsoft.com/library/jj219698\(v=office.16\).aspx)。
  
|||  
|-|-|  
|**(1)**|從 SQL Server 安裝所安裝的 SharePoint 服務。 您可以建立一或多個 Reporting Services 服務應用程式。|  
|**(2)**|適用於 SharePoint 產品的 Reporting Services 增益集會在 SharePoint 伺服器上提供使用者介面元件。|  
|**(3)**|由 Power View 和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]所使用的 Excel 服務應用程式。 適用於 SharePoint 2016 的單一伺服器部署未提供這個項目。 需要 [Office Online Server](https://technet.microsoft.com/library/jj219437\(v=office.16\).aspx) 。|  
|**(4)**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務應用程式。|  
  
 ![SSRS SharePoint 模式單一伺服器部署](../../reporting-services/install-windows/media/rs-sharepoint-1server-deployment.gif "SSRS SharePoint 模式單一伺服器部署")  
  
> [!TIP]  
>  如需更多複雜的部署範例，請參閱 [SharePoint 中 SQL Server BI 功能的部署拓撲](/previous-versions/sql/sql-server-2016/hh231674(v=sql.130))。  
  
##  <a name="setup-accounts"></a><a name="bkmk_setupaccounts"></a> 安裝程式帳戶

 本節描述用於 SharePoint 模式之 Reporting Services 主要部署步驟的帳戶和權限。  
  
 **安裝和註冊 Reporting Services 服務：**  
  
-   在安裝 SharePoint 模式之 Reporting Services 期間使用的目前帳戶 (稱為「安裝程式」帳戶) 需要擁有本機電腦的系統管理權限。 如果您要在安裝 SharePoint 之後安裝 Reporting Services，而且「安裝程式」帳戶也是 SharePoint 伺服器陣列管理員群組的成員，Reporting Services 安裝程序將會為您註冊 Reporting Services 服務。 如果您在安裝 SharePoint 之前安裝 Reporting Services，或者「安裝程式」帳戶不是伺服器陣列管理員群組的成員，您就必須手動註冊服務。 請參閱＜ [步驟 2：註冊並啟動 Reporting Services SharePoint 服務](#bkmk_install_SSRS_sharedservice)。  
  
 **建立 Reporting Services 服務應用程式**  
  
-   安裝並註冊 Reporting Services 服務之後，請建立一或多個 Reporting Services 服務應用程式。 「SharePoint 伺服器陣列服務帳戶」需要暫時成為本機 Administrators 群組的成員，才能建立 Reporting Services 服務應用程式。 如需 SharePoint 2013 帳戶權限的詳細資訊，請參閱 [SharePoint 2013 中的帳戶權限及安全性設定](/SharePoint/install/account-permissions-and-security-settings-in-sharepoint-server-2016) (https://technet.microsoft.com/library/cc678863.aspx) ，若為 SharePoint 2016，則請參閱 [SharePoint 2016 中的帳戶權限及安全性設定](https://technet.microsoft.com/library/cc678863\(v=office.16\).aspx)。  
  
     安全性最佳作法是避免讓 SharePoint 伺服陣列管理員帳戶同時成為本機作業系統管理員帳戶。 如果您在安裝程序中，將伺服陣列管理員帳戶加入至本機 Administrators 群組，建議您在安裝完成之後，從本機 Administrators 群組中移除該帳戶。  
  
##  <a name="step-1-install-reporting-services-report-server-in-sharepoint-mode"></a><a name="bkmk_install_SSRS"></a> 步驟 1：在 SharePoint 模式下安裝 Reporting Services 報表伺服器

 這個步驟會在 SharePoint 模式下安裝 Reporting Services 報表伺服器以及適用於 SharePoint 產品的 Reporting Services 增益集。 根據電腦上已經安裝的元件而定，您可能不會看見下列步驟所描述的部分安裝頁面。  
 
 > [!IMPORTANT]
 > 對於 SharePoint 2016，將安裝 Reporting Services 的 SharePoint 伺服器需要具有 [自訂]  伺服器角色。 Reporting Services 部署將在非 [自訂]  角色的 SharePoint 伺服器上成功，但在下一個 SharePoint 維護期間，MinRole 將停止 Reporting Services 服務，因為它偵測到 SharePoint-整合模式中的 Reporting Services 未指出支援任何其他 SharePoint 伺服器角色。 Reporting Services 服務應用程式僅支援 [自訂]  角色。
 
 > [!NOTE]
 > 如果您也打算在 SharePoint 2016 上安裝 Power Pivot 服務，請先安裝該服務，再安裝 Reporting Services。 只能在 SharePoint 伺服器上的 **自訂角色** 中安裝 Power Pivot 服務。
 
 ### <a name="apply-the-custom-server-role-to-a-sharepoint-2016-server"></a>將自訂伺服器角色套用至 SharePoint 2016 伺服器
 
 > [!NOTE]
 > 這不適用於 SharePoint 2013。
 
 1. 登入您想要安裝 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]。
 
 2. 以系統管理員身分啟動 **SharePoint 2016 管理命令介面** 。 
  
    您可以用滑鼠右鍵按一下 [SharePoint 2016 管理命令介面]  ，然後選取 [以系統管理員身分執行]  。

3. 從 PowerShell 命令提示字元中，執行下列命令。

    > [!NOTE]
    > 請確定您指定正確的 SharePoint 伺服器名稱。
    
    ```powershell
    Set-SPServer SERVERNAME -Role Custom
    ```

4. 您應該會看到已排程計時器工作的回應。 您必須等到工作執行。

5. 使用下列命令來確認伺服器的已指派角色。

    ```powershell
    Get-SPServer SERVERNAME 
    ```
 
 6. [角色]  應該會列出 [自訂]  。
 
 ### <a name="install-reporting-services"></a>安裝 Reporting Services
  
1.  執行 [SQL Server 安裝精靈] \(Setup.exe)。  
  
2.  在精靈的左側選取 [安裝]  ，然後選取 [新增 SQL Server 獨立安裝或將功能新增至現有安裝]  。  

3.  如果您看見 [產品金鑰]  頁面，請輸入您的金鑰或接受 "Enterprise Evaluation" 版本的預設值。  
  
     選取 [下一步]  。  
  
4.  如果您看見 [授權條款] 頁面，請檢閱並接受這些授權條款。 Microsoft 感謝您同意傳送功能使用資料，協助改進產品功能及支援。  
  
     選取 [下一步]  。  

5.  建議您選取 [使用 Microsoft Update 檢查更新 (建議使用)]  。 這是選擇性的。
  
     選取 [下一步]  。   
  
6.  在 [安裝安裝程式檔案]  頁面上，根據電腦上已經安裝的元件而定，您可能會看見下列訊息：  
  
    -   「一個或多個受影響的檔案有暫止的作業。 您必須在安裝程序完成之後重新啟動電腦。」  
  
    -   選取 [下一步]  。  
  
7.  如果您看見 [安裝規則]  頁面。 檢閱任何警告或封鎖問題。 然後選取 [下一步]  。
 
8. 在 **[特徵選取]** 頁面上，選取下列選項：  
  
    -   **Reporting Services - SharePoint**  
  
    -   **適用於 SharePoint 產品的 Reporting Services 增益集**。  
  
    -   您也可以選擇性地選取完整環境的 [Database Engine 服務]  不過，您應該會有主控 SharePoint 資料庫的 SQL Server Database Engine 執行個體。  
  
     選取 [下一步]  。  
  
     ![已選取 [Reporting Services - SharePoint] 和 [適用於 SharePoint 產品的 Reporting Services 增益集] 選項的 [特徵選取] 頁面螢幕擷取畫面。](../../reporting-services/install-windows/media/rs-setupfeatureselection-sharepoint-with-circles.png)
  
9. 如果您選取 Database Engine 服務，請接受 **[執行個體組態]** 頁面上的預設 **[MSSQLSERVER]** 執行個體，然後按 **[下一步]** 。  
  
     ![注意](/analysis-services/analysis-services/instances/install-windows/media/ssrs-fyi-note.png "注意")Reporting Services SharePoint 服務架構不以 SQL Server「執行個體」為基礎，和舊版的 Reporting Services 架構不同。  
  
10. 如果您看見 **[伺服器組態]** 頁面，請輸入適當的認證。 如果您想要使用 Reporting Services 資料警示或訂閱功能，則必須將 SQL Server Agent 的 [啟動類型]  變更為 [自動]  。 根據電腦上已經安裝的元件而定，您可能不會看見 **[伺服器組態]** 頁面。  
  
     選取 [下一步]  。  
  
11. 如果您已選取 Database Engine 服務，就會看到 [資料庫引擎設定]  頁面。請將適當的帳戶新增至 SQL 系統管理員清單，然後選取 [下一步]  。  
  
12. 在 **[Reporting Services 組態]** 頁面上，您應該會看到已選取 **[只安裝]** 選項。 這個選項會安裝報表伺服器檔案，但是不會設定 Reporting Services 的 SharePoint 環境。  
  
    > [!NOTE]
    > 當 SQL Server 安裝完成時，請遵循本主題其他章節來設定 SharePoint 環境。 這包括安裝 Reporting Services 共用服務以及建立 Reporting Services 服務應用程式。  
  
     ![已選取且已標註 [只安裝] 選項的 [Reporting Services SharePoint 整合模式] 區段螢幕擷取畫面。](../../reporting-services/install-windows/media/ssrs-2016-setup-configuration.png)
  
13. 如果您停在此頁面上，請檢閱任何警告，然後選取 [功能設定規則] 頁面上的 [下一步]。  
  
14. 在 [準備安裝]  頁面上，檢閱安裝摘要。 此摘要將包括其值顯示為 **[SharePointFilesOnlyMode]** 的 **[Reporting Services SharePoint 模式]** 子節點。 選取 [安裝]  。  
  
15. 安裝需要幾分鐘的時間。 您將會看見 **[完成]** 頁面，其中列出功能以及每項功能的狀態。 您可能會看見資訊對話方塊，指出電腦需要重新啟動。  
  
##  <a name="step-2-register-and-start-the-reporting-services-sharepoint-service"></a><a name="bkmk_install_SSRS_sharedservice"></a> 步驟 2：註冊並啟動 Reporting Services SharePoint 服務  
 ![PowerShell 相關內容](/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相關內容")  
  
> [!NOTE]
> 如果您要在現有的 SharePoint 伺服器陣列中進行安裝，則不需要完成本節中的步驟。 當您在本文件的上一節執行 SQL Server 安裝精靈時，就會安裝並啟動 Reporting Services SharePoint 服務。  
  
 您需要手動註冊 Reporting Services 服務的常見原因如下。  
  
-   您在安裝 SharePoint 之前已安裝 Reporting Services SharePoint 模式。  
  
-   此用來安裝 Reporting Services SharePoint 模式的帳戶，不是 SharePoint 伺服器陣列管理員群組的成員。 如需詳細資訊，請參閱＜ [Setup accounts](#bkmk_setupaccounts)＞一節。  
  
 必要檔案會隨 [SQL Server 安裝精靈] 安裝，但是您必須在 SharePoint 伺服器陣列中註冊服務。  
  
 下列步驟將引導您開啟 SharePoint 管理命令介面並執行 PowerShell Cmdlet：  
  
1.  選取 [開始]  按鈕  
  
2.  選取 [Microsoft SharePoint 2016 產品]  或 [Microsoft SharePoint 2013 產品]  群組。  
  
3.  以滑鼠右鍵按一下 [SharePoint 2016 管理命令介面]  或 [SharePoint 2013 管理命令介面]  ，然後選取 [以系統管理員身分執行]  。 

    > [!NOTE]
    > 標準 Windows PowerShell 視窗無法辨識 SharePoint 命令。 使用 [SharePoint 管理命令介面]  。  
  
4.  執行下列 PowerShell 命令安裝 Reporting Services SharePoint 服務。 成功完成命令會在管理命令介面中顯示新行。 成功完成命令之後，**不會有任何訊息傳回** 管理命令介面：  
  
    ```  
    Install-SPRSService  
    ```  
  
5.  執行下列 PowerShell 命令安裝 Reporting Services 服務 Proxy。 成功完成命令會在管理命令介面中顯示新行。 成功完成命令之後，**不會有任何訊息傳回** 管理命令介面：  
  
    ```  
    Install-SPRSServiceProxy  
    ```  
  
6.  執行下列 PowerShell 命令以啟動服務，或參閱下列附註，以取得有關如何從 SharePoint 管理中心啟動服務的指示：  
  
    ```  
    get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
    ```  
  
    > [!IMPORTANT]
    > 如果您看到類似下列的錯誤訊息：  
    >   
    ```powershell
    >     Install-SPRSService : The term 'Install-SPRSService' **is not recognized** as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.  
    ```
    >
    > 您使用的可能是 Windows Powershell 而非 SharePoint 管理命令介面，或者未安裝 Reporting Services SharePoint 模式。 如需 Reporting Services 和 PowerShell 的詳細資訊，請參閱 [Reporting Services SharePoint 模式的 PowerShell Cmdlet](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)。  
  
 您也可以從 SharePoint 管理中心啟動服務，而不是執行第三個 PowerShell 命令。 下列步驟也可用於確認服務是否執行。  
  
1.  在 SharePoint 管理中心內，按一下 **[系統設定]** 群組中的 **[管理伺服器上的服務]** 。  
  
2.  找到 **[SQL Server Reporting Services 服務]** ，然後按一下 [動作] 欄中的 **[啟動]** 。  
  
3.  Reporting Services 服務的狀態會從 **[已停止]** 變更為 **[已啟動]** 。 如果清單中沒有 Reporting Services 服務，請使用 PowerShell 安裝該服務。  
  
    > [!NOTE]  
    >  如果 Reporting Services 服務停留在 [啟動中] 狀態，而未變更為 [已啟動]，請確認已在 Windows 伺服器管理員中啟動 'SharePoint 2013 Administration' 服務。  
  
##  <a name="step-3-create-a-reporting-services-service-application"></a><a name="bkmk_create_serrviceapplication"></a> 步驟 3：建立 Reporting Services 服務應用程式  
 本節提供建立服務應用程式的步驟，以及屬性的描述 (如果您要檢閱現有的服務應用程式)。  
  
1.  在 SharePoint 管理中心的 [應用程式管理] 群組中，選取 [管理服務應用程式]。  
  
2.  在 SharePoint 功能區中，選取 [新增] 按鈕。  
  
3.  在 [新增] 功能表中，選取 [SQL Server Reporting Services 服務應用程式]。  
  
    > [!IMPORTANT]  
    >  如果清單中未出現 Reporting Services 選項，**表示未安裝 Reporting Services 共用服務**。 檢閱上一節中，如何使用 PowerShell Cmdlt 來安裝 Reporting Services 服務的相關資訊。  
  
4.  在 **[建立新的 SQL Server Reporting Services 服務應用程式]** 頁面中，輸入應用程式的名稱。 如果您要建立多個 Reporting Services 服務應用程式，描述性名稱和命名慣例將有助於您組織管理作業。  
  
5.  在 **[應用程式集區]** 區段中，建立應用程式的新應用程式集區 (建議)。 如果您針對應用程式集區和服務應用程式使用相同的名稱，可讓進行中的管理更容易。 這可能也會受到您將建立的服務應用程式數目以及是否需要在單一應用程式集區中使用許多應用程式所影響。 請參閱 SharePoint Server 文件集以取得應用程式集區管理的建議事項和最佳作法。  
  
     針對應用程式集區選取或建立安全性帳戶。 請務必指定網域使用者帳戶。 網域使用者帳戶會啟用 SharePoint 受管理帳戶功能，好讓您在一個地方更新密碼和帳戶資訊。 如果您計劃將部署向外延展，以包括在相同識別下執行的其他服務執行個體，也需要網域帳戶。  
  
6.  在 **[資料庫伺服器]** 中，您可以使用目前的伺服器或選擇不同的 SQL Server。  
  
7.  在 **[資料庫名稱]** 中，預設值是 `ReportingService_<guid>`，這是唯一的資料庫名稱。 若您要輸入新值，請輸入唯一值。 這是專門針對服務應用程式所建立的新資料庫。  
  
8.  在 **[資料庫驗證]** 中，預設值是 Windows 驗證。 如果您選擇 **[SQL 驗證]** ，請參考 SharePoint 文件，以了解在 SharePoint 部署中使用這個驗證類型的最佳作法。  
  
9. 在 **[Web 應用程式關聯]** 區段中，選取要佈建以供目前 Reporting Services 服務應用程式存取的 Web 應用程式。 您可以建立一個 Reporting Services 服務應用程式與一個 Web 應用程式的關聯。 如果目前所有的 Web 應用程式已有相關聯的 Reporting Services 服務應用程式，則會顯示警告訊息。  
  
10. 選取 [確定]。  
  
11. 服務應用程式的建立程序會需要數分鐘才能完成。 完成後，您會看到確認訊息及 **[提供訂閱和警示]** 頁面的連結。 如果您想要使用 Reporting Services 訂閱功能或資料警示功能，請完成提供步驟。 如需詳細資訊，請參閱 [SSRS 服務應用程式的佈建訂用帳戶及警示](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)。  
  
 ![PowerShell 相關內容](/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "PowerShell 相關內容") 如需使用 PowerShell 建立 Reporting Services 服務應用程式的資訊，請參閱：  
  
-   請參閱下一節[步驟 1 到 4 的 Windows PowerShell 指令碼](#bkmk_full_script)。  
  
-   [使用 PowerShell 建立 Reporting Services 服務應用程式](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md)主題。  

##  <a name="step-4-activate-the-power-view-site-collection-feature"></a><a name="bkmk_powerview"></a> 步驟 4：啟動 Power View 的網站集合功能。

 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] (適用於 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint 產品的 SQL Server 2016 Reporting Services 增益集功能) 是網站集合功能。 將會針對根網站集合以及安裝 Reporting Services 增益集之後所建立的網站集合自動啟用此功能。 如果您打算使用 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]，請確認此功能是否已啟用。  
  
 如果您在安裝 SharePoint Server 之後安裝適用於 SharePoint 產品的 Reporting Services 增益集，只會針對根網站集合啟用報表伺服器整合功能和 Power View 整合功能。 如果是其他網站集合，請手動啟用這些功能。  
  
#### <a name="to-activate-or-verify-the-power-view-site-collection-feature"></a>啟用或確認 Power View 網站集合功能  
  
1.  下列步驟會假設您的 SharePoint 網站設定為適用於 SharePoint 2013 的 2013 **體驗版**。  
  
     開啟瀏覽器，移至所要的 SharePoint 網站。 例如， https://\<servername>/sites/bi  
  
2.  選取 [設定]![SharePoint 設定](/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 設定")。  
  
3.  選取 [網站設定]。  
  
4.  在 [網站集合管理] 群組中，選取 [網站集合功能]。  
  
5.  在清單中尋找 **[Power View 整合功能]** 。  
  
6.  選取 [啟用]。 功能狀態會變更為 **[使用中]** 。  
  
 每個網站集合都已完成這個程序。 如需詳細資訊，請參閱 [Activate the Report Server and Power View Integration Features in SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)。  
  
##  <a name="windows-powershell-script-for-steps-1-4"></a><a name="bkmk_full_script"></a> 步驟 1 到 4 的 Windows PowerShell 指令碼  
 本節中的 PowerShells 指令碼與上一節的完成步驟 1 到 4 相同。 此指令碼完成下列各項：  
  
-   安裝 Reporting Services 服務和服務 Proxy，以及啟動服務。  
  
-   建立名為 "Reporting Services" 的服務 Proxy。  
  
-   建立名為 "Reporting Services Application" 的 Reporting Services 服務應用程式。  
  
-   啟用網站集合的 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 功能。  
  
 參數  
  
-   更新服務 Proxy 的 **-Account** 。 帳戶必須是 SharePoint 伺服器陣列中受管理的服務帳戶。 如需詳細資訊，請參閱 SharePoint 主題＜ [規劃 SharePoint 2013 管理帳戶及服務帳戶](/SharePoint/security-for-sharepoint-server/plan-for-administrative-and-service-accounts)＞。  
  
-   更新服務應用程式的 **-DatabaseServer** 參數。 這個參數是 Database Engine 執行個體  
  
-   更新您想要啟用 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 功能之網站的 **-url** 參數。  
  
 **若要使用指令碼：**  
  
1.  使用系統管理權限來開啟 Windows PowerShell。  
  
2.  將下列程式碼複製到指令碼視窗。  
  
3.  更新上一節中描述的三個參數，然後執行指令碼。  
  
```  
#This script Configures SQL Server Reporting Services SharePoint mode  
  
$starttime=Get-Date  
write-host -foregroundcolor DarkGray StartTime>> $starttime   
  
Write-Host -ForegroundColor Green "Import the SharePoint PowerShell snappin"  
Add-PSSnapin Microsoft.Sharepoint.Powershell -EA 0  
  
Write-Host -ForegroundColor Green "Install SSRS Service and Service Proxy, and start the service"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
  
    Write-Host -ForegroundColor Green "Install the Reporting Services Shared Service"  
    Install-SPRSService  
  
    Write-Host -ForegroundColor Green " Install the Reporting Services Service Proxy"  
    Install-SPRSServiceProxy  
  
    # Get the ID of the RS Service Instance and start the service   
    Write-Host -ForegroundColor Green "Start the Reporting Services Service"  
    $RS = Get-SPServiceInstance | Where {$_.TypeName -eq "SQL Server Reporting Services Service"}  
    Start-SPServiceInstance -Identity $RS.Id.ToString()  
  
    # Wait for the Reporting Services Service to start...  
    $Status = Get-SPServiceInstance $RS.Id.ToString()  
    While ($Status.Status -ne "Online")  
    {  
        Write-Host -ForegroundColor Green "SSRS Service Not Online...Current Status = " $Status.Status  
        Start-Sleep -Seconds 2  
        $Status = Get-SPServiceInstance $RS.Id.ToString()  
    }  
  
$time=Get-Date  
write-host -foregroundcolor DarkGray StartTime>> $starttime   
write-host -foregroundcolor DarkGray $time  
  
Write-Host -ForegroundColor Green "Create a new application pool and Reporting Services service application"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Write-Host -ForegroundColor Green "Create a new application pool"  
#!!!! update "-Account" with an existing Managed Service Account  
New-SPServiceApplicationPool -Name "Reporting Services" -Account "<domain>\User name>"  
$appPool = Get-SPServiceApplicationPool "Reporting Services"  
  
Write-Host -ForegroundColor Green " Create the Reporting Services Service Application"  
#!!!! Update "-DatabaseServer", an instance of the SQL Server database engine   
$rsService = New-SPRSServiceApplication -Name "Reporting Services Application" -ApplicationPool $appPool -DatabaseName "Reporting_Services_Application" -DatabaseServer "<server name>"  
  
Write-Host -ForegroundColor Green "Create the Reporting Services Service Application Proxy"  
$rsServiceProxy = New-SPRSServiceApplicationProxy -Name "Reporting Services Application Proxy" -ServiceApplication $rsService  
  
Write-Host -ForegroundColor Green "Associate service application proxy to default web site and grant web applications rights to SSRS application pool"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"     
# Associate the Reporting Services Service Applicatoin Proxy to the default web site...  
Get-SPServiceApplicationProxyGroup -default | Add-SPServiceApplicationProxyGroupMember -Member $rsServiceProxy  
  
$time=Get-Date  
write-host -foregroundcolor DarkGray StartTime>> $starttime   
write-host -foregroundcolor DarkGray $time  
  
Write-Host -ForegroundColor Green "Enable the PowerView and reportserver site features"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
#!!!! update "-url"  of the site where you want the features enabled  
Enable-SPfeature -identity "powerview" -Url https://server/sites/bi  
Enable-SPfeature -identity "reportserver" -Url https://server/sites/bi  
  
####To Verify, you can run the following:  
#Get-SPRSServiceApplication  
#Get-SPServiceApplicationPool | where {$_.name -like "reporting*"}  
#Get-SPRSServiceApplicationProxy  
  
```  
  
##  <a name="additional-configuration"></a><a name="bkmk_additional_config"></a> 其他設定  
 本節描述多數 SharePoint 部署中重要的其他組態步驟。  
  
###  <a name="configure-excel-services-and-power-pivot"></a><a name="bkmk_configure_ECS"></a> 設定 Excel Services 和 Power Pivot  
 如果您想要在 SharePoint 中檢視 Excel 2016 或 Excel 2013 活頁簿中的 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] Power View 報表，就必須將 Excel Services 設定為使用 Power Pivot 模式中的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器。 
 
 對於 SharePoint 2016，必須設定 [Office Online Server](https://technet.microsoft.com/library/jj219456\(v=office.16\).aspx) ，才能使用 Excel Services。 如需詳細資訊，請參閱下列技術白皮書。
 
 - [在 SharePoint 2016 中部署 SQL Server 2016 PowerPivot 和 Power View](/analysis-services/instances/install-windows/deploying-sql-server-2016-powerpivot-and-power-view-in-sharepoint-2016)
 
 - [在多層式 SharePoint 2016 伺服器陣列中部署 SQL Server 2016 PowerPivot 和 Power View](/analysis-services/instances/install-windows/deploy-powerpivot-and-power-view-multi-tier-sharepoint-2016-farm)
 
 對於 SharePoint 2016，您需要建立和設定 Excel Services 應用程式。 如需詳細資訊，請參閱下列：  
  
-   [以 Power Pivot 模式安裝 Analysis Services](/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)中的＜針對 Analysis Services 整合設定 Excel Services＞一節。  
  
-   [管理 Excel Services 資料模型設定 (SharePoint Server 2013)](/SharePoint/administration/manage-excel-services-data-model-settings)。  

此外，Reporting Services 服務應用程式所使用的應用程式集區安全性帳戶必須是 Analysis Services 伺服器的系統管理員。
  
###  <a name="provision-subscriptions-and-alerts"></a><a name="bkmk_provision_agent"></a> 提供訂閱和警示  
 Reporting Services 訂閱和資料警示功能可能需要設定 SQL Server Agent 權限。 如果您看到錯誤訊息，指出需要 SQL Server Agent，且您已確認 SQL Server Agent 正在執行，則請更新權限。 您可以在成功建立服務應用程式頁面上，按一下 **[提供訂閱和警示]** 連結，以移至其他頁面並提供 SQL Server Agent。 如果您的部署跨電腦界限 (例如 SQL Server 資料庫執行個體位於其他電腦上)，則需要提供步驟。 如需詳細資訊，請參閱 [SSRS 服務應用程式的佈建訂閱及警示](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)。  
  
### <a name="configure-e-mail-for-ssrs-service-applications"></a>設定 SSRS 服務應用程式的電子郵件  
 Reporting Services 資料警示功能會以電子郵件訊息傳送警示。 若要傳送電子郵件，您可能需要設定 Reporting Services 服務應用程式，以及修改服務應用程式的電子郵件傳遞延伸模組。 如果您計劃針對 Reporting Services 訂閱功能使用電子郵件傳遞延伸模組，則需要電子郵件設定。 如需詳細資訊，請參閱[設定 Reporting Services 服務應用程式的電子郵件 &#40;SharePoint 2013 和 SharePoint 2016&#41;](./configure-e-mail-for-a-reporting-services-service-application.md)。 
  
### <a name="add-reporting-services-content-types-to-content-libraries"></a>將 Reporting Services 內容類型新增至內容庫  
 Reporting Services 提供預先定義的內容類型，可用來管理共用資料來源 (.rsds) 檔案和報表產生器的報表定義 (.rdl) 檔案。 將 [報表產生器報表] 和 [報表資料來源] 內容類型新增至文件庫會啟用 [新增] 命令，讓您能夠建立該類型的新文件。 如需詳細資訊，請參閱 [將 Reporting Services 內容類型加入至 SharePoint 文件庫](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)。  
  
### <a name="activate-the-report-server-file-sync-feature"></a>啟動報表伺服器檔案同步處理功能  
 如果使用者經常直接上傳已發行的報表項目至 SharePoint 文件庫， **[報表伺服器檔案同步處理]** 網站層級功能會很有協助。 檔案同步處理功能會更頻繁地同步處理報表伺服器目錄與文件庫中的項目。 如需詳細資訊，請參閱 [在 SharePoint 管理中心啟動報表伺服器檔案同步處理功能](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)。  
  
##  <a name="verify-the-installation"></a><a name="bkmk_verify_installation"></a> 驗證安裝  
 以下是驗證 Reporting Services SharePoint 模式部署的建議步驟和程序。  
  
-   請參閱驗證主題＜ [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)＞中的＜SharePoint＞一節。  
  
-   在 SharePoint 文件庫中，建立只包含一個文字方塊 (例如標題) 的基本 Reporting Services 報表。 此報表不包含任何資料來源或資料集。 目標是確認您可以開啟報表產生器、建立基本報表和預覽報表。  
  
     將報表儲存至文件庫，然後從文件庫中執行報表。 如需使用報表產生器建立報表的詳細資訊，請參閱 [啟動報表產生器 (報表產生器)](../report-builder/start-report-builder.md)。  
  
## <a name="next-steps"></a>後續步驟

[Reporting Services SharePoint 模式的 PowerShell Cmdlet](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)   
[升級和移轉 Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[SQL Server 2016 的版本及支援功能](../../sql-server/editions-and-components-of-sql-server-2016.md)   
[Reporting Services SharePoint 服務和服務應用程式](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)