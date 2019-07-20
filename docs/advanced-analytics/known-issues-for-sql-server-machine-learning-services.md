---
title: R 語言和 Python 整合的已知問題
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 547a567b00474f0c1538d907d70d8a808bebf851
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344938"
---
# <a name="known-issues-in-machine-learning-services"></a>Machine Learning 服務中的已知問題
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明在使用 R 和 Python [SQL Server 2016 R services](install/sql-r-services-windows-install.md)和[SQL Server 2017 Machine Learning 服務](install/sql-machine-learning-services-windows-install.md)中提供的機器學習服務元件已知問題或限制。

## <a name="setup-and-configuration-issues"></a>安裝和設定問題

如需與初始安裝和設定相關的處理常式和常見問題的說明, 請參閱[升級和安裝常見問題](r/upgrade-and-installation-faq-sql-server-r-services.md)。 其中包含升級、並存安裝, 以及安裝新的 R 或 Python 元件的相關資訊。

### <a name="1-inconsistent-results-in-mkl-computations-due-to-missing-environment-variable"></a>1.因為遺失環境變數而導致的 MKL 計算不一致

**適用於：** R_SERVER 二進位檔9.0、9.1、9.2 或9.3。

R_SERVER 使用 Intel 數學核心程式庫 (MKL)。 對於涉及 MKL 的計算, 如果您的系統遺失環境變數, 可能會產生不一致的結果。 

設定環境變數`'MKL_CBWR'=AUTO` , 以確保 R_SERVER 中的條件式數值重現性。 如需詳細資訊, 請參閱[條件式數值重現性 (CNR) 簡介](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)。

**因應措施**

1. 在 [控制台] 中, 按一下 [**系統及安全性** > **系統** > ] [系統**設定** > ] [**環境變數**]。

2. 建立新的使用者或系統變數。 

  + 將 [變數名稱] 設定為 ' MKL_CBWR '。
  + 將 [變數值] 設定為 [自動]。

3. 重新開機 R_SERVER。 在 SQL Server 上, 您可以重新開機 SQL Server Launchpad 服務。

> [!NOTE]
> 如果您在 Linux 上執行 SQL Server 2019 Preview, 請在使用者的主目錄中編輯或建立*bash_profile* , 並新增這`export MKL_CBWR="AUTO"`一行。 在 bash 命令提示字元`source .bash_profile`中輸入來執行此檔案。 在 R 命令提示`Sys.getenv()`字元中輸入, 以重新開機 R_SERVER。

### <a name="2-r-script-runtime-error-sql-server-2017-cu5-cu7-regression"></a>2.R 腳本執行階段錯誤 (SQL Server 2017 CU5-CU7 回歸)

針對 SQL Server 2017, 在累計更新5到7中, **rlauncher**中的臨時目錄檔案路徑包含空格的回歸。 這個回歸會在 CU8 中修正。

執行 R 腳本時, 您會看到的錯誤包含下列訊息:

> *無法與 ' R ' 腳本的執行時間通訊。請檢查 ' R ' 執行時間的需求。*
>
> 來自外部腳本的 STDERR 訊息: 
>
> *嚴重錯誤: 無法建立 ' R_TempDir '*

**因應措施**

當 CU8 可供使用時, 將其套用。 或者, 您也可以在提升許可權的命令提示字元上執行**registerrext.exe** , 以重新建立**rlauncher。** 

```cmd
<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /uninstall /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>

<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /install /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>
```

下列範例顯示具有預設實例 "MSSQL14." 的命令。MSSQLSERVER "已安裝到" C:\Program Files\Microsoft\"SQL Server:

```cmd
"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /uninstall /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER

"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /install /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER
```

### <a name="3-unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>3.無法在網域控制站上安裝 SQL Server 機器學習功能

如果您嘗試在網域控制站上安裝 SQL Server 2016 R Services 或 SQL Server 2017 Machine Learning 服務, 安裝程式會失敗, 並出現下列錯誤:

> *功能的安裝過程中發生錯誤*
> 
> *找不到具有身分識別的群組*
> 
> *元件錯誤碼:0x80131509*

