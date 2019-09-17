---
title: 在 Linux 上安裝 SQL Server 機器學習服務 (R、Python)
description: 了解如何在 Red Hat、Ubuntu 和 SUSE 上安裝 SQL Server 機器學習服務 (R、Python)。
author: dphansen
ms.author: davidph
ms.reviewer: vanto
manager: cgronlun
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 91bacc4ab4c8876ac49a09b58d1821f1c2853a3c
ms.sourcegitcommit: 3bd813ab2c56b415a952e5fbd5cfd96b361c72a2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/11/2019
ms.locfileid: "70913557"
---
# <a name="install-sql-server-machine-learning-services-r-python-on-linux"></a>在 Linux 上安裝 SQL Server 機器學習服務 (R、Python)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

從 SQL Server 2019 的此預覽版本開始，[SQL Server 機器學習服務](../advanced-analytics/index.yml)可在 Linux 作業系統上執行。 請遵循此文章中的步驟來安裝適用於 R 和 Python 的機器學習服務擴充功能。

機器學習和程式設計擴充功能是資料庫引擎的附加元件。 雖然您可以[同時安裝資料庫引擎和機器學習服務](#install-all)，但最佳做法是先安裝和設定 SQL Server 資料庫引擎，以便在新增更多元件之前解決任何問題。 

R 和 Python 擴充功能的套件位置在 SQL Server Linux 來源存放庫中。 如果您已經為資料庫引擎安裝設定來源存放庫，您可以使用相同的存放庫登錄來執行 **mssql-mlservices** 套件安裝命令。

Linux 容器上也支援機器學習服務。 我們沒有提供含機器學習服務的預先建立容器，但您可以使用 [GitHub 上提供的範例範本](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices) \(英文\)，從 SQL Server 容器建立一個。

## <a name="uninstall-previous-ctp"></a>將先前的 CTP 解除安裝

套件清單已經隨最近數個 CTP 版本變更，套件數量也因此減少。 我們建議您先將 CTP 2.x 解除安裝，以在安裝 CTP 3.2 之前移除所有先前的套件。 不支援多個版本的並存安裝。

### <a name="1-confirm-package-installation"></a>1.確認套件安裝

首先，建議您檢查先前的安裝是否存在。 下列檔案表示現有安裝存在：checkinstallextensibility.sh、exthost、launchpad。

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-previous-ctp-2x-packages"></a>2.將先前的 CTP 2.x 套件解除安裝

在最低套件層級解除安裝。 相依於低層級套件的任何上游套件都會自動解除安裝。

  + 針對 R 整合，請移除 **microsoft-r-open***
  + 針對 Python 整合，請移除 **mssql-mlservices-python**

下表中顯示移除套件的命令。

| 平台  | 套件移除命令 | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove microsoft-r-open-mro-3.4.4`<br/>`sudo yum remove msssql-mlservices-python` |
| SLES  | `sudo zypper remove microsoft-r-open-mro-3.4.4`<br/>`sudo zypper remove msssql-mlservices-python` |
| Ubuntu    | `sudo apt-get remove microsoft-r-open-mro-3.4.4`<br/>`sudo apt-get remove msssql-mlservices-python`|

> [!Note]
> 取決於您先前安裝的 CTP 版本，Microsoft R Open 3.4.4 是由兩個或三個套件組成。 (在 CTP 2.2 中，foreachiterators 套件已合併至主要 mro 套件)。如果移除 microsoft-r-open-mro-3.4.4 之後任何這些套件仍存在，您應該個別將它們移除。
> ```
> microsoft-r-open-foreachiterators-3.4.4
> microsoft-r-open-mkl-3.4.4
> microsoft-r-open-mro-3.4.4
> ```

### <a name="3-proceed-with-ctp-32-install"></a>3.繼續進行 CTP 3.2 安裝

使用此文章中適用於您作業系統的指示，在最高套件層級安裝。

針對每個 OS 特定的安裝指示集，「最高套件層級」  為適用於安裝完整一組套件的**範例 1 - 完整安裝**，或適用於可行安裝所需最少套件數目的**範例 2 - 最小安裝**。

1. 針對 R 整合，請從 [MRO](#mro) 開始，因為它是先決條件。 沒有它就無法安裝 R 整合。

2. 使用適用於您作業系統的套件管理員和語法來執行安裝命令： 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>Prerequisites

+ Linux 版本必須[受 SQL Server 支援](sql-server-linux-release-notes-2019.md#supported-platforms)，但不包含 Docker 引擎。 支援的版本包含：

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ (僅限 R) [Microsoft R Open](#mro) 為 SQL Server 中的 R 功能提供基底 R 散發

+ 您應該有執行 T-SQL 命令的工具。 必須使用查詢編輯器進行安裝後設定和驗證。 我們推薦 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux) \(部分機器翻譯\)，這是在 Linux 上執行的免費下載。

<a name="mro"></a>

### <a name="microsoft-r-open-mro-installation"></a>Microsoft R Open (MRO) 安裝

Microsoft 的 R 基底散發是使用 RevoScaleR、MicrosoftML 和其他隨機器學習服務安裝之 R 套件的先決條件。

所需的版本為 MRO 3.5.2。

從下列兩個方法中選一個來安裝 MRO：

+ 從 MRAN 下載 MRO Tarball、將它解壓縮，然後執行其 install.sh 指令碼。 如果您要使用此方法，可以遵循 [MRAN 上的安裝指示](https://mran.microsoft.com/releases/3.5.2) \(英文\)。

+ 或者，如下所述登錄 **packages.microsoft.com** 存放庫，以安裝組成 MRO 散發的兩個套件：microsoft-r-open-mro 和 microsoft-r-open-mkl。 

下列命令會登錄提供 MRO 的存放庫。 登錄後，安裝其他 R 套件 (例如，mssql-mlservices-mml-r) 的命令會自動包含在 MRO 中作為套件相依性。

#### <a name="mro-on-ubuntu"></a>Ubuntu 上的 MRO

```bash
# Install as root
sudo su

# Optionally, if your system does not have the https apt transport option
apt-get install apt-transport-https

# Set the location of the package repo the "prod" directory containing the distribution.
# This example specifies 16.04. Replace with 14.04 if you want that version
wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the repo
dpkg -i packages-microsoft-prod.deb

# Update packages on your system (required), including MRO installation
sudo apt-get update
```

#### <a name="mro-on-rhel"></a>RHEL 上的 MRO

```bash
# Import the Microsoft repository key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc


# Set the location of the package repo at the "prod" directory
# The following command is for version 7.x
# For 6.x, replace 7 with 6 to get that version
rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm

# Update packages on your system (optional)
yum update
```
#### <a name="mro-on-suse"></a>SUSE 上的 MRO

```bash
# Install as root
sudo su

# Set the location of the package repo at the "prod" directory containing the distribution
# This example is for SLES12, the only supported version of SUSE in Machine Learning Server
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com

# Update packages on your system (optional)
zypper update
```

## <a name="package-list"></a>套件清單

在連線到網際網路的裝置上，系統會使用每個作業系統的套件安裝程式，獨立地下載及安裝套件。 下表描述只適用於 R 和 Python 的所有可用套件，您可以指定提供完整功能安裝或最基本功能安裝的套件。

| 封裝名稱 | 適用於 | Description |
|--------------|----------|-------------|
|mssql-server-extensibility  | All | 用來執行 R 和 Python 程式碼的擴充性架構。 |
| microsoft-openmpi  | Python、R | 針對 Linux 上用於平行處理，Revo* 程式庫所使用的訊息傳遞介面。 |
| mssql-mlservices-python | Python | Anaconda 和 Python 的開放原始碼散發。 |
|mssql-mlservices-mlm-py  | Python | *完整安裝*。 提供 revoscalepy、microsoftml、適用於影像特徵化和文字情感分析的預先定型的模型。| 
|mssql-mlservices-packages-py  | Python | 「最小安裝」  。 提供 revoscalepy 和 microsoftml。 <br/>排除預先定型的模型。 | 
| [microsoft-r-open*](#mro) | R | R 的開放原始碼散發，由三個套件組成。 |
|mssql-mlservices-mlm-r  | R | *完整安裝*。 提供 RevoScaleR，MicrosoftML、sqlRUtils、olapR、適用於影像特徵化和文字情感分析的預先定型的模型。| 
|mssql-mlservices-packages-r  | R | 「最小安裝」  。 提供 RevoScaleR、sqlRUtils、MicrosoftML、olapR。 <br/>排除預先定型的模型。 | 
|mssql-mlservices-mml-py  | 僅限 CTP 2.0-2.1 | 已在 CTP 2.2 中淘汰，因為 Python 套件彙總至 mssql-mslservices-python。 提供 revoscalepy。 排除預先定型的模型和 microsoftml。| 
|mssql-mlservices-mml-r  | 僅限 CTP 2.0-2.1 | 已在 CTP 2.2 中淘汰，因為 R 套件彙總至 mssql-mslservices-python。 提供 RevoScaleR、sqlRUtils、olapR。 排除預先定型的模型和 MicrosoftML。  |

<a name="RHEL"></a>

## <a name="redhat-commands"></a>RedHat 命令

您可以依所需的任何組合 (單一或多個語言) 來安裝語言支援。 針對 R 和 Python，有兩個套件可以選擇。 其中一個提供所有可用功能，其特性為「完整安裝」  。 替代選項會排除預先定型機器學習模型，且視為「最小安裝」  。

> [!Tip]
> 可能的話，請在安裝之前執行 `yum clean all`，以重新整理系統上的套件。

### <a name="example-1----full-installation"></a>範例 1 - 完整安裝 

包含開放原始碼 R 和 Python、擴充性架構、microsoft-openmpi、擴充功能 (R、Python)、機器學習程式庫，以及適用於 R 和 Python 的預先定型模型。 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.7*
sudo yum install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>範例 2 - 最小安裝 

包含開放原始碼 R 和 Python、擴充性架構、microsoft-openmpi、core Revo* 程式庫和適用於 R 和 Python 的機器學習程式庫。 排除預先定型的模型。

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.7*
sudo yum install mssql-mlservices-packages-r-9.4.7*
```

<a name="ubuntu"></a>

## <a name="ubuntu-commands"></a>Ubuntu 命令

您可以依所需的任何組合 (單一或多個語言) 來安裝語言支援。 針對 R 和 Python，有兩個套件可以選擇。 其中一個提供所有可用功能，其特性為「完整安裝」  。 替代選項會排除預先定型機器學習模型，且視為「最小安裝」  。

> [!Tip]
> 可能的話，請在安裝之前執行 `apt-get update`，以重新整理系統上的套件。 此外，某些 Ubuntu 的 Docker 映像可能沒有 HTTPS apt 傳輸選項。 若要安裝它，請使用 `apt-get install apt-transport-https`。

### <a name="example-1----full-installation"></a>範例 1 - 完整安裝 

包含開放原始碼 R 和 Python、擴充性架構、microsoft-openmpi、擴充功能 (R、Python)、機器學習程式庫，以及適用於 R 和 Python 的預先定型模型。 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
```

### <a name="example-2---minimum-installation"></a>範例 2 - 最小安裝 

包含開放原始碼 R 和 Python、擴充性架構、microsoft-openmpi、core Revo* 程式庫和適用於 R 和 Python 的機器學習程式庫。 排除預先定型的模型。 

```bash
# Install as root or sudo
# Minimum install of R, Python
# No aasterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
```

<a name="suse"></a>

## <a name="suse-commands"></a>SUSE 命令

您可以依所需的任何組合 (單一或多個語言) 來安裝語言支援。 針對 R 和 Python，有兩個套件可以選擇。 其中一個提供所有可用功能，其特性為「完整安裝」  。 替代選項會排除預先定型機器學習模型，且視為「最小安裝」  。

### <a name="example-1----full-installation"></a>範例 1 - 完整安裝 

包含開放原始碼 R 和 Python、擴充性架構、microsoft-openmpi、擴充功能 (R、Python)、機器學習程式庫，以及適用於 R 和 Python 的預先定型模型。 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.7*
sudo zypper install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>範例 2 - 最小安裝 

包含開放原始碼 R 和 Python、擴充性架構、microsoft-openmpi、core Revo* 程式庫和適用於 R 和 Python 的機器學習程式庫。 排除預先定型的模型。 

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.7*
sudo zypper install mssql-mlservices-packages-r-9.4.7*
```

## <a name="post-install-config-required"></a>安裝後設定 (必要)

其他設定主要是透過 [mssql-conf 工具](sql-server-linux-configure-mssql-conf.md)來設定。


1. 新增用來執行 SQL Server 服務的 mssql 使用者帳戶。 如果您先前未執行安裝程式，則這是必要的。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. 接受開放原始碼 R 和 Python 的授權合約。 有數個方式可以執行此動作。 如果您先前已接受 SQL Server 授權，而且現在正在新增 R 或 Python 擴充功能，則下列命令會同意其條款：

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```

   替代工作流程是，如果您尚未接受 SQL Server 資料庫引擎授權合約，安裝程式會在執行 `mssql-conf setup` 時偵測 mssql-mlservices 套件，並提示接受 EULA。 如需 EULA 參數的詳細資訊，請參閱[使用 mssql-conf 工具設定 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-eula)。

3. 啟用輸出網路存取。 預設會停用輸出網路存取。 若要啟用輸出要求，請使用 mssql-conf 工具來設定 "outboundnetworkaccess" 布林值屬性。 如需詳細資訊，請參閱[使用 mssql-conf 在 Linux 上設定 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access)。

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. 若只需要 R 功能整合，請設定 **MKL_CBWR** 環境變數，以確保輸出與來自 Intel 數學核心程式庫 (MKL) 計算的[一致](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)。

   + 在您的使用者主目錄中編輯或建立名為 **bash_profile** 的檔案，並將 `export MKL_CBWR="AUTO"` 這一行新增至檔案。

   + 在 bash 命令提示字元中輸入 `source .bash_profile` 來執行此檔案。

5. 重新啟動 SQL Server Launchpad 服務和資料庫引擎執行個體，以從 INI 檔案讀取更新後的值。 每當修改擴充性相關設定時，系統會顯示重新啟動訊息提醒您。  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

6. 使用 Azure Data Studio 或 SQL Server Management Studio (僅限 Windows) 等執行 Transact-SQL 的另一種工具，來啟用外部指令碼執行。 

   ```bash
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. 重新啟動 Launchpad 服務。

## <a name="verify-installation"></a>確認安裝

您可以在 `/opt/mssql/mlservices/libraries/RServer` 找到 R 程式庫 (MicrosoftML、RevoScaleR 和其他)。

您可以在 `/opt/mssql/mlservices/libraries/PythonServer` 找到 Python 程式庫 (microsoftml 和 revoscalepy)。

若要驗證安裝，請執行 T-SQL 指令碼，以執行叫用 R 或 Python 的系統預存程序。 您將需要此工作的查詢工具。 Azure Data Studio 是不錯的選擇。 其他常用的工具，例如，SQL Server Management Studio 或 PowerShell，則只適用於 Windows。 如果您有包含這些工具的 Windows 電腦，請使用它來連線到您的 Linux 安裝資料庫引擎。

執行下列 SQL 命令，以在 SQL Server 中測試 R 執行。 如果指令碼未執行，請嘗試服務重新啟動 (`sudo systemctl restart mssql-server.service`)。

```r
EXEC sp_execute_external_script   
@language =N'R', 
@script=N' 
OutputDataSet <- InputDataSet', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```
 
執行下列 SQL 命令，以在 SQL Server 中測試 Python 執行。 
 
```python
EXEC sp_execute_external_script  
@language =N'Python', 
@script=N' 
OutputDataSet = InputDataSet; 
', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```

<a name="install-all"></a>

## <a name="chained-combo-install"></a>鏈結「組合」安裝

藉由在安裝資料庫引擎的命令附加 R 或 Python 套件和參數，您可以在一個程序中安裝及設定資料庫引擎和機器學習服務。 

1. 針對 R 整合，請安裝必要的 [Microsoft R Open](#mro)。 如果不安裝 R 功能，請略過此步驟。

2. 提供包含資料庫引擎以及語言擴充功能的命令列。

  您可以將單一功能 (例如 Python 整合) 新增至資料庫引擎安裝。

  ```bash
  sudo yum install -y mssql-server mssql-mlservices-packages-r-9.4.7* 
  ```

  或新增兩個擴充功能 (R、Python)。

  ```bash
  sudo yum install -y mssql-server mssql-mlservices-packages-r-9.4.7* mssql-mlservices-packages-py-9.4.7*
  ```

3. 接受授權合約，並完成安裝後設定。 使用 **mssql-conf** 工具來執行此工作。

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  系統會提示您接受資料庫引擎授權合約、選擇版本，以及設定系統管理員密碼。 系統也會提示您接受機器學習服務的授權合約。

4. 如果系統提示，請重新啟動服務。

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>自動安裝

使用資料庫引擎的[自動安裝](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended) \(部分機器翻譯\)，新增 mssql-mlservices 和 EULA 的套件。

您應該記得，安裝程式或 mssql-conf 工具會提示您接受授權合約。 如果您已經設定 SQL Server 資料庫引擎並接受其 EULA，請針對開放原始碼 R 和 Python 散發使用其中一個 mlservices 特定的 EULA 參數：

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

所有可能的 EULA 接受方式記載在[使用 mssql-conf 工具在 Linux 上設定 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-eula)。

## <a name="offline-installation"></a>離線安裝

遵循[離線安裝](sql-server-linux-setup.md#offline)指示，以取得安裝套件的步驟。 尋找您的下載網站，然後使用以下套件清單下載特定套件。

> [!Tip]
> 數個套件管理工具都提供協助您判斷套件相依性的命令。 若是 yum，請使用 `sudo yum deplist [package]`。 若是 Ubuntu，請使用 `sudo apt-get install --reinstall --download-only [package name]`，後面接著 `dpkg -I [package name].deb`。


#### <a name="download-site"></a>下載網站

您可以從 [https://packages.microsoft.com/](https://packages.microsoft.com/) 下載套件。 所有適用於 R 和 Python 的 mlservices 套件都與資料庫引擎套件共存。 mlservices 套件的基本版本是 9.4.5 (針對 CTP 2.0) 9.4.6 (針對 CTP 2.1 和更新版本)。 您應該記得，microsoft-r-open 套件在[其他存放庫](#mro)中。

#### <a name="rhel7-paths"></a>RHEL/7 路徑

|||
|--|----|
| mssql/mlservices 套件 | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |
| microsoft-r-open 套件 | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 路徑

|||
|--|----|
| mssql/mlservices 套件 | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |
| microsoft-r-open 套件 | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>SLES/12 路徑

|||
|--|----|
| mssql/mlservices 套件 | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| microsoft-r-open 套件 | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) | 

#### <a name="package-list"></a>套件清單

取決於您想要使用的擴充功能，下載適用於特定語言的必要套件。 確切的檔案名稱會在尾碼中包含平台資訊，但下面的檔案名稱應該足以讓您判斷要取得的檔案。

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# R
microsoft-openmpi-3.0.0
microsoft-r-open-mkl-3.5.2
microsoft-r-open-mro-3.5.2
mssql-mlservices-packages-r-9.4.7.64
mssql-mlservices-mlm-r-9.4.7.64


# Python
microsoft-openmpi-3.0.0
mssql-mlservices-python-9.4.7.64
mssql-mlservices-packages-py-9.4.7.64
mssql-mlservices-mlm-py-9.4.7.64
```

## <a name="add-more-rpython-packages"></a>新增更多 R/Python 套件 
 
您可以安裝其他 R 和 Python 套件，並在 SQL Server 2019 上執行的指令碼中使用它們。

### <a name="r-packages"></a>R 套件 
 
1. 啟動 R 工作階段。

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R 
   ```

2. 安裝稱為 [glue](https://mran.microsoft.com/package/glue) \(英文\) 的 R 套件以測試套件安裝。

   ```r
   # install.packages("glue",lib="/opt/mssql/mlservices/libraries/RServer") 
   ```
   或者，您可以從命令列安裝 R 套件 

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R CMD INSTALL -l /opt/mssql/mlservices/libraries/RServer glue_1.1.1.tar.gz 
   ```

3. 在 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 中匯入 R 套件。

   ```r
   EXEC sp_execute_external_script  
   @language = N'R', 
   @script = N'library(glue)' 
   ```

### <a name="python-packages"></a>Python 套件 
 
1. 使用 pip 安裝名為 [httpie](https://httpie.org/) 的 Python 套件。 

   ```python
   # sudo /opt/mssql/mlservices/bin/python/python -m pip install httpie 
   ``` 

2. 在 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 中匯入 Python 套件。
 
   ```python
   EXEC sp_execute_external_script  
   @language = N'Python',  
   @script = N'import httpie' 
   ```

## <a name="limitations-in-ctp-releases"></a>CTP 版本中的限制

Linux 上的 R 和 Python 整合仍在開發中。 預覽版本中尚未啟用下列功能。

+ 目前在 Linux 上的機器學習服務中無法使用隱含驗證，這表示您無法從進行中的 R 或 Python 指令碼連線回到伺服器，以存取資料或其他資源。 

### <a name="resource-governance"></a>資源管理

針對外部資源集區的[資源管理](../t-sql/statements/create-external-resource-pool-transact-sql.md)，Linux 與 Windows 之間有同位，但 [sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) 的統計資料在 Linux 上目前有不同單位。 在即將推出的 CTP 中，單位將會保持一致。
 
| 資料行名稱   | Description | Linux 上的值 | 
|---------------|--------------|---------------|
|peak_memory_kb | 用於資源集區的記憶體數量上限。 | 在 Linux 上，此統計資料是來自 CGroups 記憶體子系統，其中的值為 memory.max_usage_in_bytes |
|write_io_count | 重設 Resource Governor 統計資料之後發出的寫入 IO 總數。 | 在 Linux 上，此統計資料來自 CGroups blkio 子系統，其中寫入資料列上的值為 blkio.throttle.io_serviced | 
|read_io_count | 重設 Resource Governor 統計資料之後發出的讀取 IO 總數。 | 在 Linux 上，此統計資料來自 CGroups blkio 子系統，其中讀取資料列上的值為 blkio.throttle.io_serviced | 
|total_cpu_kernel_ms | 重設 Resource Governor 統計資料之後的累計 CPU 使用者核心時間 (以毫秒為單位)。 | 在 Linux 上，此統計資料來自 CGroups cpuacct 子系統，其中使用者資料列上的值為 cpuacct.stat |  
|total_cpu_user_ms | 重設 Resource Governor 統計資料之後的累計 CPU 使用者時間 (以毫秒為單位)。| 在 Linux 上，此統計資料來自 CGroups cpuacct 子系統，其中系統資料列值上的值為 cpuacct.stat | 
|active_processes_count | 在要求當時正在執行的外部處理序數目。| 在 Linux 上，此統計資料是來自 CGroups pids 記憶體子系統，其中的值為 pids.current | 

## <a name="next-steps"></a>後續步驟

R 開發人員可以從一些簡單的範例開始，並了解 R 如何搭配 SQL Server 使用的基本概念。 如需下一個步驟，請參閱下列連結：

+ [教學課程：在 T-SQL 中執行 R](../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [教學課程：適用於 R 開發人員的資料庫內分析](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 開發人員可以遵循下列教學課程，以了解如何搭配使用 Python 與 SQL Server：

+ [教學課程：在 T-SQL 中執行 Python](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [教學課程：適用於 Python 開發人員的資料庫內分析](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

若要檢視以真實世界案例為基礎的機器學習範例，請參閱[機器學習服務教學課程](../advanced-analytics/tutorials/machine-learning-services-tutorials.md)。
