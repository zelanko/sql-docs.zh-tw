---
title: "SQL Server 機器學習的升級及安裝常見問題集 |Microsoft 文件"
ms.date: 10/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 001e66b9-6c3f-41b3-81b7-46541e15f9ea
caps.latest.revision: "59"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 3c4fb79f04daeff6d98856b521fa1602a2334cdd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning"></a>SQL Server 機器學習的升級及安裝常見問題集

本主題提供有關機器學習中 SQL Server 功能安裝的一些常見問題的解答。 其中也涵蓋關於升級常見問題的解答。

+ 從發行前版本，只能使用升級會發生一些問題。 因此，我們建議您識別您的版本與版別先再讀取這些資訊。
+ 升級至最新的版本或儘速，服務版本，來解決任何最新版本中已修正的問題。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務 （資料庫）

## <a name="performing-setup-for-the-first-time"></a>第一次執行安裝程式

請依照下列程序設定[!INCLUDE[sscurrent_md](../../includes/sscurrent_md.md)]和 R 元件，如下所示： 

+ [設定 SQL Server R 服務或機器學習服務資料庫](../r/set-up-sql-server-r-services-in-database.md)
+ [設定 SQL Server 2017 使用 Python](../python/setup-python-machine-learning-services.md)
+ [建立獨立 R 伺服器](../r/create-a-standalone-r-server.md)

> [!IMPORTANT]
> 
> 您已安裝 SQL Server 和機器學習功能，才能使用 R 或 Python 指令碼之後，您必須完成一些額外的設定步驟。 這是因為預設不啟用外部指令碼執行功能。

### <a name="requirements-and-restrictions"></a>需求和限制

根據您要安裝的 SQL Server 的組建，下列限制的部分可能適用於：

- 在早期版本的 SQL Server 2016 R 服務，包含的工作目錄的磁碟機上需要 8.3 標記法。 如果您已安裝發行前版本，升級至 SQL Server 2016 Service Pack 1 應可修正此問題。 這項需求不適用於發行之後 SP1。

- 目前，您無法安裝[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]容錯移轉叢集上。 

- 在 Azure VM 中，可能需要一些額外的設定。 例如，您可能需要建立防火牆例外，以支援遠端存取。

- 不支援與另一個版本的 R，或其他來自 Revolution Analytics 的版本來並行安裝。

- 不支援任何 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 發行前版本的新安裝。 如果您使用發行前版本，升級儘速。

- 停用病毒掃描再開始安裝程式。 安裝程式完成之後，我們建議暫停所使用的資料夾上的病毒掃描[!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]。 最好是暫止掃描整個[!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]樹狀目錄中。

### <a name="licensing-agreements-for-unattended-installs"></a>進行自動安裝的授權合約

如果您使用命令列升級的 SQL Server 執行個體時，請確定命令列包含同時[!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]R，並將 Python 的授權合約參數和新的授權合約參數。

### <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server"></a>離線安裝的當地語系化版本的 SQL Server 的機器學習服務元件

當您安裝[!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]機器學習並沒有網際網路存取的電腦上的元件，您必須採取一些額外的步驟：

+ 執行 SQL Server 安裝程式之前，請 R 或 Python 元件安裝程式下載至本機資料夾。
+ 在某些情況下，您可能需要編輯安裝程式檔案，請確認已安裝正確的語言。
+ 機器學習元件所使用的語言識別碼必須是相同的 SQL Server 安裝程式語言，或您無法完成安裝程式。

如需詳細資訊，請參閱[安裝沒有網際網路存取的機器學習元件](../r/installing-ml-components-without-internet-access.md)。

## <a name="post-installation-configuration"></a>後續安裝設定

若要使用 R 或 Python 的機器學習，某些則需要其他組態之後執行 SQL Server 安裝程式。 所需的確切步驟取決於伺服器，以及您如何設定您的 SQL Server 執行個體和資料庫的安全性層級。

檢閱清單中的後續安裝指示，以查看每個額外步驟可能需要您的環境中的所有選項。

+ [設定 SQL Server 機器學習服務資料庫中](set-up-sql-server-r-services-in-database.md) 

## <a name="upgrades-or-uninstallation"></a>升級或解除安裝

本章節包含特定的升級案例的詳細的指示。

### <a name="how-to-upgrade-sql-server"></a>如何將 SQL Server 升級

您可以重新執行安裝程式精靈來升級您的 SQL Server 版本。

