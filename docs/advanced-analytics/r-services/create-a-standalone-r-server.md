---
title: "建立獨立 R 伺服器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 408e2503-5c7d-4ec4-9d3d-bba5a8c7661d
caps.latest.revision: 35
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 27
---
# 建立獨立 R 伺服器
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝程式包含安裝 **Microsoft R Server (獨立式) 的選項**。 此選項可讓您在 Windows 上開發高效能的 R 解決方案，同時連接到您選擇的資料庫或資料來源。 只有 Enterprise Edition 提供 Microsoft R Server  
  
 當您安裝 Microsoft R Server 時，您會獲得 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 提供的相同增強 R 套件和連線工具，但不需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，R 指令碼會在獨立的電腦上執行，不是在資料庫中執行。  
  
> [!NOTE]  
>  Microsoft R Server 現在也可以透過簡化的安裝程式來取得，此程式會註冊[新式週期原則](https://support.microsoft.com/help/447912)中的執行個體。 這項支援項目可確保您能一直使用最新版的 R。如需使用簡化之安裝程式的詳細資訊，請參閱[執行 Microsoft R Server for Windows](https://msdnstage.redmond.corp.microsoft.com/microsoft-r/rserver-install-windows?branch=r-server-nov16-dev)。
>  
> 如果透過簡化的安裝程式來安裝 Microsoft R Server，您也可以轉換任何指定的 R Services 執行個體，使用新的支援原則並取得更頻繁的 R 元件更新。如需詳細資訊，請參閱[使用 sqlBindR.exe 升級 R Services 的執行個體](http://www.bing.com)。   
  
##  <a name="a-namebkmkinstallrservicesindatabasea-install-microsoft-r-server-standalone"></a><a name="bkmk_installRServicesInDatabase"></a> 安裝 Microsoft R Server (獨立式)  
  
1.  如已安裝舊版的 Microsoft R Server，您必須先解除安裝。  請參閱[從舊版的 Microsoft R Server 升級](#bkmk_Uninstall)。 

2. 執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式。  
  
2.  在 [安裝]  索引標籤上，按一下 [New R Server (Standalone) installation] (R 伺服器 (獨立) 的新安裝)  。  
  
     ![Setup option for R Server Standalone](../../advanced-analytics/r-services/media/rsql-rstandalonesetup.png "Setup option for R Server Standalone")  
  
3.  在 [功能選擇]  頁面上，應該已經選取下列選項：  
  
    -   **R Server (獨立式)**  
  
         此選項會安裝共用的功能，包括開放原始碼 R 工具和基底套件，以及 Microsoft R 隨附的增強型 R 套件和連線工具。  
  
     您可以忽略所有其他選項。  
  
4.  接受授權條款，下載並安裝 Microsoft R Open。 無法使用 [接受] 按鈕時，您可以按一下 [下一步]。 安裝這些元件 (及其所需的任何必要元件) 可能需要一些時間。   
  
5.  在 [準備安裝] 頁面上，確認您的選項並按一下 [安裝]。  
  
> [!TIP]
> 如需自動或離線安裝的詳細資訊，請參閱[從命令列安裝 Microsoft R Server](../../advanced-analytics/r-services/install-microsoft-r-server-from-the-command-line.md)。

  
## <a name="what-is-installed-and-where-to-find-r-packages"></a>安裝的項目以及尋找 R 套件位置  
 Microsoft R Server 包含 R 基底套件和一組增強的 R 套件，支援平行處理、改善的效能以及資料來源連線，包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Hadoop。  
  
-   **R 套件**  
  
     R 程式庫會隨 Microsoft SQL Server 2016 安裝的其他工具和公用程式一起安裝。 例如：  
  
     `C:\Program Files\Microsoft SQL Server\130\R_SERVER`  
  
     此外，您會在這個資料夾中發現 R 基底套件的文件、範例資料和 R 工具和執行階段的文件。  
  
    > [!NOTE]  
    >  如果您已在同一部電腦上安裝了使用 R Services (資料庫內) 的 SQL Server 執行個體，R 程式庫和工具會安裝到不同的資料夾中︰`C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`  
    >   
    >  請勿使用與 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體相關聯的 R 套件或公用程式。 一律使用 R_SERVER 資料夾中的 R 工具和套件。  
  
-   **R 工具**  
  
     安裝過程中不會安裝 R 開發 IDE。 您可以安裝 RStudio、[!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 或您偏好的任何其他開發環境。  
  
     但不需要其他工具。 所有的標準基底 R 工具都隨附於 `C:\Program Files\Microsoft SQL Server\130\R_SERVER\bin`。  
  
     如需詳細資訊，請參閱[安裝或設定 R 工具](../../advanced-analytics/r-services/setup-or-configure-r-tools.md)。  


 
## <a name="troubleshooting"></a>疑難排解  

### <a name="incompatible-version-of-r-client-and-r-server"></a>不相容的 R Client 及 R Server 版本

如果安裝最新版的 Microsoft R Client，並在使用遠端計算內容的 SQL Server 上用它來執行 R，可能會發生下列錯誤︰

*您電腦上執行的是 9.0.0 版的 Microsoft R Client，與 Microsoft R Server 8.0.3 版不相容。請下載並安裝相容版本。*

一般而言，隨 SQL Server R Services 一起安裝的 R版本會在服務版本發佈時更新。 為確保一律有最新版本的 R 元件，請安裝所有的 Service Pack。 為與 Microsoft R Client 9.0.0 相容，您必須安裝本[技術支援文件](https://support.microsoft.com/kb/3210262)中描述的更新。 


### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>將 Microsoft R Server 安裝在安裝於 Windows Core 的 SQL Server 執行個體上
在 SQL Server 2016 發行版本中，已知將 Microsoft R Server 新增至 Windows Server Core 版本執行個體時會發生問題。 這個問題已經修正。 

如果您遇到這個問題，您可以套用 [KB3164398](https://support.microsoft.com/kb/3164398) 所述的修正，將 R 功能新增至 Windows Server Core 的現有執行個體。   如需詳細資訊，請參閱[無法在 Windows Server Core 作業系統上安裝 Microsoft R 伺服器 (獨立式)](https://support.microsoft.com/kb/3168691)。


###  <a name="a-namebkmkuninstalla-upgrading-from-an-older-version-of-microsoft-r-server"></a><a name="bkmk_Uninstall"></a> 從舊版的 Microsoft R Server 升級  
 如已安裝 Microsoft R Server 發行前版本，您必須先解除安裝它，才能升級至較新版本。  
  
**解除安裝 R Server (獨立式)**  
  
1.  在 [控制台] 中，按一下 [新增/移除程式] 並選取 [`Microsoft SQL Server 2016 <version number>`]。  
  
2.  在有 [新增]、[修復] 或 [移除] 元件選項的對話方塊中，選取 [移除]。  
  
3.  在 [選取功能] 頁面下的 [共用功能] 中，選取 [R Server (獨立式)]。 按一下 [下一步]，然後按一下 [完成] 只解除安裝選取的元件。  
   
### <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>安裝失敗，錯誤為「一次只能安裝一項 Revolution Enterprise 產品。」  
如已安裝舊版的 Revolution Analytics 產品或 SQL Server R Services 的發行前版本，您可能會遇到這個錯誤。 您必須先解除安裝任何舊版本，才能安裝較新版的 Microsoft R Server。 不支援與其他版本的 Revolution Enterprise 工具並存安裝。  

但下列情況支援並存安裝：使用 R Server (獨立式) 搭配 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 和 
  
### <a name="unable-to-uninstall-older-components"></a>無法解除安裝舊版元件   
  
如果移除較舊版本有問題，您可能需要編輯登錄才能移除相關的索引鍵。  

> [!IMPORTANT]
> 只有安裝了 Microsoft R Server 發行前版本或 CTP 版的 SQL Server 2016 R Services，才適用此問題。
  
1. 開啟 Windows 登錄並找到此機碼︰`HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`。  
2. 如有下列任一項目，且索引鍵只包含值 `sEstimatedSize2`，請予以刪除：  
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972        (8.0.2 版)  
  
    -   46695879-954E-4072-9D32-1CC84D4158F4        (8.0.1 版)  
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (8.0.0 版)  
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (7.5.0 版)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft R Server](../../advanced-analytics/r-services/r-server-standalone.md)  
  
  