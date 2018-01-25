---
title: "機器學習服務中的已知問題 |Microsoft 文件"
ms.date: 01/19/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2b37a63a-5ff5-478e-bcc2-d13da3ac241c
caps.latest.revision: "53"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 197bfc48d000246b59b983fbf890e998cc2b5beb
ms.sourcegitcommit: d7dcbcebbf416298f838a39dd5de6a46ca9f77aa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/23/2018
---
# <a name="known-issues-in-machine-learning-services"></a>機器學習服務中的已知的問題

本文說明已知的問題或限制使用機器學習中 SQL Server 2016 和 SQL Server 2017 的選項中提供的元件。

這裡的資訊適用於所有的下列程式碼，除非：

* SQL Server 2016

  - R Services (資料庫內)
  - Microsoft R Server (獨立式)

* SQL Server 2017

  - 機器學習服務 （資料庫）
  - 機器學習服務 for Python （資料庫）
  - Machine Learning 伺服器 (獨立式)

## <a name="setup-and-configuration-issues"></a>安裝和設定問題

如需處理程序和初始安裝和設定相關的常見問題的說明，請參閱[升級及安裝常見問題集](r/upgrade-and-installation-faq-sql-server-r-services.md)。 它包含升級、-並存安裝及安裝新的 R 或 Python 元件的相關資訊。

### <a name="unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>無法在網域控制站上安裝 SQL Server 的機器學習功能

如果您嘗試在網域控制站上安裝 SQL Server 2016 R Services 或 SQL Server 2017 機器學習服務，則安裝程式會失敗，發生下列錯誤：

>*「 錯誤發生之功能的安裝程序期間 」。*
> 
>*「 找不到群組識別...」*
> 
>*「 元件錯誤程式碼： 0x80131509"*

