---
title: 在 Linux 上安裝
titleSuffix: SQL Server Machine Learning Services
description: 了解如何在 Linux 上安裝 SQL Server 機器學習服務 (Python 和 R)：Red Hat、Ubuntu 和 SUSE。
author: cawrites
ms.author: chadam
ms.reviewer: davidph
manager: cgronlun
ms.date: 03/05/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning-services
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 34e33ea3fbb3ff0ef10e237bc7bdc0ad61c223db
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2020
ms.locfileid: "86484620"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-linux"></a>在 Linux 上安裝 SQL Server 機器學習服務 (Python 和 R)

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

本文會引導您在 Linux 上安裝 [SQL Server 機器學習服務](../machine-learning/index.yml)。 您可使用機器學習服務來在資料庫中執行 Python 和 R 指令碼。

> [!NOTE]
> 根據預設，系統會在 SQL Server 巨量資料叢集上安裝機器學習服務。 如需詳細資訊，請參閱[在巨量資料叢集上使用機器學習服務 (Python 和 R)](../big-data-cluster/machine-learning-services.md)

<a name="mro"></a>

## <a name="pre-install-checklist"></a>預先安裝檢查清單

* [在 Linux 上安裝 SQL Server](sql-server-linux-setup.md) 並驗證安裝。

