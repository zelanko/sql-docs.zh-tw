---
title: 針對機器學習服務的資料收集進行疑難排解
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c7566d9b25b15a334e48380daca6cb81e92f6a2b
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715237"
---
# <a name="troubleshoot-data-collection-for-machine-learning"></a>針對機器學習服務的資料收集進行疑難排解

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明您在嘗試自行解決問題, 或透過 Microsoft 客戶支援服務的協助時, 應使用的資料收集方法。

## <a name="sql-server-version-and-edition"></a>SQL Server 版本和版

SQL Server 2016 R Services 是 SQL Server 的第一版, 其中包含整合式 R 支援。 SQL Server 2016 Service Pack 1 (SP1) 包含數個主要的改良功能, 包括執行外部腳本的能力。 如果您使用 SQL Server 2016, 則應該考慮安裝 SP1 或更新版本。

SQL Server 2017 和更新版本具有 Python 語言整合。 您無法在先前的版本中取得 Python 功能整合。

如需取得版本和版本的協助, 請參閱這篇文章, 其中列出每個[SQL Server 版本](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions)的組建編號。

根據您所使用的 SQL Server 版本而定, 某些機器學習功能可能無法使用或受到限制。 下列文章列出 Enterprise、Developer、Standard 和 Express 版本中的機器學習服務功能。

* [SQL Server 的版本和支援功能](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016)
* [依 SQL Server 版本的 R 和 Python 功能](r/differences-in-r-features-between-editions-of-sql-server.md)

## <a name="r-language-and-tool-versions"></a>R 語言和工具版本

一般而言, 當您選取 [R Services] 功能或 [Machine Learning Services] 功能時所安裝的 Microsoft R 版本, 是由 SQL Server 組建編號所決定。 如果您升級或修補 SQL Server, 您也必須升級或修補其 R 元件。

