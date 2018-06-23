---
title: 檢視及瀏覽原生模式報表使用 SharePoint Web 組件 (SSRS) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dee8ee42-156b-43b6-b202-02dfb9404284
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 2073a7317ea012f2eb1dc1d4888778763cba1611
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032220"
---
# <a name="view-and-explore-native-mode-reports-using-sharepoint-web-parts-ssrs"></a>View and Explore Native Mode Reports Using SharePoint Web Parts (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供數種 Web 組件，可與特定版本的報表伺服器，以及在特定的部署模式下搭配使用。  
  
-   **原生模式** ：如果您想要從原生模式報表伺服器存取 SharePoint 網站上的報表伺服器內容，請使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]隨附的 SharePoint 2.0 Web 組件報表總管和報表檢視器。 在本主題中有提供關於安裝與使用 2.0 Web 組件的指示。  
  
-   **SharePoint 模式** ：如果您想要存取以 SharePoint 模式執行的報表伺服器，請使用適用於 SharePoint 產品之 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集所安裝的 Web 組件。 如需增益集的詳細資訊，請參閱 [尋找適用於 SharePoint 產品之 Reporting Services 增益集的位置](../install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)。  
  
-   > [!NOTE]  
    >  原生模式的報表檢視器 Web 組件 (SPViewer.dwp) 與適用於 SharePoint 產品之 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集所安裝的 Web 組件 (ReportViewer.dwp) 有所不同。 這些 Web 組件具有不同的結構描述和實作，但是它們可以安裝在相同的 SharePoint 伺服器陣列上。 視覺上，您可以透過下列特性區分這兩個 Web 組件：透過增益集安裝之報表檢視器 Web 組件的工具列具有 [動作] 功能表。  
  
 如需報表伺服器模式的詳細資訊，請參閱 [Reporting Services Report Server](../reporting-services-report-server.md)。  
  
 本主題內容：  
  
