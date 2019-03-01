---
title: 針對機器學習服務-SQL Server 機器學習服務的資料集合進行疑難排解
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: edfacb2e4d519d4f709d352f52645526cb341fad
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017934"
---
# <a name="troubleshoot-data-collection-for-machine-learning"></a>疑難排解適用於 machine learning 的資料收集

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

此文章說明您應該使用時嘗試解決您自己的問題，或藉助 Microsoft 客戶支援的資料收集方法。

**適用於：** SQL Server 2016 R Services、 SQL Server 2017 Machine Learning 服務 （R 和 Python）

## <a name="sql-server-version-and-edition"></a>SQL Server 版本與版別

SQL Server 2016 R Services 是以包含整合式的 R 支援的 SQL Server 的第一個版本。 SQL Server 2016 Service Pack 1 (SP1) 包含數個重大的改進，包括執行外部指令碼的能力。 如果您是 SQL Server 2016 的客戶，您應該考慮安裝 SP1 或更新版本。

SQL Server 2017 新增 Python 語言整合。 在舊版中，您無法取得 Python 功能整合。

如協助取得版本和版本，請參閱這篇文章列出每個組建編號[SQL Server 版本](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions)。

根據您使用的 SQL Server 版本中，有些機器學習服務功能可能無法使用，或只有有限的。 下列文件清單的 Enterprise、 Developer、 Standard 和 Express 版本中的機器學習服務功能。

* [版本和支援的 SQL Server 功能](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016)
* [R 和 Python 的 SQL Server 的版本支援的功能](r/differences-in-r-features-between-editions-of-sql-server.md)

## <a name="r-language-and-tool-versions"></a>R 語言和工具版本

當您選取 R Services 功能或機器學習服務功能已安裝的 Microsoft R 的強大功能的版本在一般情況下，取決於 SQL Server 組建編號。 如果您升級或修補 SQL Server 時，也必須升級或修補程式及其的 R 元件。

