---
title: Machine Learning 服務中的已知問題 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2d3396aecca9cbc1e250a26a9ddffd7cc69eb4c0
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51704106"
---
# <a name="known-issues-in-machine-learning-services"></a>在 Machine Learning 服務的已知的問題
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文會說明已知的問題或限制與機器學習服務會提供這個選項在 SQL Server 2016 和 SQL Server 2017 中的元件。

此處提供的資訊適用於所有的下列程式碼，除非另有說明：

SQL Server 2016

- R Services (資料庫內)
- Microsoft R Server (獨立式)

SQL Server 2017

- 機器學習服務 （資料庫）
- 機器學習服務適用於 Python （資料庫）
- Machine Learning 伺服器 (獨立式)

## <a name="setup-and-configuration-issues"></a>設定和組態問題

如需程序和初始設定和組態相關的一般問題的說明，請參閱 <<c0> [ 升級及安裝常見問題集](r/upgrade-and-installation-faq-sql-server-r-services.md)。 它包含升級、 並排顯示安裝及安裝新的 R 或 Python 元件的相關資訊。

### <a name="r-script-runtime-error-sql-server-2017-cu5-cu7-regression"></a>R 指令碼執行階段錯誤 （SQL Server 2017 CU5 CU7 迴歸）

SQL Server 2017，在累計更新 5 到 7，沒有中的迴歸**rlauncher.config**檔案的暫存目錄的檔案路徑包含空格的位置。 CU8 更正此迴歸。

執行 R 指令碼時，您會看到錯誤訊息包含下列訊息：

> *無法與 'R' 指令碼的執行階段通訊。請檢查 'R' 執行階段的需求。*
>
> 來自外部指令碼的 STDERR 訊息： 
>
> *嚴重錯誤： 無法建立 'R_TempDir'*

**因應措施**

可供使用時，請套用 CU8。 或者，您可以重新建立**rlauncher.config**藉由執行**registerrext**與解除安裝/安裝在已提高權限的命令提示字元上。 

```text
<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /uninstall /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>

<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /install /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>
```

下列範例顯示的命令，使用預設執行個體 」 MSSQL14。MSSQLSERVER"安裝到"C:\Program Files\Microsoft SQL Server\":

```text
"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /uninstall /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER

"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /install /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER
```

### <a name="unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>無法在網域控制站上安裝 SQL Server 機器學習服務功能

如果您嘗試在網域控制站上安裝 SQL Server 2016 R Services 或 SQL Server 2017 Machine Learning 服務，則安裝會失敗，發生下列錯誤：

> *此功能的安裝程序期間發生錯誤*
> 
> *找不到具有身分識別的群組*
> 
> *元件的錯誤程式碼： 0x80131509*

因為網域控制站上的服務無法建立 20 個的本機帳戶，才能執行機器學習服務，就會發生失敗。 一般情況下，我們不建議在網域控制站上安裝 SQL Server。 如需詳細資訊，請參閱 <<c0> [ 支援公告 2032911](https://support.microsoft.com/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont)。

### <a name="install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>安裝最新的服務版本確保與 Microsoft R Client 相容性

如果您安裝最新版的 Microsoft R Client，並使用它來執行 SQL Server 上的 R，在遠端計算內容中，您可能會發生的錯誤，如下所示：

> *您的 Microsoft R Client 版本 9.x.x 上執行您的電腦，也就是與 Microsoft R Server 版本 8.x.x 不相容。請下載並安裝相容版本。*

SQL Server 2016 需要在用戶端上的 R 程式庫會完全符合伺服器上的 R 程式庫。 限制已移除版本晚於 R Server 9.0.1 （英文)。 不過，如果您遇到這個錯誤時，驗證由您的用戶端和伺服器，並視需要更新用戶端以符合伺服器版本的 R 程式庫版本。

R 與 SQL Server R Services 一起安裝的版本會更新在安裝 SQL Server 的服務版本。 若要確保一律有最新版本的 R 元件，請務必安裝所有 service pack。

