---
title: SQL Server 機器學習的升級及安裝常見問題集 |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 52ff43f13ff3f17f21ed96313d3134d8ee31dd86
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
ms.locfileid: "31204210"
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>SQL Server 機器學習或 R Server 升級及安裝常見問題集
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本主題提供有關機器學習中 SQL Server 功能安裝的一些常見問題的解答。 其中也涵蓋關於升級常見問題的解答。

+ 從發行前版本，只能使用升級會發生一些問題。 因此，我們建議您識別您的版本與版別先再讀取這些資訊。 若要取得版本資訊，請執行`@@VERSION`從 SQL Server Management Studio 查詢中。
+ 升級至最新的版本或儘速，服務版本，來解決任何最新版本中已修正的問題。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務 （資料庫）

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>需求和在舊版的 SQL Server 2016 上的限制 

根據您要安裝的 SQL Server 的組建，下列限制的部分可能適用於：

- 在早期版本的 SQL Server 2016 R 服務，包含的工作目錄的磁碟機上需要 8.3 標記法。 如果您已安裝發行前版本，升級至 SQL Server 2016 Service Pack 1 應可修正此問題。 這項需求不適用於發行之後 SP1。

- 不支援與另一個版本的 R，或其他來自 Revolution Analytics 的版本來並行安裝。

- 停用病毒掃描再開始安裝程式。 安裝程式完成之後，我們建議暫停所使用的資料夾上的病毒掃描[!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]。 最好是暫止掃描整個[!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]樹狀目錄中。

 - Windows Core 上安裝 SQL Server 執行個體上安裝 Microsoft R Server。 在 SQL Server 2016 RTM 版本中，時的已知的問題 Microsoft R Server 新增至 Windows Server Core 版本上執行個體。 這個問題已經修正。 如果您遇到此問題，您可以將套用所述的修正[KB3164398](https://support.microsoft.com/kb/3164398)將 R 功能新增至 Windows Server Core 上的現有執行個體。 如需詳細資訊，請參閱 [無法在 Windows Server Core 作業系統上安裝 Microsoft R 伺服器 (獨立式)](https://support.microsoft.com/kb/3168691)。


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>離線安裝的當地語系化版本的 SQL Server 2016 的機器學習服務元件

早期發行版本的 SQL Server 2016 無法在沒有網際網路連線的離線安裝期間安裝的地區設定特定的.cab 檔。 在更新版本，已修正此問題，但如果安裝程式會傳回訊息，指出它無法安裝正確的語言，您可以編輯的檔案名稱，以允許安裝程式才能繼續。

+ 手動編輯安裝程式檔案，以確保已安裝正確的語言。 例如，若要安裝日文版的 SQL Server，您會變更檔案的名稱從 SRS_8.0.3.0_**1033年**SRS_8.0.3.0_ 的.cab**1041年**.cab。
+ 機器學習元件所使用的語言識別碼必須是相同的 SQL Server 安裝程式語言，或您無法完成安裝程式。

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>發行前版本： 支援原則、 升級和已知的問題

新安裝的任何發行前版本的[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]不再支援。 如果您使用發行前版本，升級儘速。

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

| 版本 | 建置         |
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

###  <a name="bkmk_Uninstall"></a> 解除安裝然後再從較舊版本的 Microsoft R Server 升級

如已安裝 Microsoft R Server 發行前版本，您必須先解除安裝它，才能升級至較新版本。

1.  在 [控制台] 中，按一下 [新增/移除程式] 並選取 [ `Microsoft SQL Server 2016 <version number>`]。

2.  在有 [新增] 、[修復] 或 [移除]  元件選項的對話方塊中，選取 [移除] 。
  
3.  在 [選取功能]  頁面下的 [共用功能] 中，選取 [R Server (獨立式)] 。 按一下 [下一步] ，然後按一下 [完成]  只解除安裝選取的元件。

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>R 服務和 R 伺服器 （獨立） 的並行錯誤 

在舊版的 SQL Server 2016 中，安裝 R Server （獨立） 和 R 服務 （資料庫） 在相同的時間有時會造成安裝程式失敗並出現 「 拒絕存取 」 訊息。 Service Pack 1 中已修正此問題，SQL Server 2016。

如果您遇到這個錯誤，而且必須升級這些功能，請執行 SQL Server 2016 with SP1 匯集安裝。 有兩種方式來解決問題，這需要解除安裝再重新安裝。

1. 解除安裝 R 服務 （資料庫），並確定 SQLRUserGroup 的使用者帳戶會移除。

2. 重新啟動伺服器，然後再重新安裝 R Server （獨立）。

3. 執行的 SQL Server 安裝程式一次的詳細資訊，以及這一次選取**將功能加入至現有的 SQL Server**。

4. 選擇在執行個體，然後選取**R 服務 （資料庫）** 選項來加入。

如果此程序無法解決問題，請嘗試下列因應措施：

1. 解除安裝 R 服務 （資料庫） 和 R 伺服器 （獨立），在相同的時間。

2. 移除本機使用者帳戶 (SQLRUserGroup)。

3. 重新啟動伺服器。

4. 執行 SQL Server 安裝程式，並新增 R 服務 （資料庫） 只功能。 請勿選取**R 伺服器 （獨立）**。

一般而言，我們建議請勿安裝 R 服務 （資料庫） 和 R 伺服器 （獨立） 在相同電腦上。 不過，假設伺服器有足夠的容量，您可能會發現 R 伺服器獨立可能會很有用的開發工具。 另一個可能的情況是，您需要使用實施 R Server 功能，但也想要存取不需要移動資料的 SQL Server 資料。

## <a name="incompatible-version-of-r-client-and-r-server"></a>不相容的 R Client 及 R Server 版本

如果您安裝 Microsoft R 用戶端，並使用它來執行 R 遠端的 SQL Server 計算內容中，您可能會收到如下錯誤：

*您正在 Microsoft R 用戶端版本 9.0.0 您與 Microsoft R Server 8.0.3 版本不相容的電腦。請下載並安裝相容版本。*

在 SQL Server 2016 中，所需的 SQL Server R 服務正在執行的 R 版本會完全與 Microsoft R 用戶端中的程式庫相同。 在新版中已移除這項需求。 不過，我們建議您一律取得最新版的機器學習的元件，並安裝所有 service pack。 

如果您有舊版的 Microsoft R Server，而且需要以確保相容性與 Microsoft R 用戶端 9.0.0，安裝所述的更新，在這個[技術支援文件](https://support.microsoft.com/kb/3210262)。


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>安裝失敗，錯誤為「一次只能安裝一項 Revolution Enterprise 產品。」

如已安裝舊版的 Revolution Analytics 產品或 SQL Server R Services 的發行前版本，您可能會遇到這個錯誤。 您必須先解除安裝任何舊版本，才能安裝較新版的 Microsoft R Server。 不支援與其他版本的 Revolution Enterprise 工具並存安裝。

不過，使用獨立式 R Server 搭配 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 或 SQL Server 2016 時，則支援並存安裝。

## <a name="registry-cleanup-to-uninstall-older-components"></a>若要解除安裝舊元件的登錄清除

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

 [SQL Server 機器學習服務 （資料庫）](../r/sql-server-r-services.md)

 [SQL Server 機器學習服務伺服器 （獨立）](../r/r-server-standalone.md)
