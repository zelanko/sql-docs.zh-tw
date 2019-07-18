---
title: 在 Linux 上安裝 SQL Server Machine Learning 服務 （R、 Python）
description: 在 Red Hat、 Ubuntu 與 SUSE，了解如何安裝 SQL Server Machine Learning 服務 （R、 Python）。
author: dphansen
ms.author: davidph
ms.reviewer: vanto
manager: cgronlun
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5e64f19c7495a58c02852d9c1207b047de669758
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834678"
---
# <a name="install-sql-server-2019-machine-learning-services-r-python-on-linux"></a>安裝 SQL Server 2019 Machine Learning 服務 （R、 Python） 在 Linux 上

[SQL Server Machine Learning 服務](../advanced-analytics/what-is-sql-server-machine-learning.md)可開始在此預覽版本中的 SQL Server 2019 的 Linux 作業系統上執行。 請遵循本文，以安裝擴充功能適用於 machine learning R 和 Python 中的步驟。 

機器學習服務和程式設計延伸模組是 database engine 的附加元件。 雖然您可以[同時安裝 database engine 和 Machine Learning 服務](#install-all)，它是安裝和設定 SQL Server database engine 第一次，讓您能夠解決任何問題，然後再加入其他最佳作法元件。 

將 R 和 Python 延伸模組的封裝位置是在 SQL Server Linux 來源存放庫中。 如果您已經設定資料庫引擎安裝的來源存放庫，您可以執行**mssql mlservices**封裝使用相同的存放庫註冊的安裝命令。

Machine Learning 服務也支援在 Linux 容器。 我們不會提供預先建置的容器使用機器學習服務，但您可以從建立一個使用的 SQL Server 容器[可在 GitHub 上的範例範本](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices)。

## <a name="uninstall-previous-ctp"></a>解除安裝先前的 CTP

套件清單已變更透過最後幾個 CTP 版本中，導致較少的封裝。 我們建議您解除安裝 CTP 2.x 安裝 CTP 3.1 之前先移除所有先前的封裝。 不支援多個版本的並存安裝。

### <a name="1-confirm-package-installation"></a>1.確認封裝安裝

您可能想要檢查的第一個步驟中先前的安裝存在。 下列檔案表示現有的安裝： checkinstallextensibility.sh exthost、 啟動列。

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-previous-ctp-2x-packages"></a>2.解除安裝先前的 CTP 2.x 套件

解除安裝最低的套件層級。 會自動解除安裝任何相依於較低層級套件的上游套件。

  + R 整合，移除**microsoft r 開啟***
  + 對於 Python 整合移除**mssql-mlservices-python**

移除封裝的命令會顯示下表中。

| 平台  | 套件移除命令 | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove microsoft-r-open-mro-3.4.4`<br/>`sudo yum remove msssql-mlservices-python` |
| SLES  | `sudo zypper remove microsoft-r-open-mro-3.4.4`<br/>`sudo zypper remove msssql-mlservices-python` |
| Ubuntu    | `sudo apt-get remove microsoft-r-open-mro-3.4.4`<br/>`sudo apt-get remove msssql-mlservices-python`|

> [!Note]
> Microsoft R Open 3.4.4 組成兩個或三個封裝，取決於其的 CTP 版本您先前已安裝。 （foreachiterators 封裝已結合成 CTP 2.2 中主要的 mro 封裝）。如果任何這些套件仍移除 microsoft-r-開啟-mro-3.4.4 之後，您應該個別移除它們。
> ```
> microsoft-r-open-foreachiterators-3.4.4
> microsoft-r-open-mkl-3.4.4
> microsoft-r-open-mro-3.4.4
> ```

### <a name="3-proceed-with-ctp-31-install"></a>3.繼續進行 CTP 3.1 的安裝

在最高的封裝層級使用這篇文章中的指示，適用於您作業系統的安裝。

每個 OS 特定集的安裝指示*最高的封裝層級*是**範例 1-完整安裝**提供完整的封裝，或**範例 2-最小安裝**將最基本的可行安裝所需的套件數目。

1. 對於 R 整合開頭[MRO](#mro)因為它是必要條件。 沒有它，不會安裝 R 整合。

2. 執行使用適用於您作業系統的套件管理員和語法的安裝命令： 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>先決條件

+ Linux 版本必須是[SQL Server 支援](sql-server-linux-release-notes-2019.md#supported-platforms)，但不包含 Docker 引擎。 支援的版本包括：

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ (只有 R)[Microsoft R Open](#mro)提供基底 R 散發 SQL Server 中的 R 功能

+ 您應該有的工具執行 T-SQL 命令。 查詢編輯器是後續安裝組態和驗證所需的項目。 我們建議[Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux)，供免費下載，在 Linux 上執行。

<a name="mro"></a>

### <a name="microsoft-r-open-mro-installation"></a>Microsoft R Open (MRO) 安裝

Microsoft 的基底 R 散發是使用 RevoScaleR、 MicrosoftML 和使用機器學習服務已安裝其他 R 套件的必要條件。

MRO 3.5.2 所需的版本。

若要安裝 MRO 選擇下列兩種方法：

+ 從 MRAN 下載 MRO tarball、 解除封裝，並執行其 install.sh 指令碼。 您可以依照[MRAN 需安裝指示](https://mran.microsoft.com/releases/3.5.2)如果您想要這種方法。

+ 或者，註冊**packages.microsoft.com**存放庫，如下所述，安裝兩個套件組成 MRO 發佈： microsoft r open-mro 和 microsoft r open-mkl。 

下列命令註冊存放庫提供 MRO。 註冊，安裝其他 R 套件，例如 mssql-mlservices-mml-r，命令就會自動包含 MRO 為封裝相依性。

#### <a name="mro-on-ubuntu"></a>在 Ubuntu 上的 MRO

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

#### <a name="mro-on-rhel"></a>在 RHEL 上的 MRO

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
#### <a name="mro-on-suse"></a>在 SUSE 上的 MRO

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

在連線網際網路的裝置，套件會下載並安裝獨立資料庫引擎的每個作業系統使用套件安裝程式。 下表描述所有可用的套件，但對 R 和 Python，您會指定提供完整的功能安裝或最小功能安裝的套件。

| 封裝名稱 | Applies-to | 描述 |
|--------------|----------|-------------|
|mssql-server-extensibility  | All | 用來執行 R 和 Python 程式碼的擴充性架構。 |
| microsoft-openmpi  | Python, R | 訊息傳遞介面 Revo * 程式庫用來在 Linux 上的平行處理。 |
| mssql-mlservices-python | Python | Anaconda 和 Python 的開放原始碼散發套件。 |
|mssql-mlservices-mlm-py  | Python | *完整安裝*。 提供 revoscalepy，microsoftml，預先定型的影像特徵化和文字情感分析模型。| 
|mssql-mlservices-packages-py  | Python | *最小安裝*。 提供 revoscalepy 和 microsoftml。 <br/>排除預先定型的模型。 | 
| [microsoft-r-open*](#mro) | R | 開放原始碼 R，包含三個封裝發佈。 |
|mssql-mlservices-mlm-r  | R | *完整安裝*。 提供第 sqlRUtils RevoScaleR，MicrosoftML、 olapR，預先定型的影像特徵化和文字情感分析模型。| 
|mssql-mlservices-packages-r  | R | *最小安裝*。 提供 RevoScaleR，sqlRUtils，MicrosoftML、 olapR。 <br/>排除預先定型的模型。 | 
|mssql-mlservices-mml-py  | 僅限 CTP 2.0 2.1 | 因為 Python 套件的彙總到 mssql-mslservices-python 的 CTP 2.2 已過時。 提供 revoscalepy。 預先定型的模型和 microsoftml 排除。| 
|mssql-mlservices-mml-r  | 僅限 CTP 2.0 2.1 | 因為 R 套件的彙總到 mssql-mslservices-python 的 CTP 2.2 已過時。 RevoScaleR sqlRUtils、 olapR 提供。 預先定型的模型和 MicrosoftML 排除。  |

<a name="RHEL"></a>

## <a name="redhat-commands"></a>RedHat 命令

您可以安裝語言支援在任何組合，您需要 （單一或多個語言）。 如需 R 和 Python，有可從中選擇的兩個套件。 其中一個提供所有可用的功能，具備的特性*完整安裝*。 替代的選擇排除預先定型的機器學習服務模型，而且會被視為*最小安裝*。

> [!Tip]
> 可能的話，請執行`yum clean all`重新整理在安裝之前的系統上的封裝。

### <a name="example-1----full-installation"></a>範例 1： 完整安裝 

包含 R 和 Python 的開放原始碼 R 和 Python 擴充性架構，microsoft openmpi，延伸模組 （R、 Python），與機器學習程式庫和預先定型的模型。 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.7*
sudo yum install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>範例 2-最小安裝 

包含 R 和 Python 的開放原始碼 R 和 Python，extensibility framework、 microsoft-openmpi、 core Revo * 程式庫和機器學習程式庫。 排除預先定型的模型。

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.7*
sudo yum install mssql-mlservices-packages-r-9.4.7*
```

<a name="ubuntu"></a>

## <a name="ubuntu-commands"></a>Ubuntu 的命令

您可以安裝語言支援在任何組合，您需要 （單一或多個語言）。 如需 R 和 Python，有可從中選擇的兩個套件。 其中一個提供所有可用的功能，具備的特性*完整安裝*。 替代的選擇排除預先定型的機器學習服務模型，而且會被視為*最小安裝*。

> [!Tip]
> 可能的話，請執行`apt-get update`重新整理在安裝之前的系統上的封裝。 此外，某些的 docker 映像的 Ubuntu 可能沒有 https apt 的傳輸選項。 若要安裝，請使用`apt-get install apt-transport-https`。

### <a name="example-1----full-installation"></a>範例 1： 完整安裝 

包含 R 和 Python 的開放原始碼 R 和 Python 擴充性架構，microsoft openmpi，延伸模組 （R、 Python），與機器學習程式庫和預先定型的模型。 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
```

### <a name="example-2---minimum-installation"></a>範例 2-最小安裝 

包含 R 和 Python 的開放原始碼 R 和 Python，extensibility framework、 microsoft-openmpi、 core Revo * 程式庫和機器學習程式庫。 排除預先定型的模型。 

```bash
# Install as root or sudo
# Minimum install of R, Python
# No aasterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
```

<a name="suse"></a>

## <a name="suse-commands"></a>SUSE 命令

您可以安裝語言支援在任何組合，您需要 （單一或多個語言）。 如需 R 和 Python，有可從中選擇的兩個套件。 其中一個提供所有可用的功能，具備的特性*完整安裝*。 替代的選擇排除預先定型的機器學習服務模型，而且會被視為*最小安裝*。

### <a name="example-1----full-installation"></a>範例 1： 完整安裝 

包含 R 和 Python 的開放原始碼 R 和 Python 擴充性架構，microsoft openmpi，延伸模組 （R、 Python），與機器學習程式庫和預先定型的模型。 

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.7*
sudo zypper install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>範例 2-最小安裝 

包含 R 和 Python 的開放原始碼 R 和 Python，extensibility framework、 microsoft-openmpi、 core Revo * 程式庫和機器學習程式庫。 排除預先定型的模型。 

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.7*
sudo zypper install mssql-mlservices-packages-r-9.4.7*
```

## <a name="post-install-config-required"></a>後續安裝組態 （必要）

主要透過其他設定，就[mssql-conf 工具](sql-server-linux-configure-mssql-conf.md)。


1. 新增用來執行 SQL Server 服務 mssql 使用者帳戶。 如果您還沒有執行安裝程式之前，這是必要的。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. 接受授權合約的開放原始碼 R 和 Python。 有數種方式可以執行這項操作。 如果您先前接受 SQL Server 授權，而且現在要新增的 R 或 Python 的延伸模組，則下列命令會是貴用戶同意其條款：

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```

   替代的工作流程時，如果您還未接受授權合約的 SQL Server database engine，安裝程式偵測到 mssql mlservices 封裝並接受會提示您輸入時`mssql-conf setup`執行。 如需 「 授權合約 」 參數的詳細資訊，請參閱[mssql-conf 工具與設定 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-eula)。

3. 啟用輸出網路存取。 預設會停用輸出網路存取。 若要啟用輸出要求，請設定"outboundnetworkaccess 」 使用 mssql-conf 工具的布林值屬性。 如需詳細資訊，請參閱 <<c0> [ 設定 SQL Server on Linux 使用 mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access)。

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. 適用於 R 功能整合，將**MKL_CBWR**環境變數，以[確保一致的輸出](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)從 Intel 數學核心程式庫 (MKL) 計算。

   + 編輯或建立名為 **.bash_profile**在使用者主目錄中，將這一行加入`export MKL_CBWR="AUTO"`檔案。

   + 執行此檔案輸入`source .bash_profile`bash 命令提示字元。

5. 重新啟動 SQL Server Launchpad 服務和資料庫引擎執行個體讀取 INI 檔案中的更新後的值。 重新啟動訊息會提醒您每次修改擴充性相關的設定。  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

6. 啟用外部指令碼執行使用 Azure Data Studio 或 SQL Server Management Studio (僅 Windows) 等其他工具執行 Transact SQL。 

   ```bash
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. 重新啟動 Launchpad 服務。

## <a name="verify-installation"></a>確認安裝

R 程式庫 （MicrosoftML、 RevoScaleR，以及其他），請參閱`/opt/mssql/mlservices/libraries/RServer`。

（microsoftml 和 revoscalepy） 的 Python 程式庫，請參閱`/opt/mssql/mlservices/libraries/PythonServer`。

若要驗證安裝，執行的 T-SQL 指令碼執行系統預存程序叫用 R 或 Python。 您必須針對這項工作的查詢工具。 Azure Data Studio 是不錯的選擇。 其他常用於工具，例如 SQL Server Management Studio 或 PowerShell 是僅限 Windows。 如果您有使用這些工具的 Windows 電腦，請使用它來連接到 database engine 的 Linux 安裝。

執行下列 SQL 命令來測試 SQL Server 中的 R 執行。 如果指令碼未執行，請嘗試重新啟動服務， `sudo systemctl restart mssql-server.service`。

```r
EXEC sp_execute_external_script   
@language =N'R', 
@script=N' 
OutputDataSet <- InputDataSet', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```
 
執行下列 SQL 命令來測試 SQL Server 中的 Python 執行。 
 
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

## <a name="chained-combo-install"></a>鏈結的 「 組合 」 安裝

您可以安裝並在程序中設定 database engine 和 Machine Learning 服務，藉由附加 R 或 Python 的封裝和參數在命令中安裝資料庫引擎。 

1. 針對 R 整合安裝[Microsoft R Open](#mro)做為必要條件。 如果您不想要安裝 R 功能，請略過此步驟。

2. 提供命令列，其中包含資料庫引擎，再加上語言擴充功能。

  您可以新增單一的功能，例如整合到 database engine 安裝的 Python。

  ```bash
  sudo yum install -y mssql-server mssql-mlservices-packages-r-9.4.7* 
  ```

  或者，新增這兩個延伸模組 （R、 Python）。

  ```bash
  sudo yum install -y mssql-server mssql-mlservices-packages-r-9.4.7* mssql-mlservices-packages-py-9.4.7*
  ```

3. 接受授權合約，並完成後續安裝組態。 使用**mssql conf**這項工作的工具。

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  將提示您接受授權合約，database engine、 選擇版本，並設定系統管理員密碼。 您也會提示接受授權合約，Machine Learning 服務。

4. 如果系統提示您這樣做，請重新啟動服務。

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>自動安裝

使用[自動的安裝](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended)資料庫引擎中，新增 mssql mlservices 和 Eula 的套件。

回想一下，安裝程式或 mssql-conf 工具提示接受授權合約。 如果您已設定 SQL Server 資料庫引擎，並接受其授權條款，請使用 mlservices 特定使用者授權合約參數的其中一個開放原始碼 R 和 Python 散發套件：

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

接受的所有可能的排列方式會記載於[在 Linux 上使用 mssql-conf 工具的 設定 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-eula)。

## <a name="offline-installation"></a>離線安裝

請遵循[離線安裝](sql-server-linux-setup.md#offline)安裝套件的步驟的指示。 尋找您的下載網站，然後下載 使用下列套件清單的特定套件。

> [!Tip]
> 數個封裝管理工具提供命令，可協助您判斷封裝相依性。 使用 yum， `sudo yum deplist [package]`。 對於 Ubuntu，使用`sudo apt-get install --reinstall --download-only [package name]`後面接著`dpkg -I [package name].deb`。


#### <a name="download-site"></a>下載網站

您可以從套件下載[ https://packages.microsoft.com/ ](https://packages.microsoft.com/)。 R 和 Python 的 mlservices 套件全都與資料庫引擎套件共置。 Mlservices 套件的基底版本是 （適用於 CTP 2.0) 的 9.4.5 9.4.6 （CTP 2.1 和更新版本）。 提醒您，microsoft r 開放封裝位於[不同的存放庫](#mro)。

#### <a name="rhel7-paths"></a>RHEL/7 路徑

|||
|--|----|
| mssql/mlservices 套件 | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |
| microsoft-r-open packages | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 路徑

|||
|--|----|
| mssql/mlservices 套件 | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |
| microsoft-r-open packages | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>SLES/12 路徑

|||
|--|----|
| mssql/mlservices 套件 | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| microsoft-r-open packages | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) | 

#### <a name="package-list"></a>套件清單

根據哪些延伸模組，您想要使用、 下載所需的特定語言套件。 確切的檔名包含平台資訊的後置詞，但應該關閉，以判斷哪些檔案，以便取得下列檔案名稱。

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
 
您可以安裝其他 R 和 Python 套件，並在 SQL Server 2019 執行的指令碼中使用它們。

### <a name="r-packages"></a>R 套件 
 
1. 啟動 R 工作階段。

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R 
   ```

2. 安裝 R 套件，稱為[黏附](https://mran.microsoft.com/package/glue)來測試套件的安裝。

   ```r
   # install.packages("glue",lib="/opt/mssql/mlservices/libraries/RServer") 
   ```
   或者，您可以從命令列安裝 R 封裝 

   ```r
   # sudo /opt/mssql/mlservices/bin/R/R CMD INSTALL -l /opt/mssql/mlservices/libraries/RServer glue_1.1.1.tar.gz 
   ```

3. 匯入中的 R 封裝[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

   ```r
   EXEC sp_execute_external_script  
   @language = N'R', 
   @script = N'library(glue)' 
   ```

### <a name="python-packages"></a>Python 套件 
 
1. 安裝 Python 套件，稱為[httpie](https://httpie.org/)使用 pip。 

   ```python
   # sudo /opt/mssql/mlservices/bin/python/python -m pip install httpie 
   ``` 

2. 匯入中的 Python 套件[sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。
 
   ```python
   EXEC sp_execute_external_script  
   @language = N'Python',  
   @script = N'import httpie' 
   ```

## <a name="limitations-in-ctp-releases"></a>在 CTP 版本中的限制

在 Linux 上的 R 和 Python 整合是仍在作用中的開發。 預覽版中尚未啟用下列功能。

+ 隱含的驗證目前無法使用。 在 Linux 上的 Machine Learning 服務在此階段，這表示您無法從進行中 R 或 Python 指令碼來存取資料或其他資源連線至伺服器 

### <a name="resource-governance"></a>資源控管

沒有 Linux 和 Windows 的之間的同位檢查[資源控管](../t-sql/statements/create-external-resource-pool-transact-sql.md)外部資源集區，但的統計資料[sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md)目前有在 Linux 上的不同單位。 單位將會在即將推出的 CTP 中對齊。
 
| 資料行名稱   | 描述 | 在 Linux 上的值 | 
|---------------|--------------|---------------|
|peak_memory_kb | 最大資源集區使用的記憶體數量。 | 在 Linux 上，這項統計資料被來自在 CGroups 記憶體子系統，其中的值是 memory.max_usage_in_bytes |
|write_io_count | 已重設資源管理員統計資料之後發出的 Io 寫入總數。 | 在 Linux 上，這項統計資料被來自 CGroups blkio 子系統，其中上寫入的資料列的值是 blkio.throttle.io_serviced | 
|read_io_count | 讀取已重設資源管理員統計資料之後發出的 Io 總數。 | 在 Linux 上，這項統計資料被來自在 CGroups blkio 子系統，其中讀取的資料列的值是 blkio.throttle.io_serviced | 
|total_cpu_kernel_ms | 累計 CPU 使用者核心時間 （毫秒） 重設資源管理員統計資料之後。 | 在 Linux 上，這項統計資料被來自在 CGroups cpuacct 子系統，其中的使用者資料列上的值是 cpuacct.stat |  
|total_cpu_user_ms | 累計 CPU 使用者時間 （毫秒） 重設資源管理員統計資料之後。| 在 Linux 上，這項統計資料被來自 CGroups cpuacct 子系統上的系統資料列值的值所在 cpuacct.stat | 
|active_processes_count | 要求的目前執行的外部處理序數目。| 在 Linux 上，這項統計資料被來自 GGroups pid 子系統，其中的值是 pids.current | 

## <a name="next-steps"></a>後續步驟

R 開發人員可以開始使用一些簡單的範例，並了解 R 與 SQL Server 的運作方式的基本概念。 下一個步驟中，請參閱下列連結：

+ [教學課程：在 T-SQL 中執行 R](../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [教學課程：適用於 R 開發人員的資料庫內分析](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 開發人員可以了解如何使用 SQL Server 中的 Python，遵循這些教學課程：

+ [教學課程：在 T-SQL 中執行 Python](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [教學課程：適用於 Python 開發人員的資料庫內分析](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

若要檢視機器學習服務依據真實世界案例的範例，請參閱[機器學習服務教學課程](../advanced-analytics/tutorials/machine-learning-services-tutorials.md)。