若要確保與 Microsoft R Client 9.0.0 相容，請安裝所述的更新在此[技術支援文件](https://support.microsoft.com/kb/3210262)。

若要避免發生問題的 R 封裝，您也可以升級的版本中所述，變更您的服務合約以使用新式生命週期支援原則，在伺服器上，安裝的 R 程式庫[下一節](#bkmk_sqlbindr)。 當您這樣做時，會更新相同的排程更新的 machine Learning 伺服器 (先前稱為 Microsoft R Server) 所使用的 R 與 SQL Server 一起安裝的版本。

**適用於：** SQL Server 2016 R Services 中，使用 R 伺服器 9.0.0 版或更早版本

### <a name="r-components-missing-from-cu3-setup"></a>遺漏 CU3 安裝的 R 元件

有限的數目的 Azure 虛擬機器已佈建，而不應包含與 SQL Server 的 R 安裝檔案。 此問題適用於在 2018年-01-05 2018年-01-23 的週期中佈建的虛擬機器。 如果您套用 SQL Server 2017 CU3 更新期間從 2018年-01-05 2018年-01-23，此問題也可能會影響在內部部署安裝。

服務版本中已提供，包括 R 安裝檔案正確版本。

+ [SQL Server 2017 KB4052987 的累計更新套件 3](https://www.microsoft.com/download/details.aspx?id=56128)。

若要安裝元件，並修復 SQL Server 2017 cu3 開始，您必須解除安裝 cu3 開始，並重新安裝更新的版本：

1. 下載更新的 CU3 安裝檔案，其中包含的 R 安裝程式。
2. 解除安裝 CU3。 在 [控制台] 中搜尋**解除安裝的更新**，然後選取 「 SQL Server 2017 (KB4052987) （64 位元） 的 Hotfix 3015"。 繼續進行解除安裝步驟。
3. 重新安裝 cu3 開始更新，方法是按兩下 KB4052987 您剛才下載的更新： `SQLServer2017-KB4052987-x64.exe`。 遵循安裝指示進行。

### <a name="unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>無法在離線安裝的 SQL Server 2017 CTP 2.0 或更新版本中安裝 Python 元件

如果您沒有網際網路存取的電腦上安裝 SQL Server 2017 的發行前版本，安裝程式可能無法顯示頁面會提示已下載的 Python 元件的位置。 在這種情況下，您可以安裝 Machine Learning 服務功能，但不是 Python 元件。

在發行版本會修正此問題。 此外，這項限制不適用於 R 元件。

**適用於：** 使用 Python 的 SQL Server 2017

### <a name="bkmk_sqlbindr"></a> 當您從連接到較舊版本的 SQL Server R Services 用戶端使用不相容版本的警告 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

當您在中執行 R 程式碼計算內容的 SQL Server 2016 時，您可能會看到下列錯誤：

> *您電腦上執行的是 9.0.0 版的 Microsoft R Client，與 Microsoft R Server 8.0.3 版不相容。請下載並安裝相容版本。*

如果下列兩個陳述式為 true，會顯示這個訊息

+ 用戶端電腦上安裝 R Server （獨立式） 使用的安裝精靈[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]。
+ 使用安裝 Microsoft R Server[不同的 Windows installer](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)。

若要確保伺服器和用戶端都使用相同的版本，您可能需要使用_繫結_、 支援 Microsoft R 伺服器 9.0 和更新版本中，若要升級 SQL Server 2016 執行個體中的 R 元件。 若要判斷是否支援升級為可用，如您的 R Services 的版本，請參閱[執行個體的 R Services 使用 SqlBindR.exe 升級](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

**適用於：** SQL Server 2016 R Services 中，使用 R 伺服器 9.0.0 版或更早版本

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>SQL Server 2016 服務版本的安裝程式可能無法安裝較新版本的 R 元件

當您安裝累積更新，或未連線到網際網路的電腦上安裝 SQL Server 2016 的 service pack 時，安裝精靈可能無法顯示提示，可讓您使用已下載的封包檔中更新 R 元件。 當 database engine 一起安裝的多個元件時，通常就會發生此失敗。

因應措施，您可以使用命令列，並指定安裝的版本更新服務`MRCACHEDIRECTORY`引數，在此範例中，這會安裝 CU1 更新中所示：

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

若要取得最新的安裝程式，請參閱[安裝沒有網際網路存取的機器學習服務元件](install/sql-ml-component-install-without-internet-access.md)。

**適用於：** SQL Server 2016 R Services 中，使用 R 伺服器 9.0.0 版或更早版本

### <a name="launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>若要啟動的版本是 R 版本不同，Launchpad 服務無法

如果您安裝 SQL Server R Services 分別從資料庫引擎，而組建版本不同，您可能會看到系統事件記錄檔中的下列錯誤：

> *SQL Server Launchpad 服務無法啟動，因為發生下列錯誤： 服務未啟動或控制要求及時回應。*

比方說，這項錯誤可能如果您使用的發行版本安裝 database engine 就會發生、 套用修補程式以升級資料庫引擎，和使用的發行版本，以新增 R Services 功能。

若要避免這個問題，使用公用程式在檔案管理員等比較 Launchpad.exe SQL 二進位檔案，例如 sqldk.dll 版的版本。 所有元件都應有相同的版本號碼。 如果升級某個元件，所有其他已安裝的元件請務必套用相同的升級。

尋找在 Launchpad`Binn`執行個體的資料夾。 例如，在預設安裝的 SQL Server 2016 中，路徑可能是`C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn`。 

### <a name="remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>Azure 虛擬機器執行的 SQL Server 執行個體的防火牆封鎖遠端計算內容

如果您已安裝[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]Windows Azure 虛擬機器上，您可能無法使用需要虛擬機器的工作區使用的計算內容。 原因是，根據預設，Azure 虛擬機器上的防火牆包含封鎖網路本機 R 使用者帳戶的存取權的規則。

因應措施，Azure VM 上開啟**具有進階安全性的 Windows 防火牆**，選取**輸出規則**，然後停用下列規則：**封鎖中 R 本機使用者帳戶的網路存取權SQL Server 執行個體 MSSQLSERVER**。 您也可以保留啟用，此規則，但變更安全性屬性，以**允許安全**。

### <a name="implied-authentication-in-sqlexpress"></a>SQLEXPRESS 的隱含驗證

當您從遠端資料科學工作站執行 R 作業使用整合式 Windows 驗證時，會使用 SQL Server*隱含的驗證*來產生指令碼可能會要求任何本機 ODBC 呼叫。 不過，這項功能在 SQL Server Express Edition 的 RTM 組建中不作用。

若要修正此問題，建議您升級至較新的服務版本。

如果升級不可行，因應措施，使用 SQL 登入來執行可能需要內嵌的 ODBC 呼叫的遠端 R 作業。

**適用於：** SQL Server 2016 R Services Express Edition

### <a name="performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>SQL Server 所使用的程式庫呼叫的其他工具時的效能限制

您可呼叫的機器學習程式庫，從外部應用程式，例如 RGui 適用於 SQL Server 安裝。 如此一來，可能是最方便的方式來完成特定工作，例如安裝新的封裝，或在非常短的程式碼範例上執行臨機操作測試。 不過，外部 SQL Server，可能會限制效能。 

比方說，即使您使用 SQL Server Enterprise Edition，R 執行在單一執行緒模式中執行 R 程式碼使用外部工具時。 若要取得 SQL Server 中的效能的優勢，啟動 SQL Server 連線，並使用[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)呼叫外部指令碼執行階段。

一般情況下，避免呼叫 machine learning 程式庫所使用的 SQL Server 上，從外部工具。 如果您要偵錯 R 或 Python 程式碼，則通常更容易，若要這樣做的 SQL Server 外部。 若要取得 SQL Server 中的相同程式庫，您可以安裝 Microsoft R Client [SQL Server 2017 Machine Learning Server （獨立式）](install/sql-machine-learning-standalone-windows-install.md)，或[SQL Server 2016 R Server （獨立式）](install/sql-r-standalone-windows-install.md)。

### <a name="sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>SQL Server Data Tools 不支援外部指令碼所需的權限

當您使用 Visual Studio 或 SQL Server Data Tools 來發行資料庫專案中，如果任何主體擁有外部指令碼執行的特定權限時，您可能會收到如下錯誤：

> *TSQL 模型： 反向工程的資料庫時偵測到的錯誤。權限無法辨識，以及未匯入。*

目前的 DACPAC 模型不支援 R Services 或機器學習服務，例如授與任何的外部指令碼或 EXECUTE ANY EXTERNAL SCRIPT 所使用的權限。 未來版本會修正此問題。

因應措施，在部署後指令碼陳述式執行額外的授與。

### <a name="external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>執行外部指令碼已節流處理，因為資源控管預設值

在 Enterprise Edition 中，您可以使用資源集區來管理外部指令碼程序。 在一些早期發行的組建，無法配置給 R 處理序的記憶體上限是 20%。 因此，如果伺服器有 32GB 的 RAM，R 可執行檔 （RTerm.exe 和 BxlServer.exe） 無法使用上限 6.4 GB 的單一要求中。

如果您遇到資源限制，請檢查目前的預設值。 如果 20%不夠時，請參閱文件[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]如何變更此值。

**適用於：** SQL Server 2016 R 服務，Enterprise Edition

## <a name="r-script-execution-issues"></a>R 指令碼執行問題

本節包含專屬於 SQL Server 上執行 R 的已知的問題，以及相關的 R 程式庫和工具，Microsoft，包括 RevoScaleR 所發行的一些問題。

如需其他可能會影響 R 解決方案的已知問題，請參閱[Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues)站台。

### <a name="access-denied-warning-when-executing-r-scripts-on-sql-server-in-a-non-default-location"></a>存取遭拒的非預設位置中的 SQL Server 上執行 R 指令碼時的警告

如果 SQL Server 執行個體已安裝到非預設位置，例如外部`Program Files`資料夾中，當您嘗試執行安裝套件的指令碼時，會引發 ACCESS_DENIED 警告。 例如：

> *在  `normalizePath(path.expand(path), winslash, mustWork)` ： 路徑 [2] ="~ExternalLibraries/R/8/1 」: 存取遭拒*

原因是 R 函式嘗試讀取此路徑，且如果將會失敗的內建的使用者群組**SQLRUserGroup**，沒有讀取權限。 就會引發警告不會封鎖執行目前的 R 指令碼，但警告可能會重複發生，每當使用者執行任何其他的 R 指令碼。

如果您已安裝 SQL Server 的預設位置，這不會發生錯誤，因為所有的 Windows 使用者擁有讀取權限上`Program Files`資料夾。

在即將推出的服務版本中解決這個問題 ia。 因應措施，提供群組中， **SQLRUserGroup**，使用的所有父資料夾的讀取權限`ExternalLibraries`。

### <a name="serialization-error-between-old-and-new-versions-of-revoscaler"></a>RevoScaleR 的舊和新版本之間的序列化錯誤

當您傳遞使用遠端 SQL Server 執行個體的序列化的格式的模型時，您可能會收到錯誤： 

> *MemDecompress 中的錯誤 (資料、 類型 = 解壓縮) 中的發生內部錯誤-3 memDecompress(2)。*

如果您儲存使用序列化函式的最新版本的模型，就會引發此錯誤[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)，但您還原序列化模型的 SQL Server 執行個體有較舊版本的 RevoScaleR Api，從 SQLServer 2017 CU2 或更早版本。

因應措施，您可以升級至 CU3 或更新版本的 SQL Server 2017 執行個體。

如果 API 版本是一樣的或如果您要移動與較舊的序列化函式來使用序列化 API 的較新版本的伺服器儲存的模型，則不會出現錯誤。

換句話說，使用相同版本的 RevoScaleR 為序列化和還原序列化作業。

### <a name="real-time-scoring-does-not-correctly-handle-the-learningrate-parameter-in-tree-and-forest-models"></a>即時評分無法正確處理_learningRate_樹狀結構和樹系模型中的參數

如果您使用決策樹或決策樹系方法來建立模型，並指定學習速率，使用時，您可能會看到不一致的結果`sp_rxpredict`或 SQL`PREDICT`函式，相較於使用`rxPredict`。

原因是 API 中的錯誤，序列化處理序模型，並僅限於`learningRate`參數： 例如，在[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees)，或

在即將推出的服務版本中已解決這個問題。

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>R 作業處理器相似性的限制

在 SQL Server 2016 的初始發行組建，您可以設定只會針對第一個 k 群組中的 Cpu 處理器親和性。 比方說，如果伺服器是具有兩個 k 群組 2 通訊端機器，便會從第一個 k 群組的唯一處理器用於 R 處理序。 當您設定 R 指令碼工作的資源控管時，適用相同的限制。

SQL Server 2016 Service Pack 1 已修正這個問題。 我們建議您升級至最新的服務版本。

**適用於：** SQL Server 2016 R 服務 RTM 版本

### <a name="changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>讀取 SQL Server 計算內容中的資料，無法變更資料行類型。

如果您的計算內容設為 SQL Server 執行個體，則您無法使用 _colClasses_ 引數 (或其他類似的引數) 來變更 R 程式碼中的資料行資料類型。

例如，如果資料行 CRSDepTimeStr 還不是整數，則下列陳述式會產生錯誤︰

```R
data <- RxSqlServerData(
  sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall", 
  connectionString = connectionString, 
  colClasses = c(CRSDepTimeStr = "integer"))
```

因應措施，您可以重新撰寫 SQL 查詢，以使用 CAST 或 CONVERT，並向 R 呈現資料，使用正確的資料類型。 一般情況下，效能會更好當您使用的資料使用 SQL，而不是藉由變更 R 程式碼中的資料。

**適用於：** SQL Server 2016 R Services

### <a name="limits-on-size-of-serialized-models"></a>序列化模型大小限制

當您將模型儲存至 SQL Server 資料表時，您必須序列化模型，並將它儲存為二進位格式。 理論上可以使用這個方法儲存模型的大小上限為 2GB，也就是 SQL Server 中的 varbinary 資料行的大小上限。

如果您需要使用較大的模型，以下的因應措施是使用：

+ 採取步驟來縮小您的模型。 某些開放原始碼 R 封裝在模型物件中包含大量資訊，而且大部分的這項資訊可以移除部署。 
+ 您可以使用 特徵選取來移除不必要的資料行。
+ 如果您使用的開放原始碼演算法，請考慮使用 MicrosoftML 或 RevoScaleR 中的對應演算法的相似實作。 這些套件都已針對部署案例最佳化。
+ 如果已合理化模型的大小縮減使用上述步驟後，請參閱 < [memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress)基底 R 中的函式可用來降低模型的大小，再將它傳遞至 SQL Server。 當模型很接近 2 GB 的限制，最好使用此選項。
+ 針對較大的模型，您可以使用 SQL Server [FileTable](..\relational-databases\blob\filetables-sql-server.md)功能來儲存模型，而不是使用 varbinary 資料行。

    若要使用 Filetable，您必須新增防火牆例外狀況，因為 Filetable 中所儲存的資料由 SQL Server 中的 Filestream 檔案系統驅動程式管理，且預設的防火牆規則封鎖檔案的網路存取。 如需詳細資訊，請參閱 <<c0> [ 啟用 FileTable 的必要條件](../relational-databases/blob/enable-the-prerequisites-for-filetable.md)。 

    您已啟用 FileTable 之後，撰寫模型，您取得的路徑，從 SQL 使用 FileTable 的 API，並從您的程式碼然後寫入至該位置的模型。 當您需要讀取模型時，您會從 SQL 取得的路徑，然後呼叫 模型使用從您的指令碼的路徑。 如需詳細資訊，請參閱 <<c0> [ 使用檔案輸入輸出 Api 存取 Filetable](../relational-databases/blob/access-filetables-with-file-input-output-apis.md)。

### <a name="avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>避免在執行中的 R 程式碼時，清除工作區[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]計算內容

如果您使用 R 命令清除物件工作區執行 R 程式碼時[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]計算內容，或如果您清除工作區為 R 指令碼的一部分使用呼叫[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，您可能會收到這個錯誤:*找不到工作區物件 revoScriptConnection*

`revoScriptConnection` 是 R 工作區的物件，包含從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]呼叫之 R 工作階段的相關資訊。 不過，如果 R 程式碼包含清除工作區的命令，例如 `rm(list=ls()))`，則也會清除工作階段所有資訊和 R 工作區的其他物件。

因應措施，避免任意清除變數和其他物件執行 R 時[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 雖然在 R 主控台中工作時，清除工作區是常見的它可以有非預期的結果。

* 若要刪除特定的變數，請使用 R`remove`函式： 例如， `remove('name1', 'name2', ...)`
* 如有多個變數要刪除，請將暫存變數名稱儲存至清單，並執行定期記憶體回收。

### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>可作為輸出提供給 R 指令碼的資料限制

您無法在 R 指令碼中使用下列類型的查詢結果：

- 來自 [!INCLUDE[tsql](../includes/tsql-md.md)] 查詢 (參考永遠加密資料行) 的資料。
  
- 來自 [!INCLUDE[tsql](../includes/tsql-md.md)] 查詢 (參考遮罩資料行) 的資料。
  
     若您需要在 R 指令碼中使用遮罩的資料，一項可行的因應措施是在暫存資料表中製作資料複本，並改用該資料。

### <a name="use-of-strings-as-factors-can-lead-to-performance-degradation"></a>做為字串的因素可能會導致效能降低

因為因素可能會大幅增加的 R 作業所使用的記憶體數量，請使用字串類型的變數。 一般情況下，這是 R 的已知的問題，並在主題上有許多文章。 例如，請參閱 <<c0> [ 因素不在 R 中，John 掛接，在 R 部落客的第一等公民)](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/)或是[stringsAsFactors： 未經授權的自傳，由 Roger Peng](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/)。 

雖然此問題不是 SQL Server 特有的它可能會大幅影響執行 SQl Server 中的 R 程式碼的效能。 字串通常會儲存為 varchar 或 nvarchar，以及如果字串資料行有許多唯一值，在內部轉換成整數，再回復成字串的 R 這些程序甚至可能導致記憶體配置錯誤。

如果您不一定需要字串資料類型進行其他作業，將字串值對應到一個數字 （整數） 資料類型的資料準備過程中會很有幫助的效能和延展性的觀點。

如需此問題和其他秘訣的討論，請參閱[R Services-資料最佳化的效能](r/r-and-data-optimization-r-services.md)。

### <a name="arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>引數*varsToKeep*並*varsToDrop*不支援 SQL Server 資料來源

當您使用 rxDataStep 函式，將結果寫入資料表時，使用*varsToKeep*並*varsToDrop*是便利的方式，指定要包含或排除作業的一部分的資料行。 不過，這些引數不支援 SQL Server 資料來源。

### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>SQL 預存程序中的資料類型的支援有限\_執行\_外部\_指令碼

並非所有的資料類型所支援的 SQL 可用於。因應措施，請考慮不支援的資料類型轉換成支援的資料型別再將資料傳遞至預存程序\_執行\_外部\_指令碼。

如需詳細資訊，請參閱 < [R 程式庫和資料類型](r/r-libraries-and-data-types.md)。

### <a name="possible-string-corruption"></a>字串可能損毀

字串資料從任何往返[!INCLUDE[tsql](../includes/tsql-md.md)]到 R 再到[!INCLUDE[tsql](../includes/tsql-md.md)]一次可能會導致損毀。 這是因為使用 R 與不同的編碼方式[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，以及各種不同的定序和所支援的 R 語言和[!INCLUDE[tsql](../includes/tsql-md.md)]。 任何非 ASCII 編碼的字串都可能不正確地處理。

當您將字串資料傳送至 R 時，將其轉換為 ASCII 表示法中，如果可能的話。

這項限制適用於 SQL Server 與 Python 之間以及傳遞的資料。 多位元組字元應該傳遞為 utf-8，並儲存為 Unicode。

### <a name="only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>只有一個值的型別`raw`可以從傳回 `sp_execute_external_script`

當二進位資料類型 (R**原始**資料類型) 會傳回從 R，值必須在輸出資料框架中傳送。

資料類型以外**原始**，您可以加上 OUTPUT 關鍵字，以傳回參數的值，以及預存程序的結果。 如需詳細資訊，請參閱 <<c0> [ 參數](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters)。

如果您想要使用多個輸出集包含值的型別**原始**，其中一個可能的解決方法是以進行多次呼叫預存程序中，或傳送結果集傳回[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 ODBC。

### <a name="loss-of-precision"></a>遺失有效位數

因為[!INCLUDE[tsql](../includes/tsql-md.md)]和 R 支援不同的資料類型、 數字資料類型可以在轉換期間會遺失有效位數。

如需有關隱含資料類型轉換的詳細資訊，請參閱 < [R 程式庫和資料類型](r/r-libraries-and-data-types.md)。

### <a name="variable-scoping-error-when-you-use-the-transformfunc-parameter"></a>變數約制錯誤，當您使用 transformFunc 參數

若要轉換資料，當您建立模型時，您可以傳遞*transformFunc*這類函式中的引數`rxLinmod`或`rxLogit`。 不過，巢狀函式呼叫可能會導致發生約制錯誤，在 SQL Server 計算內容中，即使呼叫會在本機計算內容中正確運作。

> *分析範例資料集沒有任何變數*

例如，假設您已定義兩個函式，`f`並`g`，在您的本機全域環境，和`g`呼叫`f`。 在分散式或遠端呼叫涉及`g`，呼叫`g`可能會發生此錯誤，失敗，因為`f`找不到，即使您已通過兩者`f`和`g`給遠端呼叫。

若遇到此問題，您可以在 `f` 定義內嵌 `g`的定義以解決此問題， `g` 前的任何位置則會正常呼叫 `f`。

例如：

```r
f <- function(x) { 2*x * 3 }
g <- function(y) {
              a <- 10 * y
               f(a)
}
```

若要避免此錯誤，請重寫的定義，如下所示：

```r
g <- function(y){
              f <- function(x) { 2*x +3}
              a <- 10 * y
              f(a)
}
```

### <a name="data-import-and-manipulation-using-revoscaler"></a>使用 RevoScaleR 匯入及操作資料

當**varchar**讀取資料行是從資料庫中，會修剪空白字元。 若要避免此情況，請在字串頭尾使用非空白字元。

當這類函式`rxDataStep`用來建立資料庫資料表，其中有**varchar**會依據資料範例估計的資料行，資料行寬度。 如果寬度可能會不同，它可能需要所有字串都填補到常見長度。

使用 `rxImport` 或 `rxTextToXdf` 的重複呼叫來匯入或附加資料列，將多個輸入檔案結合成單一 .xdf 檔案時，不支援使用轉換來變更變數的資料類型。

### <a name="limited-support-for-rxexec"></a>RxExec 的有限的支援

在 SQL Server 2016 中，`rxExec`函式所提供的 RevoScaleR 封裝可以用於只能在單一執行緒模式中。

平行處理原則`rxExec`多個處理序已規劃在未來的版本。

### <a name="increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>提高參數大小上限以支援 rxGetVarInfo

如果您使用搭配變數數目極大的資料集 (例如 40,000 個以上)，設定`max-ppsize`當您啟動 R，以使用類似如下的函式的旗標`rxGetVarInfo`。 `max-ppsize` 旗標會指定指標保護堆疊的大小上限。

如果您使用 R 主控台 （例如 RGui.exe 或 RTerm.exe），您可以設定的值_max ppsize_為 500000，輸入：

```R
R --max-ppsize=500000
```

### <a name="issues-with-the-rxdtree-function"></a>RxDTree 函數的問題

`rxDTree` 函數目前不支援公式內的轉換。 尤其不支援使用 `F()` 語法即時建立因數。 不過，自動分類收納數字的資料。

要求的因數會被視為與所有 RevoScaleR 分析函數中的因數相同，除了 `rxDTree`以外。

## <a name="python-script-execution-issues"></a>Python 指令碼執行問題

本節包含專屬於執行 SQL Server，以及由 Microsoft 發佈的 Python 套件相關的問題 Python 的已知的問題包括[revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)和[microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

### <a name="call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>如果模型的路徑過長，就會失敗呼叫預先定型的模型

如果您在早期版本的 SQL Server 2017 中安裝預先定型的模型，訓練的模型檔案的完整路徑可能太長，適用於 Python 讀取。 這項限制被固定的一個版本的服務。

有數個可能的因應措施： 

+ 當您安裝預先定型的模型時，請選擇 自訂的位置。
+ 可能的話，請使用較短的路徑，例如 C:\SQL\MSSQL14 安裝自訂安裝路徑中的 SQL Server 執行個體。MSSQLSERVER。
+ 使用 Windows 公用程式[Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx)建立永久連結，將模型檔案對應至較短的路徑。
+ 更新至最新的服務版本。

### <a name="error-when-saving-serialized-model-to-sql-server"></a>儲存時發生錯誤序列化模型，以 SQL Server

當您將模型傳遞至遠端 SQL Server 執行個體，並嘗試將二進位模型使用讀取`rx_unserialize`函式中[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)，您可能會收到錯誤： 

> *NameError： 未定義名稱 'rx_unserialize_model'*

如果您已儲存使用序列化函式的最新版本的模型，但是您還原序列化之模型的 SQL Server 執行個體無法辨識序列化 API，會引發此錯誤。

若要解決此問題，請升級至 CU3 或更新版本的 SQL Server 2017 執行個體。

### <a name="failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>若要初始化 varbinary 變數失敗會造成 BxlServer 中的錯誤

如果您執行 Python 程式碼中使用 SQL Server `sp_execute_external_script`，和程式碼具有輸出的型別 varbinary （max）、 varchar （max） 或類似的型別變數，變數必須初始化，或是設定為您的指令碼的一部分。 否則，資料 exchange 元件 BxlServer，所引發的錯誤並停止運作。

在即將推出的服務版本中，將會修正這項限制。 因應措施，請確定在 Python 指令碼中初始化變數。 可以使用任何有效的值，如下列範例所示：

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

### <a name="telemetry-warning-on-successful-execution-of-python-code"></a>在成功執行 Python 程式碼的遙測資料警告

從 SQL Server 2017 CU2 開始，即使是已成功執行 Python 程式碼，否則可能會出現下列訊息：

> *來自外部指令碼的 STDERR 訊息：*
> **~PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger*
> *SyntaxWarning: telemetry_state 是使用全域宣告之前*


在 SQL Server 2017 累積更新 3 (CU3) 中已修正此問題。 

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise 和 Microsoft R Open

本節列出 R 連線能力、 開發和 Revolution Analytics 所提供的效能工具的特定問題。 中的發行前版本提供這些工具[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]。

一般情況下，我們建議您解除安裝這些舊的版本，並安裝最新版的 SQL Server 或 Microsoft R Server。

### <a name="revolution-r-enterprise-is-not-supported"></a>不支援 revolution R Enterprise

安裝任何版本的 Revolution R Enterprise 並存[!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)]不支援。

如果您將現有的授權的 Revolution R Enterprise 時，您就必須將它放在同時從另一部電腦上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體和您想要用於連線到任何工作站[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體。

某些發行前版本[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]適用於 Windows 的 Revolution Analytics 建立包含 R 開發環境。 此工具不再提供，並不支援。

相容性[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]，我們建議您改為安裝 Microsoft R Client。 [適用於 Visual Studio R 工具](https://www.visualstudio.com/vs/rtvs/)並[Visual Studio Code](https://code.visualstudio.com/)也支援 Microsoft R 解決方案。

### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>SQLite ODBC 驅動程式與 RevoScaleR 的相容性問題

SQLite ODBC 驅動程式的修訂 0.92 是與 RevoScaleR 不相容。 修訂 0.88-0.91 和 0.93 及更新版本則已知相容性。

## <a name="see-also"></a>另請參閱

[SQL Server 2016 的新功能](../sql-server/what-s-new-in-sql-server-2016.md)

[疑難排解 SQL Server 中的機器學習服務](machine-learning-troubleshooting-faq.md)
