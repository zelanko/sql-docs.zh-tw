---
title: "疑難排解 SQL Server 的機器學習-資料收集"
ms.custom: 
ms.date: 06/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8ebbf404640ab909c500cd5ef39bd5b2b7653a15
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="troubleshoot-data-collection-for-machine-learning"></a>疑難排解機器學習的資料收集

本文將討論當您嘗試解決問題的安裝程式、 組態或了解 SQL Server 中的機器的效能時，即應收集的資料種類。 這些資料包括記錄、 錯誤訊息，以及系統資訊。

本文將告訴您最有用的資訊來源當您執行診斷自助為基礎。 收集這項資訊也很有用時要求 SQL Server 的機器學習功能的相關問題的技術支援人員。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 機器學習服務 （R 和 Python）

## <a name="sql-server-and-r-versions"></a>SQL Server 和 R 版本

請注意版本是否為新的安裝或升級。 如果是升級，來判斷執行方式：

- 您未從升級哪個版本？ 
- 您是否已移除舊的元件，或您升級就地？
- 您在升級期間變更任何功能選取項目嗎？ 

### <a name="which-edition-of-sql-server-is-installed-and-which-version"></a>已安裝哪些版本的 SQL Server，以及哪個版本？ 

SQL Server 2016 中引進了 SQL Server R Services。 先前的版本不支援機器學習。 此外，2016年發行的後續 service pack 包含許多 bug 修正和增強功能。 第一個步驟中，您應該考慮安裝 Service Pack 1 或更新版本。

在 SQL Server 2017，支援已擴充為 Python 語言。 在舊版中未提供對 Python 的支援。

如果您需要協助以判斷有哪些版本及版本，請參閱這篇文章會針對每個列出的組建編號， [SQL Server 版本](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions)。

根據您所使用的 SQL Server 版本中，有些機器學習功能可能無法使用，或只有有限的。

請參閱下列主題中的 Enterprise、 Developer、 Standard 和 Express 版本中的機器學習功能清單。

