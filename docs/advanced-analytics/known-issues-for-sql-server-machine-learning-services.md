---
title: "機器學習服務的已知問題 |Microsoft 文件"
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
ms.assetid: 2b37a63a-5ff5-478e-bcc2-d13da3ac241c
caps.latest.revision: 53
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b7b9d53a87490e83f888b47b1cff87191b9693a8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="known-issues-for-machine-learning-services"></a>機器學習服務的已知的問題

本主題描述已知的問題或限制使用機器學習中 SQL Server 2016 和 SQL Server 2017 的選項中提供的元件。

除非特別指示，適用於所有下列：

+ SQL Server 2016

  - R 服務 (資料庫內)
  - Microsoft R Server (獨立式)

+ SQL Server 2017

  - 機器學習服務 （資料庫）
  - 機器學習服務 for Python （資料庫）
  - Machine Learning 伺服器 (獨立式)

## <a name="setup-and-configuration-issues"></a>安裝和組態問題

這裡列出與初始安裝和設定相關的處理和一般問題的描述：[升級及安裝常見問題集](r/upgrade-and-installation-faq-sql-server-r-services.md)。

另請參閱本文的升級、-並存安裝及安裝新的 R 或 Python 元件的相關資訊。

### <a name="unable-to-install-python-components-in-in-offline-installs-of-sql-server-2017"></a>無法安裝在離線的 Python 元件中安裝的 SQL Server 2017

如果您沒有網際網路存取的電腦上安裝 SQL Server 2017，安裝程式可能無法顯示頁面，提示為元件的位置下載 Python;因此，您可以安裝的機器學習服務功能，而非 Python 元件。

近期版本中，將會修正此問題。 因應措施，您可以暫時安裝期間啟用網際網路存取。 這項限制不適用於。

**適用於：** SQL Server 2017 使用 Python

### <a name="install-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>安裝最新的服務版本確保與 Microsoft R Client 相容

如果您安裝最新版的 Microsoft R 用戶端，並使用它來執行 R 使用遠端 SQL Server 計算內容，您可能會發生錯誤，如下所示：

*您正在 Microsoft R 用戶端版本 9.x.x 您與 Microsoft R Server 版本 8.x.x 不相容的電腦。請下載並安裝相容版本。*

SQL Server 2016 所需的用戶端上的 R 程式庫會完全符合伺服器上的 R 程式庫。 限制已移除該版本的 R 伺服器 9.0.1 較新版本。 不過，如果您遇到這個錯誤，請確認您的用戶端使用此版本的 R 程式庫和 nad 必要時，伺服器更新用戶端與伺服器版本相符。

安裝 SQL Server 服務版本時，會更新 R 與 SQL Server R Services 一起安裝的版本。 因此，若要確保一直擁有最新版本的 R 元件，您應該安裝所有 service pack。

