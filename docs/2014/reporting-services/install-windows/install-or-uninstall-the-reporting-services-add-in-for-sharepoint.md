---
title: 安裝或卸載適用于 SharePoint 的 Reporting Services 增益集（SharePoint 2010 和 SharePoint 2013） |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c2804a9a-08ea-4f4a-805d-a2c19c68733d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 63f45fa174296e4ce79985236da2d97d3f11e937
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2020
ms.locfileid: "78173607"
---
# <a name="install-or-uninstall-the-reporting-services-add-in-for-sharepoint-sharepoint-2010-and-sharepoint-2013"></a>安裝或解除安裝 SharePoint 的 Reporting Services 增益集 (SharePoint 2010 和 SharePoint 2013)
  在 sharepoint 伺服器上[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]執行適用于 sharepoint 產品的安裝封裝增益集（rssharepoint.msi .msi），以[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]在 sharepoint 部署中啟用功能。 功能包含 Power View、報表檢視器 Web 組件、URL Proxy 端點、內容類型以及應用程式頁面，讓您可以建立、檢視及管理報表、報表模型、資料來源以及在 SharePoint 網站上的其他報表伺服器內容。 適用於 SharePoint 產品的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集是以 SharePoint 模式執行之報表伺服器的必要元件。 增益集可以從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝精靈安裝，或是從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 功能套件下載 rsSharePoint.msi。 如需增益集版本和下載頁面的清單，請參閱 [尋找適用於 SharePoint 產品之 Reporting Services 增益集的位置](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)。

||
|-|
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|

 **本主題內容：**

