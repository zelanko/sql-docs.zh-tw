---
title: "建立獨立式 R Server | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 408e2503-5c7d-4ec4-9d3d-bba5a8c7661d
caps.latest.revision: 35
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4f39a03ecf7b74e0e1305d692a71c28609c80bf0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-standalone-r-server"></a>建立獨立 R 伺服器

SQL Server 安裝程式包含安裝的機器學習 SQL Server 外部執行的伺服器的選項。 

這個選項可能會很有用，如果您要開發在 Windows 中，高效能 R 解決方案，然後在其他平台間共用方案。 您也可以使用 [伺服器] 選項來設定這些執行支援遠端計算內容所需的建置解決方案的環境：
  
  + 執行 R Services 的 SQL Server 執行個體
  + 使用 Hadoop 或 Spark 叢集的 R Server 執行個體
  + Teradata 資料庫內分析
  + 在 Linux 中執行的 R Server 

本主題描述 Microsoft R Server 和 Microsoft 機器學習 Server 在 SQL Server 安裝程式的安裝步驟。

## <a name="which-should-i-install"></a>我的安裝？

**Microsoft R Server**第一次提供 SQL Server 2016 的一部分，並支援的 R 語言。 Microsoft R Server 的最後一個版本已 9.0.1。
在 SQL Server 2017，R 伺服器已重新命名**Microsoft Machine Learning 伺服器**，新增對 Python 的支援。 最新版的 Microsoft Machine Learning 伺服器是 9.1.0。

Microsoft R Server 和 Microsoft Machine Learning 伺服器需要 Enterprise Edition。