為與 Microsoft R Client 9.0.0 相容，您必須安裝本 [技術支援文件](https://support.microsoft.com/kb/3210262)中描述的更新。

若要避免發生問題的 R 封裝，您也可以升級會在伺服器上，安裝中所述，將變更為現代化的生命週期原則的 R 程式庫版本[本節](#bkmk_sqlbindr)。 當您這樣做時，R 與 SQL Server 一起安裝的版本會更新相同的排程的更新會發行 Microsoft R 伺服器，請確定伺服器和用戶端永遠可以有最新版本的 Microsoft。

**適用於：** SQL Server 2016 R Services 中，使用 R Server 9.0.0 版本或更早版本

### <a name="bkmk_sqlbindr"></a>從使用的用戶端連接到舊版的 SQL Server R Services 時，不相容版本的警告[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

如已使用 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] 安裝精靈或 [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)的新獨立安裝程式，在用戶端電腦上安裝 Microsoft R Server，並在使用舊版的 SQL Server R Services 計算內容中執行 R 程式碼，您可能會看到類似下列的錯誤︰

*您電腦上執行的是 9.0.0 版的 Microsoft R Client，與 Microsoft R Server 8.0.3 版不相容。請下載並安裝相容版本。*

Microsoft R Server 9.0 版提供的 **SqlBindR.exe** 工具支援 SQL Server 執行個體升級到相容的 9.0 版。 在 SQL Server 服務即將發行的服務版本中，會加入 R Services 執行個體升級至 9.0 的支援。 適合未來的升級版本包含 SQL Server 2016 RTM CU3 + SP1 + 和 SQL Server 2017 CTP 1.1。

**適用於：** SQL Server 2016 R Services 中，使用 R Server 9.0.0 版本或更早版本

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>SQL Server 2016 服務版本的安裝程式可能無法安裝較新版本的 R 元件

當您安裝累積更新，或在未連接到網際網路的電腦上安裝 SQL Server 2016 Service Pack 時，安裝精靈可能無法顯示提示，以讓您使用下載的封包檔來更新 R 元件。 當多個元件和資料庫引擎一起安裝時通常會發生此問題。

因應措施，您可以使用命令列，並指定安裝的版本更新服務*/MRCACHEDIRECTORY*引數，此範例中，這會安裝 CU1 更新中所示：

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

若要取得最新的安裝程式，請參閱[安裝機器學習 Components without Internet Access](r/installing-ml-components-without-internet-access.md)。

**適用於：** SQL Server 2016 R Services 中，使用 R Server 9.0.0 版本或更早版本

### <a name="launchpad-services-fails-to-start-if-version-is-different-than-r-version"></a>如果版本與 R 版本不同，Launchpad 服務無法啟動。

如果您安裝 R 服務分別從資料庫引擎，而且組建版本不同，您可能會看到系統事件記錄檔中的這個錯誤：_的 SQL Server Launchpad 服務無法啟動，因為發生下列錯誤： 服務不提供支援啟動或控制要求能夠及時回應。_

例如，如果您安裝使用發行版本的資料庫引擎、套用修補程式以升級資料庫引擎，然後加入使用發行版本的 R Services，可能會發生此錯誤。

為避免此問題，請確定所有的元件都有相同的版本號碼。 如果升級某個元件，所有其他已安裝的元件請務必套用相同的升級。

若要檢視 SQL Server 2016 各版本所需的 R 版本號碼清單，請參閱 [安裝沒有網際網路存取的 R 元件](r/installing-ml-components-without-internet-access.md)。

### <a name="remote-compute-contexts-blocked-by-firewall-in-sql-server-instances-running-on-azure-virtual-machines"></a>遠端計算內容遭到執行於 Azure 虛擬機器的 SQL Server 執行個體中防火牆封鎖

若您在 Windows Azure 虛擬機器上安裝了 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] ，則可能無法使用需要虛擬機器工作區的計算內容。 原因在於 Azure VM 防火牆預設包含會封鎖本機 R 使用者帳戶網路存取權的規則。

因應措施是在 Azure VM 上開啟 [具有進階安全性的 Windows 防火牆] ，選取 [輸出規則] ，然後停用以下規則：「封鎖 SQL Server 執行個體 MSSQLSERVER 中 R 本機使用者帳戶的網路存取權」。

### <a name="implied-authentication-in-sqlexpress"></a>SQLEXPRESS 的隱含驗證

當您從使用 Windows 整合式驗證的遠端資料科學工作站執行 R 作業時，SQL Server 會使用「隱含的驗證」  來產生指令碼可能需要的任何本機 ODBC 呼叫。 不過，這項功能在 SQL Server Express Edition 的 RTM 組建中不作用。

若要修正此問題，建議您升級至較新的服務版本。

如果無法升級，您可以使用 SQL 登入來執行可能需要內嵌 ODBC 呼叫的遠端 R 作業。

**適用於：** SQL Server 2016 R Services Express Edition

### <a name="performance-limits-when-r-libraries-are-called-from-standalone-r-tools"></a>從獨立 R 工具呼叫 R 程式庫時，會限制效能

您可呼叫的 R 工具和程式庫從 RGui 之類的外部 R 應用程式安裝的 SQL Server R Services。 當您安裝新的封裝，或在非常短的程式碼範例執行臨機操作測試，這可能會很方便。