發生失敗的原因是, 在網域控制站上, 服務無法建立執行機器學習所需的20個本機帳戶。 一般而言, 我們不建議您在網域控制站上安裝 SQL Server。 如需詳細資訊, 請參閱[支援公告 2032911](https://support.microsoft.com/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont)。

### <a name="4-install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>4.安裝最新的服務版本以確保與 Microsoft R Client 的相容性

如果您安裝最新版本的 Microsoft R Client, 並使用它在遠端計算內容的 SQL Server 上執行 R, 您可能會收到類似下列的錯誤:

> *您的電腦上執行的 Microsoft R Client 版本為 6.x, 這與 Microsoft R Server 版本8不相容。 x.x。請下載並安裝相容版本。*

SQL Server 2016 要求用戶端上的 R 程式庫必須完全符合伺服器上的 R 程式庫。 已移除比 R Server 9.0.1 更早版本的限制。 不過, 如果您遇到這個錯誤, 請確認用戶端和伺服器所使用的 R 程式庫版本, 並視需要更新用戶端以符合伺服器版本。

當安裝 SQL Server 服務版本時, 會更新隨 SQL Server R Services 安裝的 R 版本。 若要確保您一律擁有最新版本的 R 元件, 請務必安裝所有 service pack。

若要確保與 Microsoft R Client 9.0.0 相容, 請安裝此[支援文章](https://support.microsoft.com/kb/3210262)中所述的更新。

若要避免 R 封裝發生問題, 您也可以將服務協定變更為使用新式生命週期支援原則, 藉此升級安裝在伺服器上的 R 程式庫版本, 如下一[節](#bkmk_sqlbindr)所述。 當您這麼做時, 隨 SQL Server 安裝的 R 版本會依照 machine Learning Server (先前稱為 Microsoft R Server) 更新所用的相同排程進行更新。

**適用於：** 使用 R Server 9.0.0 版或更早版本的 SQL Server 2016 R Services

### <a name="5-r-components-missing-from-cu3-setup"></a>5.CU3 安裝程式遺失 R 元件

已布建有限數量的 Azure 虛擬機器, 但不含應包含在 SQL Server 中的 R 安裝檔案。 此問題適用于從2018-01-05 到2018-01-23 的期間布建的虛擬機器。 如果您已在2018-01-05 到2018-01-23 期間套用 SQL Server 2017 的 CU3 更新, 此問題可能也會影響內部部署安裝。

已提供服務發行, 其中包含正確版本的 R 安裝檔案。

+ [SQL Server 2017 KB4052987 的累計更新套件 3](https://www.microsoft.com/download/details.aspx?id=56128)。

若要安裝元件並修復 SQL Server 2017 CU3, 您必須卸載 CU3, 然後重新安裝更新的版本:

1. 下載更新的 CU3 安裝檔案, 其中包含 R 安裝程式。
2. 卸載 CU3。 在 [控制台] 中, 搜尋 [**卸載更新**], 然後選取 [適用于 SQL Server 2017 (KB4052987) (64-bit) 的修補程式 3015]。 繼續進行卸載步驟。
3. 按兩下您剛才下載的 KB4052987 更新, 重新安裝 CU3 更新: `SQLServer2017-KB4052987-x64.exe`。 遵循安裝指示進行。

### <a name="6-unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>6.無法在 SQL Server 2017 CTP 2.0 或更新版本的離線安裝中安裝 Python 元件

如果您在沒有網際網路存取的電腦上安裝 SQL Server 2017 的發行前版本, 安裝程式可能無法顯示提示您所下載 Python 元件位置的頁面。 在這種情況下, 您可以安裝 Machine Learning Services 功能, 而不是 Python 元件。

發行版本已修正此問題。 此外, 這項限制並不適用于 R 元件。

**適用於：** 使用 Python SQL Server 2017

### <a name="bkmk_sqlbindr"></a>當您使用從用戶端連接到舊版的 SQL Server R Services 時, 出現不相容版本的警告[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

當您在 SQL Server 2016 計算內容中執行 R 程式碼時, 您可能會看到下列錯誤:

> *您電腦上執行的是 9.0.0 版的 Microsoft R Client，與 Microsoft R Server 8.0.3 版不相容。請下載並安裝相容版本。*

如果下列兩個語句的其中一個為 true, 則會顯示此訊息。

+ 您已使用的安裝程式[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)], 在用戶端電腦上安裝 R Server (獨立式)。
+ 您已使用[個別的 Windows installer](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)來安裝 Microsoft R Server。

為確保伺服器和用戶端使用相同的版本, 您可能需要使用支援  Microsoft R server 9.0 和更新版本的系結, 以升級 SQL Server 2016 實例中的 R 元件。 若要判斷您的 R Services 版本是否有支援升級, 請參閱[使用 SqlBindR 升級 R services 的實例](install/upgrade-r-and-python.md)。

**適用於：** 使用 R Server 9.0.0 版或更早版本的 SQL Server 2016 R Services

### <a name="7-setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>7.SQL Server 2016 服務版本的安裝程式可能無法安裝較新版本的 R 元件

當您在未連線到網際網路的電腦上安裝累積更新或安裝 SQL Server 2016 的 Service Pack 時, 安裝精靈可能無法顯示提示, 讓您使用下載的 CAB 檔案來更新 R 元件。 當多個元件與資料庫引擎一起安裝時, 通常會發生此失敗。

因應措施是, 您可以使用命令列來安裝服務版本, 並指定`MRCACHEDIRECTORY`引數, 如下列範例所示, 這會安裝 CU1 更新:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

若要取得最新的安裝程式, 請參閱[安裝沒有網際網路存取的機器學習服務元件](install/sql-ml-component-install-without-internet-access.md)。

**適用於：** 使用 R Server 9.0.0 版或更早版本的 SQL Server 2016 R Services

### <a name="8-launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>8.如果版本與 R 版本不同, 則啟動列服務無法啟動

如果您從 database engine 分別安裝 SQL Server R Services, 且組建版本不同, 您可能會在系統事件記錄檔中看到下列錯誤:

> *SQL Server Launchpad 服務無法啟動, 因為發生下列錯誤:服務並未及時回應啟動或控制要求。*

例如, 如果您使用發行版本安裝 database engine、套用修補程式升級 database engine, 然後使用發行版本加入 R Services 功能, 就可能會發生這個錯誤。

若要避免這個問題, 請使用 [檔案管理員] 之類的公用程式來比較啟動列的版本與 SQL 二進位檔的版本, 例如 sqldk。 所有元件都應該具有相同的版本號碼。 如果升級某個元件，所有其他已安裝的元件請務必套用相同的升級。

在實例的`Binn`資料夾中尋找 [啟動列]。 例如, 在 SQL Server 2016 的預設安裝中, 路徑可能是`C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn`。 

### <a name="9-remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>9.在 Azure 虛擬機器上執行的 SQL Server 實例中, 防火牆封鎖了遠端計算內容

如果您已在[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Windows Azure 虛擬機器上安裝, 您可能無法使用需要使用虛擬機器工作區的計算內容。 原因是, 根據預設, Azure 虛擬機器上的防火牆包含封鎖本機 R 使用者帳戶網路存取的規則。

因應措施是在 Azure VM 上, 開啟 [**具有 Advanced Security 的 Windows 防火牆**], 選取 [**輸出規則**], 然後停用下列規則:**封鎖 SQL Server 實例 MSSQLSERVER 中 R 本機使用者帳戶的網路存取**。 您也可以讓規則保持啟用狀態, 但是將 [安全性] 屬性變更為 [**允許安全**]。

### <a name="10-implied-authentication-in-sqlexpress"></a>10.SQLEXPRESS 的隱含驗證

當您使用整合式 Windows 驗證從遠端資料科學工作站執行 R 作業時, SQL Server 會使用*隱含驗證*來產生腳本可能需要的任何本機 ODBC 呼叫。 不過，這項功能在 SQL Server Express Edition 的 RTM 組建中不作用。

若要修正此問題，建議您升級至較新的服務版本。

如果升級不可行, 請使用 SQL 登入來執行可能需要內嵌 ODBC 呼叫的遠端 R 作業。

**適用於：** SQL Server 2016 R Services Express Edition

### <a name="11-performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>11.從其他工具呼叫 SQL Server 所使用的程式庫時的效能限制

您可以從外部應用程式 (例如 Rgui.exe) 呼叫針對 SQL Server 所安裝的機器學習程式庫。 這麼做可能是完成某些工作最方便的方式, 例如安裝新的封裝, 或在非常短的程式碼範例上執行臨機操作測試。 不過, 在 SQL Server 外部, 效能可能會受到限制。 

例如, 即使您使用的是 Enterprise Edition 的 SQL Server, 當您使用外部工具執行 R 程式碼時, R 也會在單一執行緒模式下執行。 若要取得 SQL Server 中效能的優點, 請起始 SQL Server 連接, 並使用[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)來呼叫外部腳本執行時間。

一般來說, 請避免呼叫來自外部工具的 SQL Server 所使用的機器學習程式庫。 如果您需要 debug R 或 Python 程式碼, 通常可以在 SQL Server 之外輕鬆執行此動作。 若要取得 SQL Server 中相同的程式庫, 您可以安裝 Microsoft R Client、 [SQL Server 2017 Machine Learning Server (獨立式)](install/sql-machine-learning-standalone-windows-install.md)或[SQL Server 2016 R Server (獨立式)](install/sql-r-standalone-windows-install.md)。

### <a name="12-sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>12.SQL Server Data Tools 不支援外部腳本所需的許可權

當您使用 Visual Studio 或 SQL Server Data Tools 來發行資料庫專案時, 如果有任何主體具有外部腳本執行的特定許可權, 您可能會收到類似下面的錯誤:

> *TSQL 模型:對資料庫進行反向工程時偵測到錯誤。無法辨識許可權, 且未匯入。*

DACPAC 模型目前不支援 R Services 或 Machine Learning 服務所使用的許可權, 例如授與任何外部腳本, 或執行任何外部腳本。 未來版本會修正此問題。

因應措施是在部署後腳本中執行其他 GRANT 語句。

### <a name="13-external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>13.外部腳本執行因為資源治理預設值而受到節流

在 Enterprise Edition 中，您可以使用資源集區來管理外部指令碼程序。 在某些早期發行組建中, 可以配置給 R 進程的記憶體上限為 20%。 因此, 如果伺服器有 32 GB 的 RAM, R 可執行檔 (RTerm 和 BxlServer) 在單一要求中最多可以使用 6.4 GB。

如果您遇到資源限制, 請檢查目前的預設值。 如果 20% 不夠, 請參閱的檔以[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]瞭解如何變更此值。

**適用於：** SQL Server 2016 R 服務, Enterprise Edition

## <a name="r-script-execution-issues"></a>R 腳本執行問題

本節包含在 SQL Server 上執行 R 的特定已知問題, 以及與 Microsoft 所發佈的 R 程式庫和工具相關的一些問題, 包括 RevoScaleR。

如需可能會影響 R 解決方案的其他已知問題, 請參閱[Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues)網站。

### <a name="1-access-denied-warning-when-executing-r-scripts-on-sql-server-in-a-non-default-location"></a>1.在非預設位置的 SQL Server 上執行 R 腳本時, 發生拒絕存取的警告

如果 SQL Server 的實例已安裝到非預設位置 (例如在`Program Files`資料夾外部), 則當您嘗試執行安裝套件的腳本時, 就會引發警告 ACCESS_DENIED。 例如:

> *在`normalizePath(path.expand(path), winslash, mustWork)`中: 路徑 [2] = "~ ExternalLibraries/R/8/1":拒絕存取*

原因是 R 函數嘗試讀取路徑, 而且如果內建的使用者群組**SQLRUserGroup**沒有讀取權限, 就會失敗。 引發的警告不會封鎖目前 R 腳本的執行, 但每當使用者執行任何其他 R 腳本時, 警告可能會重複發生。

如果您已將 SQL Server 安裝到預設位置, 則不會發生此錯誤, 因為所有 Windows 使用者都擁有資料夾的`Program Files`讀取權限。

這個問題是在即將推出的服務版本中解決。 因應措施是為群組**SQLRUserGroup**提供所有父資料夾的`ExternalLibraries`讀取存取權。

### <a name="2-serialization-error-between-old-and-new-versions-of-revoscaler"></a>2.舊版和新版本的 RevoScaleR 之間的序列化錯誤

當您使用序列化格式將模型傳遞至遠端 SQL Server 實例時, 可能會收到錯誤: 

> *MemDecompress (2) 中的 memDecompress (資料, 類型 = 解壓縮) 內部錯誤發生錯誤。*

如果您使用最新版本的序列化函數[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)來儲存模型, 就會引發此錯誤, 但您還原序列化模型的 SQL Server 實例具有舊版 RevoScaleR api (從 SQL SERVER 2017 CU2 或更早版本)。

因應措施是, 您可以將 SQL Server 2017 實例升級為 CU3 或更新版本。

如果 API 版本相同, 或如果您要將使用較舊序列化函式儲存的模型移至使用較新版本之序列化 API 的伺服器, 則不會出現此錯誤。

換句話說, 針對序列化和還原序列化作業, 請使用相同版本的 RevoScaleR。

### <a name="3-real-time-scoring-does-not-correctly-handle-the-learningrate-parameter-in-tree-and-forest-models"></a>3.即時計分無法正確處理樹狀結構和樹系模型中的_learningRate_參數

如果您使用決策樹或決策樹系方法建立模型, 並指定學習速率, 則使用`sp_rxpredict`或 SQL `PREDICT`函數時可能會看到不一致的結果, 相較于`rxPredict`使用。

原因是 API 中處理序列化模型的錯誤, 而且僅限於`learningRate`參數: 例如, 在[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)中, 或

此問題會在即將推出的服務版本中解決。

### <a name="4-limitations-on-processor-affinity-for-r-jobs"></a>4.R 作業處理器相似性的限制

在 SQL Server 2016 的初始版本組建中, 您只能針對第一個 k 群組中的 Cpu 設定處理器親和性。 例如, 如果伺服器是具有兩個 k 群組的2通訊端機器, 則 R 進程只會使用第一個 k 群組中的處理器。 當您設定 R 腳本作業的資源管理時, 也適用相同的限制。

SQL Server 2016 Service Pack 1 已修正這個問題。 我們建議您升級至最新的服務版本。

**適用於：** SQL Server 2016 R Services RTM 版本

### <a name="5-changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>5.讀取 SQL Server 計算內容中的資料，無法變更資料行類型。

如果您的計算內容設為 SQL Server 執行個體，則您無法使用 _colClasses_ 引數 (或其他類似的引數) 來變更 R 程式碼中的資料行資料類型。

例如，如果資料行 CRSDepTimeStr 還不是整數，則下列陳述式會產生錯誤︰

```R
data <- RxSqlServerData(
  sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall", 
  connectionString = connectionString, 
  colClasses = c(CRSDepTimeStr = "integer"))
```

因應措施是, 您可以重寫 SQL 查詢以使用 CAST 或 CONVERT, 並使用正確的資料類型將資料呈現給 R。 一般而言, 當您使用 SQL 來處理資料, 而不是變更 R 程式碼中的資料時, 效能會更好。

**適用於：** SQL Server 2016 R Services

### <a name="6-limits-on-size-of-serialized-models"></a>6.序列化模型的大小限制

當您將模型儲存至 SQL Server 資料表時, 您必須序列化模型, 並將它儲存為二進位格式。 理論上, 可以使用這個方法來儲存的模型大小上限為 2 GB, 這是 SQL Server 中 Varbinary 資料行的大小上限。

如果您需要使用較大的模型, 有下列因應措施:

+ 採取步驟來減少模型的大小。 某些開放原始碼 R 套件在模型物件中包含大量資訊, 而這項資訊大部分都可以移除以供部署。 
+ 使用特徵選取來移除不必要的資料行。
+ 如果您使用的是開放原始碼演算法, 請考慮使用 MicrosoftML 或 RevoScaleR 中的對應演算法來執行類似的程式。 這些套件已針對部署案例進行優化。
+ 在模型已合理化, 且使用上述步驟縮減大小之後, 請查看是否可以使用基底 R 中的[memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress)函式來減少模型的大小, 然後再將它傳遞給 SQL Server。 當模型接近 2 GB 限制時, 此選項最適合。
+ 對於較大的模型, 您可以使用 SQL Server [FileTable](../relational-databases/blob/filetables-sql-server.md)功能來儲存模型, 而不是使用 Varbinary 資料行。

    若要使用 Filetable, 您必須新增防火牆例外, 因為儲存在 Filetable 中的資料是由 SQL Server 中的 Filestream filesystem 驅動程式所管理, 而預設的防火牆規則會封鎖網路檔案存取。 如需詳細資訊, 請參閱[啟用 FileTable 的必要條件](../relational-databases/blob/enable-the-prerequisites-for-filetable.md)。

    啟用 FileTable 之後, 若要撰寫模型, 您可以從 SQL 取得使用 FileTable API 的路徑, 然後從您的程式碼將模型寫入至該位置。 當您需要讀取模型時, 您會取得 SQL 的路徑, 然後使用腳本中的路徑來呼叫模型。 如需詳細資訊, 請參閱[使用檔案輸入輸出 Api 存取 filetable](../relational-databases/blob/access-filetables-with-file-input-output-apis.md)。

### <a name="7-avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>7.避免在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]計算內容中執行 R 程式碼時清除工作區

如果您在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]計算內容中執行 r 程式碼時, 使用 R 命令清除物件的工作區, 或者如果您將工作區清除為使用[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)所呼叫之 r 腳本的一部分, 則可能會收到此錯誤:*工作區找不到物件 Revoscriptconnection。*

`revoScriptConnection` 是 R 工作區的物件，包含從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]呼叫之 R 工作階段的相關資訊。 不過，如果 R 程式碼包含清除工作區的命令，例如 `rm(list=ls()))`，則也會清除工作階段所有資訊和 R 工作區的其他物件。

因應措施是在中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行 R 時, 避免任意清除變數和其他物件。 雖然在 R 主控台中工作時, 清除工作區是常見的, 但可能會產生非預期的結果。

* 若要刪除特定的變數, 請`remove`使用 R 函數: 例如,`remove('name1', 'name2', ...)`
* 如有多個變數要刪除，請將暫存變數名稱儲存至清單，並執行定期記憶體回收。

### <a name="8-restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>8.可作為輸出提供給 R 指令碼的資料限制

您無法在 R 指令碼中使用下列類型的查詢結果：

- 來自 [!INCLUDE[tsql](../includes/tsql-md.md)] 查詢 (參考永遠加密資料行) 的資料。
  
- 來自 [!INCLUDE[tsql](../includes/tsql-md.md)] 查詢 (參考遮罩資料行) 的資料。
  
     若您需要在 R 指令碼中使用遮罩的資料，一項可行的因應措施是在暫存資料表中製作資料複本，並改用該資料。

### <a name="9-use-of-strings-as-factors-can-lead-to-performance-degradation"></a>9.使用字串做為因素可能會導致效能降低

使用字串類型變數做為因素, 可能會大幅增加 R 作業所使用的記憶體數量。 這是 R 一般的已知問題, 而且主題上有許多文章。 例如, 您可以在 r 中, 透過[ [John 掛接, 在 r-博主) 或 stringsAsFactors 中查看因素不是第一](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/)級的公民:未經授權的事蹟, 由 Roger](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/)Peng。 

雖然此問題不是 SQL Server 特有的, 但它可能會大幅影響 SQl Server 中 R 程式碼執行的效能。 字串通常會儲存為 Varchar 或 Nvarchar, 如果字串資料的資料行有許多唯一的值, 則在內部將這些轉換成整數, 並由 R 傳回字串的程式甚至可能會導致記憶體配置錯誤。

如果您不一定需要字串資料類型來進行其他作業, 則在資料準備過程中, 將字串值對應至數值 (整數) 資料類型, 會從效能和規模的觀點來看。

如需此問題的討論和其他秘訣, 請參閱[R Services 的效能-資料優化](r/r-and-data-optimization-r-services.md)。

### <a name="10-arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>10.SQL Server 資料來源不支援引數*varsToKeep*和*varsToDrop*

當您使用 rxDataStep 函式將結果寫入資料表時, 使用*varsToKeep*和*varsToDrop*是一種便利的方式, 可指定要包含或排除在作業中的資料行。 不過, SQL Server 的資料來源不支援這些引數。

### <a name="11-limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>11.對 sp\_執行\_外部\_腳本中 SQL 資料類型的有限支援

並非 SQL 中支援的所有資料類型都可以在 R 中使用。因應措施是, 將不支援的資料類型轉換為支援的資料類型, 然後再將\_資料\_傳遞\_至 sp 執行外部腳本。

如需詳細資訊, 請參閱[R 程式庫和資料類型](r/r-libraries-and-data-types.md)。

### <a name="12-possible-string-corruption-using-unicode-strings-in-varchar-columns"></a>12.在 Varchar 資料行中使用 unicode 字串的可能字串損毀

將 Varchar 資料行中的 unicode [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]資料從傳送至 R/Python, 可能會導致字串損毀。 這是因為定序中[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]這些 unicode 字串的編碼方式, 可能不符合 R/Python 中使用的預設 utf-8 編碼。 

若要將任何非 ASCII 字串資料從[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]傳送至 R/Python, 請使用 utf-8 編碼 (適用于[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]), 或使用 Nvarchar 類型進行相同的。

### <a name="13-only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>13.只能從傳回一個型`raw`別的值`sp_execute_external_script`

當 R 傳回二進位資料類型 (R **raw**資料類型) 時, 此值必須在輸出資料框架中傳送。

除了**raw**以外的資料類型, 您也可以藉由新增 OUTPUT 關鍵字, 傳回參數值以及預存程式的結果。 如需詳細資訊, 請參閱[參數](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters)。

如果您想要使用多個包含**raw**類型值的輸出集, 其中一個可行的因應措施是執行預存程式的多次呼叫, 或使用 ODBC 將結果[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]集傳回給。

### <a name="14-loss-of-precision"></a>14.遺失有效位數

由於[!INCLUDE[tsql](../includes/tsql-md.md)]和 R 支援各種資料類型, 因此數值資料類型可能會在轉換期間遺失有效位數。

如需隱含資料類型轉換的詳細資訊, 請參閱[R 程式庫和資料類型](r/r-libraries-and-data-types.md)。

### <a name="15-variable-scoping-error-when-you-use-the-transformfunc-parameter"></a>15.當您使用 transformFunc 參數時, 發生變數範圍錯誤

若要在建立模型時轉換資料, 您可以在  函式 (例如`rxLinmod`或`rxLogit`) 中傳遞 transformFunc 引數。 不過, 即使在本機計算內容中呼叫正常運作, 嵌套函式呼叫也會導致 SQL Server 計算內容中的範圍錯誤。

> *分析的範例資料集沒有任何變數*

例如, 假設您已在本機全域環境中定義`f`了`g`兩個函式和, 並`g`呼叫`f`。 在涉及`g`的分散式或遠端呼叫中, 對`g`的呼叫可能會因此錯誤`f`而失敗, 因為找不到, 即使您`f`已`g`將和都傳遞給遠端呼叫也一樣。

若遇到此問題，您可以在 `f` 定義內嵌 `g`的定義以解決此問題， `g` 前的任何位置則會正常呼叫 `f`。

例如:

```R
f <- function(x) { 2*x * 3 }
g <- function(y) {
              a <- 10 * y
               f(a)
}
```

若要避免此錯誤, 請重寫定義, 如下所示:

```R
g <- function(y){
              f <- function(x) { 2*x +3}
              a <- 10 * y
              f(a)
}
```

### <a name="16-data-import-and-manipulation-using-revoscaler"></a>16.使用 RevoScaleR 匯入及操作資料

從資料庫讀取**Varchar**資料行時, 會修剪空白字元。 若要避免此情況，請在字串頭尾使用非空白字元。

當函式 ( `rxDataStep`例如) 用來建立具有**Varchar**資料行的資料庫資料表時, 會根據資料的樣本來估計資料行寬度。 如果寬度可能不同, 則可能需要將所有字串填補到通用長度。

使用 `rxImport` 或 `rxTextToXdf` 的重複呼叫來匯入或附加資料列，將多個輸入檔案結合成單一 .xdf 檔案時，不支援使用轉換來變更變數的資料類型。

### <a name="17-limited-support-for-rxexec"></a>17.有限的 rxExec 支援

在 SQL Server 2016 中, `rxExec` RevoScaleR 封裝所提供的函數只能在單一執行緒模式中使用。

### <a name="18-increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>18.增加最大參數大小以支援 rxGetVarInfo

如果您使用具有極大量變數的資料集 (例如, 超過 40000), 請在您啟動`max-ppsize` R 時設定旗標, 以使用`rxGetVarInfo`之類的函式。 `max-ppsize` 旗標會指定指標保護堆疊的大小上限。

如果您使用的是 R 主控台 (例如, Rgui.exe 或 RTerm), 您可以輸入下列命令, 將_max-ppsize_的值設定為 500000:

```R
R --max-ppsize=500000
```

### <a name="19-issues-with-the-rxdtree-function"></a>19.RxDTree 函數的問題

`rxDTree` 函數目前不支援公式內的轉換。 尤其不支援使用 `F()` 語法即時建立因數。 不過, 數值資料會自動分類收納。

要求的因數會被視為與所有 RevoScaleR 分析函數中的因數相同，除了 `rxDTree`以外。

### <a name="20-datatable-as-an-outputdataset-in-r"></a>20.[Data. table] 做為 R 中的 OutputDataSet

SQL Server `data.table` 2017 累積`OutputDataSet`更新 13 (CU13) 和更早版本中, 不支援在 R 中使用做為。 可能會出現下列訊息:

```
Msg 39004, Level 16, State 20, Line 2
A 'R' script error occurred during execution of 
'sp_execute_external_script' with HRESULT 0x80004004.
Msg 39019, Level 16, State 2, Line 2
An external script error occurred: 
Error in alloc.col(newx) : 
  Internal error: length of names (0) is not length of dt (11)
Calls: data.frame ... as.data.frame -> as.data.frame.data.table -> copy -> alloc.col

Error in execution.  Check the output for more information.
Error in eval(expr, envir, enclos) : 
  Error in execution.  Check the output for more information.
Calls: source -> withVisible -> eval -> eval -> .Call
Execution halted
```

`data.table`在 SQL Server `OutputDataSet` 2017 累計更新 14 (CU14) 和更新版本中, 支援 R 中的。

## <a name="python-script-execution-issues"></a>Python 腳本執行問題

本節包含在 SQL Server 上執行 Python 的特定已知問題, 以及與 Microsoft 所發佈的 Python 套件相關的問題, 包括[revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)和[microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)。

### <a name="1-call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>1.如果模型的路徑太長, 呼叫預先定型模型會失敗

如果您在 SQL Server 2017 的早期版本中安裝預先定型模型, 則定型模型檔案的完整路徑可能太長, 以致于 Python 無法讀取。 這項限制已在較新的服務版本中修正。

有幾個可能的因應措施: 

+ 當您安裝預先定型模型時, 請選擇自訂位置。
+ 可能的話, 請在具有較短路徑的自訂安裝路徑下安裝 SQL Server 實例, 例如 C:\SQL\MSSQL14。MSSQLSERVER.
+ 使用 Windows 公用程式[Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx)建立將模型檔案對應至較短路徑的硬連結。
+ 更新至最新的服務版本。

### <a name="2-error-when-saving-serialized-model-to-sql-server"></a>2.將序列化模型儲存至 SQL Server 時發生錯誤

當您將模型傳遞至遠端 SQL Server 實例, 並嘗試使用`rx_unserialize` [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)中的函式來讀取二進位模型時, 您可能會收到錯誤: 

> *NameError: 未定義名稱 ' rx_unserialize_model '*

如果您使用最新版本的序列化函數來儲存模型, 但您還原序列化模型的 SQL Server 實例無法辨識序列化 API, 就會引發此錯誤。

若要解決此問題, 請將 SQL Server 2017 實例升級為 CU3 或更新版本。

### <a name="3-failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>3.無法初始化 Varbinary 變數會在 BxlServer 中導致錯誤

如果您使用`sp_execute_external_script`在 SQL Server 中執行 Python 程式碼, 且程式碼具有類型 Varbinary (max)、Varchar (max) 或類似類型的輸出變數, 則變數必須初始化或設定為腳本的一部分。 否則, 資料交換元件 BxlServer 會引發錯誤並停止運作。

即將推出的服務版本將會修正這項限制。 因應措施是, 確定已在 Python 腳本內初始化變數。 您可以使用任何有效的值, 如下列範例所示:

```sql
declare @b varbinary(max);
exec sp_execute_external_script
  @language = N'Python'
  , @script = N'b = 0x0'
  , @params = N'@b varbinary(max) OUTPUT'
  , @b = @b OUTPUT;
go
```

```sql
declare @b varchar(30);
exec sp_execute_external_script
  @language = N'Python'
  , @script = N' b = ""  '
  , @params = N'@b varchar(30) OUTPUT'
  , @b = @b OUTPUT;
go
```

### <a name="4-telemetry-warning-on-successful-execution-of-python-code"></a>4.成功執行 Python 程式碼時的遙測警告

從 SQL Server 2017 CU2 開始, 即使 Python 程式碼執行成功, 也可能會出現下列訊息:

> *來自外部腳本的 STDERR 訊息:* 
>  *~ PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger* 
>  *SyntaxWarning: telemetry_state 是在全域宣告之前使用*

SQL Server 2017 累計更新 3 (CU3) 中已修正此問題。 

### <a name="5-numeric-decimal-and-money-data-types-not-supported"></a>5.不支援數值、十進位和 money 資料類型

從開始, 當搭配使用 Python 與`sp_execute_external_script`時, 不支援 SQL Server 2017 累計更新 12 (CU12)、數值、十進位和 money 資料類型。 可能會出現下列訊息:

> *錯誤碼39004, SQL 狀態:S1000] 執行 of'sp_execute_external_script 時發生 ' Python ' 腳本錯誤, HRESULT 為0x80004004。*