因為網域控制站上的服務無法建立 20 個的本機帳戶執行機器學習所需，就會發生故障。 一般情況下，我們不建議在網域控制站上安裝 SQL Server。 如需詳細資訊，請參閱[支援公告 2032911](https://support.microsoft.com/en-us/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont)。

### <a name="install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>安裝最新的版本更新服務以確保與 Microsoft R 用戶端的相容性

如果您安裝最新版的 Microsoft R 用戶端，並使用它來執行 SQL Server 上的 R 遠端計算內容中，您可能會收到類似下列錯誤：

>*您正在 Microsoft R 用戶端版本 9.x.x 您與 Microsoft R Server 版本 8.x.x 不相容的電腦。請下載並安裝相容版本。*

SQL Server 2016 需要用戶端上的 R 程式庫會完全符合伺服器上的 R 程式庫。 限制已移除版本的 R 伺服器 9.0.1 較新版本。 不過，如果您遇到這個錯誤，請確認版本的 R 程式庫會使用您的用戶端和伺服器，而且必要時，更新為符合伺服器版本的用戶端。

安裝 SQL Server 服務版本時，會更新 R 與 SQL Server R Services 一起安裝的版本。 若要確保一直擁有最新版本的 R 元件，請務必安裝所有 service pack。

為了確保與 Microsoft R 用戶端 9.0.0 相容性，安裝所述的更新在此[技術支援文件](https://support.microsoft.com/kb/3210262)。

若要避免發生問題的 R 封裝，您也可以升級的版本中所述，變更您的服務合約以使用現代的生命週期支援原則，在伺服器上，安裝的 R 程式庫[下一節](#bkmk_sqlbindr)。 當您這樣做時，會更新相同的排程更新的機器學習伺服器 （先前稱為 Microsoft R 伺服器） 所使用的 R 與 SQL Server 一起安裝的版本。

**適用於：** SQL Server 2016 R Services 中，使用 R Server 9.0.0 版本或更早版本

### <a name="unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>無法將 Python 元件安裝在離線安裝的 SQL Server 2017 CTP 2.0 或更新版本

如果您沒有網際網路存取的電腦上安裝發行前版本的 SQL Server 2017，安裝程式可能無法顯示頁面，提示下載 Python 元件的位置。 在這種情況下，您可以安裝的機器學習服務功能，而非 Python 元件。

發行版本中修正此問題。 如果您遇到此問題，以解決這個問題，您可以暫時啟用網際網路存取，安裝程式的持續時間。 這項限制不適用於。

**適用於：** SQL Server 2017 使用 Python

### <a name="bkmk_sqlbindr"></a>當您從連線到較舊版本的 SQL Server R Services 用戶端使用的不相容的版本警告[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

當您在 SQL Server 2016 的計算內容中執行 R 程式碼時，您可能會看到類似下列錯誤：

*您電腦上執行的是 9.0.0 版的 Microsoft R Client，與 Microsoft R Server 8.0.3 版不相容。請下載並安裝相容版本。*

如果下列兩個陳述式為 true，會顯示這個訊息

+ 用戶端電腦上安裝 R Server （獨立） 使用的安裝精靈[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]。
+ 您可以使用來安裝 Microsoft R Server[分隔 Windows installer](https://docs.microsoft.com/r-server/install/r-server-install-windows)。

若要確保伺服器和用戶端都使用相同的版本，您可能需要使用_繫結_、 支援的 Microsoft R Server 9.0 和更新版本中，若要升級 SQL Server 2016 執行個體中的 R 元件。 若要判斷是否支援升級為可用，如 R 服務版本，請參閱[使用 SqlBindR.exe R 服務的執行個體升級](/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

**適用於：** SQL Server 2016 R Services 中，使用 R Server 9.0.0 版本或更早版本

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>SQL Server 2016 服務版本的安裝程式可能無法安裝較新版本的 R 元件

當您安裝累計更新或未連線到網際網路的電腦上安裝 SQL Server 2016 的 service pack 時，可能會無法安裝精靈顯示提示，可讓您使用下載的 CAB 檔案更新的 R 元件。 Database engine 一起安裝的多個元件時，通常會發生這個失敗。

因應措施，您可以使用命令列，並指定安裝的版本更新服務`MRCACHEDIRECTORY`引數，此範例中，這會安裝 CU1 更新中所示：

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

若要取得最新的安裝程式，請參閱[安裝沒有網際網路存取的機器學習元件](r/installing-ml-components-without-internet-access.md)。

**適用於：** SQL Server 2016 R Services 中，使用 R Server 9.0.0 版本或更早版本

### <a name="launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>啟動控制板服務無法啟動的 R 版本不同版本時

如果您安裝 SQL Server R Services 分別從資料庫引擎，而且組建版本不同，您可能會看到系統事件記錄檔中的下列錯誤：

>_SQL Server Launchpad 服務無法啟動，因為發生下列錯誤： 服務未啟動或控制要求能夠及時回應。_

比方說，此錯誤可能會因為您安裝 database engine 所使用的發行版本、 套用修補程式來升級資料庫引擎，和使用的版本，以新增 R 服務功能。

若要避免這個問題，使用公用程式在檔案管理員例如比較 Launchpad.exe 的版本與版本的 SQL 二進位檔，例如 sqldk.dll。 所有元件都應有相同的版本號碼。 如果升級某個元件，所有其他已安裝的元件請務必套用相同的升級。

[啟動列] 中尋找`Binn`執行個體的資料夾。 例如，在預設安裝的 SQL Server 2016 中，路徑可能是"C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn"。 

### <a name="remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>Azure 虛擬機器執行的 SQL Server 執行個體中防火牆封鎖遠端計算內容

如果您已安裝[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]Windows Azure 虛擬機器，您可能無法使用需要虛擬機器的工作區中使用的計算內容。 原因在於，根據預設，Azure 虛擬機器上的防火牆包含封鎖網路本機 R 使用者帳戶存取權的規則。

因應措施，Azure VM 上開啟**具有進階安全性的 Windows 防火牆**，選取**輸出規則**，然後停用下列規則：**封鎖中 R 本機使用者帳戶的網路存取權SQL Server 執行個體 MSSQLSERVER**。 您也可以保留啟用，此規則，但變更安全性屬性，以**允許安全**。

### <a name="implied-authentication-in-sqlexpress"></a>SQLEXPRESS 的隱含驗證

當您執行 R 工作，您可以從遠端資料科學工作站使用整合式 Windows 驗證時，SQL Server 會使用*隱含的驗證*來產生指令碼可能需要任何本機 ODBC 呼叫。 不過，這項功能在 SQL Server Express Edition 的 RTM 組建中不作用。

若要修正此問題，建議您升級至較新的服務版本。

如果無法升級，您可以使用 SQL 登入來執行可能需要內嵌 ODBC 呼叫的遠端 R 作業。

**適用於：** SQL Server 2016 R Services Express Edition

### <a name="performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>SQL Server 所使用的程式庫呼叫的其他工具時的效能限制

您可呼叫機器學習從外部應用程式，例如 RGui for SQL Server 安裝的程式庫。 如此一來，可能是最方便的方式來完成特定工作，例如安裝新的封裝，或在非常短的程式碼範例執行臨機操作測試。 不過，SQL Server 外部的效能可能會有所限制。 

比方說，即使您使用 SQL Server 的 Enterprise Edition，R 以單一執行緒模式執行時使用外部工具執行 R 程式碼。 若要在 SQL Server 中取得的效能優點，啟動 SQL Server 連線，並使用[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)呼叫外部指令碼執行階段。

+ 一般情況下，避免呼叫機器學習所使用的 SQL Server 上，從外部工具的程式庫。 如果您需要偵錯 R 或 Python 程式碼，則通常更容易，若要這樣做的 SQL Server 外部。 若要取得 SQL Server 中的相同程式庫，您可以安裝 Microsoft R 用戶端或[Server 機器學習](r/create-a-standalone-r-server.md)。

### <a name="sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>SQL Server Data Tools 中不支援外部指令碼所需的權限

當您使用 Visual Studio 或 SQL Server Data Tools 來發行資料庫專案中，如果任何主體擁有外部指令碼執行的特定權限時，您可能會發生的錯誤，如下所示：

"TSQL 模型： 反向工程資料庫時偵測到的錯誤。 權限無法辨識並不會匯入。 」

目前的 DACPAC 模型不支援 R 服務或機器學習服務，例如授與任何的外部指令碼或 EXECUTE ANY EXTERNAL SCRIPT 所使用的權限。 未來版本會修正此問題。

因應措施，在部署後指令碼陳述式執行額外的授與。

### <a name="external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>執行外部指令碼已節流，因為資源控管的預設值

在 Enterprise Edition 中，您可以使用資源集區來管理外部指令碼程序。 在某些早期發行的組建，無法配置給 R 處理序的最大記憶體為 20%。 因此，如果伺服器有 32GB 的 RAM，R 可執行檔 （RTerm.exe 和 BxlServer.exe） 無法使用最多 6.4 單一要求中。

如果您遇到資源限制，請檢查目前的預設值。 若 20%不夠，請參閱文件[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]如何變更此值。

**適用於：** SQL Server 2016 R 服務、 企業版

## <a name="r-issues"></a>R 問題

本節包含專屬於 SQL Server 上執行 R 的已知的問題，以及相關的 R 程式庫和工具 Microsoft，包括 RevoScaleR 所發行的一些問題。

如需其他可能會影響 R 解決方案的已知問題，請參閱[Server 機器學習](https://docs.microsoft.com/machine-learning-server/resources-known-issues)站台。

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>R 作業處理器相似性的限制

在 SQL Server 2016 的初始發行版本，您可以設定只會針對第一個 k 群組中的 Cpu 處理器親和性。 例如，如果伺服器是包含兩個 k 群組 2 通訊端機器，便會從第一個 k 群組的唯一處理器用於 R 處理序。 當您設定資源控管的 R 指令碼工作時，適用於相同的限制。

SQL Server 2016 Service Pack 1 已修正這個問題。 我們建議您升級至最新版本更新服務。

**適用於：** SQL Server 2016 R 服務 RTM 版本

### <a name="changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>讀取 SQL Server 計算內容中的資料，無法變更資料行類型。

如果您的計算內容設為 SQL Server 執行個體，則您無法使用 _colClasses_ 引數 (或其他類似的引數) 來變更 R 程式碼中的資料行資料類型。

例如，如果資料行 CRSDepTimeStr 還不是整數，則下列陳述式會產生錯誤︰

```r
data <- RxSqlServerData(
  sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall", 
  connectionString = connectionString, 
  colClasses = c(CRSDepTimeStr = "integer"))
```

因應措施，您可以重新撰寫 SQL 查詢，以使用轉型或轉換，並將資料呈現給 R，使用正確的資料類型。 一般情況下，效能會更好當您使用的資料使用 SQL，而不是藉由變更 R 程式碼中的資料。

**適用於：** SQL Server 2016 R 服務

### <a name="limits-on-size-of-serialized-models"></a>序列化模型大小限制

當您將模型儲存至 SQL Server 資料表時，必須將模型序列化，並將它儲存在二進位格式。 理論上可以使用這個方法儲存模型的大小上限是 2 GB，也就是 SQL Server 中的 varbinary 資料行的大小上限。

如果您需要使用更大的模型，下列因應措施是使用：

+ 採取步驟來縮小您的模型。 某些開放原始碼 R 封裝中的模型物件，包含大量的資訊和大部分的這項資訊可以部署中移除。 
+ 您可以使用 特徵選取來移除不必要的資料行。
+ 如果您使用的開放原始碼演算法，請考慮使用 MicrosoftML 或 RevoScaleR 中對應的演算法的相似實作。 這些封裝已經過最佳化部署案例。
+ 如果模型已被合理化的大小縮減使用先前的步驟後，請參閱 < [memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress)在基底 R 函數可用來降低模型的大小，再將它傳遞至 SQL Server。 當模型很接近 2 GB 的限制，最好使用此選項。
+ 對於較大的模型，您可以使用 SQL Server [FileTable](..\relational-databases\blob\filetables-sql-server.md)功能來儲存模型，而不是使用 varbinary 資料行。

    若要使用 Filetable，您必須加入防火牆例外狀況，因為在 Filetable 中儲存的資料由 SQL Server 中的 Filestream 檔案系統驅動程式所管理，而預設的防火牆規則封鎖網路檔案的存取。 如需詳細資訊，請參閱[啟用 FileTable 的必要條件](../relational-databases/blob/enable-the-prerequisites-for-filetable.md)。 

    啟用 FileTable 之後，撰寫模型，您 SQL 使用 FileTable 的 API，從取得的路徑，然後撰寫模型對該位置從您的程式碼。 當您需要讀取模型時，您會從 SQL 取得的路徑，，然後呼叫模型使用從您的指令碼的路徑。 如需詳細資訊，請參閱[使用檔案輸入輸出 Api 存取 Filetable](../relational-databases/blob/access-filetables-with-file-input-output-apis.md)。

### <a name="avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>避免在執行中的 R 程式碼時，清除工作區[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]計算內容

如果您使用 R 命令來清除物件的工作區執行 R 程式碼時[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]計算內容中，如果您清除工作區一部分的 R 指令碼或透過呼叫[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，您可能會收到這個錯誤:*工作區中找不到的物件 revoScriptConnection*

`revoScriptConnection` 是 R 工作區的物件，包含從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]呼叫之 R 工作階段的相關資訊。 不過，如果 R 程式碼包含清除工作區的命令，例如 `rm(list=ls()))`，則也會清除工作階段所有資訊和 R 工作區的其他物件。

因應措施，避免任意清除變數和其他物件時您在執行 R [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 雖然使用 R 主控台時，清除工作區是很常見的它可以包含非預期的結果。

* 若要刪除特定變數，請使用 R`remove`函式： 例如，`remove('name1', 'name2', ...)`
* 如有多個變數要刪除，請將暫存變數名稱儲存至清單，並執行定期記憶體回收。

### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>可作為輸出提供給 R 指令碼的資料限制

您無法在 R 指令碼中使用下列類型的查詢結果：

- 來自 [!INCLUDE[tsql](../includes/tsql-md.md)] 查詢 (參考永遠加密資料行) 的資料。
  
- 來自 [!INCLUDE[tsql](../includes/tsql-md.md)] 查詢 (參考遮罩資料行) 的資料。
  
     若您需要在 R 指令碼中使用遮罩的資料，一項可行的因應措施是在暫存資料表中製作資料複本，並改用該資料。

### <a name="use-of-strings-as-factors-can-lead-to-performance-degradation"></a>做為字串的因素可能會導致效能降低

當因素可以大幅增加的 R 作業所使用的記憶體數量，請使用字串類型變數。 一般情況下，這是 R 的已知的問題，並在主體上有許多篇文章。 例如，請參閱[因素不是在 R 中，John 掛接，r-bloggers 中的首要)](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/)或[stringsAsFactors： 未經授權的自傳，由 Roger Peng](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/)。 

雖然並非 SQL Server 特定的問題，但它可能會大幅影響執行 SQl Server 中的 R 程式碼的效能。 字串通常會儲存為 varchar 或 nvarchar，以及如果字串資料行有許多唯一值，在內部轉換為整數，再回到字串 R 的這些程序甚至可能導致記憶體配置錯誤。

如果您不絕對需要字串資料類型的其他作業，將字串值對應至數字 （整數） 資料類型的資料準備過程中會很有幫助效能與延展性的觀點。

如需此問題和其他提示的討論，請參閱[R Services-資料最佳化的效能](r/r-and-data-optimization-r-services.md)。

### <a name="arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>引數*varsToKeep*和*varsToDrop*不支援 SQL Server 資料來源

當您使用 rxDataStep 函式將結果寫入至資料表時，使用*varsToKeep*和*varsToDrop*是很方便的方式來指定要包含或排除作業的資料行。 不過，這些引數不支援的 SQL Server 資料來源。

### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>中的 SQL 資料類型的有限的支援`sp_execute_external_script`

並非 SQL 支援的所有資料類型都能用在 R。因應措施是考慮將不支援的資料類型先轉換成支援的資料類型，再將資料傳遞至 sp_execute_external_script。

如需詳細資訊，請參閱[R 程式庫和資料型別](r/r-libraries-and-data-types.md)。

### <a name="possible-string-corruption"></a>字串可能損毀

從字串資料的任何往返[!INCLUDE[tsql](../includes/tsql-md.md)]到 R 再到[!INCLUDE[tsql](../includes/tsql-md.md)]一次會造成損毀。 這是因為在 R 和使用的編碼不同[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，不同的定序及支援的 R 語言和[!INCLUDE[tsql](../includes/tsql-md.md)]。 任何非 ASCII 編碼的字串都可能不正確地處理。

當您字串資料傳送給 R 時，將其轉換為 ASCII 表示法，如果可能的話。

這項限制適用於以及 SQL Server，並將 Python 之間傳遞資料。 多位元組字元應該傳遞為 utf-8，並儲存為 Unicode。

### <a name="only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>只有一個值的型別`raw`可從傳回`sp_execute_external_script`

當二進位資料類型 (R**原始**資料類型) 會傳回從 R，則必須將值傳送的輸出資料框架中。

具有資料類型以外**原始**，您可以藉由加入輸出關鍵字傳回參數值，以及預存程序的結果。 如需詳細資訊，請參閱[參數](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters)。

如果您想要使用包含的類型值的多個輸出集**原始**，其中一個可能的解決方法，是要進行多次呼叫預存程序，或傳送結果集傳回[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用 ODBC。

### <a name="loss-of-precision"></a>遺失有效位數

因為[!INCLUDE[tsql](../includes/tsql-md.md)]和 R 支援不同的資料類型，數值資料類型可以在轉換期間，會遺失有效位數。

如需有關隱含資料類型轉換的詳細資訊，請參閱[R 程式庫和資料型別](r/r-libraries-and-data-types.md)。

### <a name="variable-scoping-error-when-you-use-the-transformfunc-parameter-the-sample-data-set-for-the-analysis-has-no-variables"></a>變數約制錯誤，當您使用 transformFunc 參數：*分析取樣資料集沒有任何變數*

當您建立模型時，將資料轉換，您可以傳遞*transformFunc*等函數中的引數`rxLinmod`或`rxLogit`。 不過，巢狀的函數呼叫可能會導致發生約制錯誤，SQL Server 計算內容中，即使本機計算內容中呼叫運作正常。

例如，假設您已定義兩個函式，`f`和`g`，在您的本機全域環境中和`g`呼叫`f`。 在涉及 `g`的分散式或遠端呼叫中，即使您已將 `g` 和 `f` 都傳遞給遠端呼叫，對 `f` 的呼叫也可能會因為找不到 `g` 而失敗。

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

當函式，如`rxDataStep`用來建立資料庫資料表，其中有**varchar**預估根據資料的範例資料行，資料行寬度。 若寬度會有差異，可能必須將所有字串都填補到常見長度。

使用 `rxImport` 或 `rxTextToXdf` 的重複呼叫來匯入或附加資料列，將多個輸入檔案結合成單一 .xdf 檔案時，不支援使用轉換來變更變數的資料類型。

### <a name="limited-support-for-rxexec"></a>有限的支援 rxExec

在 SQL Server 2016，`rxExec`是提供可以在使用 RevoScaleR 封裝只能在單一執行緒模式中的函式。

平行處理原則`rxExec`多個處理序已計劃針對未來的版本。

### <a name="increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>參數大小上限以支援 rxGetVarInfo

如果您使用的變數數目極大的資料集 (例如 40,000) 上，設定`max-ppsize`旗標，當您開始使用函式，例如 R `rxGetVarInfo`。 `max-ppsize` 旗標會指定指標保護堆疊的大小上限。

如果您使用 R 主控台 （例如，RGui.exe 或 RTerm.exe），您可以設定的值_max ppsize_設為 500000，輸入：

```R
R --max-ppsize=500000
```

### <a name="issues-with-the-rxdtree-function"></a>RxDTree 函數的問題

`rxDTree` 函數目前不支援公式內的轉換。 尤其不支援使用 `F()` 語法即時建立因數。 不過，自動分類收納數字資料。

要求的因數會被視為與所有 RevoScaleR 分析函數中的因數相同，除了 `rxDTree`以外。

## <a name="python-code-execution-or-python-package-issues"></a>Python 程式碼執行，或是 Python 封裝問題

本節包含專屬於 SQL Server，以及 Microsoft 所發行的 Python 封裝相關的問題上執行 Python 的已知的問題包括[revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)和[microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

### <a name="call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>預先定型的模型的呼叫失敗，則模型路徑太長

如果您在 SQL Server 2017 早期發行版本中安裝預先定型的模型，定型的模型檔案的完整路徑可能會對讀取 Python 而言太長。 這項限制被固定的下一個版本的服務。

有數個可能的因應措施： 

+ 當您安裝的預先定型的模型時，請選擇 自訂位置。
+ 可能的話，請使用較短的路徑，例如 C:\SQL\MSSQL14 安裝自訂安裝路徑下的 SQL Server 執行個體。MSSQLSERVER。
+ 使用 Windows 公用程式[Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx)建立永久連結的來源，將模型檔案對應到較短的路徑。 
+ 更新為最新版本更新服務。

### <a name="failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>無法初始化 varbinary 變數 BxlServer 會導致錯誤

如果您執行 Python 程式碼中使用 SQL Server `sp_execute_external_script`，而且程式碼具有輸出類型 varbinary （max）、 varchar （max） 或類似類型的變數，變數必須初始化，或您的指令碼中設定。 否則，資料 exchange 元件 BxlServer，會引發錯誤並停止運作。

這項限制會在服務即將發行版本中修正。 因應措施，請確定變數會初始化 Python 指令碼內。 可以使用任何有效的值，如下列範例所示：

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

### <a name="telemetry-warning-on-successful-execution-of-python-code"></a>在成功執行 Python 程式碼的遙測警告

從 SQL Server 2017 CU2，即使已成功執行 Python 程式碼，否則可能會出現下列訊息：

```text
STDERR message(s) from external script:  ~PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger
SyntaxWarning: telemetry_state is used prior to global declaration
```

SQL Server 2017 累計更新 3 (CU3) 中已修正此問題。 

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise 和 Microsoft R Open

此區段會列出 R 連線能力、 開發和 Revolution Analytics 所提供的效能工具的特定問題。 這些工具提供的發行前版本中[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]。

一般情況下，我們建議您先解除安裝這些舊版，並安裝最新版的 SQL Server 或 Microsoft R Server。

### <a name="revolution-r-enterprise-is-not-supported"></a>Revolution R Enterprise 不支援

安裝任何版本的 Revolution R Enterprise 並存[!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)]不支援。

如果您有現有的授權 for Revolution R Enterprise 時，您就必須將它放在同時從另一部電腦[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體與您要用來連接到任何工作站[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體。

某些發行前版本[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]包含適用於 Windows 的 Revolution Analytics 建立的 R 開發環境。 此工具不再提供，並不支援。

相容性[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]，我們建議您改為安裝 Microsoft R 用戶端。 [Visual Studio 的 R 工具](https://www.visualstudio.com/vs/rtvs/)和[Visual Studio Code](https://code.visualstudio.com/)也支援 Microsoft R 解決方案。

### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>SQLite ODBC 驅動程式與 RevoScaleR 的相容性問題

SQLite ODBC 驅動程式的修訂 0.92 是與 RevoScaleR 不相容。 修訂 0.88-0.91 和 0.93 及更新版本則已知相容性。

## <a name="see-also"></a>另請參閱

[SQL Server 2016 的新功能](../sql-server/what-s-new-in-sql-server-2016.md)

[疑難排解 SQL Server 中的機器學習服務](machine-learning-troubleshooting-faq.md)