不過，請注意，SQL Server 外部的效能會受到限制。 例如，即使您已購買 SQL Server 的 Enterprise Edition，R 將執行單一執行緒模式中執行 R 程式碼使用外部工具時。 效能會更好，如果您執行 R 程式碼起始的 SQL Server 連接，並使用[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，這會為您呼叫 R 程式庫。

+ 避免從外部 R 工具呼叫 SQL Server 所使用的 R 程式庫。
+ 如果您需要 SQL Server 電腦上執行大量的 R 程式碼，而不使用 SQL server 安裝 R，例如 Microsoft R 用戶端，個別執行個體，然後確定您的 R 開發工具會指向新的程式庫。

如需詳細資訊，請參閱 [建立獨立式 R Server](r/create-a-standalone-r-server.md)。

### <a name="r-script-throttled-due-to-resource-governance-default-values"></a>因為資源控管的預設值，所以節流的 R 指令碼

在 Enterprise Edition 中，您可以使用資源集區來管理外部指令碼程序。 在某些早期發行的組建，無法配置給 R 處理序的最大記憶體為 20%。 因此，如果伺服器有 32 GB 的 RAM，R 可執行檔 (RTerm.exe 和 BxlServer.exe) 無法在單一要求中使用上限 6.4 GB。

如果遇到資源限制，請檢查目前的預設值，如果 20% 不夠，請參閱 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的文件以了解如何變更此值。

**適用於：** SQL Server 2016 R 服務、 企業版

## <a name="r-code-execution-and-package-or-function-issues"></a>執行 R 程式碼和封裝或函式的問題

本節包含專屬於 SQL Server 上執行 R 的已知的問題，以及與 R 程式庫和工具由 Microsoft，包括 RevoScaleR 發行相關的一些問題。

如需其他可能會影響 R 解決方案的已知的問題，請參閱 Microsoft R Server 站台：[與 Microsoft R Server 的已知問題](https://msdn.microsoft.com/microsoft-r/rserver-known-issues)

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>R 作業處理器相似性的限制

在 SQL Server 2016 的初始發行版本，您可以設定只會針對第一個 k 群組中的 Cpu 處理器親和性。 例如，如果伺服器是有 2 個 k 群組的雙通訊端機器，R 處理程序只會使用第一個 k 群組中的處理器。 設定 R 指令碼作業的資源控管時，適用相同的限制。

SQL Server 2016 Service Pack 1 已修正這個問題。

**適用於：** SQL Server 2016 R 服務 RTM 版本

### <a name="changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>讀取 SQL Server 計算內容中的資料，無法變更資料行類型。

如果您的計算內容設為 SQL Server 執行個體，則您無法使用 _colClasses_ 引數 (或其他類似的引數) 來變更 R 程式碼中的資料行資料類型。

例如，如果資料行 CRSDepTimeStr 還不是整數，則下列陳述式會產生錯誤︰

~~~~
data <- RxSqlServerData(sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall",
                                connectionString = connectionString,
                                colClasses = c(CRSDepTimeStr = "integer"))
~~~~

未來版本會修正此問題。

因應措施是，您可以重新撰寫 SQL 查詢以使用 CAST 或 CONVERT，並使用正確的資料類型向 R 呈現資料。 通常最好是使用 SQL 時能有效使用資料，而不是在 R 程式碼中變更資料。

**適用於：** SQL Server 2016 R 服務

### <a name="avoid-clearing-workspaces-when-executing-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>避免在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 計算內容中執行 R 程式碼時清除工作區。

如果在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 計算內容中執行 R 程式碼時，使用 R 命令清除物件工作區，或如果將工作區當成使用 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)呼叫之 R 指令碼的一部分清除，您可能會發生此錯誤︰找不到工作區物件 'revoScriptConnection'。 

`revoScriptConnection` 是 R 工作區的物件，包含從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]呼叫之 R 工作階段的相關資訊。 不過，如果 R 程式碼包含清除工作區的命令，例如 `rm(list=ls()))`，則也會清除工作階段所有資訊和 R 工作區的其他物件。

因應措施是在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中執行 R 時，避免任意清除變數和其他物件。 雖然在 R 主控台內工作時，清除工作區是常見的，但它可能造成意料之外的結果。

