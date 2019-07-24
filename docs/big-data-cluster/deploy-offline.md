---
title: 離線部署
titleSuffix: SQL Server big data clusters
description: 瞭解如何執行 SQL Server big data 叢集的離線部署。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: cd8b3128fc11037a5ade494813611d473c995f8f
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419364"
---
# <a name="perform-an-offline-deployment-of-a-sql-server-big-data-cluster"></a>執行 SQL Server big data 叢集的離線部署

本文說明如何執行 SQL Server 2019 big data cluster (預覽) 的離線部署。 Big data 叢集必須能夠存取 Docker 存放庫, 以從中提取容器映射。 離線安裝是將所需的映射放入私人 Docker 存放庫的其中一個。 該私用存放庫接著會當做新部署的映射來源使用。

## <a name="prerequisites"></a>先決條件

- 在任何支援的 Linux 發行版本或適用於 Mac/Windows 上的 Docker 安裝 Docker 引擎 1.8 以上版本。 如需詳細資訊，請參閱[安裝 Docker](https://docs.docker.com/engine/installation/)。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="load-images-into-a-private-repository"></a>將映射載入私人存放庫

下列步驟說明如何從 Microsoft 存放庫提取 big data cluster 容器映射, 然後將其推送至您的私人存放庫。

> [!TIP]
> 下列步驟說明此程式。 不過, 若要簡化工作, 您可以使用[自動化腳本](#automated), 而不是手動執行這些命令。

1. 重複下列命令, 以提取 big data cluster 容器映射。 取代`<SOURCE_IMAGE_NAME>`為每個[映射名稱](#images)。 以`<SOURCE_DOCKER_TAG>` big data cluster 版本的標記取代, 例如**2019-ctp 3.2-ubuntu**。  

   ```PowerShell
   docker pull mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG>
   ```

1. 登入目標私人 Docker 登錄。

   ```PowerShell
   docker login <TARGET_DOCKER_REGISTRY> -u <TARGET_DOCKER_USERNAME> -p <TARGET_DOCKER_PASSWORD>
   ```

1. 使用下列命令為每個映射標記本機映射:

   ```PowerShell
   docker tag mcr.microsoft.com/mssql/bdc/<SOURCE_IMAGE_NAME>:<SOURCE_DOCKER_TAG> <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

1. 將本機映射推送至私人 Docker 存放庫:

   ```PowerShell
   docker push <TARGET_DOCKER_REGISTRY>/<TARGET_DOCKER_REPOSITORY>/<SOURCE_IMAGE_NAME>:<TARGET_DOCKER_TAG>
   ```

### <a id="images"></a>Big data cluster 容器映射

離線安裝需要下列 big data cluster 容器映射:

 - **mssql-appdeploy-init**
 - **mssql-monitor-fluentbit**
 - **mssql-monitor-collectd**
 - **mssql-server-data**
 - **mssql-hadoop**
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
 - **mssql-安全性-支援**

## <a id="automated"></a>自動化腳本

您可以使用自動化的 python 腳本來自動提取所有必要的容器映射, 並將其推送至私人存放庫。

> [!NOTE]
> Python 是使用腳本的必要條件。 如需有關如何安裝 Python 的詳細資訊, 請參閱[Python 檔](https://wiki.python.org/moin/BeginnersGuide/Download)。

1. 從 bash 或 PowerShell 下載包含**捲曲**的腳本:

   ```PowerShell
   curl -o push-bdc-images-to-custom-private-repo.py "https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/deployment/offline/push-bdc-images-to-custom-private-repo.py"
   ```

1. 然後使用下列其中一個命令來執行腳本:

   **時段**

   ```PowerShell
   python deploy-sql-big-data-aks.py
   ```

   **廠商**

   ```bash
   sudo python deploy-sql-big-data-aks.py
   ```

1. 遵循提示輸入 Microsoft 存放庫和您的私人存放庫資訊。 腳本完成之後, 所有必要的映射都應該位於您的私用存放庫中。

## <a name="install-tools-offline"></a>離線安裝工具

Big data cluster 部署需要數項工具, 包括**Python**、 **azdata**和**kubectl**。 使用下列步驟, 在離線服務器上安裝這些工具。

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

### <a id="azdata"></a>離線安裝 azdata

1. 在具有網際網路存取和[Python](https://wiki.python.org/moin/BeginnersGuide/Download)的電腦上, 執行下列命令以將所有**azdata**套件下載至目前的資料夾。

   ```PowerShell
   pip download -r https://aka.ms/azdata
   ```

1. 將下載的套件和**需求 .txt**檔案複製到目的電腦。

1. 在目的電腦上執行下列命令, 並指定您將先前檔案複製到其中的資料夾。

   ```PowerShell
   pip install --no-index --find-links <path-to-packages> -r <path-to-requirements.txt>
   ```

### <a id="kubectl"></a>離線安裝 kubectl

若要將**kubectl**安裝到離線電腦, 請使用下列步驟。

1. 使用 [**捲曲**] 將**kubectl**下載至您選擇的資料夾。 如需詳細資訊, 請參閱[Install kubectl binary using 捲曲](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl)。

1. 將資料夾複製到目的電腦。

## <a name="deploy-from-private-repository"></a>從私人存放庫部署

若要從私人存放庫進行部署, 請使用[部署指南](deployment-guidance.md)中所述的步驟, 但使用自訂的部署設定檔, 以指定您的私人 Docker 存放庫資訊。 下列**azdata**命令示範如何在名為**control. json**的自訂部署設定檔中變更 Docker 設定:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.repository=<your-docker-repository>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.registry=<your-docker-registry>"
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.docker.imageTag=<your-docker-image-tag>"
```

部署會提示您提供 docker 使用者名稱和密碼, 或者您可以在**DOCKER_USERNAME**和**DOCKER_PASSWORD**環境變數中指定它們。

## <a name="next-steps"></a>後續步驟

如需有關 big data cluster 部署的詳細資訊, 請參閱[如何在 Kubernetes 上部署 SQL Server big data](deployment-guidance.md)叢集。
