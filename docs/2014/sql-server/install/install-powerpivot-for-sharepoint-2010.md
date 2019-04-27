---
title: 安裝 PowerPivot for SharePoint 2010 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: eec38696-5e26-46fa-bc83-aa776f470ce8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e02b80c1967059f91e3a97fb940a2715c6beebb8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62656742"
---
# <a name="install-powerpivot-for-sharepoint-2010"></a>安裝 PowerPivot for SharePoint 2010
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 是中間層級後端服務的集合，可以在 SharePoint 2010 伺服器陣列中提供 PowerPivot 資料存取功能。 如果您的組織使用用戶端應用程式 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 2010 來建立包含分析資料的活頁簿，您必須要有 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]，才能在伺服器環境中存取該資料。 本主題會逐步引導您完成基本安裝程序，而且提供了其他主題的連結，可協助您設定 PowerPivot。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010|  
  
 
  
 如需有關如何安裝指示[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]並[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]在相同伺服器上，請參閱[部署檢查清單：Reporting Services、 Power View 及 PowerPivot for SharePoint](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md)。  
  
## <a name="prerequisites"></a>先決條件  
  
1.  您必須是本機系統管理員，才能執行 SQL Server 安裝程式。  
  
2.  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 需要 SharePoint Server 2010 Enterprise 版。 您也可以使用 Evaluation Enterprise 版。  
  
3.  您必須安裝 SharePoint Server 2010 SP2。 若未安裝，則無法設定伺服器陣列使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 功能。  
  
4.  電腦必須加入網域。  
  
5.  您必須要有網域使用者帳戶，才能佈建 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 在 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安裝中，Analysis Services 服務帳戶必須是可以從管理中心進行管理的網域使用者帳戶。 您將會在輸入的帳戶和認證**伺服器組態**頁面歸屬於這份文件中的步驟。  
  
6.  必須要有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 執行個體名稱。 在您要安裝 PowerPivot for SharePoint 的電腦上，不能有現存的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 具名執行個體。  
  
7.  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 執行個體不得為 SQL Server 容錯移轉叢集的一部分。 使用 SharePoint 產品的高可用性功能。 例如，Excel Services 會管理 PowerPivot for SharePoint 伺服器的負載平衡。 如需詳細資訊，請參閱 <<c0> [ 管理 Excel Services 資料模型設定 (SharePoint Server 2013)](https://technet.microsoft.com/library/jj219780.aspx) (https://technet.microsoft.com/library/jj219780.aspx)。  
  
8.  如果您要在現存的伺服器陣列上安裝 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]，必須要有一個或多個為傳統模式驗證所設定的 SharePoint Web 應用程式。 Web 應用程式必須支援傳統模式驗證，[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料存取才能運作。 如需有關傳統模式需求的詳細資訊，請參閱 < [PowerPivot 驗證及授權](../../analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization.md)。  
  
9. 請檢閱下列其他主題，以了解系統與版本需求：  
  
    -   [在 SharePoint 2010 伺服器陣列中使用 SQL Server BI 功能的指引](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
##  <a name="InstallSQL"></a> 步驟 1：安裝 PowerPivot for SharePoint  
 在此步驟中，您要執行 SQL Server 安裝程式來安裝 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]。 在後續步驟中，您會將伺服器設定為安裝後工作。  
  
1.  插入安裝媒體或是開啟包含 SQL Server 安裝程式檔案的資料夾，然後按兩下**setup.exe**。  
  
2.  按一下 **安裝**左側的導覽窗格中。  
  
3.  按一下 **[新增 SQL Server 獨立安裝或將功能加入至現有安裝]**。  
  
4.  在 **產品金鑰**頁面上，指定 evaluation edition 或是輸入 enterprise edition 授權複本的產品金鑰。  
  
     按一下 [下一步] 。  
  
5.  接受 Microsoft 軟體授權合約的條款，而且如果您一併開啟客戶經驗和錯誤報告，我們會非常感激。 按一下 [下一步] 。  
  
6.  如果系統提示您如此做，請更新安裝程式檔。  
  
7.  在 [**安裝的規則**] 頁面上，安裝程式會識別可能導致無法安裝的任何問題。 檢閱清單以判斷安裝程式是否已偵測到系統上的潛在問題。  
  
    > [!NOTE]  
    >  由於已啟用 Windows 防火牆，因此系統會警告您開放通訊埠才可啟用遠端存取。 這個警告通常不適用於 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 安裝。 與 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 服務及資料檔案之間的連接，是使用已針對 SharePoint 服務對服務通訊所開啟的 SharePoint 連接埠來建立。  
  
     按一下 [下一步] 。 正在伺服器上安裝 SQL Server 安裝程式檔案，請稍候。  
  
8.  在 **[安裝程式角色]** 頁面上，選取 **[SQL Server PowerPivot for SharePoint]**。  
  
9. 您可選擇性地在安裝中加入一項 Database Engine 的執行個體。 如果您要設定新的伺服器陣列，且需要資料庫伺服器以執行伺服器陣列的組態和內容資料庫，您可能會這麼做。 若您加入 Database Engine，將會安裝為 PowerPivot 具名執行個體。 每當您需要指定 （例如，在伺服器陣列組態精靈 如果您要使用該精靈設定伺服器陣列)，這個執行個體的連接輸入資料庫名稱，格式如下： <`servername`> \PowerPivot。  
  
     ![GMNI_SetupUI_FeatureRole](../../../2014/sql-server/install/media/gmni-setupui-featurerole.gif "GMNI_SetupUI_FeatureRole")  
  