* [版本和支援的 SQL Server 功能](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016)
* [R 功能的 SQL Server 版本之間的差異](https://docs.microsoft.com/sql/advanced-analytics/r/differences-in-r-features-between-editions-of-sql-server)

### <a name="which-version-of-microsoft-r-is-installed"></a>所安裝的 Microsoft R 版本？

當您選取的 R 服務功能或機器學習服務功能已安裝的 Microsoft R 版本在一般情況下，取決於 SQL Server 組建編號。 如果您升級或修補程式 SQL Server，您也必須升級或修補程式及其 R 元件。

如需的版本與 R 元件下載的連結清單，請參閱[安裝沒有網際網路存取的機器學習元件](https://docs.microsoft.com/sql/advanced-analytics/r/installing-ml-components-without-internet-access)。 在電腦上具有網際網路存取權，必要的 R 版本，同時自動安裝。

您可個別升級 R 伺服器元件，從稱為繫結的程序中的 SQL Server 資料庫引擎。 因此，您使用 SQL Server 中執行 R 程式碼時的 R 版本可能會與不同，視安裝的 SQL Server 版本和是否有伺服器移轉到最新的 R 版本而定。

#### <a name="determine-the-r-version"></a>判斷 R 版本

若要判斷 R 版本最簡單方式是，以取得執行階段屬性執行的陳述式，如下所示：

```SQL
exec sp_execute_external_script
       @language = N'R'
       , @script = N'
# Transform R version properties to data.frame
OutputDataSet <- data.frame(
  property_name = c("R.version", "Revo.version"), 
  property_value = c(R.Version()$version.string, Revo.version$version.string),
  stringsAsFactors = FALSE)
# Retrieve properties like R.home, libPath & default packages
OutputDataSet <- rbind(OutputDataSet, data.frame(
  property_name = c("R.home", "libPaths", "defaultPackages"),
  property_value = c(R.home(), .libPaths(), paste(getOption("defaultPackages"), collapse=", ")),
  stringsAsFactors = FALSE)
)
'
WITH RESULT SETS ((PropertyName nvarchar(100), PropertyValue nvarchar(4000)));

```

> [!TIP] 
> 如果 R 服務沒有運作，請嘗試從 RGui 執行 R 指令碼部份。

最後一個步驟中，您可以開啟來判斷已安裝的版本的伺服器上的檔案。 若要這樣做，請找出 rlauncher.config 檔案，以取得 R 執行階段和目前工作目錄的位置。 我們建議您製作並開啟檔案的複本，因此您不小心不要變更任何屬性。

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

若要取得的 R 版本與 RevoScaleR 版本，開啟 R 命令提示字元中，或開啟具有執行個體相關聯 RGui。

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`


R 主控台會在啟動時顯示的版本資訊。 例如，下列版本代表 SQL Server 2017 CTP 2.0 的預設組態：

    *Microsoft R Open 3.3.3*
    
    *The enhanced R distribution from Microsoft*
    
    *Microsoft packages Copyright (C) 2017 Microsoft*
    
    *Loading Microsoft R Server packages, version 9.1.0.*


### <a name="what-version-of-python-is-installed"></a>已安裝的 Python 版本？

僅適用於 SQL Server 2017 社群技術預覽 (CTP) 2.0 和更新版本 Python 的支援。

有幾種方式可取得的 Python 版本。 最簡單的方式是從 Management Studio 或任何其他的 SQL 查詢工具執行此陳述式：

```SQL
-- Get Python runtime properties:
exec sp_execute_external_script
       @language = N'Python'
       , @script = N'
import sys
import pkg_resources
OutputDataSet = pandas.DataFrame(
                    {"property_name": ["Python.home", "Python.version", "Revo.version", "libpaths"],
                    "property_value": [sys.executable[:-10], sys.version, pkg_resources.get_distribution("revoscalepy").version, str(sys.path)]}
)
'
with WITH RESULT SETS (SQL keywords) ((PropertyName nvarchar(100), PropertyValue nvarchar(4000)));
```

如果機器學習服務未在執行中，您可以查看 pythonlauncher.config 檔來判斷已安裝的 Python 版本。 我們建議您製作並開啟檔案的複本，因此您不小心不要變更任何屬性。

1. 僅適用於 SQL 伺服器 2017年:`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config `
2. 取得值**PYTHONHOME**。
3. 取得目前工作目錄的值。


> [!NOTE]
> 如果您有安裝 Python 和 R 中 SQL Server 2017，工作目錄和背景工作帳戶的集區共用的 R 和 Python 語言。

### <a name="are-multiple-instances-of-r-or-python-installed"></a>R 的多個執行個體或 Python 安裝嗎？

請檢查電腦上是否已安裝的 R 程式庫的多個複本。 如果，可能會發生這種重複狀況：

* 在安裝期間您可以選取 R 服務 （資料庫） 和 R 伺服器 （獨立）。 
* 您安裝 Microsoft R 用戶端，除了 SQL Server。
* 使用 R Tools for Visual Studio、 R Studio、 Microsoft R 用戶端或其他的 R IDE，已安裝一組不同的 R 程式庫。
* 電腦主控多個 SQL Server 執行個體和一個以上的執行個體會使用機器學習。

相同的條件是套用至 Python。

如果您發現安裝多個程式庫或執行階段，請確定您取得只有 SQL Server 執行個體所使用的 Python 或 R 執行階段的相關錯誤。

## <a name="errors-and-messages"></a>錯誤和訊息

當您嘗試執行 R 程式碼時，您會看到的錯誤可以來自任何下列來源：

- SQL Server 資料庫引擎，包括預存程序 sp_execute_external_script
- 信任的 SQL Server Launchpad 
- 擴充性架構，包括 R，並將 Python launchers 和附屬程序的其他元件
- 提供者，例如 Microsoft 開啟資料庫連接 (ODBC)
- R 語言

當您使用第一次服務時，可能很難判斷哪些訊息是來自哪一個服務。 我們建議您擷取不僅確切的訊息文字，而且您已看到訊息的內容。 請注意您用來執行機器學習程式碼的用戶端軟體：

- 您會使用 Management Studio 嗎？ 外部應用程式嗎？
- 在遠端用戶端，或直接在預存程序中執行 R 程式碼的？

### <a name="what-errors-has-sql-server-logged"></a>SQL Server 已記錄哪些錯誤？

取得最新的 SQL Server 錯誤記錄檔。 一組完整的錯誤記錄檔包含下列的預設記錄目錄中的檔案：

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE] 
> 一模一樣的資料夾名稱而異的執行個體名稱。


### <a name="what-errors-were-returned-by-the-spexecuteexternalscript-command"></a>Sp_execute_external_script 命令所傳回哪些錯誤？

如果有的話，當您執行 sp_execute_external_script 命令，取得會傳回錯誤的完整文字。 

若要將不考慮移除 R 或 Python 的問題，您可以執行這個指令碼，會啟動 R 或 Python 執行階段和來回傳遞資料。

**R**

```sql
exec sp_execute_external_script @language =N'R',  
@script=N'OutputDataSet<-InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

**Python**

```sql
exec sp_execute_external_script @language =N'Python',  
@script=N'OutputDataSet= InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

### <a name="what-errors-are-generated-by-the-extensibility-framework"></a>擴充性架構，會產生哪些錯誤？

SQL Server 會產生不同的外部指令碼語言執行階段記錄檔。 這些錯誤不會產生 Python 或 R 語言。 它們是從 SQL Server，包括語言特有 launchers 和其附屬程序中的擴充性元件所產生。

您可以從下列的預設位置，以取得這些記錄檔：

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog `

> [!NOTE] 
> 一模一樣的資料夾名稱與此執行個體名稱。 根據您的組態資料夾可能在不同的磁碟機上。

例如，下列記錄檔訊息與擴充性架構：

* *使用者 MSSQLSERVER01 LogonUser 失敗*
  
  這可能表示執行外部指令碼的背景工作帳戶無法存取執行個體。

* *InitializePhysicalUsersPool 失敗* 
  
  此訊息可能表示，您的安全性設定會導致安裝程式無法建立所需執行外部指令碼的背景工作帳戶的集區。

* *安全性內容管理員初始化失敗* 

* *附屬項目工作階段管理員初始化失敗*

### <a name="are-there-any-related-system-events"></a>是否有任何相關的系統事件？

1. 開啟 Windows 事件檢視器，並搜尋**系統事件**記錄檔中的訊息，其中包含字串*啟動控制板*。 
2. 開啟 ExtLaunchErrorlog 檔案，並尋找字串*ErrorCode*。 檢視訊息與錯誤碼相關聯。

例如，下列訊息是 SQL Server 擴充性架構與相關的常見系統錯誤： 

* *SQL Server Launchpad (MSSQLSERVER) 服務無法啟動，因為發生下列錯誤：<text>*

* *服務未啟動或控制要求能夠及時回應。* 

* *逾時等候連接 SQL Server Launchpad (MSSQLSERVER) 服務達到 （120000 毫秒為單位）。* 

### <a name="did-any-components-start-and-then-crash"></a>沒有任何元件啟動，然後損毀？

如果您了解偵錯時，您可以使用傾印檔案來分析 [啟動列] 中的失敗。

1. 找出包含 SQL Server 安裝程式的啟動程序記錄檔的資料夾。 例如，在 SQL Server 2016 中，預設路徑為 C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log。
2. 開啟啟動程序的記錄子資料夾的特定擴充性。
3. 如果您需要提交支援要求，將此資料夾的整個內容加入 zip 檔案。 例如，C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog。
  
確切的位置可能會與您系統上的不同，而且它可能在 C 磁碟機以外的磁碟機上。 請務必取得機器學習服務安裝所在的執行個體的記錄。 


## <a name="related-tools-and-configuration"></a>相關的工具和設定

此區段會列出其他元件，或是當您執行 R 或 Python 指令碼時，可能是錯誤的來源提供者。

### <a name="what-network-protocols-are-available"></a>哪些網路通訊協定可供使用？

機器學習服務需要下列網路通訊協定擴充性元件之間的內部通訊，以及與外部 R 或 Python 用戶端進行通訊。

* 具名管道
* TCP/IP

開啟 SQL Server 組態管理員來判斷是否已安裝的通訊協定，如果已安裝，以判斷是否已啟用。

### <a name="security-configuration-and-permissions"></a>安全性組態和權限

背景工作帳戶：

1. 在控制台中開啟**使用者和群組**，並找出用來執行外部指令碼作業的群組。 根據預設，群組是**SQLRUserGroup**。
2. 請確認此群組存在且其中包含至少一個背景工作帳戶。
3. 在 SQL Server Management Studio，選取 執行個體，其中 R 或 Python 工作執行，則選取**安全性**，然後決定是否為 SQLRUserGroup 的登入。
4. 檢閱使用者群組的權限。

為個別使用者帳戶：

1. 判斷執行個體支援混合模式驗證，SQL 登入或僅限 Windows 驗證。 這個設定會影響您的 R 或 Python 程式碼的需求。
2. 每個使用者需要執行 R 程式碼，決定需要的每個資料庫，其中將寫入物件、 可存取資料，或將會建立物件的權限等級。
3. 若要啟用指令碼執行，建立角色，或將使用者新增至下列角色，在必要時：

   - 以外的所有*db_owner*： 需要 EXECUTE ANY EXTERNAL SCRIPT。
   - *db_datawriter*： 從 R 或 Python 寫入結果。 
   - *db_ddladmin*： 若要建立新的物件。 
   - *db_datareader*： 讀取資料，以供 R 或 Python 程式碼。 
4. 請注意是否安裝 SQL Server 2016 時變更任何預設的啟動帳戶。
5. 如果使用者需要安裝新的 R 封裝，或使用其他使用者所安裝的 R 封裝，您可能需要啟用執行個體上的封裝管理，然後再指派其他權限。 如需詳細資訊，請參閱[啟用或停用的 R 封裝管理](r\r-package-how-to-enable-or-disable.md)。

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>防毒軟體鎖定受限於哪些資料夾？

防毒軟體可以鎖定資料夾，使這兩個機器學習功能和成功的指令碼執行的安裝程式。 判斷是否受病毒掃描 SQL 伺服器樹狀目錄中的任何資料夾。

不過，當執行個體上安裝了多個服務或功能，很難列舉執行個體所使用的所有可能資料夾。 比方說，當您加入新功能，新的資料夾必須是識別和排除。

此外，某些功能建立新的資料夾以動態方式在執行階段。 比方說，記憶體中 OLTP 資料表、 預存程序和函式所有執行階段建立新的目錄。 這些資料夾名稱通常會包含 Guid，而且無法預測。 SQL Server 信任 Launchpad R 為建立新的工作目錄和 Python 指令碼工作。

因為它不可能排除所有的資料夾所需的 SQL Server 處理序和它的功能，我們建議您排除整個 SQL Server 執行個體目錄樹狀結構。

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>適用於 SQL Server 在防火牆開啟？ 執行個體是否支援遠端連線？

1. 若要判斷 SQL Server 是否支援遠端連線，請參閱[設定遠端伺服器連接](../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md)。

2. 判斷是否已經建立 SQL Server 的防火牆規則。 基於安全性理由，在預設安裝中，它可能不會為遠端 R 或 Python 用戶端，連接到執行個體。 如需詳細資訊，請參閱[疑難排解連接到 SQL Server](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)。

### <a name="can-you-run-r-script-outside-t-sql"></a>您可以執行 R 指令碼外 T-SQL 嗎？

您可以嘗試執行 R 執行階段相關聯 SQL Server 執行個體使用其他的 R 工具。 這樣一來，您可以判斷是否已安裝必要的程式庫。

R 的基底安裝包含多項工具可讓您從命令列，以及 RGui 的 R 指令碼執行的指令碼的互動執行。

如果 R 執行階段正常運作，但您的指令碼會傳回錯誤，我們建議您嘗試偵錯專用的 R 開發環境，例如 R Tools for Visual Studio 中的指令碼。

我們也建議您檢閱，並可稍微重寫指令碼來更正 R 和 database engine 之間移動資料時可能發生的資料類型的任何問題。 如需詳細資訊，請參閱[R 程式庫和資料型別](r/r-libraries-and-data-types.md)。

此外，您可以使用 sqlrutils 封裝來封裝您的 R 指令碼是做為預存程序更方便取用的格式。 如需詳細資訊，請參閱：
* [使用 sqlrutils 封裝產生 R 程式碼的預存程序](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
* [使用 sqlrutils 建立預存程序](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="see-also"></a>另請參閱

[疑難排解 SQL Server 中的機器學習服務](machine-learning-troubleshooting-faq.md)
