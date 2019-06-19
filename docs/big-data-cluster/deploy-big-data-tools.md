---
title: 安裝巨量資料工具
titleSuffix: SQL Server big data clusters
description: 了解如何安裝 SQL Server 2019 巨量資料叢集 （預覽） 搭配使用的工具。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 01/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: cbb4860cd747e454a09f1374d3b166fae466ee33
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797919"
---
# <a name="install-sql-server-2019-big-data-tools"></a>安裝 SQL Server 2019 巨量資料工具

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

這篇文章說明應安裝於管理，來建立，用戶端工具，並使用 SQL Server 2019 巨量資料叢集 （預覽）。 下一節提供工具和安裝指示的連結的清單。 在部署巨量資料叢集之前，設定標示為需要在 Windows 或 Linux 的工具。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="big-data-cluster-tools"></a>巨量資料叢集工具

下表列出常見的巨量資料叢集工具和如何加以安裝：

| 工具 | 必要項 | 描述 | 安裝 |
|---|---|---|---|
| **mssqlctl** | 是 | 安裝和管理的巨量資料叢集的命令列工具。 | [安裝](deploy-install-mssqlctl.md) |
| **kubectl**<sup>1</sup> | 是 | 監視基礎 Kuberentes 叢集的命令列工具 ([進一歩](https://kubernetes.io/docs/tasks/tools/install-kubectl/))。 | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management) |
| **Azure Data Studio** | 是 | 查詢 SQL Server 的跨平台圖形化工具 ([進一歩](https://docs.microsoft.com/sql/azure-data-studio/what-is?view=sql-server-ver15))。 | [安裝](../azure-data-studio/download.md) |
| **SQL Server 2019 延伸模組** | 是 | 適用於支援連接至巨量資料叢集的 Azure 資料 Studio 的延伸模組。 也提供資料虛擬化精靈。 | [安裝](../azure-data-studio/sql-server-2019-extension.md) |
| **Azure CLI**<sup>2</sup> | 供 AKS 使用 | 現代的命令列介面來管理 Azure 服務。 搭配 AKS 巨量資料叢集部署 ([進一歩](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest))。 | [安裝](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | 選擇性 | 查詢 SQL Server 的新式命令列介面 ([進一歩](https://github.com/dbcli/mssql-cli/blob/master/README.rst))。 | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | 如需一些指令碼 | 查詢 SQL Server 的傳統命令列工具 ([進一歩](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15))。 | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| **curl** <sup>3</sup> | 如需一些指令碼 | 使用 Url 的資料傳輸的命令列工具。 | [Windows](https://curl.haxx.se/windows/) \| Linux： 安裝 curl 的套件 |

<sup>1</sup>您必須使用 kubectl 1.10 或更新版本的版本。 此外，kubectl 的版本應該是加號或減號的 Kubernetes 叢集中的一個次要版本。 如果您想要安裝 kubectl 用戶端上的特定版本，請參閱[安裝 kubectl 二進位透過 curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl) （Windows 10 上使用 cmd.exe，而非 Windows PowerShell 來執行 curl）。 

> [!TIP]
> 若要使用 kubectl 與先前部署的叢集在 Azure Kubernetes Service (AKS) 中，您必須設定叢集內容，使用下列 Azure CLI 命令：
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup>您必須使用 Azure CLI 2.0.4 版或更新版本。 執行`az --version`以尋找版本，如有需要。

<sup>3</sup>如果您在 Windows 10 上執行**curl**已在您的路徑時從命令提示字元執行。 對於其他版本的 Windows 中，下載**curl**使用連結，並將它放在您的路徑。

## <a name="which-tools-are-required"></a>需要哪些工具？

先前的表格會提供所有常用的工具與巨量資料叢集搭配使用。 必要的工具取決於您的案例。 但在一般情況下，下列工具是最重要的管理、 連線和查詢叢集：

- **mssqlctl**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 延伸模組**

在某些情況下只需要其餘的工具。 **Azure CLI**可用來管理與 AKS 部署相關聯的 Azure 服務。 **mssql cli**是選擇性的但很有用的工具，可讓您連接到 SQL Server 主要執行個體在叢集中，並從命令列執行查詢。 並**sqlcmd**並**curl**是必要的如果您打算使用 GitHub 的指令碼安裝範例資料。

## <a name="next-steps"></a>後續步驟

之後設定工具，將 SQL Server 2019 巨量資料叢集部署到雲端或內部部署環境中的 Kubernetes。 如需詳細資訊，請參閱下列的部署文件：

- [快速入門：部署 Azure Kubernetes Service (AKS) 上的 SQL Server 巨量資料叢集](quickstart-big-data-cluster-deploy.md)
- [如何部署 SQL Server 在 Kubernetes 上的巨量資料叢集](deployment-guidance.md)

如需巨量資料叢集的詳細資訊，請參閱[什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)。
