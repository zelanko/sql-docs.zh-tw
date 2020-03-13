---
title: 安裝 SharePoint 2013 Reporting Services SharePoint 模式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: b29d0f45-0068-4c84-bd7e-5b8a9cd1b538
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 8874d4c57e2fb7b94e4efac44c90e93865d2b40f
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79289616"
---
# <a name="install-reporting-services-sharepoint-mode-for-sharepoint-2013"></a>安裝適用於 SharePoint 2013 的 Reporting Services SharePoint 模式
  本主題中的程序會引導您完成 SharePoint 模式之 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的單一伺服器安裝。 這些步驟包含執行 [SQL Server 安裝精靈]，以及使用 SharePoint 管理中心的設定工作。 本主題也可以用於更新現有安裝的個別程序，例如建立 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Sharepoint 2013 &#124;**注意：** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sharepoint 模式不**支援 sharepoint** Server 多重租用。|  
  
 如需有關將其他 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 伺服器加入至現有伺服器陣列的詳細資訊，請參閱下列主題：  
  
-   [將其他報表伺服器加入至伺服器陣列 &#40;SSRS 相應放大&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md)  
  
-   [將其他 Reporting Services Web 前端加入至伺服器陣列](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)  
  
 單一伺服器安裝對開發和測試案例很實用，但是不建議在實際執行環境中使用。  
  
 **本主題內容：**  
  
-   [單一伺服器部署範例](#bkmk_singleserver)  
  
-   [安裝程式帳戶](#bkmk_setupaccounts)  
  
-   [步驟1：在 SharePoint 模式中安裝 Reporting Services 報表伺服器](#bkmk_install_SSRS)  
  
-   [步驟2：註冊並啟動 Reporting Services SharePoint 服務](#bkmk_install_SSRS_sharedservice)  
  
-   [步驟3：建立 Reporting Services 服務應用程式](#bkmk_create_serrviceapplication)  
  
-   [步驟4：啟動 Power View 網站集合功能。](#bkmk_powerview)  
  
-   [適用于步驟1-4 的 Windows PowerShell 腳本](#bkmk_full_script)  
  
-   [額外](#bkmk_additional_config)的設定，包括布建訂閱和[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]警示、內容類型，以及將 Excel Services 設定為使用 Analysis Services 伺服器。  
  
-   [驗證安裝](#bkmk_verify_installation)  
  
##  <a name="bkmk_singleserver"></a>單一伺服器部署範例  
 單一伺服器安裝對開發和測試案例很實用，但是不建議在實際執行環境中使用單一伺服器。 單一伺服器環境是指在同一部電腦上安裝 SharePoint 和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 元件的單一電腦。 本主題並未涵蓋具有多部 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 伺服器的向外延展。  
  
 下圖說明單一伺服器 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 部署之一部分的元件。  
  
|||  
|-|-|  
|**sha-1**|從 SQL Server 安裝所安裝的 SharePoint 服務。 您可以建立一個或多個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。|  
|**2**|
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 適用於 SharePoint 產品的增益集會在 SharePoint 伺服器上提供使用者介面元件。|  
|**第**|由 Power View 和 PowerPivot 所使用的 Excel 服務應用程式。|  
|**4gb**|PowerPivot 服務應用程式。|  
  
 ![SSRS SharePoint 模式單一伺服器部署](../../../2014/sql-server/install/media/rs-sharepoint-1server-deployment.gif "SSRS SharePoint 模式單一伺服器部署")  
  
> [!TIP]  
>  如需更多複雜的部署範例，請參閱 [SharePoint 中 SQL Server BI 功能的部署拓撲](deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)。  
  
##  <a name="bkmk_setupaccounts"></a>安裝程式帳戶  
 本節將描述用於 SharePoint 模式之 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 主要部署步驟的帳戶和權限。  
  
 **安裝和註冊[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服務：**  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]在 SharePoint 模式下，安裝期間的目前帳戶（稱為「安裝程式」帳戶）必須具有本機電腦的系統管理許可權。 如果您是在[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]安裝 sharepoint 之後安裝，而且「安裝程式」帳戶也是 sharepoint 伺服器陣列系統管理員群組的成員， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]則安裝將會[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]為您註冊服務。 如果您在[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]安裝 SharePoint 之前安裝，或者「安裝程式」帳戶不是伺服器陣列管理員群組的成員，您就必須手動註冊服務。 請參閱＜ [步驟 2：註冊並啟動 Reporting Services SharePoint 服務](#bkmk_install_SSRS_sharedservice)。  
  
 **建立[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服務應用程式**  
  
-   安裝並註冊 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務之後，請建立一個或多個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。 「SharePoint 伺服器陣列服務帳戶」需要暫時成為本機 Administrators 群組的成員，才能建立 Reporting Services 服務應用程式。 如需 SharePoint 2013 帳戶許可權的詳細資訊，請參閱[sharepoint 2013 中的帳戶許可權及安全性設定](https://technet.microsoft.com/library/cc678863.aspx)（https://technet.microsoft.com/library/cc678863.aspx)。  
  
     安全性最佳作法是避免讓 SharePoint 伺服陣列管理員帳戶同時成為本機作業系統管理員帳戶。 如果您在安裝程序中，將伺服陣列管理員帳戶加入至本機 Administrators 群組，建議您在安裝完成之後，從本機 Administrators 群組中移除該帳戶。  
  
##  <a name="bkmk_install_SSRS"></a>步驟1：在 SharePoint 模式中安裝 Reporting Services 報表伺服器  
 這個步驟會在 SharePoint 模式下安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器以及適用於 SharePoint 產品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集。 根據電腦上已經安裝的元件而定，您可能不會看見下列步驟所描述的部分安裝頁面。  
  
1.  執行 [SQL Server 安裝精靈] \(Setup.exe)。  
  
2.  在精靈的左側按一下 **[安裝]** ，然後按一下 **[新增 SQL Server 獨立安裝或將功能加入至現有安裝]**。  
  
3.  在 **[安裝程式支援規則]** 頁面上按一下 **[確定]** (假設已通過所有規則)。  
  
4.  在 **[安裝程式支援檔案]** 頁面中按一下 **[安裝]** 。 根據電腦上已經安裝的元件而定，您可能會看見下列訊息：  
  
    -   「一個或多個受影響的檔案有暫止的作業。 您必須在安裝程序完成之後重新啟動電腦。」  
  
    -   按一下 [確定]****。  
  
5.  在支援檔案完成安裝而且 **[支援規則]** 頁面顯示 **[通過]** 狀態之後，請按 **[下一步]**。 檢閱任何警告或封鎖問題。  
  
6.  在 **[安裝類型]** 頁面上，按一下 **[將功能加入到現有的 SQL Server 2014 執行個體]**。 在下拉式清單中選取正確的執行個體，然後按 **[下一步]**。  
  
7.  如果您看見 [產品金鑰]**** 頁面，請輸入您的金鑰或接受 "Enterprise Evaluation" 版本的預設值。  
  
     按 [下一步]  。  
  
8.  如果您看見 [授權條款] 頁面，請檢閱並接受這些授權條款。 Microsoft 感謝您同意傳送功能使用資料，協助改進產品功能及支援。  
  
     按 [下一步]  。  
  
9. 如果您看見 **[安裝程式角色]** 頁面，請選取 **[SQL Server 功能安裝]**  
  
     按 [下一步]****  
  
     ![適用於安裝程式角色的 SQL Server 功能安裝](../../../2014/sql-server/install/media/rs-setuprole.gif "適用於安裝程式角色的 SQL Server 功能安裝")  
  
10. 在 **[特徵選取]** 頁面上，選取下列選項：  
  
    -   **Reporting Services-SharePoint**  
  
    -   **適用于 SharePoint 產品的 Reporting Services 增益集**。  
  
         ![注意](../../../2014/reporting-services/media/rs-fyinote.png "注意")安裝增益集的 [安裝精靈] 選項是[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]版本的新功能。  
  
    -   如果您尚未有 SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體，您也可以針對完整的環境選取 **[Database Engine Services]** 和 **[管理工具 - 完整]** 。  
  
     按 [下一步]  。  
  
     ![適用于 SharePoint 模式的 SSRS 功能選取](../../../2014/sql-server/install/media/rs-setupfeatureselection-sharepoint-with-circles.gif "適用于 SharePoint 模式的 SSRS 功能選取")  
  
11. 如果您看見 **[安裝規則]** 頁面， 檢閱任何警告或封鎖問題。 然後按 **[下一步]**  
  
12. 如果您選取 Database Engine 服務，請接受 **[執行個體組態]** 頁面上的預設 **[MSSQLSERVER]** 執行個體，然後按 **[下一步]**。  
  
     ![注意](../../../2014/reporting-services/media/rs-fyinote.png "注意")Reporting Services SharePoint 服務架構不是以 SQL Server 「實例」為基礎，如同先前的 Reporting Services 架構。  
  
13. 檢閱 **[磁碟空間需求]** 頁面，然後按 **[下一步]**。  
  
14. 如果您看見 **[伺服器組態]** 頁面，請輸入適當的認證。 如果您想要使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料警示或訂閱功能，則必須將 SQL Server Agent 的 **[啟動類型]** 變更為 **[自動]**。 根據電腦上已經安裝的元件而定，您可能不會看見 **[伺服器組態]** 頁面。  
  
     按 [下一步]  。  
  
15. 如果您選取了 Database Engine 服務，就會看到 **[資料庫引擎組態]** 頁面。請將適當的帳戶加入至 SQL 管理員清單，然後按 **[下一步]**。  
  
16. 在 **[Reporting Services 組態]** 頁面上，您應該會看到已選取 **[只安裝]** 選項。 這個選項會安裝報表伺服器檔案，但是不會設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的 SharePoint 環境。  
  
    > [!NOTE]  
    >  當 SQL Server 安裝完成時，請遵循本主題其他章節來設定 SharePoint 環境。 包括安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共用服務及建立 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式。  
  
     ![SQL Server 安裝精靈 - SSRS 組態頁面](../../../2014/sql-server/install/media/rs-2012sp1-setup-ssrs-configpage-with-circles.gif "SQL Server 安裝精靈 - SSRS 組態頁面")  
  
17. 按一下 **[錯誤報告]** 頁面上的核取方塊傳送錯誤報告，協助 Microsoft 改進 SQL Server 功能與服務。  
  
     按 [下一步]  。  
  
18. 檢閱任何警告，然後在 **[安裝組態規則]** 頁面上按 **[下一步]** 。  
  
19. 在 **[準備安裝]** 頁面上檢閱安裝摘要，然後按 **[下一步]**。 此摘要將包括其值顯示為 **[SharePointFilesOnlyMode]** 的 **[Reporting Services SharePoint 模式]** 子節點。 按一下 **[安裝]**。  
  
20. 安裝需要幾分鐘的時間。 您將會看見 **[完成]** 頁面，其中列出功能以及每項功能的狀態。 您可能會看見資訊對話方塊，指出電腦需要重新啟動。  
  
##  <a name="bkmk_install_SSRS_sharedservice"></a>步驟2：註冊並啟動 Reporting Services SharePoint 服務  
 ![PowerShell 相關內容](../../../2014/reporting-services/media/rs-powershellicon.jpg "PowerShell 相關內容")  
  
> [!NOTE]  
>  如果您要在現有的 SharePoint 伺服器陣列中進行安裝，則不需要完成本節中的步驟。 當您在本文件的上一節執行 SQL Server 安裝精靈時，就會安裝並啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 服務。  
  
 您需要手動註冊 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務的常見原因如下。  
  
-   您在安裝 SharePoint 之前已安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。  
  
-   此用來安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式的帳戶，不是 SharePoint 伺服器陣列管理員群組的成員。 如需詳細資訊，請參閱＜ [Setup accounts](#bkmk_setupaccounts)＞一節。  
  
 必要檔案會隨 [SQL Server 安裝精靈] 安裝，但是您必須在 SharePoint 伺服器陣列中註冊服務。 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本引進了適用於 SharePoint 模式中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的 PowerShell 支援。  
  
 下列步驟將引導您開啟 SharePoint 管理命令介面並執行指令程式：  
  
1.  按一下 [**開始**] 按鈕  
  
2.  按一下 **[Microsoft SharePoint 2013 產品]** 群組。  
  
3.  以滑鼠右鍵按一下 **[SharePoint 2013 管理命令介面]** ，然後按一下 **[以系統管理員身分執行]**。 注意：標準 Windows PowerShell 視窗無法辨識 SharePoint 命令。 請使用 **[SharePoint 2013 管理命令介面]**。  
  
4.  執行下列 PowerShell 命令安裝 SharePoint 服務。 成功完成命令會在管理命令介面中顯示新行。 當命令成功完成時，**不會將任何訊息傳回**管理命令介面：  
  
    ```powershell
    Install-SPRSService  
    ```  
  
    > [!IMPORTANT]  
    >  如果您看到類似下列的錯誤訊息：  
    >   
    >  安裝-Install-sprsserviceinstall-sprsservice： ' Install-Install-sprsserviceinstall-sprsservice ' 一詞**無法**辨識為  
    > Cmdlet、函數、指令檔或可執行程式的名稱。 請參閱  
    > 名稱拼字是否正確，如果包含路徑的話，請確認路徑是否  
    > 正確，然後再試一次。  
  
5.  執行下列 PowerShell 命令以安裝服務 Proxy。 成功完成命令會在管理命令介面中顯示新行。 當命令成功完成時，**不會將任何訊息傳回**管理命令介面：  
  
    ```powershell
    Install-SPRSServiceProxy  
    ```  
  
6.  執行下列 PowerShell 命令以啟動服務，或參閱下列附註，以取得有關如何從 SharePoint 管理中心啟動服務的指示：  
  
    ```powershell
    Get-SPServiceInstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
    ```  
  
 您使用的可能是 Windows Powershell 而非 SharePoint 管理命令介面，或者未安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式。 如需 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 PowerShell 的詳細資訊，請參閱 [Reporting Services SharePoint 模式的 PowerShell Cmdlet](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)。  
  
 您也可以從 SharePoint 管理中心啟動服務，而不是執行第三個 PowerShell 命令。 下列步驟也可用於確認服務是否執行。  
  
1.  在 SharePoint 管理中心內，按一下 **[系統設定]** 群組中的 **[管理伺服器上的服務]** 。  
  
2.  找到 **[SQL Server Reporting Services 服務]** ，然後按一下 [動作] 欄中的 **[啟動]** 。  
  
3.  Reporting Services 服務的狀態會從 **[已停止]** 變更為 **[已啟動]**。 如果清單中沒有 Reporting Services 服務，請使用 PowerShell 安裝該服務。  
  
    > [!NOTE]  
    >  如果 Reporting Services 服務停留在 [啟動中]**** 狀態，而未變更為 [已啟動]****，請確認已在 Windows 伺服器管理員中啟動 'SharePoint 2013 Administration' 服務。  
  
##  <a name="bkmk_create_serrviceapplication"></a>步驟3：建立 Reporting Services 服務應用程式  
 本節提供建立服務應用程式的步驟，以及屬性的描述 (如果您要檢閱現有的服務應用程式)。  
  
1.  在 [SharePoint 管理中心] 的 [**應用程式管理**] 群組中，按一下 [**管理服務應用程式**]。  
  
2.  在 SharePoint 功能區中，按一下 **[新增]** 按鈕。  
  
3.  在 [新增] 功能表中，按一下 **[SQL Server Reporting Services 服務應用程式]**。  
  
    > [!IMPORTANT]  
    >  如果此[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]選項未出現在清單中，表示**未安裝[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]共用服務**。 檢閱上一節中，如何使用 PowerShell Cmdlt 來安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務的相關資訊。  
  
4.  在 **[建立新的 SQL Server Reporting Services 服務應用程式]** 頁面中，輸入應用程式的名稱。 如果您要建立多個 Reporting Services 服務應用程式，描述性名稱和命名慣例將有助於您組織管理作業。  
  
5.  在 **[應用程式集區]** 區段中，建立應用程式的新應用程式集區 (建議)。 如果您針對應用程式集區和服務應用程式使用相同的名稱，可讓進行中的管理更容易。 這可能也會受到您將建立的服務應用程式數目以及是否需要在單一應用程式集區中使用許多應用程式所影響。 請參閱 SharePoint Server 文件集以取得應用程式集區管理的建議事項和最佳作法。  
  
     針對應用程式集區選取或建立安全性帳戶。 請務必指定網域使用者帳戶。 網域使用者帳戶會啟用 SharePoint 受管理帳戶功能，好讓您在一個地方更新密碼和帳戶資訊。 如果您計劃將部署向外延展，以包括在相同識別下執行的其他服務執行個體，也需要網域帳戶。  
  
6.  在 **[資料庫伺服器]** 中，您可以使用目前的伺服器或選擇不同的 SQL Server。  
  
7.  在 **[資料庫名稱]** 中，預設值是 `ReportingService_<guid>`，這是唯一的資料庫名稱。 若您要輸入新值，請輸入唯一值。 這是專門針對服務應用程式所建立的新資料庫。  
  
8.  在 **[資料庫驗證]** 中，預設值是 Windows 驗證。 如果您選擇 **[SQL 驗證]**，請參考 SharePoint 文件，以了解在 SharePoint 部署中使用這個驗證類型的最佳作法。  
  
9. 在 **[Web 應用程式關聯]** 區段中，選取要佈建以供目前 Reporting Services 服務應用程式存取的 Web 應用程式。 您可以建立一個 Reporting Services 服務應用程式與一個 Web 應用程式的關聯。 如果目前所有的 Web 應用程式已有相關聯的 Reporting Services 服務應用程式，則會顯示警告訊息。  
  
10. 按一下 [確定]  。  
  
11. 服務應用程式的建立程序會需要數分鐘才能完成。 完成後，您會看到確認訊息及 **[提供訂閱和警示]** 頁面的連結。 如果您想要使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱功能或資料警示功能，請完成提供步驟。 如需詳細資訊，請參閱 [SSRS 服務應用程式的佈建訂用帳戶及警示](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)。  
  
 ![PowerShell 相關內容](../../../2014/reporting-services/media/rs-powershellicon.jpg "PowerShell 相關內容")如需使用 PowerShell 建立[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]服務應用程式的相關資訊，請參閱：  
  
-   請參閱下一節[步驟 1 到 4 的 Windows PowerShell 指令碼](#bkmk_full_script)。  
  
-   
  [使用 PowerShell 建立 Reporting Services 服務應用程式](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md#bkmk_powershell_create_ssrs_serviceapp)主題。  
  
##  <a name="bkmk_powerview"></a>步驟4：啟動 Power View 網站集合功能。  
 
  [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] (適用於 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SharePoint 產品之 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] 增益集的功能) 是網站集合功能。 將會針對根網站集合以及安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集之後所建立的網站集合自動啟用此功能。 如果您打算使用 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]，請確認此功能是否已啟用。  
  
 如果您在安裝 SharePoint Server 之後安裝適用於 SharePoint 產品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集，只會針對根網站集合啟用報表伺服器整合功能和 Power View 整合功能。 如果是其他網站集合，請手動啟用這些功能。  
  
#### <a name="to-activate-or-verify-the-power-view-site-collection-feature"></a>若要啟動或確認 Power View 網站集合功能  
  
1.  下列步驟會假設您的 SharePoint 網站設定為 2013 **體驗版**。  
  
     開啟瀏覽器，移至所要的 SharePoint 網站。 例如，http://\<伺服器名稱>/sites/bi  
  
2.  按一下 [**設定**] [![SharePoint 設定](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint 設定")]。  
  
3.  按一下 [**網站設定**]。  
  
4.  在 **[網站集合管理]** 群組中，按一下 **[網站集合功能]**。  
  
5.  在清單中尋找 **[Power View 整合功能]** 。  
  
6.  按一下 [啟用]  。 功能狀態會變更為 **[使用中]**。  
  
 每個網站集合都已完成這個程序。 如需詳細資訊，請參閱 [Activate the Report Server and Power View Integration Features in SharePoint](../../../2014/reporting-services/activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)。  
  
##  <a name="bkmk_full_script"></a>適用于步驟1-4 的 Windows PowerShell 腳本  
 本節中的 PowerShells 指令碼與上一節的完成步驟 1 到 4 相同。 此指令碼完成下列各項：  
  
-   安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務和服務 Proxy，以及啟動服務。  
  
-   建立名為 "Reporting Services" 的服務 Proxy。  
  
-   建立名[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]為 "Reporting Services application" 的服務應用程式。  
  
-   啟用網站集合的 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 功能。  
  
 參數  
  
-   更新服務 Proxy 的 **-Account** 。 帳戶必須是 SharePoint 伺服器陣列中受管理的服務帳戶。 如需詳細資訊，請參閱 SharePoint 主題＜ [規劃 SharePoint 2013 管理帳戶及服務帳戶](https://technet.microsoft.com/library/cc263445.aspx)＞。  
  
-   更新服務應用程式的 **-DatabaseServer** 參數。 這個參數是 Database Engine 執行個體  
  
-   更新您想要啟用 ** 功能之網站的 **-url[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 參數。  
  
 **若要使用腳本：**  
  
1.  使用系統管理權限來開啟 Windows PowerShell。  
  
2.  將下列程式碼複製到指令碼視窗。  
  
3.  更新上一節中描述的三個參數，然後執行指令碼。  
  
```powershell
#This script Configures SQL Server Reporting Services SharePoint mode  
  
$starttime = Get-Date  
Write-Host -foregroundcolor DarkGray StartTime>> $starttime   
  
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
  
$time = Get-Date  
Write-Host -foregroundcolor DarkGray StartTime>> $starttime   
Write-Host -foregroundcolor DarkGray $time  
  
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
Write-Host -foregroundcolor DarkGray StartTime>> $starttime   
Write-Host -foregroundcolor DarkGray $time  
  
Write-Host -ForegroundColor Green "Enable the PowerView and reportserver site features"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
#!!!! update "-url"  of the site where you want the features enabled  
Enable-SPfeature -identity "powerview" -Url http://server/sites/bi  
Enable-SPfeature -identity "reportserver" -Url http://server/sites/bi  
  
####To Verify, you can run the following:  
#Get-SPRSServiceApplication  
#Get-SPServiceApplicationPool | where {$_.name -like "reporting*"}  
#Get-SPRSServiceApplicationProxy
```  
  
##  <a name="bkmk_additional_config"></a>其他設定  
 本節描述多數 SharePoint 部署中重要的其他組態步驟。  
  
###  <a name="bkmk_configure_ECS"></a>設定 Excel Services 和 PowerPivot  
 如果您想要在 SharePoint 中檢視 Excel 2013 活頁簿中的 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] Power View 報表，就必須將伺服器陣列上的 Excel Services 應用程式設定為使用 SharePoint 模式中的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器。 此外， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式所使用的應用程式集區安全性帳戶必須是 Analysis Services 伺服器的系統管理員。 如需詳細資訊，請參閱下列：  
  
-   [PowerPivot for SharePoint 2013 安裝](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)中的「設定適用于 Analysis Services 整合的 Excel Services」一節。  
  
-   [管理 Excel Services 資料模型設定（SharePoint Server 2013）](https://technet.microsoft.com/library/jj219780.aspx)。  
  
###  <a name="bkmk_provision_agent"></a>布建訂閱和警示  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱和資料警示可能需要 SQL Server Agent 權限組態。 如果您看到錯誤訊息，指出需要 SQL Server Agent，且您已確認 SQL Server Agent 正在執行，則請更新權限。 您可以在成功建立服務應用程式頁面上，按一下 **[提供訂閱和警示]** 連結，以移至其他頁面並提供 SQL Server Agent。 如果您的部署跨電腦界限 (例如 SQL Server 資料庫執行個體位於其他電腦上)，則需要提供步驟。 如需詳細資訊，請參閱[SSRS 服務應用程式的布建訂閱和警示](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)  
  
### <a name="configure-e-mail-for-ssrs-service-applications"></a>設定 SSRS 服務應用程式的電子郵件  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料警示功能會以電子郵件訊息傳送警示。 若要傳送電子郵件，您可能需要設定 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服務應用程式，以及修改服務應用程式的電子郵件傳遞延伸模組。 如果您計劃針對 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 訂閱功能使用電子郵件傳遞延伸模組，則需要電子郵件設定。 如需詳細資訊，請參閱[設定 Reporting Services 服務應用程式的電子郵件 &#40;SharePoint 2010 和 SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)。  
  
### <a name="add-reporting-services-content-types-to-content-libraries"></a>將 Reporting Services 內容類型加入至內容庫  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會提供預先定義的內容類型，可用來管理共用資料來源 (.rsds) 檔、報表模型 (.smdl) 檔，以及報表產生器的報表定義 (.rdl) 檔。 將 **[報表產生器報表]**、 **[報表模型]** 和 **[報表資料來源]** 內容類型加入至文件庫會啟用 **[新增]** 命令，讓您能夠建立該類型的新文件。 如需詳細資訊，請參閱[將報表伺服器內容類型加入至程式庫 &#40;SharePoint 整合模式中的 Reporting Services&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)。  
  
### <a name="activate-the-report-server-file-sync-feature"></a>啟動報表伺服器檔案同步處理功能  
 如果使用者經常直接上傳已發行的報表項目至 SharePoint 文件庫， **[報表伺服器檔案同步處理]** 網站層級功能會很有協助。 檔案同步處理功能會更頻繁地同步處理報表伺服器目錄與文件庫中的項目。 如需詳細資訊，請參閱 [在 SharePoint 管理中心啟動報表伺服器檔案同步處理功能](../../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)。  
  
##  <a name="bkmk_verify_installation"></a>確認安裝  
 以下是驗證 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式部署的建議步驟和程序。  
  
-   請參閱驗證主題＜ [Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)＞中的＜SharePoint＞一節。  
  
-   在 SharePoint 文件庫中，建立只包含一個文字方塊 (例如標題) 的基本 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表。 此報表不包含任何資料來源或資料集。 目標是確認您可以開啟報表產生器、建立基本報表和預覽報表。  
  
     將報表儲存至文件庫，然後從文件庫中執行報表。 如需使用報表產生器建立報表的詳細資訊，請參閱 [啟動報表產生器 (報表產生器)](https://technet.microsoft.com/library/ms159221.aspx)。  
  
## <a name="see-also"></a>另請參閱  
 [適用于 Reporting Services SharePoint 模式的 PowerShell Cmdlet](../../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)   
 [升級和移轉 Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
 [內容藍圖：安裝及設定 SharePoint Server 和 SQL Server BI](https://technet.microsoft.com/library/dn205112.aspx)   
 [SQL Server 2012 版本所支援的功能](https://go.microsoft.com/fwlink/?linkid=232473)   
 [Reporting Services SharePoint 服務和服務應用程式](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md)
