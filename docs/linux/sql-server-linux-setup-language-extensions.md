---
title: 在 Linux 上安裝 SQL Server 語言延伸模組 (Java) |Microsoft Docs
description: 在 Red Hat、 Ubuntu 與 SUSE，了解如何安裝 SQL Server 語言擴充功能 (Java)。
author: dphansen
ms.author: davidph
manager: cgronlun
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b694cde8784a1607c85ed9ab7dfcc4d770a6d938
ms.sourcegitcommit: 3b266dc0fdf1431fdca6b2ad34ae5fd38abe9f69
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/24/2019
ms.locfileid: "66186812"
---
# <a name="install-sql-server-2019-language-extensions-java-on-linux"></a>在 Linux 上安裝 SQL Server 2019 語言延伸模組 (Java)

語言擴充功能是 database engine 的附加元件。 雖然您可以[同時安裝 database engine 和語言擴充功能](#install-all)，它會安裝及設定 SQL Server database engine 第一次，以便您解決任何問題然後再加入更多元件的最佳作法。 

請遵循這篇文章，若要安裝的 Java 語言擴充功能中的步驟。

Java 延伸模組的封裝位置是在 SQL Server Linux 來源存放庫中。 如果您已經設定資料庫引擎安裝的來源存放庫，您可以執行**mssql 伺服器擴充性-java**封裝使用相同的存放庫註冊的安裝命令。

語言擴充功能也支援在 Linux 容器。 我們不會提供預先建置的容器具有語言擴充功能，但您可以從建立一個使用的 SQL Server 容器[可在 GitHub 上的範例範本](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices)。

## <a name="uninstall-previous-ctp"></a>解除安裝先前的 CTP

套件清單已變更透過最後幾個 CTP 版本中，導致較少的封裝。 我們建議您解除安裝 CTP 2.x 安裝 CTP 3.0 之前先移除所有先前的封裝。 不支援多個版本的並存安裝。

### <a name="1-confirm-package-installation"></a>1.確認封裝安裝

您可能想要檢查的第一個步驟中先前的安裝存在。 下列檔案表示現有的安裝： checkinstallextensibility.sh exthost、 啟動列。

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-previous-ctp-2x-packages"></a>2.解除安裝先前的 CTP 2.x 套件

解除安裝最低的套件層級。 會自動解除安裝任何相依於較低層級套件的上游套件。

  + Java 整合移除**mssql 伺服器擴充性-java**

移除封裝的命令會顯示下表中。

| 平台  | 套件移除命令 | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove msssql-server-extensibility-java` |
| SLES  | `sudo zypper remove msssql-server-extensibility-java` |
| Ubuntu    | `sudo apt-get remove msssql-server-extensibility-java`|

### <a name="3-proceed-with-ctp-30-install"></a>3.繼續進行 CTP 3.0 安裝

在最高的封裝層級使用這篇文章中的指示，適用於您作業系統的安裝。

每個 OS 特定集的安裝指示*最高的封裝層級*是**範例 1-完整安裝**提供完整的封裝，或**範例 2-最小安裝**將最基本的可行安裝所需的套件數目。

1. 執行您 Linux 散發套件使用套件管理員和語法的安裝命令： 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>先決條件

+ Linux 版本必須是[SQL Server 支援](sql-server-linux-release-notes-2019.md#supported-platforms)，但不包含 Docker 引擎。 支援的版本包括：

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ 您應該有的工具執行 T-SQL 命令。 查詢編輯器是後續安裝組態和驗證所需的項目。 我們建議[Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux)，供免費下載，在 Linux 上執行。

## <a name="package-list"></a>套件清單

在連線網際網路的裝置，套件會下載並安裝獨立資料庫引擎的每個作業系統使用套件安裝程式。 下表描述所有可用的套件。

| 封裝名稱 | Applies-to | 描述 |
|--------------|----------|-------------|
|mssql-server-extensibility  | 所有語言 | 用來執行 Java 程式碼的擴充性架構。 |
|mssql-server-extensibility-java | Java | 載入的 Java 執行環境的 Java 延伸模組。 沒有任何額外的程式庫或適用於 Java 的封裝。 |

<a name="RHEL"></a>

## <a name="install-language-extensions"></a>安裝語言擴充功能

您可以安裝語言擴充功能和 Java 在 Linux 上安裝**mssql 伺服器擴充性-java**。 當您安裝**mssql 伺服器擴充性-java**，封裝會自動安裝 JRE 8，如果尚未安裝。 另外還會新增至名為 JRE_HOME 環境變數的 JVM 路徑。

> [!Note]
> 在連線網際網路的伺服器上，會下載封裝相依性，以及將其安裝主套件安裝過程中。 如果您的伺服器未連線到網際網路，請參閱中的更多詳細資料[離線安裝程式](#offline-install)。

### <a name="redhat-install-command"></a>RedHat 安裝命令

您可以使用下列命令的 RedHat 上安裝適用於 Java 的語言擴充功能。

> [!Tip]
> 可能的話，請執行`yum clean all`重新整理在安裝之前的系統上的封裝。

```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

### <a name="ubuntu-install-command"></a>Ubuntu 安裝命令

您可以使用下列命令在 Ubuntu 上安裝適用於 Java 的語言擴充功能。

> [!Tip]
> 可能的話，請執行`apt-get update`重新整理在安裝之前的系統上的封裝。 此外，某些的 docker 映像的 Ubuntu 可能沒有 https apt 的傳輸選項。 若要安裝，請使用`apt-get install apt-transport-https`。

```bash
# Install as root or sudo
sudo apt-get install mssql-server-extensibility-java
```

<a name="suse"></a>

### <a name="suse-install-command"></a>SUSE 安裝命令

您可以使用下列命令的 SUSE 上安裝適用於 Java 的語言擴充功能。

```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>後續安裝組態 （必要）

1. 在 Linux 上的 授與權限

    您不需要執行此步驟中，如果您使用外部程式庫。 工作的建議的方式使用外部程式庫。 從您的 jar 檔案建立外部程式庫的協助，請參閱[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)

    如果您不使用外部程式庫，您需要 SQL Server 提供的 jar 中執行的 Java 類別的權限。

    若要授與讀取及執行 jar 檔案的存取權，請執行下列**chmod**命令將 jar 檔案。 我們建議您一律將類別檔案放在 jar 中，當您使用 SQL Server。 如需建立 jar 的說明，請參閱[如何建立的 jar 檔案](https://docs.microsoft.com/sql/language-extensions/how-to/create-a-java-jar-file-from-class-files)。

    ```cmd
    chmod ug+rx <MyJarFile.jar>
    ```

    您也需要提供 mssql_satellite 權限以讀取/執行 jar 檔案。

    ```cmd
    chown mssql_satellite:mssql_satellite <MyJarFile.jar>
    ```

    主要透過其他設定，就[mssql-conf 工具](sql-server-linux-configure-mssql-conf.md)。

2. 新增用來執行 SQL Server 服務 mssql 使用者帳戶。 如果您還沒有執行安裝程式之前，這是必要的。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

3. 啟用輸出網路存取。 預設會停用輸出網路存取。 若要啟用輸出要求，請設定"outboundnetworkaccess 」 使用 mssql-conf 工具的布林值屬性。 如需詳細資訊，請參閱 <<c0> [ 設定 SQL Server on Linux 使用 mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access)。

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. 重新啟動 SQL Server Launchpad 服務和資料庫引擎執行個體讀取 INI 檔案中的更新後的值。 重新啟動訊息會提醒您每次修改擴充性相關的設定。  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

5. 啟用外部指令碼執行使用 Azure Data Studio 或 SQL Server Management Studio (僅 Windows) 等其他工具執行 Transact SQL。

   ```bash
   EXEC sp_configure 'external scripts enabled', 1
   RECONFIGURE WITH OVERRIDE
   ```

6. 重新啟動`mssql-launchpadd`服務一次。

7. 針對您想要使用的語言擴充功能，在每個資料庫，您需要註冊的外部語言[建立外部語言](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql)。

## <a name="verify-installation"></a>確認安裝

Java 功能整合不包含程式庫，但您可以執行`grep -r JRE_HOME /etc`確認建立 JAVA_HOME 環境變數。

若要驗證安裝，請執行 T-SQL 指令碼會執行系統預存程序叫用 Java。 您必須針對這項工作的查詢工具。 Azure Data Studio 是不錯的選擇。 其他常用於工具，例如 SQL Server Management Studio 或 PowerShell 是僅限 Windows。 如果您有使用這些工具的 Windows 電腦，請使用它來連接到 database engine 的 Linux 安裝。

<a name="install-all"></a>

## <a name="full-install-of-sql-server-and-language-extensions"></a>SQL Server 和語言擴充功能的完整安裝

您可以安裝並在程序中設定 database engine 和語言擴充功能，藉由附加的 Java 套件和安裝 database engine 的命令的參數。

1. 提供命令列，其中包含資料庫引擎，再加上語言擴充功能。

  您可以新增到資料庫引擎的擴充性安裝的 Java。

  ```bash
  sudo yum install -y mssql-server mssql-server-extensibility-java 
  ```

3. 接受授權合約，並完成後續安裝組態。 使用**mssql conf**這項工作的工具。

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  將提示您接受授權合約，database engine、 選擇版本，並設定系統管理員密碼。 

4. 如果系統提示您這樣做，請重新啟動服務。

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>自動安裝

使用[自動的安裝](https://docs.microsoft.com/sql/linux/sql-server-linux-setup#unattended)資料庫引擎中，新增 mssql 伺服器擴充性-java 的套件。

<a name="offline-install"></a>


## <a name="offline-installation"></a>離線安裝

請遵循[離線安裝](sql-server-linux-setup.md#offline)安裝套件的步驟的指示。 尋找您的下載網站，然後下載 使用下列套件清單的特定套件。

> [!Tip]
> 數個封裝管理工具提供命令，可協助您判斷封裝相依性。 使用 yum， `sudo yum deplist [package]`。 對於 Ubuntu，使用`sudo apt-get install --reinstall --download-only [package name]`後面接著`dpkg -I [package name].deb`。

#### <a name="download-site"></a>下載網站

您可以從套件下載[ https://packages.microsoft.com/ ](https://packages.microsoft.com/)。 所有適用於 Java 的套件會與資料庫引擎套件共置。 

#### <a name="redhat7-paths"></a>RedHat/7 路徑

|||
|--|----|
| mssql/擴充性-java 套件 | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |

#### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 路徑

|||
|--|----|
| mssql/擴充性-java 套件 | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |

#### <a name="suse12-paths"></a>SUSE/12 路徑

|||
|--|----|
| mssql/擴充性-java 套件 | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |

#### <a name="package-list"></a>套件清單

根據哪些延伸模組，您想要使用、 下載所需的特定語言套件。 確切的檔名包含平台資訊的後置詞，但應該關閉，以判斷哪些檔案，以便取得下列檔案名稱。

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# Java
mssql-server-extensibility-java-15.0.1000
```

## <a name="limitations-in-ctp-releases"></a>在 CTP 版本中的限制

在 Linux 上的語言擴充功能和 Java 擴充性是仍在作用中的開發。 預覽版中尚未啟用下列功能。

+ 隱含的驗證目前不是在 Linux 上使用在這個階段，這表示您無法從進行中的 Java 存取資料或其他資源連接至伺服器。


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

Java 開發人員可以開始使用一些簡單的範例，並了解 Java 與 SQL Server 的運作方式的基本概念。 下一個步驟中，請參閱下列連結：

+ [教學課程：使用 Java 的規則運算式](../language-extensions/tutorials/search-for-string-using-regular-expressions-in-java.md)