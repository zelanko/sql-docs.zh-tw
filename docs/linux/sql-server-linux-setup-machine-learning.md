---
title: 在 Linux 上安裝 SQL Server 機器學習服務 (Python、R)
description: 了解如何在 Linux 上安裝 SQL Server 機器學習服務 (Python 和 R)：Red Hat、Ubuntu 和 SUSE。
author: cawrites
ms.author: chadam
ms.reviewer: vanto
manager: cgronlun
ms.date: 03/05/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bf474ff8a7587c916591e6d7ba4dc82052b516f7
ms.sourcegitcommit: fc99fdd586eabc2d60f33056123398f263d5913d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/09/2020
ms.locfileid: "78937654"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-linux"></a>在 Linux 上安裝 SQL Server 機器學習服務 (Python 和 R)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文會引導您在 Linux 上安裝 [SQL Server 機器學習服務](../advanced-analytics/index.yml)。 您可使用機器學習服務來在資料庫中執行 Python 和 R 指令碼。

[!NOTE]
> 根據預設，系統會在 SQL Server 巨量資料叢集上安裝機器學習服務。 如需詳細資訊，請參閱[在巨量資料叢集上使用機器學習服務 (Python 和 R)](../big-data-cluster/machine-learning-services.md)

## <a name="what-are-machine-learning-services"></a>什麼是機器學習服務

機器學習服務是資料庫引擎的功能附加元件。

請先安裝和設定 SQL Server 資料庫引擎，讓您可在新增更多元件之前解決所有問題。

## <a name="pre-install-checklist"></a>預先安裝檢查清單

