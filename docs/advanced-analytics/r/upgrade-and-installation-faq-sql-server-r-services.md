---
title: "升級及安裝常見問題集 (SQL Server R Services) |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 001e66b9-6c3f-41b3-81b7-46541e15f9ea
caps.latest.revision: 59
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: 395554af6b9d014d560d8b6520d032966630c5b2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/08/2017

---
# <a name="upgrade-and-installation-faq-sql-server-r-services"></a>升級及安裝常見問題集 (SQL Server R Services)

本主題提供有關機器學習中 SQL Server 功能安裝的一些常見問題的解答。 其中也涵蓋關於升級常見問題的解答。 從發行前版本，只能使用升級會發生一些問題。 因此，我們建議您識別您的版本與版本，然後升級至最新的版本或版本更新服務儘速。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務 （資料庫）

## <a name="performing-setup-for-the-first-time"></a>第一次執行安裝程式

請依照下列程序設定 [！INCLUDEssCurrent] 和 R 元件，如下所示： 

+ [設定 SQL Server R 服務或機器學習服務資料庫](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)
+ [設定 SQL Server 2017 使用 Python](../python/setup-python-machine-learning-services.md)
+ [建立獨立式 R Server](create-a-standalone-r-server.md)

您已安裝 SQL Server，以使用外部的 R 或 Python 指令碼之後, 您必須完成一些額外的設定。 這是因為預設不啟用外部指令碼執行功能。

> [!NOTE]
> 請勿使用已發行公用版本的 SQL Server 2016 之前的安裝指示。 完全改變早期版本之間的正式發行版本的安裝程序。 

### <a name="requirements-and-restrictions"></a>需求和限制

根據您要安裝的 R 服務的組建，下列限制的部分可能適用於：

- 在早期版本的 SQL Server 2016 R 服務，包含的工作目錄的磁碟機上需要 8.3 標記法。 如果您已安裝發行前版本，則升級至 SQL Server 2016 Service Pack 1 應該移除這項需求。

- 您無法在容錯移轉叢集上安裝 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 。 

- 在 Azure VM 中，可能需要一些額外的設定。 例如，您可能需要建立防火牆例外，以支援遠端存取。

- 不支援與另一個版本的 R，或其他來自 Revolution Analytics 的版本來並行安裝。

- 不支援任何 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 發行前版本的新安裝。 如果您使用發行前版本，升級儘速。

- 停用病毒掃描再開始安裝程式。 安裝程式完成之後，我們建議暫停 SQL Server （最好是整個樹狀結構） 所使用的資料夾上的病毒掃描。

### <a name="licensing-agreements-for-unattended-installs"></a>進行自動安裝的授權合約

如果您使用命令列升級的 SQL Server 執行個體時，請確定命令列包含新的授權合約參數*/IACCEPTROPENLICENSEAGREEMENT*。 如果您不使用這個參數，安裝程式可能會失敗。

### <a name="offline-installation-of-r-components-for-a-localized-version-of-sql-server"></a>離線安裝的 SQL Server 的當地語系化版本的 R 元件

當您在沒有網際網路存取的電腦上安裝 R 服務時，您必須採取額外兩個步驟。 您執行 SQL Server 安裝程式，並編輯安裝程式檔案，請確認已安裝正確的語言之前，請下載至本機資料夾的 R 元件安裝程式。

R 元件所使用的語言識別碼必須是 SQL Server 安裝程式語言，與相同或**下一步**按鈕已停用，因此您無法完成安裝程式。

如需詳細資訊，請參閱[Installing R Components without internet access](../../advanced-analytics/r-services/installing-ml-components-without-internet-access.md)。

## <a name="post-installation-configuration"></a>後續安裝設定

若要使用 R 或 Python 的機器學習，某些則需要其他組態之後執行 SQL Server 安裝程式。 額外的步驟可能需要根據伺服器和 SQL Server 執行個體和資料庫的安全性層級。 檢閱安裝指示，以判斷任何額外的設定可能會需要這些步驟。

[設定 SQL Server R 服務中的資料庫](set-up-sql-server-r-services-in-database.md)

- 支援執行外部指令碼，例如 R 或 Python，此功能會為資料庫安全性，預設會停用，且必須啟用。

- 確定 [啟動列] 用來執行 R 或 Python 的背景工作帳戶存取的執行個體。

- 您可能需要啟用遠端存取的伺服器上，或建立的防火牆規則允許輸入與 SQL Server 通訊。

- 根據計劃的工作負載，您可能需要最佳化的機器學習工作的伺服器。 

## <a name="upgrades-or-uninstallation"></a>升級或解除安裝

本章節包含特定的升級案例的詳細的指示。

不再支援從 SQL Server 2016 R 服務的發行前版本升級。 我們建議您解除安裝發行前版本，並儘速安裝發行版本。

### <a name="support-for-slipstream-upgrades"></a>匯集升級支援

匯集安裝程式是指將補充程式或更新套用至失敗的執行個體安裝，以修正現有問題的功能。 這個方法的優點是，SQL Server 會更新一次您執行安裝程式，避免個別重新啟動更新版本。

如果伺服器沒有網際網路存取，請務必下載 SQL Server 安裝程式。 您也必須在開始更新程序「之前」，另外下載對應的 R 元件安裝程式版本。 

如需下載位置，請參閱[安裝 R 元件沒有網際網路存取](installing-ml-components-without-internet-access.md)。

當所有安裝檔案都複製到本機目錄後，在命令列輸入 SETUP.EXE 來啟動安裝公用程式。

- 使用*/UPDATESOURCE*引數來指定包含 SQL Server 更新，例如累計更新或 service pack 發行版本的本機檔案的位置。