+ [安裝 Microsoft R Server （獨立） 使用 SQL Server 安裝程式](#bkmk_installRServer)
+ [安裝 Microsoft Machine Learning 伺服器 （獨立） 使用 SQL Server 安裝程式](#bkmk_installRServer) 

  安裝程式需要 SQL Server 授權，而升級通常與 SQL Server 發行步調一致。 這可確保您的開發工具與在 SQL Server 計算內容中執行的版本同步。

+ [安裝 R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)

  使用此選項時，會使用現代的生命週期支援原則安裝 R 伺服器。 您也可以在安裝 SQL Server 2016 的執行個體升級之後執行此安裝程式。 目前，您_無法_安裝 Python 支援使用此選項。 若要取得 Python，您必須安裝 Server 機器學習使用 SQL Server 2017 安裝程式。

##  <a name="bkmk_installRServer"></a>如何安裝 Microsoft 機器學習服務伺服器 （獨立）
  
1. 如果您已安裝舊版的 Microsoft R Server，我們建議您解除安裝它第一次。

2. 執行 SQL Server 2017 安裝程式。
  
3. 按一下**安裝**索引標籤，然後選取**安裝新的機器學習伺服器 （獨立）**。

4. 規則檢查完成之後，接受 SQL Server 授權條款，並選取新的安裝。

5. 在**特徵選取**頁面上，下列選項應該已經選取：
    
    - Microsoft 的機器學習伺服器 （獨立）
    
    - R 和 Python 兩者預設會選取。
    
    您應該忽略所有其他選項。

6.  接受授權條款，下載並安裝的機器學習服務元件。 Microsoft R Open 和 Python 需要個別的授權合約。 
    
    無法使用 [接受]  按鈕時，您可以按一下 [下一步] 。 
    
    安裝這些元件 (及其所需的任何必要元件) 可能需要一些時間。 
    
    如果電腦沒有網際網路存取，您應該事先下載元件安裝程式。 如需詳細資訊，請參閱[安裝 ML 元件沒有網際網路存取](./installing-ml-components-without-internet-access.md)。 
    
7.  在 [準備安裝]  頁面上，確認您的選項並按一下 [安裝] 。


如需自動或離線安裝的詳細資訊，請參閱 [從命令列安裝 Microsoft R Server](../../advanced-analytics/r-services/install-microsoft-r-server-from-the-command-line.md)。

###  <a name="bkmk_installRServer"></a> 安裝 Microsoft R Server (獨立式)  

1. 如果您已安裝舊版的 Microsoft R Server 或任何版本的 Revolution Analytics 工具，您必須先解除。  請參閱 [從舊版的 Microsoft R Server 升級](#bkmk_Uninstall)。

2. 執行 SQL Server 2016 安裝程式。 我們建議您安裝 Service Pack 1 或更新版本。

3. 在 [安裝]  索引標籤上，按一下 [New R Server (Standalone) installation] (R 伺服器 (獨立) 的新安裝)  。
    
     ![獨立式 R Server 安裝選項](media/rsql-rstandalonesetup.png "R Server 獨立版安裝選項")
    
4.  在 [功能選擇]  頁面上，應該已經選取下列選項：
    
    **R Server (獨立式)**  
    
    您可以忽略所有其他選項。 請勿安裝 SQL Server 資料庫引擎或 SQL Server R Services。
    
5.  接受授權條款，下載並安裝 Microsoft R Open。 無法使用 [接受]  按鈕時，您可以按一下 [下一步] 。 
    
    安裝這些元件 (及其所需的任何必要元件) 可能需要一些時間。
    
6.  在 [準備安裝]  頁面上，確認您的選項並按一下 [安裝] 。  


### <a name="upgrade-an-existing-r-server-to-901"></a>9.0.1 要升級現有的 R 伺服器

如果您已安裝舊版的 Microsoft R Server （獨立） 您可以升級使用較新版的 R 元件執行個體。 升級也會變更伺服器現代的生命週期支援原則。 這可讓更新更頻繁地在不同的排程上比 SQL Server 版本的執行個體。

1. 安裝 Microsoft R Server (獨立式) (如果尚未安裝)。

2. 此處所列不同的 windows 安裝程式從位置下載：[執行 Microsoft R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#howtoinstall)。

3. 執行安裝程式，並遵循[這些指示](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#download-r-server-installer)。


### <a name="change-in-default-folder-for-r-packages"></a>R 封裝變更在預設資料夾

當您安裝使用 SQL Server 安裝程式時，R 程式庫會安裝在與您用於安裝的 SQL Server 版本相關聯的資料夾。 在此資料夾中，您也會找到範例資料、R 基底套件的文件，以及 R 工具和執行階段的文件。

**使用 SQL Server 2016 來進行安裝的 R Server (獨立式)**

`C:\Program Files\Microsoft SQL Server\130\R_SERVER`

**使用 SQL Server 2017 來進行安裝的 R Server (獨立式)**

`C:\Program Files\Microsoft SQL Server\140\R_SERVER`

**使用 Windows 的獨立安裝程式的安裝**

不過，如果您使用不同的 Windows installer，安裝或升級使用個別的 Windows installer，R 程式庫移到下列 R 伺服器資料夾：

`C:\Program Files\Microsoft\R Server\R_SERVER`
      
**安裝 R Services 的機器學習服務中的資料庫**

如果您使用 R 服務 （資料庫） 或機器學習服務 （資料庫），安裝 SQL Server 執行個體，該執行個體是在相同電腦上的 R 程式庫和工具預設會安裝到不同的資料夾：

`C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`

請勿直接呼叫與 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 執行個體關聯的 R 套件或公用程式。 如果 R Server 和 R 服務安裝在同一部電腦中，當您需要執行 RGui 或其他工具，可使用的 R 工具和 R_SERVER 資料夾安裝封裝。


### <a name="development-tools"></a>開發工具

開發 IDE 不會安裝成在安裝程序。 不需要額外的工具，包含所有的標準工具時，就會提供與 R 或 Python 的分佈。

我們建議您嘗試為新版本的[!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]，如 Visual Studio 支援 R 和 Python，以及 SQL Server 和 BI 工具。 不過，您可以使用任何慣用的開發環境，包括 RStudio。

## <a name="troubleshooting"></a>疑難排解  

### <a name="incompatible-version-of-r-client-and-r-server"></a>不相容的 R Client 及 R Server 版本

如果安裝最新版的 Microsoft R Client，並在使用遠端計算內容的 SQL Server 上用它來執行 R，可能會發生下列錯誤︰

*您電腦上執行的是 9.0.0 版的 Microsoft R Client，與 Microsoft R Server 8.0.3 版不相容。請下載並安裝相容版本。*

一般而言，隨 SQL Server R Services 一起安裝的 R版本會在服務版本發佈時更新。 為確保一律有最新版本的 R 元件，請安裝所有的 Service Pack。 為與 Microsoft R Client 9.0.0 相容，您必須安裝本 [技術支援文件](https://support.microsoft.com/kb/3210262)中描述的更新。 


### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>將 Microsoft R Server 安裝在安裝於 Windows Core 的 SQL Server 執行個體上

在 SQL Server 2016 RTM 版本中，時的已知的問題 Microsoft R Server 新增至 Windows Server Core 版本上執行個體。 這個問題已經修正。

如果您遇到這個問題，您可以套用 [KB3164398](https://support.microsoft.com/kb/3164398) 所述的修正，將 R 功能新增至 Windows Server Core 的現有執行個體。   如需詳細資訊，請參閱 [無法在 Windows Server Core 作業系統上安裝 Microsoft R 伺服器 (獨立式)](https://support.microsoft.com/kb/3168691)。


###  <a name="bkmk_Uninstall"></a> 從舊版的 Microsoft R Server 升級

如已安裝 Microsoft R Server 發行前版本，您必須先解除安裝它，才能升級至較新版本。

**解除安裝 R Server (獨立式)**

1.  在 [控制台] 中，按一下 [新增/移除程式] 並選取 [ `Microsoft SQL Server 2016 <version number>`]。  
  
2.  在有 [新增] 、[修復] 或 [移除]  元件選項的對話方塊中，選取 [移除] 。  
  
3.  在 [選取功能]  頁面下的 [共用功能] 中，選取 [R Server (獨立式)] 。 按一下 [下一步] ，然後按一下 [完成]  只解除安裝選取的元件。  
   
### <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>安裝失敗，錯誤為「一次只能安裝一項 Revolution Enterprise 產品。」

如已安裝舊版的 Revolution Analytics 產品或 SQL Server R Services 的發行前版本，您可能會遇到這個錯誤。 您必須先解除安裝任何舊版本，才能安裝較新版的 Microsoft R Server。 不支援與其他版本的 Revolution Enterprise 工具並存安裝。

不過，使用獨立式 R Server 搭配 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 或 SQL Server 2016 時，則支援並存安裝。

### <a name="unable-to-uninstall-older-components"></a>無法解除安裝舊版元件

如果移除較舊版本有問題，您可能需要編輯登錄才能移除相關的索引鍵。

> [!IMPORTANT]
> 只有安裝了 Microsoft R Server 發行前版本或 CTP 版的 SQL Server 2016 R Services，才適用此問題。
  
1. 開啟 Windows 登錄並找到此機碼︰ `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`。
2. 如有下列任一項目，且索引鍵只包含值 `sEstimatedSize2`，請予以刪除：
  
    -   E0B2C29E-B8FC-490B-A043-2CAE75634972        (8.0.2 版)
  
    -   46695879-954E-4072-9D32-1CC84D4158F4        (8.0.1 版)
  
    -   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (8.0.0 版)
  
    -   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (7.5.0 版)
  
## <a name="see-also"></a>另請參閱

[Microsoft R Server](../../advanced-analytics/r-services/r-server-standalone.md)