10. 按一下 [下一步] 。  
  
11. 在 [**特徵選取**] 頁面上，將安裝之特徵的唯讀清單會顯示僅供參考之用。 您不能加入或移除預先為這個角色選取的項目。 按一下 [下一步] 。  
  
12. 在 [**功能規則**頁面上，按一下**下一步]**。 您可以略過此頁面。  
  
13. 在 **[執行個體組態]** 頁面上，顯示 'PowerPivot' 的唯讀執行個體名稱是為了給使用者參考。 這個執行個體名稱**POWERPIVOT**是**所需，而且無法修改**。 但是，您可以輸入唯一的執行個體識別碼來指定描述性目錄名稱和登錄機碼。 按一下 [下一步] 。  
  
14. 在 **伺服器組態**頁面上，輸入所需的帳戶資訊。  
  
     若是 SQL Server Analysis Services，您必須指定網域使用者帳戶。 請不要指定內建帳戶。 網域帳戶所需的管理 Analysis Services 服務帳戶當做*受管理帳戶*在 SharePoint 管理中心內。  
  
     ![SSAS Server 組態](../../../2014/sql-server/install/media/ssas-powerpivotsetupsql2012sp1-serverconfiguration.gif "SSAS Server 組態")  
  
     若已新增 SQL Server Database Engine 與 SQL Server Agent，您可以將服務設定為利用網域使用者帳戶或預設虛擬帳戶加以執行。  
  
     絕不要使用您自己的網域使用者帳戶提供任何服務。 這麼做會授與伺服器您對網路中的資源所擁有的相同權限。 如果伺服器遭到惡意使用者的危害，該使用者將會以您的網域認證登入，而且能夠下載或使用您可以下載或使用的相同資料與應用程式。  
  
15. 按一下 [下一步] 。  
  
16. 若您正安裝 Database Engine，則隨即會出現 Database Engine 組態頁面。 在資料庫引擎組態 中，按一下**加入目前使用者**Database Engine 執行個體的帳戶系統管理員權限授與您的使用者。 按一下 **新增**新增其他帳戶。 按一下 [下一步] 。  
  
17. 在 **[Analysis Services 組態]** 頁面上，按一下 **[加入目前使用者]** ，為您的使用者帳戶授與管理權限。 在完成安裝程式之後，您將會需要管理權限來設定伺服器。  
  
18. 在相同的頁面上，加入也需要管理權限之任何人的 Windows 使用者帳戶。 例如，想要在 SQL Server Management Studio 中連接至 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]執行個體以疑難排解資料庫連接問題或取得版本資訊的所有使用者，都必須擁有該伺服器的系統管理權限。 請加入可能需要立即針對伺服器進行疑難排解或管理之任何人的使用者帳戶。  
  