* 查看 Python 和 R 延伸模組的 SQL Server Linux 存放庫。 
  如果您已經為資料庫引擎安裝設定來源存放庫，您可以使用相同的存放庫登錄來執行 **mssql-mlservices** 套件安裝命令。

  您可在 Red Hat Enterprise Linux (RHEL)、SUSE Linux Enterprise Server (SLES) 和 Ubuntu 上安裝 SQL Server。 如需詳細資訊，請參閱 [Linux 上的 SQL Server 安裝指引](sql-server-linux-setup.md#supportedplatforms)中的＜支援的平台＞一節。

* (僅限 R) Microsoft R Open (MRO) 為 SQL Server 中的 R 功能提供基底 R 散發，且是使用 RevoScaleR、MicrosoftML 和其他隨機器學習服務所安裝 R 套件的必要條件。
    * 所需的版本為 MRO 3.5.2。
    * 從下列兩個方法中選一個來安裝 MRO：
        * 從 MRAN 下載 MRO Tarball、將它解壓縮，然後執行其 install.sh 指令碼。 如果您要使用此方法，可以遵循 [MRAN 上的安裝指示](https://mran.microsoft.com/releases/3.5.2) \(英文\)。
        * 如下所述註冊 **packages.microsoft.com** 存放庫，以安裝 MRO 散發：microsoft-r-open-mro 和 microsoft-r-open-mkl。 
    * 請參閱以下的安裝章節，以了解如何安裝 MRO。

* 您應該有執行 T-SQL 命令的工具。 

  * 您可使用 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio)，這是在 Linux、Windows 和 macOS 上執行的免費資料庫工具。

## <a name="package-list"></a>套件清單

在連線到網際網路的裝置上，系統會使用每個作業系統的套件安裝程式，獨立地下載及安裝套件。 下表描述只適用於 R 和 Python 的所有可用套件，您可以指定提供完整功能安裝或最基本功能安裝的套件。

可用的安裝套件：

| 套件名稱 | 適用於 | 描述 |
|--------------|----------|-------------|
|mssql-server-extensibility  | 全部 | 用來執行 Python 和 R 的擴充性架構。 |
| microsoft-openmpi  | Python、R | 針對 Linux 上用於平行處理，Rev* 程式庫所使用的訊息傳遞介面。 |
| mssql-mlservices-python | Python | Anaconda 和 Python 的開放原始碼散發。 |
|mssql-mlservices-mlm-py  | Python | *完整安裝*。 提供 revoscalepy、microsoftml、適用於影像特徵化和文字情感分析的預先定型的模型。| 
|mssql-mlservices-packages-py  | Python | 「最小安裝」  。 提供 revoscalepy 和 microsoftml。 <br/>排除預先定型的模型。 | 
| [microsoft-r-open*](#mro) | R | R 的開放原始碼散發，由三個套件組成。 |
|mssql-mlservices-mlm-r  | R | *完整安裝*。 提供：RevoScaleR，MicrosoftML、sqlRUtils、olapR、適用於影像特徵化和文字情感分析的預先定型模型。| 
|mssql-mlservices-packages-r  | R | 「最小安裝」  。 提供 RevoScaleR、sqlRUtils、MicrosoftML、olapR。 <br/>排除預先定型的模型。 |

<a name="RHEL"></a>

## <a name="install-on-rhel"></a>在 RHEL 上安裝

請遵循下列步驟，在 Red Hat Enterprise Linux (RHEL) 上安裝 SQL Server 機器學習服務。

### <a name="install-mro-on-rhel"></a>在 RHEL 上安裝 MRO

下列命令會登錄提供 MRO 的存放庫。 登錄後，安裝其他 R 套件 (例如，mssql-mlservices-mml-r) 的命令會自動包含在 MRO 中作為套件相依性。
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

Python 和 R 的安裝選項：

*  根據需求安裝語言支援 (單一或多個語言)。
*  「完整安裝」  提供所有可用功能，包括預先定型的機器學習模型。
*  「最小安裝」  則會排除模型，但仍具備所有功能。

> [!Tip]
> 可能的話，請在安裝之前執行 `yum clean all`，以重新整理系統上的套件。

### <a name="full-installation"></a>完整安裝

包含：
*  開放原始碼的 Python
*  開放原始碼的 R
*  Extensibility Framework
*  Microsoft-openmpi
*  延伸模組 (Python、R)
*  機器學習程式庫
*  適用於 Python 和 R 的預先定型模型

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.7*
sudo yum install mssql-mlservices-mlm-r-9.4.7*
```

### <a name="minimum-installation"></a>最小安裝

包含：
*  開放原始碼的 Python
*  開放原始碼的 R
*  Extensibility Framework
*  Microsoft-openmpi
*  核心 Revo* 程式庫
*  機器學習程式庫

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.7*
sudo yum install mssql-mlservices-packages-r-9.4.7*
```
<a name="ubuntu"></a>

## <a name="install-on-ubuntu"></a>在 Ubuntu 上安裝

請遵循下列步驟，在 Ubuntu 上安裝 SQL Server 機器學習服務。

### <a name="install-mro-on-ubuntu"></a>在 Ubuntu 上安裝 MRO

下列命令會登錄提供 MRO 的存放庫。 登錄後，安裝其他 R 套件 (例如，mssql-mlservices-mml-r) 的命令會自動包含在 MRO 中作為套件相依性。

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

Python 和 R 的安裝選項：

*  根據需求安裝語言支援 (單一或多個語言)。
*  「完整安裝」  提供所有可用功能，包括預先定型的機器學習模型。
*  「最小安裝」  則會排除模型，但仍具備所有功能。

> [!Tip]
> 可能的話，請在安裝之前執行 `apt-get update`，以重新整理系統上的套件。 

### <a name="full-installation"></a>完整安裝 

包含：
*  開放原始碼的 Python
*  開放原始碼的 R
*  Extensibility Framework
*  Microsoft-openmpi
*  Python 擴充功能
*  R 擴充功能
*  機器學習程式庫
*  適用於 Python 和 R 的預先定型模型

```bash
# Install as root or sudo
# Add everything (all R, Python)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
```

### <a name="minimum-installation"></a>最小安裝 

包含：
*  開放原始碼的 Python
*  開放原始碼的 R
*  Extensibility Framework
*  Microsoft-openmpi
*  核心 Revo* 程式庫
*  機器學習程式庫

```bash
# Install as root or sudo
# Minimum install of R, Python
# No asterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
```

<a name="SLES"></a>

## <a name="install-on-sles"></a>在 SLES 上安裝

請遵循下列步驟，在 SUSE Linux Enterprise Server (SLES) 上安裝 SQL Server 機器學習服務。

### <a name="install-mro-on-sles"></a>在 SLES 上安裝 MRO

下列命令會登錄提供 MRO 的存放庫。 登錄後，安裝其他 R 套件 (例如，mssql-mlservices-mml-r) 的命令會自動包含在 MRO 中作為套件相依性。

```bash
# Install as root
sudo su

# Set the location of the package repo at the "prod" directory containing the distribution
# This example is for SLES12, the only supported version of SLES in Machine Learning Server
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com

# Update packages on your system (optional)
zypper update
```

Python 和 R 的安裝選項：

*  根據需求安裝語言支援 (單一或多個語言)。
*  「完整安裝」  提供所有可用功能，包括預先定型的機器學習模型。
*  「最小安裝」  則會排除模型，但仍具備所有功能。

### <a name="full-installation"></a>完整安裝 

包含：
*  開放原始碼的 Python
*  開放原始碼的 R
*  Extensibility Framework
*  Microsoft-openmpi
*  Python 和 R 的延伸模組
*  機器學習程式庫
*  適用於 Python 和 R 的預先定型模型

```bash
# Install as root or sudo
# Add everything (all R, Python)
sudo zypper install mssql-mlservices-mlm-py
sudo zypper install mssql-mlservices-mlm-r
```

### <a name="minimum-installation"></a>最小安裝 

包含：
*  開放原始碼的 Python
*  開放原始碼的 R
*  Extensibility Framework
*  Microsoft-openmpi
*  核心 Revo* 程式庫
*  機器學習程式庫 

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
sudo zypper install mssql-mlservices-packages-py
sudo zypper install mssql-mlservices-packages-r
```

## <a name="post-install-config-required"></a>安裝後設定 (必要)

其他設定主要是透過 [mssql-conf 工具](sql-server-linux-configure-mssql-conf.md)來設定。

1. 套件安裝完成之後，請執行 mssql-conf setup 並遵循提示設定 SA 密碼，然後選擇版本。 只有尚未在 Linux 上設定 SQL Server 時，才需要執行此步驟。 

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. 接受開放原始碼 Python 和 R 延伸模組的授權合約。 使用下列命令：

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```
   在執行 `mssql-conf setup` 時，安裝程式會偵測 mssql mlservices 套件，並提示是否接受 EULA (如果先前沒有接受的話)。 如需 EULA 參數的詳細資訊，請參閱[使用 mssql-conf 工具設定 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-eula)。

3. 啟用輸出網路存取。 預設會停用輸出網路存取。 若要啟用輸出要求，請使用 mssql-conf 工具來設定 "outboundnetworkaccess" 布林值屬性。 如需詳細資訊，請參閱[使用 mssql-conf 在 Linux 上設定 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access)。

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. 若只需要 R 功能整合，請設定 **MKL_CBWR** 環境變數，以確保輸出與來自 Intel 數學核心程式庫 (MKL) 計算的[一致](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)。

   + 在使用者主目錄中編輯或建立名為 `.bash_profile` 的檔案，並將 `export MKL_CBWR="AUTO"` 這一行新增至檔案。

   + 在 bash 命令提示字元中輸入 `source .bash_profile` 來執行此檔案。

5. 重新啟動 SQL Server Launchpad 服務和資料庫引擎執行個體，以從 INI 檔案讀取更新後的值。 修改擴充性相關設定時，會顯示通知訊息。  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

6. 使用 Azure Data Studio 或 SQL Server Management Studio (僅限 Windows) 等執行 Transact-SQL 的另一種工具，來啟用外部指令碼執行。

   ```sql
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. 重新啟動 Launchpad 服務。

## <a name="verify-installation"></a>確認安裝

您可以在 `/opt/mssql/mlservices/libraries/RServer` 找到 R 程式庫 (MicrosoftML、RevoScaleR 和其他)。

您可以在 `/opt/mssql/mlservices/libraries/PythonServer` 找到 Python 程式庫 (microsoftml 和 revoscalepy)。

驗證安裝：

* 使用查詢工具執行 T-SQL 指令碼，該指令碼會執行叫用 Python 或 R 的系統預存程序。 

* 執行下列 SQL 命令，以在 SQL Server 中測試 R 執行。 錯誤？ 請嘗試重新啟動服務，`sudo systemctl restart mssql-server.service`。
  ```sql
  EXEC sp_execute_external_script   
  @language =N'R', 
  @script=N' 
  OutputDataSet <- InputDataSet', 
  @input_data_1 =N'SELECT 1 AS hello' 
  WITH RESULT SETS (([hello] int not null)); 
  GO 
  ```
 
* 執行下列 SQL 命令，以在 SQL Server 中測試 Python 執行。 
 
  ```sql
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

## <a name="unattended-installation"></a>自動安裝

使用資料庫引擎的[自動安裝](sql-server-linux-setup.md#unattended) \(部分機器翻譯\)，新增 mssql-mlservices 和 EULA 的套件。

 針對開放原始碼 R 和 Python 散發，使用其中一種 mlservices 限定的 EULA 參數：

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

完整的 EULA 可在[使用 mssql-conf 工具設定 Linux 上的 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-eula) 中找到。

## <a name="offline-installation"></a>離線安裝

遵循[離線安裝](sql-server-linux-setup.md#offline)指示，以取得安裝套件的步驟。 尋找您的下載網站，然後使用以下套件清單下載特定套件。

> [!Tip]
> 數個套件管理工具都提供協助您判斷套件相依性的命令。 若是 yum，請使用 `sudo yum deplist [package]`。 若是 Ubuntu，請使用 `sudo apt-get install --reinstall --download-only [package name]`，後面接著 `dpkg -I [package name].deb`。

 
### <a name="download-site"></a>下載網站

從 [https://packages.microsoft.com/](https://packages.microsoft.com/) 下載套件。 所有適用於 Python 和 R 的 mlservices 套件都與資料庫引擎套件共存。 mlservices 套件的基底版本是 9.4.6。 您應該記得，microsoft-r-open 套件在[其他存放庫](#mro)中。

### <a name="rhel7-paths"></a>RHEL/7 路徑

|Package|下載位置|
|--|----|
| mssql/mlservices 套件 | [https://packages.microsoft.com/rhel/7/mssql-server-2019/](https://packages.microsoft.com/rhel/7/mssql-server-2019/) |
| microsoft-r-open 套件 | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 

### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 路徑

|Package|下載位置|
|--|----|
| mssql/mlservices 套件 | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/) |
| microsoft-r-open 套件 | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

### <a name="sles12-paths"></a>SLES/12 路徑

|Package|下載位置|
|--|----|
| mssql/mlservices 套件 | [https://packages.microsoft.com/sles/12/mssql-server-2019/](https://packages.microsoft.com/sles/12/mssql-server-2019/) |
| microsoft-r-open 套件 | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) | 

選取所要使用的延伸模組，並下載特定語言的必要套件。 檔案名稱會在尾碼中包含平台資訊。

### <a name="package-list"></a>套件清單

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

## <a name="next-steps"></a>後續步驟

Python 開發人員可以遵循下列教學課程，以了解如何搭配使用 Python 與 SQL Server：

+ [Python 教學課程：在 SQL Server 機器學習服務中使用線性迴歸來預測滑雪工具租用](../machine-learning/tutorials/python-ski-rental-linear-regression-deploy-model.md)
+ [Python 教學課程：將 K-Means 叢集搭配 SQL Server 機器學習服務使用來分類客戶](../machine-learning/tutorials/python-clustering-model.md)

R 開發人員可以從一些簡單的範例開始，並了解 R 如何搭配 SQL Server 使用的基本概念。 如需下一個步驟，請參閱下列連結：

+ [快速入門：在 T-SQL 中執行 R](../machine-learning/tutorials/quickstart-r-create-script.md)
+ [教學課程：適用於 R 開發人員的資料庫內分析](../machine-learning/tutorials/sqldev-in-database-r-for-sql-developers.md)
