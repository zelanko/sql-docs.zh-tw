---
title: "機器學習伺服器獨立或 R Server 獨立安裝 |Microsoft 文件"
ms.custom: 
ms.date: 02/14/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 408e2503-5c7d-4ec4-9d3d-bba5a8c7661d
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 2ecb60bd02b3fc1ee7ac7101749fa7affc2523bd
ms.sourcegitcommit: 4edac878b4751efa57601fe263c6b787b391bc7c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2018
---
# <a name="install-machine-learning-server-standalone-or-r-server-standalone"></a>安裝機器學習伺服器 （獨立） 或 R 伺服器 （獨立）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 安裝程式包含安裝的機器學習 SQL Server 外部執行的伺服器的選項。 這個選項可能會很有用，如果您要開發的高效能的機器學習解決方案可以使用遠端計算內容，或是，可以部署至多個平台，包括：
  
  + 執行個體的 SQL Server 2016 或 SQL Server 2017，啟用機器學習的位置
  + Hadoop 或 Spark 叢集中的 R 伺服器或機器學習伺服器執行個體
  + R 伺服器或在 Linux 中的機器學習伺服器

本文說明如何使用 SQL Server 安裝程式安裝的機器學習 Server 或 Microsoft R Server 的獨立版本。 如果您有 Enterprise Edition 或軟體保證，安裝獨立的機器學習 server 是免費的。