19. 按一下 [下一步] 。  
  
20. 按一下 [**下一步]** 在每個其餘的頁面，直到您到達 [準備安裝] 頁面上。  
  
21. 按一下 **[安裝]**。  
  
> [!TIP]  
>  如果您需要 SQL Server 安裝，請參閱[檢視與讀取 SQL Server Setup Log Files&lt](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)。  
  
##  <a name="bkmk_config"></a> 步驟 2：設定伺服器  
  
> [!IMPORTANT]  
>  您必須先安裝 SharePoint 2010 SP2，才能設定 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 或是使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 資料庫伺服器的 SharePoint 伺服器陣列。 如果您尚未安裝該 Service Pack，請在開始設定伺服器之前先加以安裝。  
  
 在設定好伺服器之前，安裝作業不會完成。 在此版本中，一律會執行伺服器設定為後續安裝工作，使用下列方式之一：[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 組態工具、 管理中心或 PowerShell。 若要繼續，請選擇下列其中一種方式進行：  
  
-   [設定或修復 PowerPivot for SharePoint 2010 &#40;PowerPivot 組態工具&#41;](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md)  
  
-   [管理中心的 PowerPivot 伺服器管理和設定](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
-   [使用 Windows PowerShell 的 PowerPivot 設定](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
 **連接到 Database Engine 執行個體。** 當您安裝 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 時，SQL Server 安裝程式會提供您將 Database Engine 執行個體加入安裝中的選項。 您可能已經加入 Database Engine 執行個體到您的安裝，如果您要設定新的伺服器陣列，且需要資料庫伺服器以執行伺服器陣列的組態和內容資料庫。 如果您已加入 Database Engine，其會安裝為 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 具名執行個體。 每當您需要指定 （例如，在伺服器陣列組態精靈 如果您要使用該精靈設定伺服器陣列)，這個執行個體的連接，請記得以此格式輸入資料庫名稱： <`servername`> \PowerPivot。  
  
##  <a name="bkmk_redist"></a> 步驟 3：Excel Services 應用程式伺服器上安裝 Analysis Services OLE DB 提供者  
 如果您在個別的應用程式伺服器上執行 Excel Calculation Services 和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]，則需要額外的安裝步驟。 在執行 Excel Calculation Services 的應用程式伺服器上，安裝 Analysis Services OLE DB 提供者 (MSOLAP) 的適當版本。  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的 MSOLAP 包含在 SQL Server 安裝程式中，因此只有在應用程式伺服器不是 PowerPivot 應用程式伺服器時，才需要明確安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本的 MSOLAP。  
  
    > [!NOTE]  
    >  Excel Calculation Services 應用程式伺服器也需要的檔案執行個體**Microsoft.AnalysisServices.Xmla.dll**在全域組件。 若要將此 .dll 安裝在應用程式伺服器上，請安裝 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 選取 「 管理工具-完成 」**特徵選取**SQL Server 安裝程式精靈 頁面。  
  
-   如果您希望應用程式伺服器支援舊版 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿，則需要安裝 SQL Server 2008 R2 版本的 MSOLAP。  
  
 如需有關安裝提供者，包括驗證步驟，請參閱[SharePoint 伺服器上安裝 Analysis Services OLE DB 提供者](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)  
  
##  <a name="bkmk_verify"></a> 步驟 4:確認安裝  
 在這個最後步驟中，您將驗證 SharePoint 2010 和 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 都能完整運作。 如需相關指示，請參閱 < [Verify a PowerPivot for SharePoint 安裝](../../analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md)。  
  
## <a name="see-also"></a>另請參閱  
 [PowerPivot for SharePoint 2010 安裝](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [部署檢查清單：Reporting Services、 Power View 及 PowerPivot for SharePoint](deployment-checklist-reporting-services-power-view-power-pivot-for-sharepoint.md)   
 [部署檢查清單：向外延展至 SharePoint 2010 伺服器陣列加入 PowerPivot 伺服器](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)   
 [部署檢查清單：PowerPivot for SharePoint 2010 的多伺服器安裝](../../../2014/sql-server/install/deployment-checklist-multiserver-installation-powerpivot-sharepoint-2010.md)  
  
  