-   [關於報表總管和報表檢視器](#bkmk_aboutwebparts)  
  
-   [使用 Web 組件的需求](#bkmk_requirements)  
  
-   [安裝 Web 組件](#bkmk_installingwebparts)  
  
-   [加入與設定 Web 組件](#bkmk_configurewebparts)  
  
##  <a name="bkmk_aboutwebparts"></a> 關於報表總管和報表檢視器  
 報表總管與報表檢視器是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Service Pack 2 (SP2) 導入的 SharePoint 2.0 Web 組件，而且繼續在最新的版本中提供。  
  
 這些 Web 組件可讓您從 SharePoint 網站檢視報表以及瀏覽報表伺服器資料夾階層。  
  
 請注意，不支援自訂 Web 組件。 Web 組件預期以原樣使用，因此不應加以擴充或修改。  
  
-   **報表總管** (SPExplorer.dwp) 會連接到報表伺服器電腦上的報表管理員。 您可以在報表伺服器上瀏覽可用的報表，然後訂閱個別的報表。 如果報表產生器有啟用，而且您擁有足夠的權限，您可以從報表總管 Web 組件啟動報表產生器。  
  
     報表總管會使用報表管理員中的頁面，顯示資料夾的內容，。 存取整個報表伺服器資料夾階層的個別項目和資料夾是透過報表伺服器上的角色指派控制。 當您選取報表時，會以新的瀏覽器視窗開啟。 報表伺服器上的 HTML 檢視器會顯示報表，並提供報表工具列，而非報表檢視器 Web 組件。 如果您要自訂工具列設定，請確認有在報表伺服器上指定 URL 存取參數。 如需指示，請參閱 [URL 存取參數參考](../url-access-parameter-reference.md)。  
  
-   **報表檢視器** (SPViewer.dwp) 會顯示報表，並提供您可以用於巡覽頁面、搜尋內容或匯出報表的工具列。 您可以將報表檢視器 Web 組件加入至 Web 組件頁面，以便在該頁面上永遠顯示特定的報表，或者 **您可以將其連接至報表總管** ，以顯示透過該 Web 組件開啟的報表。  
  
##  <a name="bkmk_requirements"></a> 使用 Web 組件的需求  
 使用報表檢視器與報表總管 Web 組件的需求包括：  
  
-   受支援的 SharePoint 產品版本與技術如下：  
  
    -   [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 and [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007.  
  
    -   [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 和 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]。  
  
-   原生模式報表伺服器版本必須是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 或更新版本。  
  
-   報表伺服器必須以原生模式執行。 您 **無法** 使用報表總管與報表檢視器 Web 組件來連接或檢視以 SharePoint 模式執行之報表伺服器上的報表。  
  
-   必須安裝報表管理員。  
  
 報表總管與報表檢視器 Web 組件透過包含在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中的封包 (.cab) 檔散發。 在本主題的下列章節中，提供安裝、設定與使用 Web 組件的指示。  
  
##  <a name="bkmk_installingwebparts"></a> 安裝 Web 組件  
 Web 組件會以封包 (.cab) 檔案的形式，傳遞至 SharePoint 伺服器。 請從命令列針對 .cab 檔執行 SharePoint Stsadm.exe 工具以安裝 Web 組件。 若要了解有關工具和 Web 組件部署的詳細資訊，請參閱您的 SharePoint 文件集。  
  
#### <a name="install-web-parts-using-powershell"></a>使用 PowerShell 安裝 Web 組件  
  
1.  請將 **RSWebParts.cab** 複製到 SharePoint 伺服器上的資料夾中。 您可以將其複製到 SharePoint 伺服器上的任何資料夾中，然後稍後在安裝 Web 組件後再刪除它。 根據預設， [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會將 RSWebParts.cab 檔案安裝至下列資料夾：  
  
    ```  
    C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint  
    ```  
  
2.  在已安裝 SharePoint 產品的電腦上，以 **系統管理權限** 開啟 **[SharePoint 2010 管理命令介面]**。  
  
3.  執行下列 PowerShell 命令：  
  
    ```  
    Install-SPWebPartPack -LiteralPath "C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint\RSWebParts.cab" -GlobalInstall  
    ```  
  
4.  您應該會看見類似以下的訊息，表示已部署 Web 組件。  
  
    > 名稱               方案識別碼                                             已部署  
  
    > ----                    ----------                                              -------\-  
  
    > rswebparts.cab    00000000-0000-0000-0000-000000000000     True  
  
     如需深入了解 PowerShell 的應用，請參閱 [Install-SPWebPartPack (http://technet.microsoft.com/library/ff607840.aspx)](http://technet.microsoft.com/library/ff607840.aspx)。  
  
#### <a name="install-web-parts-using-stsadmexe"></a>使用 STSADM.exe 安裝 Web 組件  
  
1.  請依照本文件的 PowerShell 章節所述，將 **RSWebParts.cab** 檔案複製到 SharePoint 伺服器上的相同位置。  
  
2.  在已安裝 SharePoint 產品的電腦上，以系統管理權限開啟 [命令提示字元] 視窗，然後巡覽至具有 **Stsadm.exe** 工具的資料夾。 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 的預設路徑如下：  
  
    > C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\14\BIN。  
  
3.  使用下列語法，執行 .cab 上的 Stsadm.exe：  
  
    ```  
    STSADM.EXE -o addwppack -filename "C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Reporting Services\SharePoint\RSWebParts.cab" -globalinstall  
    ```  
  
4.  您應該會看見「作業已成功完成」的訊息。  
  
     指定 `-globalinstall` 會將 Web 組件加入至全域組件快取 (GAC) 中。 如果您要連接 Web 組件，這是必要的步驟。  
  
##  <a name="bkmk_configurewebparts"></a> 加入與設定 Web 組件  
 安裝 Web 組件之後，您可以將它們加入至 SharePoint 網站上的一個或多個網頁。 您必須擁有建立網站和加入內容的權限。  
  
 下列程序會將這兩個 Web 組件加入至頁面，然後將報表總管與報表檢視器連接在一起。如此一來，當您在報表總管中按一下報表時，它就會顯示在報表檢視器內部。  
  
#### <a name="add-report-viewer"></a>加入報表檢視器  
  
1.  在 [網站動作] 中，按一下 **[編輯頁面]**。  
  
2.  在頁面上的區域中，按一下 **[新增 Web 組件]**。  
  
3.  在 **[新增網頁組件]** 對話方塊中，向下捲動至 **[其他]** 類別目錄。  
  
4.  選取 **[報表檢視器]**。  
  
    > [!WARNING]  
    >  請勿選取 [SQL Server Reporting Services 報表檢視器]。該 Web 組件是在您安裝適用於 SharePoint 產品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集時註冊，而且用於以 SharePoint 模式執行報表伺服器。 它無法用來檢視原生模式報表伺服器上的報表。  
  
5.  按一下 **[加入]**。  
  
6.  當頁面處於編輯模式時，在報表檢視 Web 組件中按一下 **[編輯網頁組件]** 。  
  
7.  在 **[報表管理員 URL]** 中，輸入指向報表管理員執行個體的 URL，該執行個體與您要存取的原生模式報表伺服器相關聯。 根據預設，報表管理員 URL 具有下列語法： **http://\<伺服器名稱 > /**。  
  
8.  在 **[報表路徑]** 中，指定正斜線，後面緊跟著資料夾路徑與報表名稱。 請 **勿** 加入伺服器名稱或報表管理員虛擬目錄。 例如，若要開啟 Adventure Works 資料夾中的 ‘Company Sales’ 報表，請指定 **/Adventure Works/Company Sales**。 以下是 ‘Products’ 報表位於報表伺服器根資料夾 **/Products**的另一個範例。  
  
9. 按一下 [確定] 。  
  
#### <a name="add-report-explorer-and-connect-to-report-viewer"></a>加入報表總管並連接到報表檢視器  
  
1.  在頁面的另一個區域中，按一下 **[新增網頁組件]** ，然後在 [其他] 資料夾中，按一下 **[報表總管]** 並按一下 **[新增]**。  
  
2.  在報表總管 Web 組件內容功能表中，按一下 **[編輯網頁組件]**。  
  
3.  在 **[報表管理員 URL]** 中，輸入指向報表管理員執行個體的 URL，該執行個體與您要存取的原生模式報表伺服器相關聯。  
  
4.  您可以選擇性地設定 **[起始路徑]**。 起始路徑是報表伺服器資料夾階層中的資料夾。 如果您要讓預設頁面成為比資料夾階層以下的資料夾，您可以指定起始路徑。 路徑開頭必須是正斜線。 您必須指定以報表伺服器資料夾階層之根節點開始的完整路徑，但是不包含伺服器名稱或報表管理員虛擬目錄。 例如，若要開啟根節點正下方，名稱為 Adventure Works 的資料夾，請在 [起始路徑] 中指定 **/Adventure Works** 。  
  
5.  按一下 [確定] 。  
  
6.  報表總管將會顯示報表伺服器中的報表項目清單。 根據預設，如果您按一下報表的名稱，系統將會在新視窗中開啟報表。 如果您想要將報表總管連接到報表檢視器，請完成下列步驟。如此一來，當您在報表總管中按一下報表名稱時，它就會顯示在報表檢視器中。  
  
    1.  在報表總管內容功能表中，按一下 **[連接]**。  
  
    2.  按一下 **[顯示報表於]**。  
  
    3.  按一下 **[報表檢視器]**。  
  
## <a name="see-also"></a>另請參閱  
 [報表管理員&#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)   
 [Reporting Services 報表伺服器&#40;SharePoint 模式&#41;](../reporting-services-report-server-sharepoint-mode.md)   
 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../report-server/reporting-services-report-server-native-mode.md)  
  
  