如需版本和 R 元件下載連結的清單, 請參閱[安裝沒有網際網路存取的機器學習服務元件](https://docs.microsoft.com/sql/advanced-analytics/r/installing-ml-components-without-internet-access)。 在具有網際網路存取的電腦上, 系統會自動識別並安裝所需的 R 版本。

您可以在稱為「系結」的程式中, 與 SQL Server 資料庫引擎分開升級 R 伺服器元件。 因此, 您在 SQL Server 中執行 R 程式碼時所使用的 R 版本可能會根據已安裝的 SQL Server 版本, 以及是否已將伺服器遷移至最新的 R 版本而有所不同。

### <a name="determine-the-r-version"></a>判斷 R 版本

判斷 R 版本最簡單的方式, 就是執行如下的語句來取得執行時間屬性:

```sql
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
> 如果 R Services 無法運作, 請嘗試僅從 Rgui.exe 執行 R 腳本部分。

最後一種方式是, 您可以開啟伺服器上的檔案, 以判斷已安裝的版本。 若要這麼做, 請找出 rlauncher, 以取得 R 執行時間和目前工作目錄的位置。 我們建議您建立並開啟檔案複本, 讓您不會意外地變更任何屬性。

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

若要取得 R 版本和 RevoScaleR 版本, 請開啟 R 命令提示字元, 或開啟與實例相關聯的 Rgui.exe。

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`

R 主控台會在啟動時顯示版本資訊。 例如, 下列版本代表 SQL Server 2017 的預設設定:

    *Microsoft R Open 3.3.3*

    *The enhanced R distribution from Microsoft*

    *Microsoft packages Copyright (C) 2017 Microsoft*

    *Loading Microsoft R Server packages, version 9.1.0.*

## <a name="python-versions"></a>Python 版本

有數種方式可取得 Python 版本。 最簡單的方式是從 Management Studio 或任何其他 SQL 查詢工具執行此語句:

```sql
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

如果 Machine Learning 服務並未執行, 您可以藉由查看 pythonlauncher 來判斷已安裝的 Python 版本。 我們建議您建立並開啟檔案複本, 讓您不會意外地變更任何屬性。

1. 僅適用于 SQL Server 2017:`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config`
2. 取得**PYTHONHOME**的值。
3. 取得目前工作目錄的值。

> [!NOTE]
> 如果您已在 SQL Server 2017 中安裝 Python 和 R, 則會共用 R 和 Python 語言的工作目錄和背景工作角色帳戶集區。

## <a name="are-multiple-instances-of-r-or-python-installed"></a>是否已安裝多個 R 或 Python 實例？

檢查是否已在電腦上安裝一個以上的 R 程式庫複本。 這項複製可能發生在下列情況:

* 在安裝期間, 您會選取 R Services (資料庫內) 和 R 伺服器 (獨立式)。
* 除了 SQL Server 之外, 您還可以安裝 Microsoft R Client。
* 使用 Visual Studio R 工具、R Studio、Microsoft R Client 或其他 R IDE 安裝了一組不同的 R 程式庫。
* 電腦主控 SQL Server 的多個實例, 而多個實例使用機器學習服務。

相同的條件適用于 Python。

如果您發現已安裝多個程式庫或執行時間, 請確定您只會取得與 SQL Server 實例所使用的 Python 或 R 執行時間相關聯的錯誤。

## <a name="origin-of-errors"></a>錯誤的來源

當您嘗試執行 R 程式碼時所看到的錯誤, 可能來自下列任何來源:

* SQL Server 資料庫引擎, 包括預存程式 sp_execute_external_script
* SQL Server 信任的啟動控制板
* 擴充性架構的其他元件, 包括 R 和 Python 啟動器和附屬進程
* 提供者, 例如 Microsoft 開放式資料庫連接 (ODBC)
* R 語言

當您第一次使用服務時, 可能很難分辨哪些訊息源自哪些服務。 我們建議您不要只捕獲確切的郵件內文, 而是您看到訊息的內容。 請注意您用來執行機器學習服務程式代碼的用戶端軟體:

* 您使用 Management Studio 嗎？ 外部應用程式？
* 您是在遠端用戶端中執行 R 程式碼, 還是直接在預存程式中執行？

## <a name="sql-server-log-files"></a>SQL Server 記錄檔

取得最新的 SQL Server 錯誤記錄檔。 一組完整的錯誤記錄檔是由下列預設記錄檔目錄中的檔案所組成:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> 確切的資料夾名稱會根據實例名稱而有所不同。

## <a name="errors-returned-by-spexecuteexternalscript"></a>Sp_execute_external_script 傳回的錯誤

當您執行 sp_execute_external_script 命令時, 取得傳回的完整錯誤文字 (如果有的話)。

若要從考慮中移除 R 或 Python 問題, 您可以執行此腳本, 它會啟動 R 或 Python 執行時間, 並來回傳遞資料。

**適用于 R**

```sql
exec sp_execute_external_script @language =N'R',  
@script=N'OutputDataSet<-InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

**適用于 Python**

```sql
exec sp_execute_external_script @language =N'Python',  
@script=N'OutputDataSet= InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

## <a name="errors-generated-by-the-extensibility-framework"></a>擴充性架構所產生的錯誤

SQL Server 會為外部指令碼語言執行時間產生個別的記錄檔。 這些錯誤不是由 Python 或 R 語言產生。 它們是從 SQL Server 的擴充性元件產生的, 包括特定語言的啟動器和其附屬進程。

您可以從下列預設位置取得這些記錄:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> 確切的資料夾名稱會根據實例名稱而有所不同。 視您的設定而定, 此資料夾可能位於不同的磁片磁碟機上。

例如, 下列記錄檔訊息與擴充性架構相關:

* *使用者 MSSQLSERVER01 的 LogonUser 失敗*
  
  這可能表示執行外部腳本的背景工作帳戶無法存取實例。

* *InitializePhysicalUsersPool 失敗*
  
  此訊息可能表示您的安全性設定導致安裝程式無法建立執行外部腳本所需的背景工作角色帳戶集區。

* *安全性內容管理員初始化失敗*

* *衛星會話管理員初始化失敗*

## <a name="system-events"></a>系統事件

1. 開啟 Windows 事件檢視器, 然後搜尋**系統事件**記錄檔中包含字串啟動列的訊息。
2. 開啟 ExtLaunchErrorlog 檔案, 並尋找字串*ErrorCode*。 檢查與 ErrorCode 相關聯的訊息。

例如, 下列訊息是與 SQL Server 擴充性架構相關的常見系統錯誤:

* *SQL Server Launchpad (MSSQLSERVER) 服務無法啟動, 因為發生下列錯誤:<text>*

* *服務並未及時回應啟動或控制要求。*

* *等候 SQL Server Launchpad (MSSQLSERVER) 服務連接時, 已達到超時 (120000 毫秒)。*

## <a name="dump-files"></a>傾印檔案

如果您有熟悉的調試功能, 可以使用傾印檔案來分析啟動列中的失敗。

1. 找出包含 SQL Server 設定啟動程式記錄檔的資料夾。 例如, 在 SQL Server 2016 中, 預設路徑為 C:\Program Files\Microsoft SQL Server\130\Setup Files\sql bootstrap\log
2. 開啟擴充性特有的啟動程式記錄子資料夾。
3. 如果您需要提交支援要求, 請將此資料夾的完整內容新增至壓縮檔案。 例如, C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog。
  
確切的位置在您的系統上可能會有所不同, 而且可能位於您的 C 磁片磁碟機以外的磁片磁碟機上。 請務必取得已安裝機器學習服務之實例的記錄檔。

## <a name="configuration-settings"></a>組態設定

本節列出當您執行 R 或 Python 腳本時, 可能會有錯誤來源的其他元件或提供者。

### <a name="what-network-protocols-are-available"></a>有哪些可用的網路通訊協定？

Machine Learning 服務需要下列網路通訊協定, 才能在擴充性元件之間進行內部通訊, 以及與外部 R 或 Python 用戶端進行通訊。

* 具名管道
* TCP/IP

開啟 SQL Server 組態管理員以判斷是否已安裝通訊協定, 如果已安裝, 則判斷是否已啟用它。

### <a name="security-configuration-and-permissions"></a>安全性設定和許可權

針對背景工作帳戶:

1. 在 [控制台] 中, 開啟 [**使用者和群組**], 並找出用來執行外部腳本作業的群組。 根據預設, 此群組為**SQLRUserGroup**。
2. 請確認群組是否存在, 以及它是否至少包含一個背景工作帳戶。
3. 在 SQL Server Management Studio 中, 選取將執行 R 或 Python 作業的實例, 選取 **安全性**, 然後判斷是否有 SQLRUserGroup 的登入。
4. 審查使用者群組的許可權。

針對個別使用者帳戶:

1. 判斷實例是否支援混合模式驗證、僅限 SQL 登入, 或僅限 Windows 驗證。 此設定會影響您的 R 或 Python 程式碼需求。
2. 針對每個需要執行 R 程式碼的使用者, 請在每個資料庫上, 判斷要從 R 寫入物件的所需許可權層級, 將會存取資料, 或建立物件。
3. 若要啟用腳本執行, 請視需要建立角色或將使用者新增至下列角色:

   - 除了*db_owner*:需要執行任何外部腳本。
   - *db_datawriter*：以寫入 R 或 Python 的結果。
   - *db_ddladmin*：以建立新的物件。
   - *db_datareader*：讀取 R 或 Python 程式碼所使用的資料。
4. 請注意, 當您安裝 SQL Server 2016 時, 是否已變更任何預設啟動帳戶。
5. 如果使用者需要安裝新的 R 封裝, 或使用其他使用者安裝的 R 封裝, 您可能需要在實例上啟用封裝管理, 然後再指派其他許可權。 如需詳細資訊, 請參閱[啟用或停用 R 封裝管理](r/r-package-how-to-enable-or-disable.md)。

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>哪些資料夾受到防毒軟體的鎖定？

防毒軟體可以鎖定資料夾, 這可防止設定機器學習功能和成功執行腳本。 判斷 SQL Server 樹狀目錄中是否有任何資料夾受限於病毒掃描。

不過, 在實例上安裝多個服務或功能時, 可能很難以列舉實例所使用的所有可能資料夾。 例如, 新增功能時, 必須識別並排除新的資料夾。

此外, 某些功能會在執行時間動態建立新的資料夾。 例如, 記憶體內部 OLTP 資料表、預存程式和函式都會在執行時間建立新的目錄。 這些資料夾名稱通常包含 Guid, 而且無法預測。 SQL Server 信任的啟動列會為 R 和 Python 腳本工作建立新的工作目錄。

因為可能無法排除 SQL Server 進程及其功能所需的所有資料夾, 所以我們建議您排除整個 SQL Server 實例目錄樹狀結構。

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>防火牆是否針對 SQL Server 開啟？ 實例是否支援遠端連線？

1. 若要判斷 SQL Server 是否支援遠端連線, 請參閱[設定遠端伺服器連接](../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md)。

2. 判斷是否已為 SQL Server 建立防火牆規則。 基於安全性理由, 在預設安裝中, 遠端 R 或 Python 用戶端可能無法連接到實例。 如需詳細資訊, 請參閱[疑難排解連接到 SQL Server](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)。

## <a name="see-also"></a>另請參閱

[針對 SQL Server 中的機器學習進行疑難排解](machine-learning-troubleshooting-faq.md)
