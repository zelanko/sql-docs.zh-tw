---
title: 安裝巨量資料工具
titleSuffix: SQL Server big data clusters
description: 了解如何安裝搭配 SQL Server 2019 巨量資料叢集來使用的工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d0c4f21d6fcf8f90026164dded1007de4e34164
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88765837"
---
# <a name="install-sql-server-2019-big-data-tools"></a>安裝 SQL Server 2019 巨量資料工具

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本文描述您應該安裝來建立、管理和使用 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 的用戶端工具。 下列小節提供工具和安裝指示連結的清單。 在部署巨量資料叢集之前，請先設定標示為在 Windows 或 Linux 上是必要的工具。

## <a name="big-data-cluster-tools"></a>巨量資料叢集工具

下表列出常見的巨量資料叢集工具和其安裝方式：

| 工具 | 必要 | 描述 | 安裝 |
|---|---|---|---|
| `python` | 是 | Python 是具有動態語意的直譯物件導向高階程式設計語言。 SQL Server 巨量資料叢集的許多部分都使用 python。 | [安裝 python](#python)|
| `azdata` | 是 | 用於安裝和管理巨量資料叢集的命令列工具。 | [安裝](deploy-install-azdata.md) |
| `kubectl`<sup>1</sup> | 是 | 用於監視基礎 Kuberentes 叢集的命令列工具 ([詳細資訊](https://kubernetes.io/docs/tasks/tools/install-kubectl/))。 | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \(英文\) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-using-native-package-management) \(英文\) |
| **Azure Data Studio** | 是 | 用於查詢 SQL Server 的跨平台圖形化工具。 | [安裝](https://aka.ms/getazuredatastudio) |
| **資料虛擬化延伸模組** | 是 | 提供 [資料虛擬化精靈] 之 Azure Data Studio 的延伸模組。 | [安裝](../azure-data-studio/data-virtualization-extension.md) |
| **Azure CLI**<sup>2</sup> | 對於 AKS | 用於管理 Azure 服務的新式命令列介面。 與 AKS 巨量資料叢集部署搭配使用 ([詳細資訊](/cli/azure/?view=azure-cli-latest))。 | [安裝](/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | 選用 | 用於查詢 SQL Server 的新式命令列介面 ([詳細資訊](../tools/mssql-cli.md) \(英文\))。 | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \(英文\) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) \(英文\) |
| **sqlcmd** | 對於某些指令碼 | 用於查詢 SQL Server 的舊版命令列工具 ([詳細資訊](../tools/sqlcmd-utility.md?view=sql-server-ver15) \(部分機器翻譯\))。 您可能需要先安裝 Microsoft ODBC Driver 11 for SQL Server，才能安裝 SQLCMD 套件。 | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \(英文\) \| [Linux](../linux/sql-server-linux-setup-tools.md) \(英文\) |
| `curl` <sup>3</sup> | 對於某些指令碼 | 使用 URL 傳送資料的命令列工具。 | [Windows](https://curl.haxx.se/windows/) \(英文\) \| Linux：安裝 curl 套件 |
| `oc` | 必須具備才能進行 Red Hat OpenShift 和 Azure Redhat OpenShift 部署。 |`oc` 是 Open Shift 命令列介面 (CLI)。 | [Installing the CLI](https://docs.openshift.com/container-platform/4.4/cli_reference/openshift_cli/getting-started-cli.html#installing-the-cli) (安裝 CLI)

<sup>1</sup> 您必須使用 `kubectl` 1.13 版或更新版本。 此外，`kubectl` 的版本應該是 Kubernetes 叢集的次要版本加上或減去一。 如果您想要在 `kubectl` 用戶端上安裝特定版本，請參閱[透過 curl 安裝 `kubectl` 二進位檔](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl) (在 Windows 10 上，請使用 cmd.exe 執行 curl，而不是使用 Windows PowerShell)。

> [!TIP]
> 若要搭配使用 `kubectl` 和先前部署在 Azure Kubernetes Service (AKS) 上的叢集，您必須使用下列 Azure CLI 命令來設定叢集內容：
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> 您必須使用 Azure CLI 2.0.4 版或更新版本。 如果需要，請執行 `az --version` 來尋找版本。

<sup>3</sup> 如果您是在 Windows 10 上執行，則當從命令提示字元執行時，`curl` 就已經在您的 PATH 中。 針對其他版本的 Windows，請使用連結來下載 `curl`，並將其放在您的 PATH 中。

## <a name="which-tools-are-required"></a>需要哪些工具？

上表提供與巨量資料叢集搭配使用的所有常用工具。 需要哪些工具取決於您的案例。 但一般而言，下列工具對於管理、連線及查詢叢集最為重要：

- `azdata`
- `kubectl`
- **Azure Data Studio**
- **資料虛擬化延伸模組**

其餘工具只有在某些情況下才需要。 **Azure CLI** 可以用來管理與 AKS 部署相關聯的 Azure 服務。 **mssql-cli** 是選擇性但實用的工具，可讓您連線到叢集中的 SQL Server 主要執行個體，並從命令列執行查詢。 如果您打算使用 GitHub 指令碼來安裝範例資料，則需要 **sqlcmd** 和 `curl`。

### <a name="install-python-offline"></a><a id="python"></a> 離線安裝 python

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

## <a name="download-and-install-azure-data-studio"></a>下載並安裝 Azure Data Studio

Azure Data Studio 提供專門用於 SQL Server 巨量資料叢集的功能。

[取得最新版 Azure Data Studio](https://aka.ms/getazuredatastudio)。

如需最新版本的詳細資訊，請參閱[版本資訊](./release-notes-big-data-cluster.md)。

## <a name="next-steps"></a>後續步驟

設定工具之後，將 SQL Server 2019 巨量資料叢集部署到在雲端或內部部署的 Kubernetes。 如需詳細資訊，請參閱下列部署文章：

- [快速入門：在 Azure Kubernetes Service (AKS) 上部署 SQL Server 巨量資料叢集](quickstart-big-data-cluster-deploy.md)
- [如何在 Kubernetes 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-guidance.md)

如需巨量資料叢集的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)