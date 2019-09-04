---
title: 安裝巨量資料工具
titleSuffix: SQL Server big data clusters
description: 瞭解如何安裝搭配 (預覽) [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]使用的工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: afd036dfe33ab538d3d845e73f45e804052a9903
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2019
ms.locfileid: "70238696"
---
# <a name="install-sql-server-2019-big-data-tools"></a>安裝 SQL Server 2019 巨量資料工具

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明應該安裝來建立、管理和使用[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (預覽) 的用戶端工具。 下列小節提供工具和安裝指示連結的清單。 在部署巨量資料叢集之前，請先設定標示為在 Windows 或 Linux 上是必要的工具。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="big-data-cluster-tools"></a>巨量資料叢集工具

下表列出常見的巨量資料叢集工具和其安裝方式：

| 工具 | 必要項 | 描述 | 安裝 |
|---|---|---|---|
| **python** | 是 | Python 是具有動態語意的直譯物件導向高階程式設計語言。 SQL Server 巨量資料叢集的許多部分都使用 python。 | [安裝 python](#python)|
| **azdata** | 是 | 用於安裝和管理巨量資料叢集的命令列工具。 | [安裝](deploy-install-azdata.md) |
| **kubectl**<sup>1</sup> | 是 | 用於監視基礎 Kuberentes 叢集的命令列工具 ([詳細資訊](https://kubernetes.io/docs/tasks/tools/install-kubectl/) \(英文\))。 | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management) |
| **Azure Data Studio-SQL Server 2019 候選版 (RC)** | 是 | 用於查詢 SQL Server 的跨平臺圖形化工具。 | [安裝](#download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc) |
| **SQL Server 2019 擴充功能** | 是 | 支援連線至巨量資料叢集的 Azure Data Studio 擴充功能。 也提供資料虛擬化精靈。 | [安裝](../azure-data-studio/sql-server-2019-extension.md) |
| **Azure CLI**<sup>2</sup> | 對於 AKS | 用於管理 Azure 服務的新式命令列介面。 與 AKS 巨量資料叢集部署搭配使用 ([詳細資訊](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest))。 | [安裝](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | 選擇性 | 用於查詢 SQL Server 的新式命令列介面 ([詳細資訊](https://github.com/dbcli/mssql-cli/blob/master/README.rst) \(英文\))。 | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | 對於某些指令碼 | 用於查詢 SQL Server 的舊版命令列工具 ([詳細資訊](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15) \(部分機器翻譯\))。 | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| **curl** <sup>3</sup> | 對於某些指令碼 | 使用 URL 傳送資料的命令列工具。 | [Windows](https://curl.haxx.se/windows/) \(英文\) \| Linux：安裝 curl 套件 |

<sup>1</sup>您必須使用 kubectl 1.13 版或更新版本。 此外，kubectl 的版本應該是您 Kubernetes 叢集的次要版本加上或減去一。 如果您想要在 kubectl 用戶端上安裝特定版本，請參閱[透過 curl 安裝 kubectl 二進位檔](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl) (在 Windows 10 上，請使用 cmd.exe 執行 curl，而不是使用 Windows PowerShell)。

> [!TIP]
> 若要搭配使用 kubectl 和先前部署在 Azure Kubernetes Service (AKS) 上的叢集，您必須使用下列 Azure CLI 命令來設定叢集內容：
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> 您必須使用 Azure CLI 2.0.4 版或更新版本。 如果需要，請執行 `az --version` 來尋找版本。

<sup>3</sup> 如果您是在 Windows 10 上執行，則當您從命令提示字元執行時，**curl** 就已經在您的 PATH 中。 針對其他版本的 Windows，請使用連結來下載 **curl**，並將它放在您的 PATH 中。

## <a name="which-tools-are-required"></a>需要哪些工具？

上表提供與巨量資料叢集搭配使用的所有常用工具。 需要哪些工具取決於您的案例。 但一般而言，下列工具對於管理、連線及查詢叢集最為重要：

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 擴充功能**

其餘工具只有在某些情況下才需要。 **Azure CLI** 可以用來管理與 AKS 部署相關聯的 Azure 服務。 **mssql-cli** 是選擇性但實用的工具，可讓您連線到叢集中的 SQL Server 主要執行個體，並從命令列執行查詢。 如果您打算使用 GitHub 指令碼安裝範例資料，則需要和 **sqlcmd** 和 **curl**。

### <a id="python"></a> 離線安裝 python

1. 在能存取網際網路的電腦上，下載下列其中一個包含 Python 的壓縮檔案：

   | 作業系統 | 下載 |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. 將壓縮檔案複製到目標機器，並將其解壓縮至您選擇的資料夾。

1. (僅適用於 Windows) 在該資料夾中執行 `installLocalPythonPackages.bat`，並將相同資料夾的完整路徑傳遞為參數。

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

## <a name="download-and-install-azure-data-studio-sql-server-2019-release-candidate-rc"></a>下載並安裝 Azure Data Studio SQL Server 2019 候選版 (RC)

Azure Data Studio SQL Server 2019 RC 提供特別針對 SQL Server 2019 RC 的功能和功能。

如需 Azure Data Studio 的一般生產版本, 請遵循[下載並安裝 Azure Data Studio](../azure-data-studio/download.md)中的指示。

|平台|下載|發行日期| 版本 |
|:---|:---|:---|:---|
|Windows|[使用者安裝程式 (建議)](https://go.microsoft.com/fwlink/?linkid=2102435)<br>[系統安裝程式](https://go.microsoft.com/fwlink/?linkid=2102523)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2102524)|2019年8月27日 |RC 1.11.0-內部人員|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2102436)|2019年8月27日 |RC 1.11.0-內部人員|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2102526)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2102437)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2102525)|2019年8月27日 |RC 1.11.0-內部人員|

如需最新版本的詳細資訊，請參閱[版本資訊](../big-data-cluster/release-notes-big-data-cluster.md)。

### <a name="get-azure-data-studio-for-windows"></a>取得適用於 Windows 的 Azure Data Studio

此版本的 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 包含標準的 Windows 安裝程式體驗，以及 .zip 檔案。

建議使用「使用者安裝程式」，因為不需要系統管理員權限，從而簡化安裝和升級。 使用者安裝程式位於使用者的 Local AppData (LOCALAPPDATA) 資料夾底下，因此不需要系統管理員權限。 使用者安裝程式也提供更流暢的背景更新體驗。 如需詳細資訊，請參閱 [User setup for Windows](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows) (適用於 Windows 的使用者安裝程式)。

**使用者安裝程式** (建議)

1. 下載並執行[適用於Windows 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)]「使用者」安裝程式](https://go.microsoft.com/fwlink/?linkid=2102435)。
2. 啟動 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 應用程式。

**系統安裝程式**

1. 下載並執行[適用於Windows 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)]「系統」安裝程式](https://go.microsoft.com/fwlink/?linkid=2102523)。
2. 啟動 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 應用程式。

**壓縮檔**

1. 下載[適用於 Windows 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)] .zip](https://go.microsoft.com/fwlink/?linkid=2102524)。
2. 瀏覽至下載的檔案並解壓縮。
3. 執行 `\azuredatastudio-windows\azuredatastudio.exe`

### <a name="get-azure-data-studio-for-macos"></a>取得適用於 macOS 的 Azure Data Studio

1. 下載[適用於 macOS 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)]](https://go.microsoft.com/fwlink/?linkid=2102436)。
2. 若要展開壓縮檔的內容，請按兩下檔案。
3. 若要在「啟動控制板」中提供 [!INCLUDE[name-sos](../includes/name-sos-short.md)]，請將 *Azure Data Studio.app* 拖曳至 [應用程式] 資料夾。

### <a name="get-azure-data-studio-for-linux"></a>取得適用於 Linux 的 Azure Data Studio

1. 使用其中一種安裝程式或 tar.gz 封存，下載適用於 Linux 的 [!INCLUDE[name-sos](../includes/name-sos-short.md)]：
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2102526)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2102437)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2102525)
1. 若要將檔案解壓縮並啟動 [!INCLUDE[name-sos](../includes/name-sos-short.md)]，請開啟新的終端視窗並鍵入下列命令：

   **Debian 安裝：**
   ```bash
   cd ~
   sudo dpkg -i ./Downloads/azuredatastudio-linux-<version string>.deb

   azuredatastudio
   ```

   **rpm 安裝：**
   ```bash
   cd ~
   yum install ./Downloads/azuredatastudio-linux-<version string>.rpm

   azuredatastudio
   ```

   **tar.gz 安裝：**
   ```bash 
   cd ~ 
   cp ~/Downloads/azuredatastudio-linux-<version string>.tar.gz ~ 
   tar -xvf ~/azuredatastudio-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/azuredatastudio-linux-x64"' >> ~/.bashrc
   source ~/.bashrc 
   azuredatastudio 
   ``` 

   > [!NOTE]
   > 在 Debian、Redhat 和 Ubuntu 上，您可能遺失相依性。 使用下列命令，根據您的 Linux 版本安裝這些相依性：
   

   **Debian：** 
   ```bash
   sudo apt-get install libunwind8
   ```

   **Redhat:** 
   ```bash
   yum install libXScrnSaver
   ```

   **Ubuntu:** 
   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```

### <a name="supported-operating-systems"></a>支援的作業系統

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 在 Windows、macOS 和 Linux 上執行，並支援下列平台：

#### <a name="windows"></a>視窗

- Windows 10 (64 位元)
- Windows 8.1 (64 位元)
- Windows 8 (64 位元)
- Windows 7 (SP1) (64 位元) - 需要 [KB2533623](https://www.microsoft.com/download/details.aspx?id=26767)
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2 (64 位元)
- Windows Server 2012 (64 位元)
- Windows Server 2008 R2 (64 位元)

#### <a name="macos"></a>macOS

- macOS 10.13 High Sierra
- macOS 10.12 Sierra

#### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="next-steps"></a>後續步驟

設定工具之後，將 SQL Server 2019 巨量資料叢集部署到在雲端或內部部署的 Kubernetes。 如需詳細資訊，請參閱下列部署文章：

- [快速入門：在 Azure Kubernetes Service (AKS) 上部署 SQL Server 巨量資料叢集](quickstart-big-data-cluster-deploy.md)
- [如何在 Kubernetes [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]上部署](deployment-guidance.md)

如需有關 big data 叢集的詳細資訊, 請參閱[ [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]什麼是？](big-data-cluster-overview.md)。
