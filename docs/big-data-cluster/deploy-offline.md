---
title: 離線部署
titleSuffix: SQL Server big data clusters
description: 了解如何執行離線部署的 SQL Server 的巨量資料叢集。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1300c375903eb8692b8da6dce4e74a41e91d80c0
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728928"
---
# <a name="perform-an-offline-deployment-of-a-sql-server-big-data-cluster"></a>執行離線部署的 SQL Server 的巨量資料叢集

本文說明如何執行離線部署的 SQL Server 2019 巨量資料叢集 （預覽）。 巨量資料叢集必須能夠存取 Docker 存放庫從中提取容器映像。 離線安裝是所需的影像到私人 Docker 存放庫的放置位置。 該私人存放庫，然後做映像來源新部署。

## <a name="prerequisites"></a>必要條件

- 在任何支援的 Linux 發行版本或適用於 Mac/Windows 上的 Docker 安裝 Docker 引擎 1.8 以上版本。 如需詳細資訊，請參閱[安裝 Docker](https://docs.docker.com/engine/installation/)。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="load-images-into-a-private-repository"></a>載入私人存放庫中的映像

下列步驟說明如何從 Microsoft 存放庫提取容器映像巨量資料叢集，然後將其推送至您的私人存放庫。

> [!TIP]
> 下列步驟說明此程序。 不過，若要簡化這項工作，您可以使用[自動化的指令碼](#automated)而不是手動執行這些命令。

1. 首先，登入至 Microsoft Docker 登錄**docker 登入**命令。 使用使用者名稱和密碼提供給您做為早期的採用方案的一部分，Microsoft 的資訊。

   ```PowerShell
   docker login private-repo.microsoft.com -u  <SOURCE_DOCKER_USERNAME> -p <SOURCE_DOCKER_PASSWORD>
   ```

   > [!TIP]
   > 這些命令會使用 PowerShell 為例，但您可以從 cmd、 bash 或任何可以執行 docker 的命令殼層中執行它們。 在 Linux 上，新增`sudo`給每個命令。

1. 提取的巨量資料叢集容器映像重複下列命令。 取代`<SOURCE_IMAGE_NAME>`與每個[映像名稱](#images)。 取代`<SOURCE_DOCKER_TAG>`巨量資料的標記與叢集版本中，這類**ctp3.1**。  

   ```PowerShell
   docker pull private-repo.microsoft.com/mssql-private-preview/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG>
   ```

1. 登入目標私用 Docker 登錄。

   ```PowerShell
   docker login <TARGET_DOCKER_REGISTRY> -u <TARGET_DOCKER_USERNAME> -p <TARGET_DOCKER_PASSWORD>
   ```

1. 標記本機映像，使用下列命令，每個映像：

   ```PowerShell
   docker tag private-repo.microsoft.com/mssql-private-preview/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG> <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

1. 將本機映像推送至私人 Docker 存放庫中：

   ```PowerShell
   docker push <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

### <a id="images"></a> 巨量資料叢集容器映像

下列的巨量資料叢集容器映像所需的離線安裝：

 - **mssql-appdeploy-init**
 - **mssql-monitor-fluentbit**
 - **mssql-monitor-collectd**
 - **mssql-server-data**
 - **mssql-hadoop**
 - **mssql-java**
 - **mssql-mlservices-pythonserver**
 - **mssql-mlservices-rserver**
 - **mssql-monitor-elasticsearch**
 - **mssql-monitor-influxdb**
 - **mssql-security-knox**
 - **mssql-mlserver-r-runtime**
 - **mssql-mlserver-py-runtime**
 - **mssql-controller**
 - **mssql-server-controller**
 - **mssql-monitor-grafana**
 - **mssql-monitor-kibana**
 - **mssql-service-proxy**
 - **mssql-app-service-proxy**
 - **mssql-ssis-app-runtime**
 - **mssql-monitor-telegraf**
 - **mssql-mleap-serving-runtime**
  

## <a id="automated"></a> 自動化的指令碼

您可以使用自動化的 python 指令碼，會自動提取所有必要的容器映像並將其推送至私人存放庫。

> [!NOTE]
> Python 是使用指令碼的必要條件。 如需如何安裝 Python 的詳細資訊，請參閱[Python 文件](https://wiki.python.org/moin/BeginnersGuide/Download)。

1. 從 bash 或 PowerShell，下載的指令碼**curl**:

   ```PowerShell
   curl -o push-bdc-images-to-custom-private-repo.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/offline/push-bdc-images-to-custom-private-repo.py"
   ```

1. 使用下列命令，然後執行指令碼：

   **Windows:**

   ```PowerShell
   python deploy-sql-big-data-aks.py
   ```

   **Linux:**

   ```bash
   sudo python deploy-sql-big-data-aks.py
   ```

1. 遵循提示以取得輸入過 Microsoft 存放庫和您的私人存放庫資訊。 指令碼完成之後，所有必要映像應該位於您私人存放庫。

## <a name="install-tools-offline"></a>安裝離線瀏覽工具

巨量資料叢集部署需要數個工具，包括**Python**， **mssqlctl**，並**kubectl**。 您可以使用下列步驟來離線的伺服器上安裝這些工具。

### <a id="python"></a> 安裝 python 離線

1. 在具有網際網路存取電腦上，下載下列的壓縮檔案，包含 Python 程序：

   | 作業系統 | 下載 |
   |---|---|
   | Windows | [https://go.microsoft.com/fwlink/?linkid=2074021](https://go.microsoft.com/fwlink/?linkid=2074021) |
   | Linux   | [https://go.microsoft.com/fwlink/?linkid=2065975](https://go.microsoft.com/fwlink/?linkid=2065975) |
   | OSX     | [https://go.microsoft.com/fwlink/?linkid=2065976](https://go.microsoft.com/fwlink/?linkid=2065976) |

1. 將壓縮的檔案複製到目標電腦，並將它解壓縮到您選擇的資料夾。

1. 針對 Windows，執行`installLocalPythonPackages.bat`從該資料夾，然後以相同的資料夾，做為參數傳遞的完整路徑。

   ```PowerShell
   installLocalPythonPackages.bat "C:\python-3.6.6-win-x64-0.0.1-offline\0.0.1"
   ```

### <a id="mssqlctl"></a> 安裝離線 mssqlctl

1. 具有網際網路存取的電腦上並[Python](https://wiki.python.org/moin/BeginnersGuide/Download)，執行下列命令以下載所有關閉**mssqlctl**封裝至目前的資料夾。

   ```PowerShell
   pip download -r https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt
   ```

1. 下載**requirements.txt**檔案。

   ```PowerShell
   curl -o requirements.txt "https://private-repo.microsoft.com/python/ctp-2.3/mssqlctl/requirements.txt"
   ```

1. 複製下載的套件和**requirements.txt**到目標電腦的檔案。

1. 執行下列命令的目標電腦上，指定的資料夾，複製到舊的檔案。

   ```PowerShell
   pip install --no-index --find-links <path-to-packages> -r <path-to-requirements.txt>
   ```

### <a id="kubectl"></a> 安裝 kubectl 離線

若要安裝**kubectl**到離線的電腦，請使用下列步驟。

1. 使用**curl**以下載**kubectl**到您選擇的資料夾。 如需詳細資訊，請參閱 <<c0> [ 安裝 kubectl 二進位檔使用 curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl)。

1. 將資料夾複製到目標電腦。

## <a name="deploy-from-private-repository"></a>從私人存放庫部署

若要從私人存放庫部署，使用 中所述的步驟[部署指南](deployment-guidance.md)，但使用自訂的部署組態檔，指定您的私人 Docker 存放庫資訊。 下列**mssqlctl**命令示範如何變更名為自訂部署組態檔中的 Docker 設定**custom.json**:

```bash
mssqlctl bdc config section set --config-profile custom -j "$.spec.controlPlane.spec.docker.repository=<your-docker-repository>"
mssqlctl bdc config section set --config-profile custom -j "$.spec.controlPlane.spec.docker.registry=<your-docker-registry>"
mssqlctl bdc config section set --config-profile custom -j "$.spec.controlPlane.spec.docker.imageTag=<your-docker-image-tag>"
```

部署會提示您輸入的 docker 使用者名稱和密碼，或您可以指定在**DOCKER_USERNAME**並**DOCKER_PASSWORD**環境變數。

## <a name="next-steps"></a>後續步驟

如需有關巨量資料叢集部署的詳細資訊，請參閱[如何部署 SQL Server 的巨量資料叢集的 Kubernetes 上](deployment-guidance.md)。