如需版本與 R 元件下載項目連結的清單，請參閱[安裝沒有網際網路存取的機器學習服務元件](https://docs.microsoft.com/sql/advanced-analytics/r/installing-ml-components-without-internet-access)。 在電腦上具有網際網路存取，是識別所需的 R 版本，並將其自動安裝中。

可以個別從稱為繫結的程序中的 SQL Server 資料庫引擎升級 R Server 元件。 因此，當您在 SQL Server 中執行 R 程式碼時，您使用的 R 版本可能會有所不同安裝的 SQL Server 版本及您是否移轉至最新版的 R 伺服器。

### <a name="determine-the-r-version"></a>判斷 R 版本

若要判斷 R 版本的最簡單方式是執行如下所示的陳述式來取得執行階段屬性：

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
> 如果未運作 R Services，請嘗試從 RGui 執行 R 指令碼部份。

最後的手段，您可以開啟檔案伺服器上用來判斷已安裝的版本。 若要這樣做，請找出 rlauncher.config 檔案，以取得 R 執行階段和目前的工作目錄的位置。 我們建議您製作並開啟檔案的複本，以便您不小心不要變更任何屬性。

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

若要取得 RevoScaleR 版本的 R 版本，請開啟 R 命令提示字元中，或開啟與執行個體相關聯的 RGui。

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`

R 主控台會在啟動時顯示的版本資訊。 例如，下列版本代表 SQL Server 2017 的預設組態：

    *Microsoft R Open 3.3.3*

    *The enhanced R distribution from Microsoft*

    *Microsoft packages Copyright (C) 2017 Microsoft*

    *Loading Microsoft R Server packages, version 9.1.0.*

## <a name="python-versions"></a>Python 版本

有數種方式可取得 Python 版本。 最簡單的方式是從 Management Studio 或任何其他的 SQL 查詢工具執行此陳述式：

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

如果 Machine Learning 服務未在執行中，您可以藉由查看 pythonlauncher.config 檔案來判斷已安裝的 Python 版本。 我們建議您製作並開啟檔案的複本，以便您不小心不要變更任何屬性。

1. SQL Server 2017 的只有： `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config `
2. 取得值，如**PYTHONHOME**。
3. 取得目前工作目錄的值。

> [!NOTE]
> 如果您已安裝 Python 和 R 在 SQL Server 2017 中，工作目錄和背景工作帳戶的集區共用的 R 和 Python 語言。

## <a name="are-multiple-instances-of-r-or-python-installed"></a>多個執行個體的 R 或 Python 安裝嗎？

請檢查電腦上是否已安裝的 R 程式庫的多個複本。 如果，就會發生這種重複狀況：

* 在安裝期間您可以選取 R Services （資料庫） 和 R Server （獨立式）。
* 您安裝 Microsoft R Client 除了 SQL Server。
* 使用 R Tools for Visual Studio、 Rstudio、 Microsoft R Client 或其他的 R IDE，已安裝一組不同的 R 程式庫。
* 電腦主控多個 SQL Server 執行個體和多個執行個體會使用機器學習服務。

適用於 Python 的相同的條件。

如果您發現安裝多個程式庫或執行階段，請確定您取得只將 Python 或 R 執行階段所使用的 SQL Server 執行個體相關聯的錯誤。

## <a name="origin-of-errors"></a>錯誤的來源

當您嘗試執行 R 程式碼時，您會看到的錯誤可能來自任何下列來源：

* SQL Server 資料庫引擎，包括預存程序 sp_execute_external_script
* SQL Server 受信任的 Launchpad
* 擴充性架構，包括 R 和 Python 啟動器和附屬程序的其他元件
* 提供者，例如 Microsoft 開啟資料庫連接 (ODBC)
* R 語言

當您使用第一次的服務時，很難判斷哪些訊息源自哪些服務。 我們建議您擷取不僅實際訊息文字，而且您所見訊息的內容。 請注意您用來執行機器學習服務程式碼的用戶端軟體：

* 使用 Management Studio 嗎？ 外部應用程式嗎？
* 在遠端用戶端，或直接在預存程序中執行 R 程式碼？

## <a name="sql-server-log-files"></a>SQL Server 記錄檔

取得最新的 SQL Server 錯誤記錄檔。 一組完整的錯誤記錄檔是由下列的預設記錄檔目錄中的檔案所組成：

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> 一模一樣的資料夾名稱是根據執行個體名稱而有所不同。

## <a name="errors-returned-by-spexecuteexternalscript"></a>Sp_execute_external_script 所傳回的錯誤

如果有的話，當您執行 sp_execute_external_script 命令，取得會傳回錯誤的完整文字。

若要移除的考量中的 R 或 Python 的問題，您可以執行此指令碼會啟動 R 或 Python 執行階段，並來回傳遞資料。

**適用於 R**

```sql
exec sp_execute_external_script @language =N'R',  
@script=N'OutputDataSet<-InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

**適用於 Python**

```sql
exec sp_execute_external_script @language =N'Python',  
@script=N'OutputDataSet= InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

## <a name="errors-generated-by-the-extensibility-framework"></a>擴充性架構所產生的錯誤

SQL Server 會產生個別的記錄檔的外部指令碼語言執行階段。 這些錯誤不會產生 Python 或 R 語言。 它們是從 SQL Server，包括特定語言的啟動器和其附屬程序中的擴充性元件所產生的。

您可以從下列的預設位置，以取得這些記錄檔：

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog `

> [!NOTE]
> 一模一樣的資料夾名稱有所不同的執行個體名稱。 根據您的設定，資料夾可能是不同的磁碟機上。

例如，下列記錄檔訊息與相關的擴充性架構：

* *使用者 MSSQLSERVER01 LogonUser 失敗*
  
  這可能表示執行外部指令碼的背景工作帳戶無法存取執行個體。

* *InitializePhysicalUsersPool 失敗*
  
  此訊息可能表示，您的安全性設定會防止安裝程式建立的執行外部指令碼所需的背景工作帳戶集區。

* *安全性內容管理員初始化失敗*

* *附屬工作階段管理員初始化失敗*

## <a name="system-events"></a>系統事件

1. 開啟 Windows 事件檢視器，並搜尋**系統事件**記錄檔包含字串的訊息*Launchpad*。
2. 開啟 ExtLaunchErrorlog 檔案，並尋找字串*ErrorCode*。 檢閱與錯誤碼相關聯的訊息。

例如，下列訊息是 SQL Server 擴充性架構相關的常見系統錯誤：

* *SQL Server Launchpad (MSSQLSERVER) 服務無法啟動，因為發生下列錯誤：  <text>*

* *服務未啟動或控制要求及時回應。*

* *逾時等候 SQL Server Launchpad (MSSQLSERVER) 服務連線達到 （120000 毫秒為單位）。*

## <a name="dump-files"></a>傾印檔案

如果您了解偵錯時，您可以使用傾印檔案分析啟動控制板失敗。

1. 找出包含 SQL Server 安裝程式的啟動程序記錄檔的資料夾。 例如，在 SQL Server 2016 中，預設路徑是 C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log。
2. 開啟擴充性特定的啟動程序的記錄子資料夾。
3. 如果您需要提交支援要求，將此資料夾的整個內容加入一個壓縮檔。 例如，C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog。
  
確切位置可能會在您的系統上不同，而且可能在您的 C 磁碟機以外的磁碟機上。 請務必安裝機器學習服務的執行個體取得的記錄檔。

## <a name="configuration-settings"></a>組態設定

此區段會列出其他元件，或是當您執行 R 或 Python 指令碼時，可以是錯誤的來源的提供者。

### <a name="what-network-protocols-are-available"></a>哪些網路通訊協定可供使用？

Machine Learning 服務中將需要下列網路通訊協定的擴充性元件之間的內部通訊和與外部 R 或 Python 用戶端進行通訊。

* 具名管道
* TCP/IP

開啟 SQL Server 組態管理員判斷是否已安裝的通訊協定，如果它已安裝，以判斷是否已啟用。

### <a name="security-configuration-and-permissions"></a>安全性設定和權限

背景工作帳戶：

1. 在控制台中，開啟**使用者和群組**，並找出用來執行外部指令碼工作的群組。 根據預設，群組是**SQLRUserGroup**。
2. 請確認此群組存在，而且它包含至少一個背景工作帳戶。
3. 在 SQL Server Management Studio，選取 執行個體，將執行 R 或 Python 的作業，選取**安全性**，然後判斷是否有 SQLRUserGroup 的登入。
4. 檢閱的使用者群組的權限。

針對個別使用者帳戶：

1. 判斷執行個體支援混合模式驗證，SQL 登入或只使用 Windows 驗證。 此設定會影響您的 R 或 Python 程式碼的需求。
2. 每個使用者需要執行 R 程式碼，判斷所需的層級的每個資料庫，其中物件將寫入從 R、 會存取資料，或將建立物件的權限。
3. 若要啟用指令碼執行，請建立角色，或將使用者新增至下列角色，視：

   - 以外的所有*db_owner*:需要執行任何的外部指令碼。
   - *db_datawriter*：若要從 R 或 Python 中寫入結果。
   - *db_ddladmin*：若要建立新的物件。
   - *db_datareader*：若要讀取資料，以供 R 或 Python 程式碼。
4. 請注意是否安裝 SQL Server 2016 時變更任何預設的啟動帳戶。
5. 如果使用者需要安裝新的 R 套件或使用其他使用者所安裝的 R 套件，您可能需要執行個體上啟用封裝管理，然後將指派其他權限。 如需詳細資訊，請參閱 <<c0> [ 啟用或停用 R 封裝管理](r/r-package-how-to-enable-or-disable.md)。

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>鎖定的防毒軟體受到哪些資料夾？

防毒軟體可以鎖定資料夾，使得這兩個機器學習服務功能和成功的指令碼執行安裝程式。 決定是否在 SQL Server 樹狀目錄中任何資料夾受到病毒掃描。

不過，當安裝執行個體上的多個服務或功能之後，很難列舉所有可能的資料夾所使用的執行個體。 比方說，當您加入新功能，新的資料夾必須是識別和排除。

此外，某些功能建立新的資料夾以動態方式在執行階段。 例如，記憶體中 OLTP 資料表、 預存程序和函式所有在執行階段建立新的目錄。 這些資料夾名稱通常包含 Guid，而且無法預測。 SQL Server 受信任的 Launchpad 建立新的工作目錄的 R 和 Python 指令碼工作。

因為它可能無法排除 SQL Server 處理序和其功能所需的所有資料夾，我們建議您都排除整個 SQL Server 執行個體目錄樹狀結構。

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>是適用於 SQL Server 的防火牆開啟？ 執行個體是否支援遠端連線？

1. 若要判斷 SQL Server 是否支援遠端連線，請參閱[設定遠端伺服器連接](../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md)。

2. 判斷是否已建立 SQL Server 防火牆規則。 基於安全性理由，在預設安裝中，它可能無法連接到執行個體的遠端 R 或 Python 用戶端。 如需詳細資訊，請參閱 <<c0> [ 疑難排解連線到 SQL Server](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)。

## <a name="see-also"></a>另請參閱

[疑難排解 SQL Server 中的機器學習服務](machine-learning-troubleshooting-faq.md)