+ [升級 SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
+ [使用安裝精靈升級 SQL Server](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

您可以升級機器學習元件服務使用稱為繫結程序： 
+ [使用 SqlBindR 升級機器學習服務元件](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>結束支援從發行前版本的就地升級

不再支援從發行前版本的 SQL Server 2016 的升級。 這包括 SQL Server 2016 CTP3、 CTP3.1、 CTP3.2、 RC0 或 RC1。

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

如果您不的清楚您使用哪一個版本，執行`@@VERSION`從 SQL Server Management Studio 查詢中。

一般情況下，升級程序如下所示：

1. 備份指令碼和資料。
2. 解除安裝發行前版本。
3. 安裝發行版本。

解除安裝發行前版本的 SQL Server 機器學習元件可以很複雜，而可能需要執行特殊的指令碼。 請連絡技術支援部門以尋求協助。

### <a name="support-for-slipstream-upgrades"></a>匯集升級支援

匯集安裝程式是指將補充程式或更新套用至失敗的執行個體安裝，以修正現有問題的功能。 這個方法的優點是，SQL Server 會更新一次您執行安裝程式，避免個別重新啟動更新版本。

如果伺服器沒有網際網路存取，請務必下載 SQL Server 安裝程式。 您也必須在開始更新程序「之前」，另外下載對應的 R 元件安裝程式版本。 

如需下載位置，請參閱[安裝沒有網際網路存取的機器學習元件](installing-ml-components-without-internet-access.md)。

當所有安裝檔案都複製到本機目錄後，在命令列輸入 SETUP.EXE 來啟動安裝公用程式。

- 使用*/UPDATESOURCE*引數來指定包含 SQL Server 更新，例如累計更新或 service pack 發行版本的本機檔案的位置。

- 使用*/MRCACHEDIRECTORY*引數來指定包含 R 元件封包檔的資料夾。

如需詳細資訊，請參閱此部落格由支援小組：[沒有網際網路存取的電腦上部署 R Services](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)。

### <a name="get-machine-learning-components-for-offline-installs"></a>取得機器學習元件進行離線安裝

如果您安裝或升級不會連線到網際網路的伺服器，您必須下載更新的機器學習元件手動開始重新整理之前的版本。 

+ [安裝沒有網際網路存取的機器學習元件](../../advanced-analytics/r/installing-ml-components-without-internet-access.md)。

### <a name="support-policy-and-schedule-for-update-of-machine-learning-components"></a>更新機器學習服務元件的支援原則和排程

Hotfix 或 SQL Server 的增強功能是發行之後，機器學習元件自動升級或重新整理時，您的執行個體已包含的功能。

年 12 月從 2016年開始，您可以升級以更快的步調比 SQL Server 發行週期的機器學習元件。 您只要*繫結*現代軟體生命週期原則的 SQL Server 執行個體。 每當機器學習開發小組所發行的機器學習工具的新版本，您可以下載最新版本，並將它套用到使用機器學習的 SQL Server 執行個體。

如需詳細資訊，請參閱：

+ [適用於 Microsoft R Server 和機器學習 Server 的支援時間表](https://docs.microsoft.com/machine-learning-server/resources-servicing-support)
+ [若要升級的 SQL Server 執行個體使用 SqlBindR](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

## <a name="r-server-standalone"></a>R Server (Standalone)

本章節描述 Microsoft R Server （獨立） 的安裝，請使用 SQL Server 2016 安裝程式的特定問題。 

如需有關從 R 伺服器到機器學習伺服器升級的問題，請參閱[安裝機器學習 Server for Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)。

### <a name="problems-when-r-services-and-r-server-standalone-are-installed-on-the-same-computer"></a>R 服務和 R Server 獨立安裝在同一部電腦上時的問題

在舊版的 SQL Server 2016 中，安裝 R Server （獨立） 和 R 服務 （資料庫） 在相同的時間有時會造成安裝程式失敗並出現 「 拒絕存取 」 訊息。 Service Pack 1 中已修正此問題，SQL Server 2016。

如果您遇到這個錯誤，而且必須升級這些功能，請執行 SQL Server 2016 with SP1 匯集安裝。 有兩種方式來解決問題，這需要解除安裝再重新安裝。

1. 解除安裝 R 服務 （資料庫），並確定 SQLRUserGroup 的使用者帳戶會移除。

2. 重新啟動伺服器，然後再重新安裝 R Server （獨立）。

3. 執行的 SQL Server 安裝程式一次的詳細資訊，以及這一次選取**將功能加入至現有的 SQL Server**。

4. 選擇在執行個體，然後選取**R 服務 （資料庫）**選項來加入。

如果此程序無法解決問題，請嘗試下列因應措施：

1. 解除安裝 R 服務 （資料庫） 和 R 伺服器 （獨立），在相同的時間。

2. 移除本機使用者帳戶 (SQLRUserGroup)。

3. 重新啟動伺服器。

4. 執行 SQL Server 安裝程式，並新增 R 服務 （資料庫） 只功能。 請勿選取**R 伺服器 （獨立）**。

一般而言，我們建議請勿安裝 R 服務 （資料庫） 和 R 伺服器 （獨立） 在相同電腦上。 不過，假設伺服器有足夠的容量，您可能會發現 R 伺服器獨立可能會很有用的開發工具。 另一個可能的情況是，您需要使用實施 R Server 功能，但也想要存取不需要移動資料的 SQL Server 資料。

## <a name="see-also"></a>另請參閱

 [SQL Server R 服務使用者入門](../r/getting-started-with-sql-server-r-services.md)

 [開始使用 Microsoft R Server 的獨立](../r/getting-started-with-microsoft-r-server-standalone.md)