> *錯誤碼39019, SQL 狀態:S1000] 發生外部腳本錯誤:*
> 
> *SqlSatelliteCall 錯誤:輸出架構中不支援的類型。支援的類型: bit、Smallint、int、datetime、smallmoney、real 和 float。char、Varchar 是部分支援的。*

SQL Server 2017 累計更新 14 (CU14) 中已修正此問題。

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise 和 Microsoft R Open

本節列出由革新分析所提供的 R 連線能力、開發和效能工具特有的問題。 這些工具是在舊版的[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]發行前版本中提供。

一般來說, 我們建議您將舊版卸載, 並安裝最新版的 SQL Server 或 Microsoft R Server。

### <a name="1-revolution-r-enterprise-is-not-supported"></a>1.不支援革命 R Enterprise

不支援與任何版本[!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)]並存安裝革命 R Enterprise。

如果您已有革命 R Enterprise 的現有授權, 您必須將它放在與您想要用[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]來連接[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到實例的實例和任何工作站不同的電腦上。

的[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]某些發行前版本包含由革命分析所建立的 Windows R 開發環境。 此工具已不再提供, 而且不受支援。

為了與[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]相容, 建議您改為安裝 Microsoft R Client。 [Visual Studio R 工具](https://www.visualstudio.com/vs/rtvs/)和[Visual Studio Code](https://code.visualstudio.com/)也支援 Microsoft R 解決方案。

### <a name="2-compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>2.SQLite ODBC 驅動程式與 RevoScaleR 的相容性問題

SQLite ODBC 驅動程式的修訂0.92 與 RevoScaleR 不相容。 修訂 0.88-0.91 和0.93 和更新版本已知相容。

## <a name="see-also"></a>另請參閱

[SQL Server 2016 的新功能](../sql-server/what-s-new-in-sql-server-2016.md)

[SQL Server 中的機器學習服務疑難排解](machine-learning-troubleshooting-faq.md)
