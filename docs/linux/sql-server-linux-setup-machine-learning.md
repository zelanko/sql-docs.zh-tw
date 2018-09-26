---
title: 安裝 SQL Server Machine Learning 在 Linux 上的 服務 (R、 Python、 Java) |Microsoft Docs
description: 這篇文章會說明如何安裝 SQL Server Machine Learning 服務 （R、 Python、 Java），在 Red Hat 和 Ubuntu 上。
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5d10e6646d83d90af60aa748a8265a069d961443
ms.sourcegitcommit: c3e233c13ebb6fbee60723590179da00802c3f3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2018
ms.locfileid: "47058927"
---
# <a name="install-sql-server-2019-machine-learning-services-r-python-java-on-linux"></a>安裝 SQL Server 2019 Machine Learning 在 Linux 上的服務 (R、 Python、 Java)

[SQL Server Machine Learning 服務](../advanced-analytics/what-is-sql-server-machine-learning.md)可開始在此預覽版本中的 SQL Server 2019 的 Linux 作業系統上執行。 請遵循這篇文章，以安裝 Java 程式設計延伸模組或擴充功能適用於 machine learning R 和 Python 中的步驟。 

機器學習服務和程式設計延伸模組是 database engine 的附加元件。 雖然您可以[同時安裝 database engine 和 Machine Learning 服務](#install-all)，它是安裝和設定 SQL Server database engine 第一次，讓您能夠解決任何問題，然後再加入其他最佳作法元件。 

R、 Python 和 Java 的擴充功能的封裝位置是在 SQL Server Linux 來源存放庫中。 如果您已經設定 database engine 的來源存放庫安裝，您可以執行 mssql mlservices 使用相同的存放庫註冊的套件安裝命令。

## <a name="prerequisites"></a>先決條件

+ Linux 作業系統必須是[SQL Server 支援](sql-server-linux-release-notes-2019.md#supported-platforms)、 在內部部署或在 Docker 容器中執行。

+ 您必須擁有 SQL Server 2019 Database Engine 執行個體： 

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ 適用於僅限 R [Microsoft R Open](#mro) mssql mlsservices R 套件。 

<a name="mro"></a>

### <a name="microsoft-r-open-mro"></a>Microsoft R Open (MRO)

Microsoft 的基底 R 散發是使用 RevoScaleR、 MicrosoftML 和使用機器學習服務已安裝其他 R 套件的必要條件。

下列命令註冊存放庫提供 MRO。 註冊，安裝其他 R 套件的命令就會自動包含 MRO 為封裝相依性。

#### <a name="on-ubuntu"></a>在 Ubuntu 上

```bash
# Set the location of the package repo the "prod" directory containing the distribution.
# This example specifies 16.04. Replace with 18.04 if you want that version
wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the repo
dpkg -i packages-microsoft-prod.deb
```

#### <a name="on-rhel"></a>在 RHEL 上

```bash
# Set the location of the package repo at the "prod" directory
rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm
```
#### <a name="on-suse"></a>在 SUSE 上

```bash
# Set the location of the package repo
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com
```

## <a name="package-list"></a>套件清單

在連線網際網路的裝置，套件會下載並安裝獨立資料庫引擎的每個作業系統使用套件安裝程式。 下表描述所有可用的套件，但連線到網際網路的安裝，您只需要*一個*R 或 Python 套件，以取得特定的功能組合。

| 封裝名稱 | 套用至 | 描述 |
|--------------|----------|-------------|
|mssql 伺服器擴充性  | All | 用來執行 R、 Python 或 Java 程式碼的擴充性架構。 |
|mssql server 擴充性-java | Java | 載入的 Java 執行環境的 Java 延伸模組。 沒有任何額外的程式庫或適用於 Java 的封裝。 |
| microsoft openmpi  | Python、 R | 訊息傳遞介面 Revo * 程式庫用來在 Linux 上的平行處理。 |
| microsoft r 開啟 | R | 開放原始碼 r 分布 |
| mssql-mlservices-python | Python | Anaconda 和 Python 的開放原始碼散發套件。 |
|mssql mlservices-mlm py  | Python | 完整安裝。 提供 revoscalepy，microsoftml，預先定型的影像特徵化和文字情感分析模型。| 
|mssql mlservices-mml py  | Python | 部分安裝。 提供 revoscalepy，microsoftml。 <br/>排除預先定型的模型。 | 
|mssql mlservices 封裝-py  | Python | 部分安裝。 提供 revoscalepy。 <br/>預先定型的模型和 microsoftml 排除。 | 
|mssql mlservices mlm-r  | R | 完整安裝。 提供第 sqlRUtils RevoScaleR，MicrosoftML、 olapR，預先定型的影像特徵化和文字情感分析模型。| 
|mssql mlservices mml-r  | R | 部分安裝。 RevoScaleR、 MicrosoftML、 sqlRUtils、 olapR 提供。 <br/>排除預先定型的模型。  |
|mssql mlservices 封裝-r  | R | 部分安裝。 RevoScaleR sqlRUtils、 olapR 提供。 <br/>預先定型的模型和 MicrosoftML 排除。 | 

<a name="RHEL"></a>

## <a name="rhel-commands"></a>RHEL 命令

安裝任何*一個*R 封裝，再加上任何*一個*Python 套件，以及如果您想要這項功能的 Java。 每個 R 和 Python 套件中包含功能的組合。 選擇套件，可提供您所需要的功能集。 相依的套件會自動包含在內。

> [!Tip]
> 可能的話，請執行`yum clean all`重新整理在安裝之前的系統上的封裝。

### <a name="example-1----full-installation"></a>範例 1： 完整安裝 

包含 R 和 Python 的開放原始碼 R 和 Python 擴充性架構，microsoft openmpi，延伸模組 （R、 Python、 Java），與機器學習程式庫和預先定型的模型。 R 和 Python，如果您想要完整和最小安裝-機器學習程式庫等，但不使用預先定型的模型層之間的項目以取代`mssql-mlservices-mml-r-9.4.5*`和`mssql-mlservices-mml-py-9.4.5*`改。

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# Be sure to include -9.4.5* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.5*
sudo yum install mssql-mlservices-mlm-r-9.4.5* 
sudo yum install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>範例 2-最小安裝 

包含 R 和 Python、 Java 延伸模組的開放原始碼 R 和 Python 擴充性架構，microsoft-openmpi core Revo * 程式庫。 排除預先定型的模型和機器學習程式庫對 R 和 Python。 

```bash
# Install as root or sudo
# Minimum install of R, Python, Java extensions
# Be sure to include -9.4.5* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.5*
sudo yum install mssql-mlservices-packages-r-9.4.5*
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

## <a name="ubuntu-commands"></a>Ubuntu 的命令

安裝任何*一個*R 封裝，再加上任何*一個*Python 套件，以及如果您想要這項功能的 Java。 每個 R 和 Python 套件中包含功能的組合。 選擇套件，可提供您所需要的功能集。 相依的套件會自動包含在內。

> [!Tip]
> 可能的話，請執行`apt-get update`重新整理在安裝之前的系統上的封裝。 此外，某些的 docker 映像的 Ubuntu 可能沒有 https apt 的傳輸選項。 若要安裝，請使用`apt-get install apt-transport-https`。

### <a name="prerequisite-for-1804"></a>18.04 必要條件

Ubuntu 18.04 上執行 mssql mlservices R 程式庫，需要**libpng12**從 Linux 核心會封存。 此套件已不再包含在標準的通訊，且必須以手動方式安裝。 若要取得此文件庫，請執行下列命令：

```bash
wget https://mirrors.kernel.org/ubuntu/pool/main/libp/libpng/libpng12-0_1.2.54-1ubuntu1_amd64.deb
dpkg -i libpng12-01_1.2.54-1ubuntu1_amd64.deb
```

### <a name="example-1----full-installation"></a>範例 1： 完整安裝 

包含 R 和 Python 的開放原始碼 R 和 Python 擴充性架構，microsoft openmpi，延伸模組 （R、 Python、 Java），與機器學習程式庫和預先定型的模型。 R 和 Python，如果您想要讓之間完整和最小安裝-機器學習程式庫等，但不使用預先定型的模型-改為取代 mssql mlservices mml-r 和 mssql mlservices-mml py。

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
sudo apt-get install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>範例 2-最小安裝 

包含 R 和 Python、 Java 延伸模組的開放原始碼 R 和 Python 擴充性架構，microsoft-openmpi core Revo * 程式庫。 排除預先定型的模型和機器學習程式庫對 R 和 Python。 

```bash
# Install as root or sudo
# Minimum install of R, Python, Java
# No aasterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
sudo apt-get install mssql-server-extensibility-java
```

<a name="suse"></a>

## <a name="suse-commands"></a>SUSE 命令

安裝任何*一個*R 封裝，再加上任何*一個*Python 套件，以及如果您想要這項功能的 Java。 每個 R 和 Python 套件中包含功能的組合。 選擇套件，可提供您所需要的功能集。 相依的套件會自動包含在內。 

### <a name="example-1----full-installation"></a>範例 1： 完整安裝 

包含 R 和 Python 的開放原始碼 R 和 Python 擴充性架構，microsoft openmpi，延伸模組 （R、 Python、 Java），與機器學習程式庫和預先定型的模型。 R 和 Python，如果您想要完整和最小安裝-機器學習程式庫等，但不使用預先定型的模型層之間的項目以取代`mssql-mlservices-mml-r-9.4.5*`和`mssql-mlservices-mml-py-9.4.5*`改。

```bash
# Install as root or sudo
# Add everything (all R, Python, Java)
# Be sure to include -9.4.5* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.5*
sudo zypper install mssql-mlservices-mlm-r-9.4.5* 
sudo zypper install mssql-server-extensibility-java
```

### <a name="example-2---minimum-installation"></a>範例 2-最小安裝 

包含 R 和 Python、 Java 延伸模組的開放原始碼 R 和 Python 擴充性架構，microsoft-openmpi core Revo * 程式庫。 排除預先定型的模型和機器學習程式庫對 R 和 Python。 

```bash
# Install as root or sudo
# Minimum install of R, Python, Java extensions
# Be sure to include -9.4.5* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.5*
sudo zypper install mssql-mlservices-packages-r-9.4.5*
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>後續安裝組態 （必要）

主要透過其他設定，就[mssql-conf 工具](sql-server-linux-configure-mssql-conf.md)。


1. 新增用來執行 SQL Server Launchpad 服務 mssql 使用者帳戶。

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

3. 重新啟動 SQL Server Launchpad 服務和資料庫引擎執行個體。

  ```bash
  systemctl restart mssql-launchpadd

  systemctl restart mssql-server.service
  ```

4. 啟用 SQL Server Management Studio 或其他工具執行 TRANSACT-SQL 中的外部指令碼執行。 

  ```bash
  EXEC sp_configure 'external scripts enabled', 1 
  RECONFIGURE WITH OVERRIDE 
  ```

## <a name="verify-installation"></a>確認安裝

R 程式庫 （MicrosoftML、 RevoScaleR，以及其他），請參閱`/opt/mssql/mlservices/libraries/RServer`。

（microsoftml 和 revoscalepy） 的 Python 程式庫，請參閱`/opt/mssql/mlservices/libraries/PythonServer`。

使用 SQL Server 查詢工具，執行下列 SQL 命令來測試 SQL Server 中的 R 執行。 如果指令碼未執行，請嘗試重新啟動服務， `sudo systemctl restart mssql-server`。

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

## <a name="chained-installation"></a>鏈結的安裝

您可以安裝並在程序中設定 database engine 和 Machine Learning 服務，藉由附加 R、 Python 或 Java 的封裝和參數在命令中安裝資料庫引擎。 

下列範例是 「 範本 」 圖例中的套件組合的安裝看起來像使用 Yum 套件管理員：

```bash
sudo yum install -y mssql-sqlserver mssql-server-extensibility-java 
```

此範例會安裝 database engine，並新增為相依性 extensibility framework 套件會提取的 Java 語言擴充功能。 在此範例中使用的套件的所有位於相同的路徑。 如果您已新增 R 封裝，就必須使用 microsoft r 開啟套件存放庫的註冊。

安裝後，請務必使用 mssql-conf 工具來設定整個安裝，並接受授權合約。 自動偵測到開放原始碼 R 和 Python 元件不被接受的 Eula，系統會提示您接受這些條款，以及適用於 SQL Server 使用者授權合約。

```bash
sudo /opt/mssql/bin/mssql-conf setup MSSQL_PID=Developer 
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

您可以從套件下載[ https://packages.microsoft.com/ ](https://packages.microsoft.com/)。 所有 R、 Python 和 Java 的 mlservices 套件都是共置於資料庫引擎套件。 9.4.5 mlservices 套件的基底版本。 Micrososoft r 開啟封裝是在不同的資料夾。

#### <a name="rhel7-paths"></a>RHEL/7 路徑

|||
|--|----|
| mssql/mlservices 套件 | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |
| microsoft r 開啟套件 | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 路徑

|||
|--|----|
| mssql/mlservices 套件 | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |
| microsoft r 開啟套件 | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### <a name="sles12-paths"></a>SLES/12 路徑

|||
|--|----|
| mssql/mlservices 套件 | [ https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| microsoft r 開啟套件 | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) | 

#### <a name="package-list"></a>套件清單

根據哪些延伸模組，您想要使用、 下載所需的特定語言套件。 確切的檔名包含平台資訊，但是應該關閉，以判斷哪些檔案，以便取得下列檔案名稱。

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# Java
mssql-server-extensibility-java-15.0.1000

# R
microsoft-openmpi-3.0.0
microsoft-r-open-foreachiterators-3.4.4
microsoft-r-open-mkl-3.4.4
microsoft-r-open-mro-3.4.4
mssql-mlservices-packages-r-9.4.5
mssql-mlservices-mlm-r-9.4.5
mssql-mlservices-mml-r-9.4.5

# Python
microsoft-openmpi-3.0.0
mssql-mlservices-python-9.4.5
mssql-mlservices-packages-py-9.4.5
mssql-mlservices-mlm-py-9.4.5
mssql-mlservices-mml-py-9.4.5 
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

## <a name="limitations-in-ctp-20"></a>在 CTP 2.0 中的限制

這個 CTP 版本中，有下列限制。

+ 隱含的驗證目前無法使用。 在 Linux 上的 Machine Learning 服務在此階段，這表示您無法從進行中 R 或 Python 指令碼來存取資料或其他資源連線至伺服器 

+ [CREATE EXTERNAL LIBRARY](../t-sql/statements/create-external-library-transact-sql.md) （適用於在資料庫中儲存的 R 套件） 目前不是在 Linux 上使用，且不支援 Python。  

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

+ [教學課程： 在 T-SQL 中執行 R](../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [適用於 R 開發人員教學課程： 在資料庫內分析](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 開發人員可以了解如何使用 SQL Server 中的 Python，遵循這些教學課程：

+ [教學課程： 在 T-SQL 中執行 Python](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [適用於 Python 開發人員教學課程： 在資料庫內分析](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

若要檢視機器學習服務依據真實世界案例的範例，請參閱[機器學習服務教學課程](../advanced-analytics/tutorials/machine-learning-services-tutorials.md)。