-   [必要條件](#bkmk_prereq)

-   [增益集的安裝內容為何？](#bkmk_whatinstalled)

-   [安裝方法的總覽](#bkmk_3ways_to_install)

-   [使用安裝檔 Rssharepoint.msi 安裝增益集](#bkmk_install_rssharepoint)

    -   [僅限檔案安裝](#bkmk_files_only_installation)

-   [如何移除 Reporting Services 增益集](#bkmk_remove_addin)

-   [如何從命令列修復 rssharepoint.msi](#bkmk_repair)

-   [安裝程式記錄檔](#bkmk_logfiles)

-   [升級](#bkmk_upgrade)

-   [Rscustomaction.exe .exe](#bkmk_rscustomaction)

##  <a name="bkmk_prereq"></a> 必要條件
 安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集是整合報表伺服器與 SharePoint 產品之執行個體的數個必要步驟之一。 如需有關使用 SharePoint 模式之完整需求集的詳細資訊，請參閱＜ [Hardware and Software Requirements for Reporting Services in SharePoint Mode](../../../2014/sql-server/install/hardware-and-software-requirements-for-reporting-services-in-sharepoint-mode.md)＞。 如需有關安裝和設定的[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]詳細資訊，請參閱[安裝 SharePoint 2013 Reporting Services sharepoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)。

-   若要整合 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 與具備多重 Web 前端應用程式的 SharePoint 伺服器陣列，請在具有 Web 伺服器前端的伺服器陣列中之每部電腦上安裝增益集。 請只針對將用來存取報表伺服器內容的 Web 前端進行這項處理。

-   若要安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集，您必須是電腦上的系統管理員。 例如，如果您要在命令提示字元中執行 rsSharePoint.msi，則應使用 **[以系統管理員身分執行]** 選項以系統管理員權限開啟命令提示字元。

-   您必須是 SharePoint Farm Administrators 群組成員才能安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集。

-   您必須是網站集合管理員，才能啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 整合功能。

-   如需使用增益集部署範例的圖表，請參閱[SharePoint 中 SQL SERVER BI 功能的部署拓撲](../../sql-server/install/deployment-topologies-for-sql-server-bi-features-in-sharepoint.md)。

##  <a name="bkmk_whatinstalled"></a>增益集的安裝內容為何？
 增益集的安裝程序是由兩個階段組成，這兩個階段都會在完成標準安裝時自動完成：

-   第一階段是安裝檔案至適當的資料夾。 該資料夾是 SharePoint 部署的標準。 rsCustomAction.exe 是所安裝的檔案之一。

-   安裝的第二部分是執行自訂動作集，利用 SharePoint 註冊 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 檔案。 從 rsCustomAction.exe 執行自訂動作。 當完整的兩階段安裝作業完成時，系統就會移除該 exe 檔。 您可以執行 **僅限檔案** 的安裝，在安裝結束時不執行 rsCustomAction.exe，並將其留在磁碟機中。

## <a name="the-reporting-services-installation-order"></a>Reporting Services 安裝順序
 此增益集可以在安裝 SharePoint 之前或 SharePoint 安裝之後進行安裝。 此增益集會遵循 SharePoint 預先部署標準，將檔案安裝在 SharePoint 安裝使用的位置中。

> [!NOTE]
>  在 SharePoint 產品之前安裝此增益集的好處是，當新的伺服器加入到伺服器陣列時，SharePoint 伺服器陣列將會設定和啟動 Reporting Services 增益集。

 **SharePoint 2010**

-   SharePoint 2010 產品準備工具會安裝 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 版本的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集。 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 包含 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 功能需要使用的新版本增益集。

     如果您執行 SharePoint 產品準備工具，您仍然需要安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 增益集的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本。

-   如果您先行安裝了 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 增益集的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本，則當您執行 SharePoint 產品準備工具時，會看到以下的對話方塊，表示在偵測到較新版時，準備工具並未安裝舊版增益集。 這是預期的行為

     ![已安裝 SSRS 增益集。](../../../2014/sql-server/install/media/rs-sharepointprereq-complete.gif "已安裝 SSRS 增益集。")

 **SharePoint 2013**

 SharePoint 20103 產品準備**工具不會安裝適用**于[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sharepoint 產品的增益集。

##  <a name="bkmk_3ways_to_install"></a>安裝方法的總覽
 您[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]可以使用下列兩種方法的其中一種來安裝適用于 SharePoint 產品的增益集：

-   **安裝精靈：** ![注意](../../../2014/reporting-services/media/rs-fyinote.png "注意")新的使用[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝精靈可以安裝增益集。 在精靈的 [功能選擇]**** 頁面上，選擇 [適用於 SharePoint 產品的 Reporting Services 增益集]****。

-   **rssharepoint.msi .msi：** 此增益集可以直接從安裝媒體安裝，或下載並安裝。 rsSharepoint.msi 同時支援圖形化使用者介面和命令列安裝。 您必須以系統管理員權限執行 .msi，方式是先開啟提高權限的命令提示字元，然後從命令列執行 rsSharepoint.msi。 如需下載此增益集的詳細資訊，請參閱 [尋找適用於 SharePoint 產品之 Reporting Services 增益集的位置](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)。

    > [!NOTE]
    >  如果您使用 **/q** 參數進行無訊息命令列安裝，將不會顯示使用者授權合約。 不論安裝方式為何，使用此軟體皆受到授權合約的限制，同時您有責任遵從授權合約的規定。

##  <a name="bkmk_install_rssharepoint"></a>使用安裝檔 Rssharepoint.msi 安裝增益集
 此章節與直接安裝 rssharepoint.msi 相關，可以執行 .msi 安裝精靈或命令列安裝。 如果您使用 SQL Server 安裝精靈安裝增益集，則不需遵循下列步驟。

 您可以執行下列命令以看到完整的命令列參數清單：

```
Rssharepoint.msi /?
```

1.  下載[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]增益集的安裝`rsSharepoint.msi`程式（）。 如需下載此增益集的詳細資訊，請參閱 [尋找適用於 SharePoint 產品之 Reporting Services 增益集的位置](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)。

2.  以管理員的身分執行 `rsSharepoint.msi`，執行安裝精靈。 此精靈會顯示 [歡迎使用] 頁面、軟體授權合約和註冊資訊頁面。 安裝程式會在下列路徑下建立資料夾，並將檔案複製到資料夾：

     `%program files%\common files\Microsoft Shared\Web Server Extensions\14\`

     或

     `%program files%\common files\Microsoft Shared\Web Server Extensions\15\`

3.  在 SharePoint 管理中心設定報表伺服器設定與功能啟用。 . 如需安裝和設定[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sharepoint 模式的詳細資訊，請參閱[安裝 SharePoint 2010 Reporting Services sharepoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)。

###  <a name="bkmk_files_only_installation"></a>僅限檔案安裝
 若要安裝檔案但略過自訂動作階段，請從命令列執行 rssharepoint.msi 並加上 SKIPCA 選項：

1.  
  **以系統管理員權限**開啟命令提示字元。

2.  執行以下命令：

    ```cmd
    Msiexec.exe /i rsSharePoint.msi SKIPCA=1
    ```

 將會開啟安裝使用者介面並正常運作，同時會安裝 `rsCustomAction.exe` 檔案。 但 .exe 不會在安裝結束時執行，而且當安裝完成時，`rsCustomAction.exe` 會保留在電腦中。

### <a name="use-a-two-step-installation-to-troubleshoot-installation-issues-or-install-the-content-types"></a>使用兩步驟安裝來疑難排解安裝問題，或安裝內容類型。
 若您在安裝期間發生錯誤，或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 內容類型沒有顯示在文件庫設定中，您可以從命令列將安裝程式以兩步驟的流程執行：

1.  
  **以系統管理員權限** 開啟命令提示字元，並依前一章節所述內容，執行僅限檔案安裝。

2.  執行自訂動作可執行檔：

    1.  導覽至包含 `rsCustomAction.exe` 檔案的資料夾。 此檔案會隨僅限檔案安裝增益集複製到您的電腦上。 `rsCustomAction.exe`位於 **% Temp%** 目錄中。 若要導覽至檔案，請在命令提示字元中輸入下列內容：

         **CD% temp%**。

         此檔案應該位於：**\Users\\<您的名稱\>\AppData\Local\Temp**

    2.  輸入下列命令。 完成此組態步驟將需要幾分鐘的時間。 在此程序期間，將會重新啟動 W3SVC 服務。 會以程式複製檔案、暫存器元件等形式顯示數個狀態訊息，同時會執行 SharePoint 產品設定精靈。

        ```cmd
        rsCustomAction.exe /i
        ```

    3.  根據您的伺服器環境而定，變更生效所需的時間可能會有所不同。 您也可以執行 **iisreset** 強制執行更快的更新。

### <a name="quiet-installation-for-scripting"></a>指令碼的無訊息安裝
 您可以使用 **/q**或 **/quiet**參數，進行不會顯示任何對話方塊或警告的「無訊息」安裝。 如果您想要將增益集的安裝撰寫為指令碼，無訊息安裝相當實用。

> [!NOTE]
>  如果您使用 **/q** 參數進行無訊息命令列安裝，將不會顯示使用者授權合約。 不論安裝方式為何，使用此軟體皆受到授權合約的限制，同時您有責任遵從授權合約的規定。

 若要執行無訊息安裝：

1.  
  **以系統管理員權限**開啟命令提示字元。

2.  執行以下命令：

    ```cmd
    Msiexec.exe /i rsSharePoint.msi /q
    ```

##  <a name="bkmk_remove_addin"></a>如何移除 Reporting Services 增益集
 您可以從 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Windows [控制台] 或命令列，解除安裝適用於 SharePoint 產品的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 增益集。

1.  使用 [控制台] 將會完整解除安裝目前電腦上的檔案， **並且** 從 SharePoint 伺服器陣列中移除 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 物件和功能。 移除 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 物件和功能時，您就無法再檢閱和更新報表。

2.  解除安裝增益集的命令列方法可讓您使用 LocalOnly 參數僅移除本機電腦上的增益集檔案，而伺服器陣列中的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 物件和功能不會變更。

 解除安裝增益集將會移除在報表伺服器上用以處理報表的伺服器整合功能。 同時也會從 SharePoint 管理中心及其他自訂的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 頁面，移除 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 頁面。 您可能也會想要移除受影響的 SharePoint 網站上所有不再使用的報表和其他報表伺服器項目。 移除 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集之後，即無法再執行這些項目。

 若要解除安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集，您必須有仍在執行中的 [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] 或 [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] 安裝。 如果您先解除安裝 SharePoint 2010，您必須將它重新安裝，才能解除安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集。

 解除安裝此增益集的步驟，對於獨立的伺服器和伺服器陣列而言，都是一樣的。 安裝程式會移除程式檔案以及在安裝期間所加入的任何組態設定。

 解除安裝增益集不會移除下列項目：

-   針對用來存取 SharePoint 組態和內容資料庫的報表伺服器服務帳戶所建立的登入。 您必須從用來主控 SharePoint 資料庫的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]實例，刪除報表伺服器服務帳戶的任何登入。

-   為報表使用者所建立的權限或群組。 如果您已建立自訂的權限等級或 SharePoint 群組來授與對報表伺服器功能的存取權，就應該撤銷所有不再需要的權限。

-   上傳到 SharePoint 文件庫的資料檔案，包括報表定義 (.rdl)、共用資料來源 (.rsds) 及發行的報表項目 (.rsc) 檔案。 這些檔案並沒有刪除，但無法再執行。 您必須手動刪除這些檔案。

-   安裝程式不會刪除報表伺服器資料庫或修改用於整合作業的報表伺服器執行個體。

### <a name="to-uninstall-from-windows-control-panel"></a>若要從 Windows 控制台解除安裝
 若要從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows [控制台] 啟動精靈並移除增益集：

1.  在 [控制台] 中的 **[程式]**，選取 **[解除安裝程式]**。

2.  選取 [適用於 SharePoint 的 Microsoft SQL Server RS 增益集]****。 您也可以從命令提示字元中執行 **rssharepoint.msi** (不使用任何參數)，藉以啟動解除安裝精靈。

3.  按一下 **[移除]** 。

### <a name="uninstall-from-the-command-line"></a>從命令列解除安裝
 若要從命令列解除安裝增益集：

1.  
  **以系統管理員權限**開啟命令提示字元。

2.  執行以下命令：

    ```cmd
    msiexec.exe /uninstall rsSharePoint.msi
    ```

3.  您會看到確認訊息方塊。 按一下 [是]  。

### <a name="uninstall-the-add-in-from-the-local-server-only"></a>只從本機伺服器解除安裝增益集
 上述解除安裝增益集的方法會從伺服器陣列中移除 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能和物件。 如果您擁有多伺服器的伺服器陣列，而只想要解除安裝本機電腦上的增益集，並且讓 SharePoint 伺服器陣列保持運作狀態，請完成下列步驟：

1.  
  **以系統管理員權限**開啟命令提示字元。

2.  執行以下命令：

    ```cmd
    Msiexec.exe /uninstall rsSharePoint.msi LocalOnly=1
    ```

 此作業會從 SharePoint 取消 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 元件的註冊並會移除檔案，但只作用於本機電腦上。

 如果您想要從 SharePoint 取消 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能的註冊，但將檔案留在磁碟上以供稍後使用，請完成下列步驟：

1.  
  **以系統管理員權限**開啟命令提示字元。

2.  執行以下命令：

    ```cmd
    rsCustomAction.exe /p
    ```

 上述步驟假設您已安裝 .msi 且 SkipCA=1，同時可以使用 rscusstomaction.exe。 如需詳細資訊，請參閱説明僅限檔案安裝一節。

##  <a name="bkmk_repair"></a>如何從命令列修復 rssharepoint.msi
 若要使用命令列修復或解除安裝 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集，請完成下列步驟：

1.  
  **以系統管理員權限**開啟命令提示字元。

2.  執行以下命令：

    ```cmd
    msiexec.exe /f rssharepoint.msi
    ```

##  <a name="bkmk_logfiles"></a>安裝程式記錄檔
 執行安裝程式時，會為已安裝 **增益集的使用者，將資訊記錄到** %temp% [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料夾中的記錄檔。 例如 **c:\Users\\<使用者名稱\>\AppData\Local\Temp**。檔案名稱是 **RS_SP_\<編號>.log**，例如 **RS_SP_0.log**。 該記錄檔中的每項錯誤，都會以 "SSRSCustomActionError" 字串開頭。

> [!NOTE]
>  AppData 在 Windows 作業系統中是隱藏的資料夾。 您需要修改 Windows 檔案總管資料夾的設定，才可看到隱藏的檔案與資料夾。

#### <a name="view-a-log-file-with-windows-notepad"></a>利用 Windows 記事本檢視記錄檔

1.  下列命令會變更命令提示字元路徑，列出 rs 記錄檔後利用 Windows 記事本開啟其中一個檔案：

    ```cmd
    cd %temp%
    ```

    ```cmd
    dir rs_sp*.log
    ```

    ```cmd
    notepad rs_sp_3.log
    ```

#### <a name="view-a-log-file-with-powershell"></a>利用 PowerShell 檢視記錄檔

1.  從 SharePoint 管理命令介面輸入下列命令，從包含 "ssrscustomactionerror" 的檔案傳回已篩選過的資料列清單：

    ```powershell
    Get-Content -Path C:\Users\<UserName\AppData\Local\Temp\rs_sp_0.log | Select-String "ssrscustomactionerror"
    ```

2.  輸出類似如下範例：

     `2011-05-23 12:40:12: SSRSCustomActionError: SharePoint is installed, but not configured`.

##  <a name="bkmk_upgrade"></a>更新
 如果您已擁有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集的現有安裝，則可以升級至目前版本。 增益集的安裝程式會偵測現有的版本，並提示您確認升級作業。 這些訊息類似於下列文字：

 **在您的系統上偵測到較低版本的此產品。您要升級現有的安裝嗎？**

 如果確認，將會移除舊版增益集並安裝新版本。

 請注意， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集無法感知執行個體。 在電腦上只能安裝一個增益集執行個體。 目前版本無法與相異版本並存。

##  <a name="bkmk_rscustomaction"></a>Rscustomaction.exe .exe
 下表摘要列出 rscustomaction.exe 參數：

|Switch|描述|
|------------|-----------------|
|i|安裝自訂動作。 此作業會在 SharePoint 中註冊 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 元件。 此作業會重新啟動 W3SVCservice。|
|r|修復|
|u|解除安裝。 此作業會從整個 SharePoint 伺服器陣列中取消 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 元件的註冊，但會將檔案留在磁碟中。 此作業會重新啟動 W3SVCservice。|
|p|本機解除安裝。 此作業會從本機電腦取消 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 元件的註冊。 檔案將會留在磁碟上。 此作業會重新啟動 W3SVCservice。|
|t|僅限 SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 2005。 此切換作業會測試報表伺服器是否能與報表伺服器資料庫正常連接。|

## <a name="configuring-reporting-services"></a>設定 Reporting Services
 在所有需要的電腦上安裝該增益集之後，需要從 SharePoint 管理中心設定報表伺服器。 所需要的步驟取決於不同技術之安裝順序。 如需詳細資訊，請參閱[安裝 sharepoint 2010 Reporting Services Sharepoint 模式](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)和[Reporting Services 報表伺服器 &#40;sharepoint 模式&#41;](../../../2014/reporting-services/reporting-services-report-server-sharepoint-mode.md)

## <a name="see-also"></a>另請參閱
 [Reporting Services Sharepoint 模式安裝 sharepoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md) [Reporting Services 報表伺服器 &#40;sharepoint 模式&#41;](../../../2014/reporting-services/reporting-services-report-server-sharepoint-mode.md)
