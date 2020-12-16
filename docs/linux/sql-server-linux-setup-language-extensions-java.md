---
title: 在 Linux 上安裝 Java 語言延伸模組
titleSuffix: SQL Server Language Extensions
description: 了解如何在 Red Hat、Ubuntu 和 SUSE Linux 上安裝 SQL Server Java 語言延伸模組。
author: dphansen
ms.author: davidph
manager: cgronlun
ms.date: 11/12/2020
ms.topic: how-to
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: 1036f81b62134b2301bb2d800e9481bd06dcdcee
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471459"
---
# <a name="install-sql-server-java-language-extension-on-linux"></a>在 Linux 上安裝 SQL Server Java 語言延伸模組

[!INCLUDE [SQL Server 2019 - Linux](../includes/applies-to-version/sqlserver2019-linux.md)]

了解如何在 Linux 上安裝適用於 SQL Server 的 [Java 語言延伸模組](../language-extensions/java-overview.md)元件。 Java 語言延伸模組從屬於 [SQL Server 語言延伸模組](../language-extensions/language-extensions-overview.md)，是資料庫引擎的附加元件。 

雖然您可以[同時安裝資料庫引擎和語言擴充功能](#install-all)，但最佳做法是先安裝和設定 SQL Server 資料庫引擎，以便在新增更多元件之前解決任何問題。

## <a name="prerequisites"></a>Prerequisites

+ Linux 版本必須[受 SQL Server 支援](sql-server-linux-release-notes-2019.md#supported-platforms)，但不包含 Docker 引擎。 支援的版本包含：

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)
   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)
   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ 您應該有執行 T-SQL 命令的工具。 必須使用查詢編輯器進行安裝後設定和驗證。 我們推薦 [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md?view=sql-server-2017&preserve-view=true#get-azure-data-studio-for-linux) \(部分機器翻譯\)，這是在 Linux 上執行的免費下載。

+ Java 擴充功能的套件位置在 SQL Server Linux 來源存放庫中。 如果您已經為資料庫引擎安裝設定來源存放庫，您可以使用相同的存放庫登錄來執行 **mssql-server-extensibility-java** 套件安裝命令。

+ Linux 容器上也支援語言擴充功能。 我們沒有提供含語言擴充功能的預先建立容器，但您可以使用 [GitHub 上提供的範例範本](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices) \(英文\)，從 SQL Server 容器建立一個。

+ 根據預設，系統會在 SQL Server 巨量資料叢集上安裝語言延伸模組與[機器學習服務](../machine-learning/index.yml)。 如果您使用的是巨量資料叢集，就不需要依照此文章中的步驟進行。 如需詳細資訊，請參閱[在巨量資料叢集上使用機器學習服務 (Python 和 R)](../big-data-cluster/machine-learning-services.md)。

## <a name="package-list"></a>套件清單

在連線到網際網路的裝置上，系統會使用每個作業系統的套件安裝程式，獨立地下載及安裝套件。 下表描述所有可用套件。

| 套件名稱 | 適用於 | 描述 |
|--------------|----------|-------------|
|mssql-server-extensibility  | 所有語言 | 用於 Java 語言擴充的 Extensibility Framework |
|mssql-server-extensibility-java | Java | 用於 Java 語言擴充且包含支援之 Java 執行階段的 Extensibility Framework |

<a name="RHEL"></a>

## <a name="install-java-language-extension"></a>安裝 Java 語言延伸模組

您可以藉由安裝 **mssql-server-extensibility-java**，在 Linux 上安裝語言擴充功能和 Java。 當您安裝 **mssql-server-extensibility-java** 時，套件會自動安裝 JRE 11 (如果尚未安裝)。 它也會將 JVM 路徑新增至名為 JRE_HOME 的環境變數。

> [!Note]
> 在連線到網際網路的伺服器上，套件相依性會作為主要套件安裝的一部分下載並安裝。 如果您的伺服器未連線到網際網路，請參閱[離線安裝程式](#offline-install)中的更多詳細資料。

### <a name="redhat-install-command"></a>RedHat 安裝命令

您可以使用下列命令，在 RedHat 上安裝適用於 Java 的語言擴充功能。

> [!Tip]
> 可能的話，請在安裝之前執行 `yum clean all`，以重新整理系統上的套件。

```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

### <a name="ubuntu-install-command"></a>Ubuntu 安裝命令

您可以使用下列命令，在 Ubuntu 上安裝適用於 Java 的語言擴充功能。

> [!Tip]
> 可能的話，請在安裝之前執行 `apt-get update`，以重新整理系統上的套件。 此外，某些 Ubuntu 的 Docker 映像可能沒有 HTTPS apt 傳輸選項。 若要安裝它，請使用 `apt-get install apt-transport-https`。

```bash
# Install as root or sudo
sudo apt-get install mssql-server-extensibility-java
```

<a name="suse"></a>

### <a name="suse-install-command"></a>SUSE 安裝命令

您可以使用下列命令，在 SUSE 上安裝適用於 Java 的語言擴充功能。

```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>安裝後設定 (必要)

1. 在 Linux 上授與權限

    如果您使用的是外部程式庫，則不需要執行此步驟。 建議的運作方式是使用外部程式庫。 如需從您 Jar 檔案建立外部程式庫的說明，請參閱 [CREATE EXTERNAL LIBRARY](../t-sql/statements/create-external-library-transact-sql.md)

    如果您不是使用外部程式庫，則必須提供 SQL Server 在您 Jar 中執行 Java 類別的權限。

    若要授與讀取和執行 Jar 檔案的權限，請在 Jar 檔案上執行下列 **chmod** 命令。 當您使用 SQL Server 時，建議您一律將類別檔案放在 Jar 中。 如需建立 Jar 的說明，請參閱[如何建立 Jar 檔案](../language-extensions/how-to/create-a-java-jar-file-from-class-files.md) \(英文\)。

    ```cmd
    chmod ug+rx <MyJarFile.jar>
    ```

    您也需要提供 Jar 檔案 mssql_satellite 權限以讀取/執行。

    ```cmd
    chown mssql_satellite:mssql_satellite <MyJarFile.jar>
    ```

    其他設定主要是透過 [mssql-conf 工具](sql-server-linux-configure-mssql-conf.md)來設定。

2. 新增用來執行 SQL Server 服務的 mssql 使用者帳戶。 如果您先前未執行安裝程式，則這是必要的。

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

3. 啟用輸出網路存取。 預設會停用輸出網路存取。 若要啟用輸出要求，請使用 mssql-conf 工具來設定 "outboundnetworkaccess" 布林值屬性。 如需詳細資訊，請參閱[使用 mssql-conf 在 Linux 上設定 SQL Server](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access)。

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. 重新啟動 SQL Server Launchpad 服務和資料庫引擎執行個體，以從 INI 檔案讀取更新後的值。 每當修改擴充性相關設定時，系統會顯示重新啟動訊息提醒您。  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

5. 使用 Azure Data Studio 或 SQL Server Management Studio (僅限 Windows) 等執行 Transact-SQL 的另一種工具，來啟用外部指令碼執行。

   ```bash
   EXEC sp_configure 'external scripts enabled', 1
   RECONFIGURE WITH OVERRIDE
   ```

6. 重新啟動 `mssql-launchpadd` 服務。

7. 針對您要在其中使用語言擴充功能的每個資料庫，您必須使用 [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md) 來註冊外部語言。

## <a name="register-external-language"></a>註冊外部語言

針對您要在其中使用語言擴充功能的每個資料庫，您必須使用 [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md) 來註冊外部語言。

下例範例會將稱為 Java 的外部語言新增至 Linux 上的 SQL Server 資料庫。

```SQL
CREATE EXTERNAL LANGUAGE Java
FROM (CONTENT = N'/opt/mssql-extensibility/lib/java-lang-extension.tar.gz', 
    FILE_NAME = 'javaextension.so', 
    ENVIRONMENT_VARIABLES = N'{"JRE_HOME":"/opt/mssql/lib/zulu-jre-11"}')
```
對 JAVA 延伸模組而言，環境變數 “JRE_HOME” 是用來決定尋找並初始化 JVM 的路徑。

CREATE EXTERNAL LANGUAGE DDL 會提供一個參數 (ENVIRONMENT_VARIABLES)，以特別為裝載延伸模組的程序設定環境變數。 這是設定外部語言延伸模組所需環境變數的建議方式，也是最有效的方式。

如需詳細資訊，請參閱 [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md)。

## <a name="verify-installation"></a>確認安裝

Java 功能整合不包含程式庫，但您可以執行 `grep -r JRE_HOME /etc` 來確認 JAVA_HOME 環境變數的建立。

若要驗證安裝，請執行 T-SQL 指令碼，以執行叫用 Java 的系統預存程序。 您將需要此工作的查詢工具。 Azure Data Studio 是不錯的選擇。 其他常用的工具，例如，SQL Server Management Studio 或 PowerShell，則只適用於 Windows。 如果您有包含這些工具的 Windows 電腦，請使用它來連線到您的 Linux 安裝資料庫引擎。

<a name="install-all"></a>

## <a name="full-install-of-sql-server-and-java-language-extension"></a>SQL Server 和 Java 語言延伸模組的完整安裝

只要在安裝資料庫引擎的命令中附加 Java 套件和參數，就可以在一個程序中安裝及設定資料庫引擎和 Java 語言延伸模組。

1. 提供包含資料庫引擎以及語言擴充功能的命令列。

    您可以在資料庫引擎安裝中加入 Java 擴充性。

    ```bash
    sudo yum install -y mssql-server mssql-server-extensibility-java 
    ```

1. 接受授權合約，並完成安裝後設定。 使用 **mssql-conf** 工具來執行此工作。

    ```bash
    sudo /opt/mssql/bin/mssql-conf setup
    ```

    系統會提示您接受資料庫引擎授權合約、選擇版本，以及設定系統管理員密碼。 

1. 如果系統提示，請重新啟動服務。

    ```bash
    sudo systemctl restart mssql-server.service
    ```

## <a name="unattended-installation"></a>自動安裝

使用資料庫引擎的 [自動安裝](./sql-server-linux-setup.md#unattended)，並新增 **mssql-server-extensibility-java** 的套件。

<a name="offline-install"></a>

## <a name="offline-installation"></a>離線安裝

遵循[離線安裝](sql-server-linux-setup.md#offline)指示，以取得安裝套件的步驟。 尋找您的下載網站，然後使用以下套件清單下載特定套件。

> [!Tip]
> 數個套件管理工具都提供協助您判斷套件相依性的命令。 若是 yum，請使用 `sudo yum deplist [package]`。 若是 Ubuntu，請使用 `sudo apt-get install --reinstall --download-only [package name]`，後面接著 `dpkg -I [package name].deb`。

#### <a name="download-site"></a>下載網站

您可在 [https://packages.microsoft.com/](https://packages.microsoft.com/) 下載套件。 所有的 Java 套件都與資料庫引擎套件搭配使用。

#### <a name="redhat7-paths"></a>RedHat/7 路徑

|Package|下載位置|
|--|----|
| mssql/extensibility-java packages | [https://packages.microsoft.com/rhel/7/mssql-server-2019/](https://packages.microsoft.com/rhel/7/mssql-server-2019/) |

#### <a name="ubuntu1604-paths"></a>Ubuntu/16.04 路徑

|Package|下載位置|
|--|----|
| mssql/extensibility-java packages | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/) |

#### <a name="suse12-paths"></a>SUSE/12 路徑

|Package|下載位置|
|--|----|
| mssql/extensibility-java packages | [https://packages.microsoft.com/sles/12/mssql-server-2019/](https://packages.microsoft.com/sles/12/mssql-server-2019/) |

#### <a name="package-list"></a>套件清單
取決於您想要使用的擴充功能，下載適用於特定語言的必要套件。 確切的檔案名稱會在尾碼中包含平台資訊，但下面的檔案名稱應該足以讓您判斷要取得的檔案。

```
# Core packages
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# Java
mssql-server-extensibility-java-15.0.1000
```

## <a name="limitations"></a>限制

目前在 Linux 上無法使用隱含驗證，這表示您無法從進行中的 Java 連線回到伺服器，以存取資料或其他資源。

### <a name="resource-governance"></a>資源管理

針對外部資源集區的[資源管理](../t-sql/statements/create-external-resource-pool-transact-sql.md)，Linux 與 Windows 之間有同位，但 [sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) 的統計資料在 Linux 上目前有不同單位。

| 資料行名稱   | 描述 | Linux 上的值 |
|---------------|--------------|---------------|
|peak_memory_kb | 用於資源集區的記憶體數量上限。 | 在 Linux 上，此統計資料是來自 CGroups 記憶體子系統，其中的值為 memory.max_usage_in_bytes |
|write_io_count | 重設 Resource Governor 統計資料之後發出的寫入 IO 總數。 | 在 Linux 上，此統計資料來自 CGroups blkio 子系統，其中寫入資料列上的值為 blkio.throttle.io_serviced |
|read_io_count | 重設 Resource Governor 統計資料之後發出的讀取 IO 總數。 | 在 Linux 上，此統計資料來自 CGroups blkio 子系統，其中讀取資料列上的值為 blkio.throttle.io_serviced |
|total_cpu_kernel_ms | 重設 Resource Governor 統計資料之後的累計 CPU 使用者核心時間 (以毫秒為單位)。 | 在 Linux 上，此統計資料來自 CGroups cpuacct 子系統，其中使用者資料列上的值為 cpuacct.stat |  
|total_cpu_user_ms | 重設 Resource Governor 統計資料之後的累計 CPU 使用者時間 (以毫秒為單位)。| 在 Linux 上，此統計資料來自 CGroups cpuacct 子系統，其中系統資料列值上的值為 cpuacct.stat |
|active_processes_count | 在要求當時正在執行的外部處理序數目。| 在 Linux 上，此統計資料是來自 CGroups pids 子系統，其值為 pids.current |

## <a name="next-steps"></a>後續步驟

Java 開發人員可以從一些簡單的範例開始，並了解 Java 如何搭配 SQL Server 使用的基本概念。 如需下一個步驟，請參閱下列連結：

+ [教學課程：使用 Java 的規則運算式](../language-extensions/tutorials/search-for-string-using-regular-expressions-in-java.md)