[在 Linux 上安裝 SQL Server](https://docs.microsoft.com/sql/linux/sql-server-linux-setup) 並驗證安裝。

* 查看 Python 和 R 延伸模組的 SQL Server Linux 存放庫。 
* 如果您已經為資料庫引擎安裝設定來源存放庫，您可以使用相同的存放庫登錄來執行 **mssql-mlservices** 套件安裝命令。

* [Microsoft R Open](#mro) 可提供 SQL Server 中 R 功能的基底 R 散發

* 您應該有執行 T-SQL 命令的工具。 
* 必須使用查詢編輯器進行安裝後設定和驗證。 
* 我們推薦 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux) \(部分機器翻譯\)，這是在 Linux 上執行的免費下載。


<a name="mro"></a>

### <a name="microsoft-r-open-mro-installation"></a>Microsoft R Open (MRO) 安裝

Microsoft 的 R 基底散發是使用 RevoScaleR、MicrosoftML 和其他隨機器學習服務安裝之 R 套件的先決條件。

所需的版本為 MRO 3.5.2。

從下列兩個方法中選一個來安裝 MRO：

+ 從 MRAN 下載 MRO Tarball、將它解壓縮，然後執行其 install.sh 指令碼。 如果您要使用此方法，可以遵循 [MRAN 上的安裝指示](https://mran.microsoft.com/releases/3.5.2) \(英文\)。

+ 如下所述註冊 **packages.microsoft.com** 存放庫，以安裝 MRO 散發：microsoft-r-open-mro 和 microsoft-r-open-mkl。 

<a name="RHEL"></a>

## <a name="install-on-redhat"></a>在 RedHat 上安裝

### <a name="install-mro-on-red-hat"></a>在 Red Hat 上安裝 (MRO)

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

### <a name="example-1----full-installation"></a>範例 1 - 完整安裝

包含：
*  開放原始碼的 Python
*  開放原始碼的 R
*  擴充性架構
*  microsoft-openmpi
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

### <a name="example-2---minimum-installation"></a>範例 2 - 最小安裝

包含：
*  開放原始碼的 Python
*  開放原始碼的 R
*  擴充性架構
*  microsoft-openmpi
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

### <a name="install-mro-on-ubuntu"></a>在 Ubuntu 上安裝 (MRO)

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

### <a name="example-1----full-installation"></a>範例 1 - 完整安裝 

包含：
*  開放原始碼的 Python
*  開放原始碼的 R
*  擴充性架構
*  microsoft-openmpi
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

### <a name="example-2---minimum-installation"></a>範例 2 - 最小安裝 

包含：
*  開放原始碼的 Python
*  開放原始碼的 R
*  擴充性架構
*  microsoft-openmpi
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

## <a name="install-on-suse"></a>在 SUSE 上安裝

### <a name="install-mro-on-susesles"></a>在 SUSE (SLES) 上安裝 (MRO)

```bash
# Install as root
sudo su

# Set the location of the package repo at the "prod" directory containing the distribution
# This example is for SLES12, the only supported version of SUSE in Machine Learning Server
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com

# Update packages on your system (optional)
zypper update
```

Python 和 R 的安裝選項：

*  根據需求安裝語言支援 (單一或多個語言)。
*  「完整安裝」  提供所有可用功能，包括預先定型的機器學習模型。
*  「最小安裝」  則會排除模型，但仍具備所有功能。

### <a name="example-1----full-installation"></a>範例 1 - 完整安裝 

包含：
*  開放原始碼的 Python
*  開放原始碼的 R
*  擴充性架構
*  microsoft-openmpi
*  Python 和 R 的延伸模組
*  機器學習程式庫
*  適用於 Python 和 R 的預先定型模型

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.7*
sudo zypper install mssql-mlservices-mlm-r-9.4.7* 
```

### <a name="example-2---minimum-installation"></a>範例 2 - 最小安裝 

包含：
*  開放原始碼的 Python
*  開放原始碼的 R
*  擴充性架構
*  microsoft-openmpi
*  核心 Revo* 程式庫
*  機器學習程式庫 

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.7*
sudo zypper install mssql-mlservices-packages-r-9.4.7*
```

## <a name="post-install-config-required"></a>安裝後設定 (必要)

其他設定主要是透過 [mssql-conf 工具](sql-server-linux-configure-mssql-conf.md)來設定。


1. 新增用來執行 SQL Server 服務的 mssql 使用者帳戶。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. 接受開放原始碼 Python 和 R 延伸模組的授權合約。 使用下列命令：

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```
3. 在執行 `mssql-conf setup` 時，安裝程式會偵測 mssql mlservices 套件，並提示是否接受 EULA (如果先前沒有接受的話)。 如需 EULA 參數的詳細資訊，請參閱[使用 mssql-conf 工具設定 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-eula)。

4. 啟用輸出網路存取。 預設會停用輸出網路存取。 若要啟用輸出要求，請使用 mssql-conf 工具來設定 "outboundnetworkaccess" 布林值屬性。 如需詳細資訊，請參閱[使用 mssql-conf 在 Linux 上設定 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access)。

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

5. 若只需要 R 功能整合，請設定 **MKL_CBWR** 環境變數，以確保輸出與來自 Intel 數學核心程式庫 (MKL) 計算的[一致](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)。

   + 在使用者主目錄中編輯或建立名為 `named.bash_profile` 的檔案，並將 `export MKL_CBWR="AUTO"` 這一行新增至檔案。

   + 在 bash 命令提示字元中輸入 `source.bash_profile` 來執行此檔案。

6. 重新啟動 SQL Server Launchpad 服務和資料庫引擎執行個體，以從 INI 檔案讀取更新後的值。 修改擴充性相關設定時，會顯示通知訊息。  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

7. 使用 Azure Data Studio 或 SQL Server Management Studio (僅限 Windows) 等執行 Transact-SQL 的另一種工具，來啟用外部指令碼執行。 

   ```bash
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. 重新啟動 Launchpad 服務。

## <a name="verify-installation"></a>確認安裝

您可以在 `/opt/mssql/mlservices/libraries/RServer` 找到 R 程式庫 (MicrosoftML、RevoScaleR 和其他)。

您可以在 `/opt/mssql/mlservices/libraries/PythonServer` 找到 Python 程式庫 (microsoftml 和 revoscalepy)。

驗證安裝：

- 使用查詢工具執行 T-SQL 指令碼，該指令碼會執行叫用 Python 或 R 的系統預存程序。 

針對 Windows，請使用： 
*  Azure Data Studio
*  SQL Server Management Studio 或 PowerShell

如果您有包含這些工具的 Windows 電腦，請使用它來連線到您的 Linux 安裝資料庫引擎。

執行下列 SQL 命令，以在 SQL Server 中測試 R 執行。 錯誤？ 請嘗試重新啟動服務，`sudo systemctl restart mssql-server.service`。

```
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

## <a name="unattended-installation"></a>自動安裝

使用資料庫引擎的[自動安裝](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended) \(部分機器翻譯\)，新增 mssql-mlservices 和 EULA 的套件。

 針對開放原始碼 R 和 Python 散發，使用其中一種 mlservices 限定的 EULA 參數：

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

完整的 EULA 可在[使用 mssql-conf 工具設定 Linux 上的 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-eula) 中找到。

## <a name="offline-installation"></a>離線安裝

遵循[離線安裝](sql-server-linux-setup.md#offline)指示，以取得安裝套件的步驟。 使用以下套件清單來下載特定套件。

> [!Tip]
> 數個套件管理工具都提供協助您判斷套件相依性的命令。 若是 yum，請使用 `sudo yum deplist [package]`。 若是 Ubuntu，請使用 `sudo apt-get install --reinstall --download-only [package name]`，後面接著 `dpkg -I [package name].deb`。


#### <a name="download-site"></a>下載網站

從 [https://packages.microsoft.com/](https://packages.microsoft.com/) 下載套件。 所有適用於 Python 和 R 的 mlservices 套件都與資料庫引擎套件共存。 mlservices 套件的基底版本是 9.4.6。 您應該記得，microsoft-r-open 套件在[其他存放庫](#mro)中。

#### <a name="rhel7-paths"></a>RHEL/7 路徑

|||
|--|----|
| mssql/mlservices 套件 | [https://packages.microsoft.com/rhel/7/mssql-server-2019/](https://packages.microsoft.com/rhel/7/mssql-server-2019/) |
| microsoft-r-open 套件 | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 路徑

|||
|--|----|
| mssql/mlservices 套件 | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/) |
| microsoft-r-open 套件 | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>SLES/12 路徑

|||
|--|----|
| mssql/mlservices 套件 | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| microsoft-r-open 套件 | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) |

## <a name="package-list"></a>套件清單

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

選取所要使用的延伸模組，並下載特定語言的必要套件。 檔案名稱會在尾碼中包含平台資訊。

檔案清單：

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

R 開發人員可以從一些簡單的範例開始，並了解 R 如何搭配 SQL Server 使用的基本概念。 如需下一個步驟，請參閱下列連結：

+ [教學課程：在 T-SQL 中執行 R](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [教學課程：適用於 R 開發人員的資料庫內分析](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 開發人員可以遵循下列教學課程，以了解如何搭配使用 Python 與 SQL Server：

+ [教學課程：在 T-SQL 中執行 Python](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [教學課程：適用於 Python 開發人員的資料庫內分析](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

若要檢視以真實世界案例為基礎的機器學習範例，請參閱[機器學習服務教學課程](../advanced-analytics/tutorials/machine-learning-services-tutorials.md)。