- 使用*/MRCACHEDIRECTORY*引數來指定包含 R 元件封包檔的資料夾。

如需詳細資訊，請參閱此部落格由支援小組：[沒有網際網路存取的電腦上部署 R Services](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)。

### <a name="upgrade-r-components-offline"></a>升級 R 元件離線

如果您安裝或升級不會連線到網際網路的伺服器，您必須開始重新整理之前手動下載的更新的版本的 R 元件。 如需詳細資訊，請參閱[安裝 R 元件沒有網際網路存取](../../advanced-analytics/r-services/installing-ml-components-without-internet-access.md)。

### <a name="schedule-for-update-of-r-components"></a>排程更新的 R 元件

Hotfix 或 SQL Server 2016 的增強功能會釋放，R 元件也會升級或重新整理時，您的執行個體已包含 R 服務功能。

如果您使用 SQL Server 2017，會自動安裝升級到 R 元件。

年 12 月從 2016年開始，您可以升級以更快的步調比 SQL Server 發行週期的 R 元件。 這樣做*繫結*現代軟體生命週期原則的 R 服務執行個體。 目前僅適用於 2016年執行個體的升級提供支援。 R 伺服器的新版本發行時，您可以升級至 2017年執行個體。

如需詳細資訊，請參閱[升級 SQL Server R Services 的執行個體使用 SqlBindR](../../advanced-analytics/r-services/use-sqlbindr-exe-to-upgrade-an-instance-of-r-services.md)。

### <a name="upgrade-from-a-pre-release-version-of-sql-server-2016"></a>從 SQL Server 2016 的發行前版本升級

一般情況下，任何發行前版本不支援就地升級。

若要成功地安裝 R 服務，您必須先解除安裝任何舊版的[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]及其相關的 R 元件。 這包括 SQL Server 2016 CTP3、 CTP3.1、 CTP3.2、 RC0 或 RC1。

解除安裝發行前版本，可以很複雜，而需要執行特殊的指令碼。 請連絡技術支援部門以尋求協助。

下列版本已安裝的 SQL Server 2016 的發行前版本。

| Version | 建置         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

如果您不的清楚您使用哪一個版本，執行`@@VERSION`從 SQL Server Management Studio。

### <a name="problems-with-setup-of-r-server-standalone"></a>安裝 R Server （獨立） 的問題

本章節描述 Microsoft R Server （獨立） 的安裝，請使用 SQL Server 2016 安裝程式的特定問題。 如需有關 R 伺服器升級至更一般的問題，請參閱[Microsoft R Server](https://msdn.microsoft.com/microsoft-r/) MSDN 上。

#### <a name="failure-to-install-localized-versions"></a>若要安裝當地語系化的版本失敗

當您離線安裝 R 伺服器時，發行前版本不允許您使用當地語系化的語言。

一般而言，當伺服器沒有網際網路存取，執行安裝程式之前您必須下載所有的安裝封裝 R 伺服器。 然後您會在安裝期間指定檔案的位置。

不過，如果安裝程式套件相關聯的語言識別項不是 SQL Server 安裝程式語言一樣，就會發生問題。 當您到達的 R 元件安裝頁面**下一步**按鈕已停用，您無法繼續進行安裝。 因應措施，您可以重新命名封裝使用比對識別項。

可能的安裝封裝的名稱，例如`SRO_3.2.2.0_1031.cab`。
若要安裝 SQL Server 上的 104 的語言，重新命名檔案`SRO_3.2.2.0_1041.cab`。

#### <a name="installing-r-services-and-r-server-standalone-on-the-same-computer"></a>在同一部電腦上安裝 R 服務和 R 伺服器獨立

一般而言，您無法安裝 R 服務 （資料庫） 和 R 伺服器 （獨立） 在相同電腦上。 不過，如果伺服器有足夠的容量，R 伺服器獨立可能做開發工具很實用。 您也可能需要使用實施 R Server 功能，並從 R 伺服器的 SQL Server 資料存取不需要移動資料。

請注意，是否您在相同電腦上安裝 R Server 和 R 服務，會安裝兩組不同的相同 R 程式庫。 其中一個是供 SQL Server 執行個體，且其中用於開發或 R 伺服器所使用。

在舊版的 SQL Server 2016 中，同時安裝 R Server （獨立） 和 R 服務 （資料庫） 可能會造成安裝程式失敗並出現 「 拒絕存取 」 訊息。 Service Pack 1 中已修正此問題，SQL Server 2016。

如果您遇到這個錯誤，而且必須升級這些功能，請執行 SQL Server 2016 with SP1 匯集安裝。 有兩種方式來解決問題，這需要解除安裝再重新安裝。

1. 解除安裝 R 服務 （資料庫），並確定 SQLRUserGroup 的使用者帳戶會移除。

2. 重新啟動伺服器，然後再重新安裝 R Server （獨立）。

3. 執行的 SQL Server 安裝程式一次的詳細資訊，以及這一次選取**將功能加入至現有的 SQL Server**。

4. 選擇在執行個體，然後選取**R 服務 （資料庫）**選項來加入。

在某些情況下，此程序無法解決問題。 請嘗試下列因應措施：

1. 解除安裝 R 服務 （資料庫） 和 R 伺服器 （獨立），在相同的時間。

2. 移除本機使用者帳戶 (SQLRUserGroup)。

3. 重新啟動伺服器。

4. 執行 SQL Server 安裝程式，並新增 R 服務 （資料庫） 只功能。 請勿選取**R 伺服器 （獨立）**。

## <a name="see-also"></a>另請參閱

 [SQL Server R 服務使用者入門](../r/getting-started-with-sql-server-r-services.md)

 [開始使用 Microsoft R Server 的獨立](../r/getting-started-with-microsoft-r-server-standalone.md)