+ [安裝 R Server](#bkmk_installRServer) -使用 SQL Server 2016 安裝程式
+ [安裝 Server 機器學習](#bkmk_installMLServer)-使用 SQL Server 2017 安裝程式
+ [升級現有的 Microsoft R Server 執行個體](#bkmk_upgrade)
+ [協助我決定要安裝的項目](#bkmk_tips)

##  <a name="bkmk_installMLServer"></a> 安裝機器學習服務伺服器 （獨立）

這項功能需要的企業授權或對等**SQL Server 2017**。

如果您已安裝舊版的 Microsoft R Server，我們建議您解除安裝它第一次。

如果電腦沒有網際網路存取，您應該事先下載元件安裝程式。 如需詳細資訊，請參閱[安裝沒有網際網路存取的機器學習元件](./installing-ml-components-without-internet-access.md)。

1. 執行 SQL Server 2017 安裝程式。

2. 按一下**安裝**索引標籤，然後選取**安裝新的機器學習伺服器 （獨立）**。
    
     ![機器學習 Server 獨立安裝](media/2017setup-installation-page-mlsvr.png "啟動的機器學習 Server 獨立安裝")

3. 規則檢查完成之後，接受 SQL Server 授權條款，並選取新的安裝。

4. 在**特徵選取**頁面上，下列選項應該已經選取：

    - Microsoft 的機器學習伺服器 （獨立）

    - R 和 Python 兩者預設會選取。 您可以取消選取其中一個語言，但我們建議您安裝至少其中一個支援的語言。

     ![機器學習 Server 獨立安裝](media/2017setup-features-page-mlsvr-rpy.png "啟動的機器學習 Server 獨立安裝")
    
    您應該忽略所有其他選項。 
    
    > [!NOTE]
    > 避免安裝**共用功能**如果電腦已安裝的 SQL Server 資料庫中的分析機器學習服務。 這會建立重複的程式庫。
    > 
    > 此外，SQL Server 中執行的 R 或 Python 指令碼由 SQL Server，來為未與其他 database engine 服務所使用的記憶體衝突管理，而獨立機器學習伺服器沒有這類條件約束，並可能會干擾其他資料庫作業. 最後，資料庫管理員通常會封鎖透過 RDP 工作階段，通常會使用實施，遠端存取。
    > 
    > 基於這些理由，我們通常會建議您在 SQL Server 機器學習服務從另一部電腦上安裝機器學習伺服器 （獨立）。

5.  接受授權條款，下載並安裝的機器學習服務元件。 如果您安裝這兩種語言，個別的授權合約是 Microsoft R 和 Python 需要。
    
     ![Python 授權合約](media/2017setup-python-license.png "Python 授權合約")
    
    這些元件和它們所需要的任何必要條件的安裝可能需要一點時間。 無法使用 [接受]  按鈕時，您可以按一下 [下一步] 。

6.  在 [準備安裝]  頁面上，確認您的選項並按一下 [安裝] 。

如需自動或離線安裝的詳細資訊，請參閱[從命令列安裝 Microsoft R Server](../../advanced-analytics/r/install-microsoft-r-server-from-the-command-line.md)。

##  <a name="bkmk_installRServer"></a> 安裝 Microsoft R Server (獨立式)

這項功能需要的企業授權或對等**SQL Server 2016**。

如果您已安裝任何舊版的 Revolution Analytics 工具或封裝，您必須先解除。 請參閱[從較舊版本的 Microsoft R Server 升級](#bkmk_Uninstall)。

1. 執行 SQL Server 2016 安裝程式。 我們建議您安裝 Service Pack 1 或更新版本。

2. 在**安裝**索引標籤上，按一下 **安裝新的 R 伺服器 （獨立）**。
    
     ![開始安裝 R Server 的獨立](media/2016-setup-installation-rsvr.png "啟動 R Server 的獨立安裝程式")
    
3.  在 [功能選擇]  頁面上，應該已經選取下列選項：
    
    **R Server (獨立式)**  
    
    ![功能選項的 R 伺服器獨立](media/2016setup-rserver-features.png "功能 R 伺服器獨立的選項")
    
    您可以忽略所有其他選項。 
    
    > [!NOTE]
    > 避免安裝**共用功能**如果您執行安裝程式的電腦上其中 R 服務已安裝的 SQL Server 資料庫中的分析。 這會建立重複的程式庫。
    > 
    > SQL Server 中執行 R 指令碼由 SQL Server，來為未與其他 database engine 服務所使用的記憶體衝突管理，而獨立 R 伺服器沒有這類條件約束，並可能會干擾其他資料庫作業。
    > 
    > 我們通常會建議您在 SQL Server 機器學習服務從另一部電腦上安裝機器學習伺服器 （獨立）。

4.  接受授權條款，下載並安裝 Microsoft R Open。 無法使用 [接受]  按鈕時，您可以按一下 [下一步] 。
    
    這些元件和它們所需要的任何必要條件的安裝可能需要一點時間。
    
5.  在 [準備安裝]  頁面上，確認您的選項並按一下 [安裝] 。

## <a name="bkmk_upgrade"></a> 升級現有的 R 伺服器執行個體

如果您已安裝舊版的 Microsoft R Server （獨立），您可以升級使用較新版的 R 元件執行個體。 升級也會變更為使用現代軟體生命週期支援原則的支援原則。 這可讓更新更頻繁地在不同的排程上比 SQL Server 版本的執行個體。

1. 從此處所列的位置下載個別的 windows 安裝程式： 

    + [安裝機器學習適用於 Windows 的伺服器](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
    + [安裝 R Server 9.1 適用於 Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

2. 執行安裝程式並遵循指示進行。 在您用來選取要安裝的功能頁面上，選取您想要升級的 R 伺服器的每個執行個體。

## <a name ="bkmk_tips"></a> 安裝的提示與後續工作

本節提供與設定相關的其他資訊。

### <a name="which-version-should-i-install"></a>應該安裝哪個版本？

+ **Microsoft R Server**第一次提供 SQL Server 2016 的一部分，並支援的 R 語言。 Microsoft R Server 的最後一個版本已 9.0.1。

+ **Microsoft Machine Learning 伺服器**最新版本，其中隨附於 SQL Server 2017 許多更新的功能，包括對 Python 的支援。 已發行的 SQL Server 2017 的累計更新 1，包括機器學習 Server 9.2.1.24 版本。 如果您想要最新的 Python 應用程式開發介面，我們會建議這項更新。

+ **就地升級**： 安裝程式需要 SQL Server 授權並升級通常與 SQL Server 發行日程對齊。 這可確保您的開發工具與在 SQL Server 計算內容中執行的版本同步。 不過，您可以使用個別的 windows 安裝程式以取得更頻繁的更新，現代軟體生命週期支援原則。 您也可以使用此安裝程式來升級 SQL Server 2016 或 SQL Server 2017 的執行個體。

### <a name="default-installation-folders"></a>預設安裝資料夾

當您安裝 R 伺服器或使用 SQL Server 安裝程式的機器學習伺服器，R 程式庫會安裝在與您用於安裝的 SQL Server 版本相關聯的資料夾。 在這個資料夾中，您也可以找到範例資料、 R 基底套件，文件及文件的 R 工具和執行階段。

不過，如果您使用不同的 Windows installer，安裝或升級使用個別的 Windows installer，R 程式庫會安裝在不同的資料夾。

只供參考，如果您已安裝的 SQL Server 執行個體與 R Services （資料庫） 或機器學習服務 （資料庫），且該執行個體在相同的電腦上的 R 程式庫和工具預設會安裝在不同的資料夾。

下表列出每個安裝的路徑。

|版本| 安裝方法 | 預設資料夾|
|----|----|----|
|R Server (Standalone) |SQL Server 2016 安裝程式精靈|`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|R Server (Standalone) |Windows 的獨立安裝程式|`C:\Program Files\Microsoft\R Server\R_SERVER`|
|Machine Learning 伺服器 (獨立式) |  SQL Server 2017 安裝精靈中，與 R 語言選項 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER`|
|Machine Learning 伺服器 (獨立式) |  SQL Server 2017 安裝精靈中，使用 Python 語言選項 |`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Machine Learning 伺服器 (獨立式) |  Windows 的獨立安裝程式 |`C:\Program Files\Microsoft\R Server\R_SERVER`|
|R Services (資料庫內) |SQL Server 2016 安裝程式精靈|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|
|Machine Learning 服務 (資料庫內) |SQL Server 2017 安裝精靈中，與 R 語言選項|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  |
|Machine Learning 服務 (資料庫內) |SQL Server 2017 安裝精靈中，使用 Python 語言選項| `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
### <a name="development-tools"></a>開發工具

開發 IDE 不會安裝成在安裝程序。 不需要額外的工具，包含所有的標準工具時，就會提供與 R 或 Python 的分佈。

我們建議您嘗試為新版本的[!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]。 Visual Studio 支援同時 R 和 Python，以及資料庫開發工具與 SQL Server 的連線與 BI 工具。 不過，您可以使用任何慣用的開發環境，包括 RStudio。

## <a name="troubleshooting"></a>疑難排解

本節列出一些常見的問題時要注意的機器學習伺服器或 R 伺服器安裝。

### <a name="incompatible-version-of-r-client-and-r-server"></a>不相容的 R Client 及 R Server 版本

如果您安裝 Microsoft R 用戶端，並使用它來執行 R 遠端的 SQL Server 計算內容中，您可能會收到如下錯誤：

*您正在 Microsoft R 用戶端版本 9.0.0 您與 Microsoft R Server 8.0.3 版本不相容的電腦。請下載並安裝相容版本。*

在 SQL Server 2016 中，所需的 SQL Server R 服務正在執行的 R 版本會完全與 Microsoft R 用戶端中的程式庫相同。 在新版中已移除這項需求。 不過，我們建議您一律取得最新版的機器學習的元件，並安裝所有 service pack。 

如果您有舊版的 Microsoft R Server，而且需要以確保相容性與 Microsoft R 用戶端 9.0.0，安裝所述的更新，在這個[技術支援文件](https://support.microsoft.com/kb/3210262)。

### <a name="installing-microsoft-r-server-on-an-instance-of-sql-server-installed-on-windows-core"></a>將 Microsoft R Server 安裝在安裝於 Windows Core 的 SQL Server 執行個體上

在 SQL Server 2016 RTM 版本中，時的已知的問題 Microsoft R Server 新增至 Windows Server Core 版本上執行個體。 這個問題已經修正。

如果您遇到此問題，您可以將套用所述的修正[KB3164398](https://support.microsoft.com/kb/3164398)將 R 功能新增至 Windows Server Core 上的現有執行個體。   如需詳細資訊，請參閱 [無法在 Windows Server Core 作業系統上安裝 Microsoft R 伺服器 (獨立式)](https://support.microsoft.com/kb/3168691)。

###  <a name="bkmk_Uninstall"></a> 從較舊版本的 Microsoft R Server 升級

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

[Machine Learning Server (獨立)](../../advanced-analytics/r/r-server-standalone.md)
