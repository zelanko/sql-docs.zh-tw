---
title: 安裝巨量資料工具
titleSuffix: SQL Server big data clusters
description: 瞭解如何安裝與 SQL Server 2019 big data 叢集 (預覽) 搭配使用的工具。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 757209ff89fd40dcc737b65d3b19f2a7d4ef247b
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419462"
---
# <a name="install-sql-server-2019-big-data-tools"></a>安裝 SQL Server 2019 big data 工具

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明應該安裝來建立、管理和使用 SQL Server 2019 big data 叢集 (預覽) 的用戶端工具。 下一節提供工具清單和安裝指示的連結。 在部署 big data 叢集之前, 請先設定在 Windows 或 Linux 上標示為必要的工具。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="big-data-cluster-tools"></a>Big data cluster 工具

下表列出常見的 big data 叢集工具和其安裝方式:

| 工具 | 必要項 | 描述 | 安裝 |
|---|---|---|---|
| **python** | 是 | Python 是一種以動態方式轉譯的物件導向、高階程式設計語言。 大型資料叢集的許多部分 SQL Server 使用 python。 | [安裝 python](#python)|
| **azdata** | 是 | 用於安裝和管理 big data cluster 的命令列工具。 | [安裝](deploy-install-azdata.md) |
| **kubectl**<sup>1</sup> | 是 | 用於監視基礎 Kuberentes 叢集的命令列工具 ([詳細資訊](https://kubernetes.io/docs/tasks/tools/install-kubectl/))。 | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management) |
| **Azure Data Studio (內部人員)** | 是 | 用於查詢 SQL Server 的跨平臺圖形化工具 ([詳細資訊](https://docs.microsoft.com/sql/azure-data-studio/what-is?view=sql-server-ver15))。 | [安裝](https://aka.ms/azdata-insiders) |
| **SQL Server 2019 延伸模組** | 是 | 支援連接到 big Data cluster 之 Azure Data Studio 的延伸模組。 也會提供資料虛擬化的 wizard。 | [安裝](../azure-data-studio/sql-server-2019-extension.md) |
| **Azure CLI**<sup>2</sup> | 針對 AKS | 用來管理 Azure 服務的新式命令列介面。 搭配 AKS big data cluster 部署使用 ([詳細資訊](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest))。 | [安裝](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | 選擇性 | 用於查詢 SQL Server 的新式命令列介面 ([詳細資訊](https://github.com/dbcli/mssql-cli/blob/master/README.rst))。 | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | 針對某些腳本 | 用於查詢 SQL Server 的舊版命令列工具 ([詳細資訊](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15))。 | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| **curl** <sup>3</sup> | 針對某些腳本 | 使用 Url 傳送資料的命令列工具。 | [Windows](https://curl.haxx.se/windows/)\| Linux: 安裝捲曲套件 |

<sup>1</sup>您必須使用 kubectl 1.10 版或更新版本。 此外, kubectl 的版本應該是或減去 Kubernetes 叢集的一個次要版本。 如果您想要在 kubectl 用戶端上安裝特定版本, 請參閱透過[捲曲安裝 kubectl 二進位](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl)檔 (在 Windows 10 上, 請使用 cmd.exe, 而不是 windows PowerShell 執行捲曲)。 

> [!TIP]
> 若要在 Azure Kubernetes Service (AKS) 上搭配先前部署的叢集使用 kubectl, 您必須使用下列 Azure CLI 命令來設定叢集內容:
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup>您必須使用 Azure CLI 版2.0.4 版或更新版本。 視`az --version`需要執行以尋找版本。

<sup>3</sup>如果您是在 Windows 10 上執行, 從命令提示字元執行時,**捲曲**就已經在您的路徑中。 若是其他版本的 Windows, 請使用連結來下載, 並將它放在您的路徑中。

## <a name="which-tools-are-required"></a>需要哪些工具？

上表提供與 big data 叢集搭配使用的所有常用工具。 需要哪些工具取決於您的案例。 但一般而言, 下列工具對於管理、連接及查詢叢集而言最為重要:

- **azdata**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 延伸模組**

只有在某些情況下才需要其餘的工具。 **Azure CLI**可以用來管理與 AKS 部署相關聯的 Azure 服務。 **mssql-cli**是一個選擇性但實用的工具, 可讓您連接到叢集中 SQL Server 的主要實例, 並從命令列執行查詢。 如果您打算使用 GitHub 腳本安裝範例資料, 則需要和**sqlcmd**和**捲曲**。

### <a id="python"></a>離線安裝 python

1. 在具有網際網路存取的電腦上, 下載下列其中一個包含 Python 的壓縮檔案:

   | 作業系統 | 下載 |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. 將壓縮檔案複製到目的電腦, 並將它解壓縮至您選擇的資料夾。

1. 僅適用于 Windows, `installLocalPythonPackages.bat`從該資料夾執行, 並將完整路徑傳遞至與參數相同的資料夾。

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

## <a name="next-steps"></a>後續步驟

設定工具之後, 請將 SQL Server 2019 big data 叢集部署到雲端或內部部署中的 Kubernetes。 如需詳細資訊, 請參閱下列部署文章:

- [入門Azure Kubernetes Service 上部署 SQL Server big data 叢集 (AKS)](quickstart-big-data-cluster-deploy.md)
- [如何在 Kubernetes 上部署 SQL Server big data 叢集](deployment-guidance.md)

如需 big data 叢集的詳細資訊, 請參閱[什麼是 SQL Server 2019 big data 叢集？](big-data-cluster-overview.md)。
