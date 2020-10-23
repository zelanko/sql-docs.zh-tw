---
title: 針對 SQL 機器學習進行疑難排解所收集的資料
description: 了解在嘗試自行或透過 Microsoft 客戶支援服務的協助解決問題時，如何收集資料。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/01/2020
ms.topic: troubleshooting
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cf9cf80d6ced7cfcfefecbff4f31095f82e04e1c
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194510"
---
# <a name="collect-data-to-troubleshoot-sql-machine-learning"></a>針對 SQL 機器學習進行疑難排解收集資料

[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

本文描述當嘗試解決 SQL 機器學習中的問題時，如何收集所需資料。 無論是自行解決問題，或透過 Microsoft 客戶支援服務的協助，這項資料都十分有用。

## <a name="sql-server-version-and-edition"></a>SQL Server 版本與版次

SQL Server 2016 R Services 是包括整合式 R 支援的第一個 SQL Server 版本。 SQL Server 2016 Service Pack 1 (SP1) 包括數個主要改良功能，包括執行外部指令碼的能力。 若您使用 SQL Server 2016，則應該考慮安裝 SP1 或更新版本。

SQL Server 2017 與更新版本具有 Python 語言整合。 您無法在先前的版本中取得 Python 功能整合。

如需取得版次和版本的協助，請參閱此文章，其中列出每個 [SQL Server 版本](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions)的組建編號。

視您使用的 SQL Server 版本而定，某些機器學習功能可能無法使用或受到限制。 

## <a name="r-language-and-tool-versions"></a>R 語言與工具版本

一般而言，當您選取 R Services 功能或機器學習服務功能時所安裝的 Microsoft R 版本，是由 SQL Server 組建編號所決定。 如果您升級或修補 SQL Server，您也必須升級或修補其 R 元件。

如需版本與 R 元件下載連結的清單，請參閱[在沒有網際網路存取的電腦上安裝機器學習元件](../install/sql-ml-component-install-without-internet-access.md)。 可以存取網際網路的電腦上，系統會自動識別並安裝所需的 R 版本。

您可以在稱為「繫結」的程序中，與 SQL Server 資料庫引擎分開升級 R 伺服器元件。 因此，您在 SQL Server 中執行 R 程式碼時所使用的 R 版本可能視已安裝的 SQL Server 版本，以及是否已將伺服器移轉到最新的 R 版本而異。

### <a name="determine-the-r-version"></a>判斷 R 版本

判斷 R 版本最簡單的方式，就是執行如下陳述式來取得執行階段屬性：

```sql
EXECUTE sp_execute_external_script
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
> 若 R Services 無法運作，請嘗試僅從 RGgui 執行 R 指令碼部分。

最後一種方式是，您可以開啟伺服器上的檔案，以判斷已安裝的版本。 若要這樣做，請找出 rlauncher.config 檔案，以取得 R 執行階段的位置與目前的工作目錄。 我們建議您建立並開啟檔案複本，以防意外變更任何屬性。

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

若要取得 R 版本與 RevoScaleR 版本，請開啟 R 命令提示字元，或開啟與執行個體關聯的 RGui。

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`

R 主控台會在啟動時顯示版本資訊。 例如，下列版本代表 SQL Server 2017 的預設設定：

```console
*Microsoft R Open 3.3.3*

*The enhanced R distribution from Microsoft*

*Microsoft packages Copyright (C) 2017 Microsoft*

*Loading Microsoft R Server packages, version 9.1.0.*
```

## <a name="python-versions"></a>Python 版本

有數種方式可取得 Python 版本。 最簡單的方式是從 Management Studio 或任何其他 SQL 查詢工具執行此陳述式：

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

若 Machine Learning 服務並未執行，您可以透過查看 pythonlauncher.config 檔案來判斷已安裝的 Python 版本。 我們建議您建立並開啟檔案複本，以防意外變更任何屬性。

1. 僅限 SQL Server 2017：`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config`
2. 取得 **PYTHONHOME** 的值。
3. 取得目前工作目錄的值。

> [!NOTE]
> 若您已同時在 SQL Server 2017 中安裝 Python 與 R，則 R 與 Python 語言會有相同的工作目錄與背景工作角色帳戶集區。

## <a name="are-multiple-instances-of-r-or-python-installed"></a>是否已安裝多個 R 或 Python 執行個體？

檢查是否已在電腦上安裝一個以上的 R 程式庫複本。 在下列情況中，可能會發生此重複：

* 您在安裝期間同時選取 R Services (資料庫內) 與 R Server (獨立式)。
* 除了 SQL Server 之外，您還安裝了 Microsoft R Client。
* 使用 Visual Studio R 工具、R Studio、Microsoft R Client 或其他 R IDE 安裝了一組不同的 R 程式庫。
* 電腦裝載多個 SQL Server 執行個體，而且多個執行個體使用機器學習。

相同的情況適用於 Python。

若您發現已安裝多個程式庫或執行階段，請確定您只會取得與 SQL Server 執行個體所使用之 Python 或 R 執行階段關聯的錯誤。

## <a name="origin-of-errors"></a>錯誤的來源

當您嘗試執行 R 程式碼時所看到的錯誤，可能來自下列任何來源：

* SQL Server 資料庫引擎，包括預存程序 sp_execute_external_script
* SQL Server Trusted Launchpad
* 擴充性架構的其他元件，包括 R 與 Python 啟動器與附屬處理序
* Microsoft 開放式資料庫連接 (ODBC)
* R 語言

當您第一次使用服務時，可能很難分辨哪些訊息源自哪些服務。 我們建議您不要只擷取確切的訊息文字，而是應該知道您看到之訊息的上下文。 記下您用來執行機器學習程式碼的用戶端軟體：

* 您使用 Management Studio 嗎？ 外部應用程式？
* 您是在遠端用戶端中執行 R 程式碼，或直接在預存程序中執行？

## <a name="sql-server-log-files"></a>SQL Server 記錄檔

取得最新的 SQL Server 錯誤記錄。 一組完整的錯誤記錄是由下列預設記錄檔目錄中的檔案所組成：

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> 確切資料夾名稱視執行個體名稱而異。

## <a name="errors-returned-by-sp_execute_external_script"></a>sp_execute_external_script 傳回的錯誤

當您執行 sp_execute_external_script 命令時，取得傳回的完整錯誤文字 (如果有的話)。

若要移除 R 或 Python 問題而不予考慮，您可以執行此指令碼，它會啟動 R 或 Python 執行階段，並來回傳遞資料。

**針對 R**

```sql
exec sp_execute_external_script @language =N'R',  
@script=N'OutputDataSet<-InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

**針對 Python**

```sql
exec sp_execute_external_script @language =N'Python',  
@script=N'OutputDataSet= InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

## <a name="errors-generated-by-the-extensibility-framework"></a>擴充性架構所產生的錯誤

SQL Server 會為外部指令碼語言執行階段產生個別的記錄檔。 這些錯誤不是由 Python 或 R 語言產生。 它們是從 SQL Server 中的擴充性元件產生的，包括語言特定啟動器與其附屬處理序。

您可以從下列預設位置取得這些記錄：

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> 確切資料夾名稱視執行個體名稱而異。 視您的設定而定，資料夾可能位於不同的磁碟機。

例如，下列記錄檔訊息與擴充性架構相關：

* *MSSQLSERVER01 的 LogonUser 失敗*
  
  這可能表示執行外部指令碼的背景工作角色帳戶無法存取執行個體。

* *InitializePhysicalUsersPool 失敗*
  
  此訊息可能表示您的安全性設定導致安裝程式無法建立執行外部指令碼所需的背景工作角色帳戶集區。

* *資訊安全內容管理員初始化失敗*

* *附屬工作階段管理員初始化失敗*

## <a name="system-events"></a>系統事件

1. 開啟 Windows 事件檢視器，然後在**系統事件**記錄檔中搜尋包含 *Launchpad* 字串的訊息。
2. 開啟 ExtLaunchErrorlog 檔案，並尋找 *ErrorCode* 字串。 檢閱與 ErrorCode 關聯的訊息。

例如，下列訊息是與 SQL Server 擴充性架構相關的常見系統錯誤：

* *SQL Server Launchpad (MSSQLSERVER) 服務無法啟動，因為下列錯誤：<text>*

* *服務並未以適時的方式回應啟動或控制請求。*

* *等候 SQL Server Launchpad (MSSQLSERVER) 服務連線時發生逾時 (120000 毫秒)。*

## <a name="dump-files"></a>傾印檔

若熟悉如何偵錯，您可以使用傾印檔案來分析 Launchpad 中的失敗。

1. 找出包含 SQL Server 安裝程式啟動程序記錄檔的資料夾。 例如，在 SQL Server 2016 中，預設路徑為 C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log。
2. 開啟擴充性特定的啟動程序記錄檔子資料夾。
3. 若需要提交支援要求，請將此資料夾的整個內容新增至 ZIP 檔案。 例如，C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog。
  
確切的位置在您的系統上可能不一樣，而且可能位於 C 磁碟機以外的磁碟機上。 請務必取得已安裝機器學習之執行個體的記錄檔。

## <a name="configuration-settings"></a>組態設定

此節列出當您執行 R 或 Python 指令碼時，可能會是錯誤來源的其他元件或提供者。

### <a name="what-network-protocols-are-available"></a>有哪些可用的網路通訊協定？

機器學習服務需要下列網路通訊協定，才能在擴充性元件之間進行內部通訊，以及與外部 R 或 Python 用戶端進行通訊。

* 具名管道
* TCP/IP

開啟 SQL Server 組態管理員以判斷是否已安裝通訊協定，如果已安裝，則判斷是否已啟用。

### <a name="security-configuration-and-permissions"></a>安全性設定與權限

針對背景工作角色帳戶：

1. 在 [控制台] 中，開啟 [使用者和群組]  ，然後找出用於執行外部指令碼作業的群組。 根據預設，此群組為 **SQLRUserGroup**。
2. 請確認群組是否存在，以及它是否至少包含一個背景工作角色帳戶。
3. 在 SQL Server Management Studio 中，選取將執行 R 或 Python 作業的執行個體、選取 [安全性]  ，然後判斷是否有 SQLRUserGroup 的登入。
4. 檢閱使用者群組的權限。

針對個別使用者帳戶：

1. 判斷執行個體支援混合模式驗證、僅限 SQL 登入，或僅限 Windows 驗證。 此設定會影響您的 R 或 Python 程式碼需求。
2. 針對每個需要執行 R 程式碼的使用者，請判斷要在每個資料庫從 R 寫入物件、存取資料或建立物件所需的權限層級。
3. 若要啟用指令碼執行，請視需要建立角色或將使用者新增到下列角色：

   - 所有角色，但 *db_owner* 除外：需要 EXECUTE ANY EXTERNAL SCRIPT。
   - *db_datawriter*：從 R 或 Python 寫入結果。
   - *db_ddladmin*：來建立新物件。
   - *db_datareader*：讀取 R 或 Python 程式碼所使用的資料。
4. 注意您在安裝 SQL Server 2016 時，是否已變更任何預設啟動帳戶。
5. 若使用者需要安裝新的 R 套件，或使用其他使用者安裝的 R 套件，您可能需要在執行個體上啟用套件管理，然後再指派額外權限。 

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>哪些資料夾可能會被防毒軟體鎖定？

防毒軟體可能會鎖定資料夾，這會造成您無法安裝機器學習功能及執行指令碼。 判斷 SQL Server 樹狀結構中是否有任何資料夾會由防毒軟體進行病毒掃描。

不過，當在執行個體上安裝多個服務或功能時，可能很難以列舉執行個體所使用的所有可能資料夾。 例如，新增功能時，必須識別並排除新資料夾。

此外，某些功能可能會在執行階段動態建立新資料夾。 例如，記憶體內部 OLTP 資料表、預存程序與函式都會在執行階段建立新目錄。 這些資料夾名稱通常包含 GUID，而且無法預測。 SQL Server Trusted Launchpad 會為 R 與 Python 指令碼作業建立新工作目錄。

因為可能無法排除 SQL Server 處理序與其功能所需的所有資料夾，所以我們建議您排除整個 SQL Server 執行個體目錄樹狀結構。

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>防火牆是否針對 SQL Server 開啟？ 執行個體是否支援遠端連線？

1. 若要判斷 SQL Server 是否支援遠端連線，請參閱[設定遠端伺服器連接](../../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md)。

2. 判斷是否已為 SQL Server 建立防火牆規則。 基於安全性理由，在預設安裝中，遠端 R 或 Python 用戶端可能無法連線到執行個體。 如需詳細資訊，請參閱[針對 SQL Server 連線進行疑難排解](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)。

## <a name="see-also"></a>另請參閱

[針對 SQL Server 中的機器學習進行疑難排解](machine-learning-troubleshooting-overview.md)