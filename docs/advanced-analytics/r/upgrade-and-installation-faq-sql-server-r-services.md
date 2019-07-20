---
title: 升級及安裝常見問題 (FAQ)
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
ms.author: davidph
author: dphansen
ms.openlocfilehash: 71a6149f1d89a4a1df114f376c250c203a8721cf
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344905"
---
# <a name="upgrade-and-installation-faq-for-sql-server-machine-learning-or-r-server"></a>SQL Server Machine Learning 或 R Server 的升級和安裝常見問題
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本主題提供有關在 SQL Server 中安裝機器學習功能的一些常見問題解答。 其中也涵蓋升級的相關常見問題。

+ 只有在從發行前版本升級時, 才會發生一些問題。 因此, 建議您先找出版本和版本, 再閱讀這些筆記。 若要取得版本資訊, `@@VERSION`請在 SQL Server Management Studio 的查詢中執行。
+ 儘快升級至最新的版本或服務版本, 以解決最近版本中已修正的任何問題。

**適用於：** SQL Server 2016 R Services, SQL Server 2017 Machine Learning 服務 (資料庫內)

## <a name="requirements-and-restrictions-on-older-versions-of-sql-server-2016"></a>舊版 SQL Server 2016 的需求和限制 

根據您要安裝的 SQL Server 組建而定, 可能會有下列一些限制:

- 在舊版的 SQL Server 2016 R Services 中, 包含工作目錄的磁片磁碟機上必須要有8.3 標記法。 如果您已安裝發行前版本, 升級至 SQL Server 2016 Service Pack 1 應該可以修正此問題。 這項需求不適用於 SP1 之後的版本。

- 目前, 您無法在[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]容錯移轉叢集上安裝。 不過, 如果您想要在測試環境中評估這項功能, SQL Server 2019 preview 會提供容錯移轉支援。 如需詳細資訊, 請參閱[新功能](../what-s-new-in-sql-server-machine-learning-services.md)。

- 在 Azure VM 上, 可能需要進行一些額外的設定。 例如, 您可能需要建立防火牆例外, 以支援遠端存取。

- 不支援與其他版本的 R 並存安裝, 或與革命分析的其他發行並存。