+ 若要刪除特定的變數，請使用 R「移除」  函數︰ `remove('name1', 'name2', ...)`
+ 如有多個變數要刪除，請將暫存變數名稱儲存至清單，並執行定期記憶體回收。

### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>可作為輸出提供給 R 指令碼的資料限制

您無法在 R 指令碼中使用下列類型的查詢結果：

- 來自 [!INCLUDE[tsql](../includes/tsql-md.md)] 查詢 (參考永遠加密資料行) 的資料。
  
- 來自 [!INCLUDE[tsql](../includes/tsql-md.md)] 查詢 (參考遮罩資料行) 的資料。
  
     若您需要在 R 指令碼中使用遮罩的資料，一項可行的因應措施是在暫存資料表中製作資料複本，並改用該資料。

### <a name="arguments-varstokeep-and-varstodrop-not-supported-for-sql-server-data-sources"></a>引數*varsToKeep*和*varsToDrop*不支援 SQL Server 資料來源

當您使用 rxDataStep 函式將結果寫入至資料表時，使用*varsToKeep*和*varsToDrop*是很方便的方式來指定要包含或排除作業的資料行。 目前，SQL Server 資料來源不支援這些引數。

一個版本將移除這項限制。

### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>中的 SQL 資料類型的有限的支援`sp_execute_external_script`

並非 SQL 支援的所有資料類型都能用在 R。因應措施是考慮將不支援的資料類型先轉換成支援的資料類型，再將資料傳遞至 sp_execute_external_script。

如需詳細資訊，請參閱[R 程式庫和資料型別](r/r-libraries-and-data-types.md)。

### <a name="possible-string-corruption"></a>字串可能損毀

任何從 [!INCLUDE[tsql](../includes/tsql-md.md)] 到 R 再到 [!INCLUDE[tsql](../includes/tsql-md.md)] 的字串資料來回行程都可能造成損毀。 這是因為在 R 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中使用的編碼不同，而且 R 和 [!INCLUDE[tsql](../includes/tsql-md.md)]也支援不同定序及語言。 任何非 ASCII 編碼的字串都可能不正確地處理。

請盡可能在將字串資料傳送給 R 時，將其轉換為 ASCII 表示法。

### <a name="only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>只有一個值的型別`raw`可從傳回`sp_execute_external_script`

當 R 傳回二進位資料類型 (R **raw** 資料類型) 時，該值必須是輸出資料框架中的值。

後續版本中將新增多個 **raw** 輸出的支援。

若想要多個輸出集，一項可行的因應措施是對預存程序進行多次呼叫，並使用 ODBC 將結果集傳回 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。

請注意，只要加上 OUTPUT 關鍵字，參數值就可以和預存程序的結果一起傳回。 如需詳細資訊，請參閱 [使用 OUTPUT 參數傳回資料](https://technet.microsoft.com/library/ms187004.aspx)。

### <a name="loss-of-precision"></a>遺失有效位數

[!INCLUDE[tsql](../includes/tsql-md.md)] 和 R 支援不同資料類型；因此數值資料類型可能會在轉換期間遺失有效位數。

如需有關隱含資料類型轉換的詳細資訊，請參閱＜ [Working with R Data Types](r/r-libraries-and-data-types.md)＞。

### <a name="variable-scoping-error-the-sample-data-set-for-the-analysis-has-no-variables-when-using-the-transformfunc-parameter"></a>使用 transformFunc 參數時發生變數約制錯誤「用於分析的範例資料集沒有任何變數」

您可以在 *rxLinmod* 或 `rxLinmod` 等函數中傳遞 `rxLogit` to transf等函數中傳遞m the data while modelling. 不過，巢狀函數呼叫可能會造成 SQL Server 計算內容中發生約制錯誤，即使本機計算內容中的呼叫運作正常亦然。

例如，假設您已在本機全域環境中定義了兩個函數 `f` 和 `g` ，而 `g` 呼叫 `f`。 在涉及 `g`的分散式或遠端呼叫中，即使您已將 `g` 和 `f` 都傳遞給遠端呼叫，對 `f` 的呼叫也可能會因為找不到 `g` 而失敗。

若遇到此問題，您可以在 `f` 定義內嵌 `g`的定義以解決此問題， `g` 前的任何位置則會正常呼叫 `f`。

例如：

```  
f <- function(x) { 2*x + 3 }  
g <- function(y) {   
              a <- 10 * y  
               f(a)  
}  
  
```  


若要避免此錯誤，請重寫，如下所示：

```  
g <- function(y){  
              f <- function(x) { 2*x +3}  
              a <- 10 * y  
              f(a)  
}  
  
```  

### <a name="data-import-and-manipulation-using-revoscaler"></a>使用 RevoScaleR 匯入及操作資料

從資料庫讀取 **varchar** 資料行時，會修剪空白字元。 若要避免此情況，請在字串頭尾使用非空白字元。

使用 `rxDataStep` 等函數建立包含 **varchar** 資料行的資料庫資料表時，會依據資料範例來估計資料行寬度。 若寬度會有差異，則可能需要將所有字串填補到常見長度。

使用 `rxImport` 或 `rxTextToXdf` 的重複呼叫來匯入或附加資料列，將多個輸入檔案結合成單一 .xdf 檔案時，不支援使用轉換來變更變數的資料類型。

### <a name="limited-support-for-rxexec"></a>有限的支援 rxExec

在 SQL Server 2016， `rxExec` RevoScaleR 封裝所提供的函式只能用於單一執行緒模式。

近期版本中將新增多個處理序間的 `rxExec` 平行處理原則。

### <a name="increase-maximum-parameter-size-to-support-rxgetvarinfo"></a>請提高參數大小上限以支援 rxGetVarInfo

若您使用變數數目極大 (例如 40,000 個以上) 的資料集，就必須在啟動 R 時設定 `max-ppsize` 旗標，才能使用 `rxGetVarInfo`等函數。  `max-ppsize` 旗標會指定指標保護堆疊的大小上限。

若您使用 R 主控台 (例如在 rgui.exe 或 rterm.exe)，可以將 max-ppsize 的值設為 500000，方法是輸入：

```  
R --max-ppsize=500000  
```  
  
若您使用的是 [!INCLUDE[rsql_developr](../includes/rsql-developr-md.md)] 環境，則可以設定 `max-ppsize` 旗標，方法是對 RevoIDE 可執行檔進行此呼叫：

```  
RevoIDE.exe /RCommandLine --max-ppsize=500000  
```  

### <a name="issues-with-the-rxdtree-function"></a>RxDTree 函數的問題

`rxDTree` 函數目前不支援公式內的轉換。 尤其不支援使用 `F()` 語法即時建立因數。 不過，數值資料會自動量化。

要求的因數會被視為與所有 RevoScaleR 分析函數中的因數相同，除了 `rxDTree`以外。

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise 和 Microsoft R Open

本節列出 Revolution Analytics 提供的 R 連線能力、開發及效能工具的特定問題。 舊版的  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]發行前版本提供這些工具。 

一般情況下，我們建議您先解除安裝這些舊版，並安裝最新版的 SQL Server 或 Microsoft R Server。

### <a name="running-side-by-side-versions-of-revolution-r-enterprise"></a>並存執行 Revolution R Enterprise 版本

不支援與任何版本 [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] 並存安裝 Revolution R Enterprise。

若您獲授權可使用其他 Revolution R Enterprise 版本，則必須將其放在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體及任何要用以連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的工作站以外電腦。

### <a name="use-of-r-productivity-environment-not-supported"></a>使用 R Productivity Environment 不支援的

某些 [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] 發行前版本包含 Revolution Analytics 建立的 Windows R 開發環境。 此工具不會再提供，並不支援。

相容性[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]，我們強烈建議您安裝 Microsoft R 用戶端或 Microsoft R Server 而不是 Revolution Analytics 工具。 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/) 是支援 Microsoft R 解決方案的另一個建議用戶端。

### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>SQLite ODBC 驅動程式與 RevoScaleR 的相容性問題

SQLite ODBC 驅動程式的修訂 0.92 與 RevoScaleR 不相容；修訂 0.88-0.91 和 0.93 及更新版本則已知相容。

## <a name="see-also"></a>另請參閱

[SQL Server 2016 的新功能](../sql-server/what-s-new-in-sql-server-2016.md)