- 開始安裝之前, 請先停用病毒掃描。 安裝完成之後, 建議您在所使用[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]的資料夾上暫停病毒掃描。 最好是暫停整個[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]樹狀結構上的掃描。

 - 在安裝于 Windows Core 上 SQL Server 的實例上安裝 Microsoft R Server。 在 SQL Server 2016 的 RTM 版本中, 將 Microsoft R Server 新增至 Windows Server Core 版本上的實例時, 有一個已知的問題。 這個問題已經修正。 如果您遇到這個問題, 您可以套用[KB3164398](https://support.microsoft.com/kb/3164398)中所述的修正程式, 將 R 功能新增至 Windows Server Core 上的現有實例。 如需詳細資訊，請參閱 [無法在 Windows Server Core 作業系統上安裝 Microsoft R 伺服器 (獨立式)](https://support.microsoft.com/kb/3168691)。


## <a name="offline-installation-of-machine-learning-components-for-a-localized-version-of-sql-server-2016"></a>SQL Server 2016 的當地語系化版本之機器學習元件的離線安裝

SQL Server 2016 的早期發行版本無法在離線安裝期間 (沒有網際網路連線) 安裝地區設定特定的 .cab 檔案。 此問題已在更新的版本中修正, 但如果安裝程式傳回的訊息指出無法安裝正確的語言, 您可以編輯檔案名, 以允許安裝程式繼續進行。

+ 手動編輯安裝程式檔案, 以確保已安裝正確的語言。 例如, 若要安裝日文版的 SQL Server, 您可以將檔案的名稱從 SRS_ 8.0.3.0 _**1033**變更為 srs_ 8.0.3.0 _**1041**.cab。
+ 用於機器學習元件的語言識別項必須與 SQL Server 安裝程式語言相同, 否則您無法完成安裝程式。

## <a name="pre-release-versions-support-policies-upgrade-and-known-issues"></a>發行前版本: 支援原則、升級和已知問題

已不再支援任何發行前版本的[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]新安裝。 如果您使用的是發行前版本, 請儘快升級。

本節包含特定升級案例的詳細指示。

### <a name="how-to-upgrade-sql-server"></a>如何升級 SQL Server

您可以重新執行安裝程式, 以升級您的 SQL Server 版本。

+ [升級 SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)
+ [使用安裝精靈升級 SQL Server](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

您可以使用稱為「系結」的程式來僅升級機器學習元件: 
+ [使用 SqlBindR 升級機器學習服務元件](../install/upgrade-r-and-python.md)

### <a name="end-of-support-for-in-place-upgrades-from-prerelease-versions"></a>終止發行前版本的就地升級支援

不再支援從 SQL Server 2016 的發行前版本進行升級。 這包括 SQL Server 2016 CTP3、CTP 3.1、CTP 3.2、RC0 或 RC1。

下列版本已與 SQL Server 2016 的發行前版本一起安裝。

| 版本 | 建置         |
|---------|---------------|
| CTP 3.0 | 13.0.xxx      |
| CTP 3.1 | 13.0.801.12   |
| CTP 3.2 | 13.0.900.73   |
| CTP 3.3 | 13.0.1000.281 |
| RC1     | 13.0.1200.242 |
| RC2     | 13.0.1300.275 |
| RC3     | 13.0.1400.361 |

如果您不確定所使用的版本, 請在 SQL Server Management Studio 的`@@VERSION`查詢中執行。

一般來說, 升級的程式如下所示:

1. 備份腳本和資料。
2. 卸載發行前版本。
3. 安裝發行版本。

卸載 SQL Server 機器學習元件的發行前版本可能很複雜, 而且可能需要執行特殊的腳本。 請連絡技術支援部門以尋求協助。

###  <a name="bkmk_Uninstall"></a>從舊版的 Microsoft R Server 升級之前卸載

如已安裝 Microsoft R Server 發行前版本，您必須先解除安裝它，才能升級至較新版本。

1.  在 [控制台]  中，按一下 [新增/移除程式]  並選取 [ `Microsoft SQL Server 2016 <version number>`]。

2.  在有 [新增]  、[修復]  或 [移除]  元件選項的對話方塊中，選取 [移除]  。
  
3.  在 [選取功能]  頁面下的 [共用功能]  中，選取 [R Server (獨立式)]  。 按一下 [下一步]  ，然後按一下 [完成]  只解除安裝選取的元件。

## <a name="r-services-and-r-server-standalone-side-by-side-errors"></a>R Services 和 R Server (獨立式) 並存錯誤 

在舊版的 SQL Server 2016 中, 同時安裝 R Server (獨立式) 和 R Services (資料庫內) 時, 有時會導致安裝程式失敗並出現「拒絕存取」訊息。 此問題已在 Service Pack 1 中針對 SQL Server 2016 修正。

如果您遇到這個錯誤, 而且需要升級這些功能, 請執行 SQL Server 2016 SP1 的彙集安裝。 有兩種方式可以解決此問題, 這兩種方法都需要卸載和重新安裝。

1. 將 R Services (資料庫內) 卸載, 並確定已移除 SQLRUserGroup 的使用者帳戶。

2. 重新開機伺服器, 然後重新安裝 R Server (獨立式)。

3. 再執行一次 SQL Server 安裝程式, 這次請選取 [**將功能加入到現有 SQL Server**]。

4. 選擇實例, 然後選取 [ **R Services (資料庫內)** ] 選項來加入。

如果此程式無法解決問題, 請嘗試下列因應措施:

1. 同時卸載 R Services (資料庫內) 和 R 伺服器 (獨立式)。

2. 移除本機使用者帳戶 (SQLRUserGroup)。

3. 重新啟動伺服器。

4. 執行 SQL Server 安裝程式, 並只新增 R Services (資料庫內) 功能。 請勿選取 **[R Server (獨立式)** ]。

一般來說, 我們建議您不要在同一部電腦上同時安裝 R Services (資料庫內) 和 R 伺服器 (獨立式)。 不過, 假設伺服器有足夠的容量, 您可能會發現 R Server 獨立式可能做為開發工具。 另一個可能的情況是, 您必須使用 R Server 的運算化功能, 但也想要存取 SQL Server 資料, 而不需要移動資料。

## <a name="incompatible-version-of-r-client-and-r-server"></a>不相容的 R Client 及 R Server 版本

如果您安裝 Microsoft R Client 並使用它在遠端 SQL Server 計算內容中執行 R, 您可能會收到類似下面的錯誤:

*您的電腦上執行的 Microsoft R client 版本為 9.0.0, 與 Microsoft R Server 版本8.0.3 版不相容。請下載並安裝相容版本。*

在 SQL Server 2016 中, 在 SQL Server R Services 中執行的 R 版本, 必須與 Microsoft R Client 中的程式庫完全相同。 該需求已在較新版本中移除。 不過, 我們建議您一律取得最新版本的機器學習服務元件, 並安裝所有 service pack。 

如果您有舊版的 Microsoft R Server, 而且需要確保與 Microsoft R Client 9.0.0 的相容性, 請安裝此[支援文章](https://support.microsoft.com/kb/3210262)中所述的更新。


## <a name="installation-fails-with-error-only-one-revolution-enterprise-product-can-be-installed-at-a-time"></a>安裝失敗，錯誤為「一次只能安裝一項 Revolution Enterprise 產品。」

如已安裝舊版的 Revolution Analytics 產品或 SQL Server R Services 的發行前版本，您可能會遇到這個錯誤。 您必須先解除安裝任何舊版本，才能安裝較新版的 Microsoft R Server。 不支援與其他版本的 Revolution Enterprise 工具並存安裝。

不過，使用獨立式 R Server 搭配 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 或 SQL Server 2016 時，則支援並存安裝。

## <a name="registry-cleanup-to-uninstall-older-components"></a>用來卸載舊版元件的登錄清除

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

 [SQL Server Machine Learning 服務 (資料庫內)](../r/sql-server-r-services.md)

 [SQL Server Machine Learning Server (獨立式)](../r/r-server-standalone.md)
