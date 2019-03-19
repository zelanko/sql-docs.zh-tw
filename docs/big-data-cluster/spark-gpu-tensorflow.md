---
title: GPU 支援和 TensorFlow
titleSuffix: SQL Server 2019 big data clusters
description: 部署具有 GPU 支援的巨量資料叢集，並在 Azure 資料 Studio Notebook 中使用 TensorFlow。
author: lgongmsft
ms.author: shivprashant
ms.reviewer: jroth
manager: craigg
ms.date: 03/14/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9f766c343152fa601cc22e59e3385c454ec23879
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161952"
---
# <a name="deploy-a-big-data-cluster-with-gpu-support-and-run-tensorflow"></a>部署具有 GPU 支援的巨量資料叢集並執行 TensorFlow

這篇文章會示範如何部署巨量資料叢集在 Azure Kubernetes Service (AKS) 支援已啟用 GPU 的節點集區的計算密集型工作負載。 然後，您會執行範例 notebook 中執行 TensorFlow 映像分類適用於 GPU 的 Azure Data Studio。

## <a name="prerequisites"></a>先決條件

- [巨量資料工具](deploy-big-data-tools.md):
  - **mssqlctl**
  - **kubectl**
  - **Azure Data Studio**
  - **SQL Server 2019 延伸模組**
  - **Azure CLI**

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="create-an-aks-cluster"></a>建立 AKS 叢集

下列步驟使用 Azure CLI 來建立 AKS 叢集支援的 Gpu。

1. 在命令提示字元中，執行下列命令，並遵循提示來登入您的 Azure 訂用帳戶：

    ```azurecli
    az login
    ```

1. 建立的資源群組**az 群組建立**命令。 下列範例會建立名為的資源群組`sqlbigdatagroupgpu`在`eastus`位置。

   ```azurecli
   az group create --name sqlbigdatagroupgpu --location eastus
   ```

1. 在與 AKS 建立 Kubernetes 叢集[az aks 建立](https://docs.microsoft.com/cli/azure/aks)命令。 下列範例會建立名為 Kubernetes 叢集`gpucluster`在`sqlbigdatagroupgpu`資源群組。

   ```azurecli
   az aks create --name gpucluster --resource-group sqlbigdatagroupgpu --generate-ssh-keys --node-vm-size Standard_NC6 --node-count 3 --node-osdisk-size 50 --kubernetes-version 1.11.7 --location eastus
   ```

   > [!NOTE]
   > 此叢集會使用**Standard_NC6** [GPU 最佳化的虛擬機器大小](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-gpu)，而這也是特製化適用於單一或多個 NVIDIA Gpu 的虛擬機器。 如需詳細資訊，請參閱 <<c0> [ 計算密集型工作負載在 Azure Kubernetes Service (AKS) 中使用 Gpu](https://docs.microsoft.com/azure/aks/gpu-cluster)。

1. 若要設定 kubectl 來連線到 Kubernetes 叢集，請執行[az aks get-credentials 來取得認證](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials)命令。

   ```azurecli
   az aks get-credentials --overwrite-existing --resource-group=sqlbigdatagroupgpu --name gpucluster
   ```

## <a name="apply-yaml-manifest"></a>套用 YAML 資訊清單

1. 使用**kubectl**建立名為 Kubernetes 命名空間`gpu-resources`。

   ```
   kubectl create namespace gpu-resources
   ```

1. 將下列 YAML 檔案的內容儲存到名為的檔案**nvidia 裝置-外掛程式 ds.yaml**。 您正在執行的電腦上的工作目錄儲存這**kubectl**從。

   更新`image: nvidia/k8s-device-plugin:1.11`半向下的資訊清單，以符合您的 Kubernetes 版本。 例如，如果您的 AKS 叢集中執行 Kubernetes 1.12 版，更新的標記`image: nvidia/k8s-device-plugin:1.12`。

   ```yaml
   apiVersion: extensions/v1beta1
   kind: DaemonSet
   metadata:
     labels:
       kubernetes.io/cluster-service: "true"
     name: nvidia-device-plugin
     namespace: gpu-resources
   spec:
     template:
       metadata:
         # Mark this pod as a critical add-on; when enabled, the critical add-on scheduler
         # reserves resources for critical add-on pods so that they can be rescheduled after
         # a failure.  This annotation works in tandem with the toleration below.
         annotations:
           scheduler.alpha.kubernetes.io/critical-pod: ""
         labels:
           name: nvidia-device-plugin-ds
       spec:
         tolerations:
         # Allow this pod to be rescheduled while the node is in "critical add-ons only" mode.
         # This, along with the annotation above marks this pod as a critical add-on.
         - key: CriticalAddonsOnly
           operator: Exists
         containers:
         - image: nvidia/k8s-device-plugin:1.11 # Update this tag to match your Kubernetes version
           name: nvidia-device-plugin-ctr
           securityContext:
             allowPrivilegeEscalation: false
             capabilities:
               drop: ["ALL"]
           volumeMounts:
             - name: device-plugin
               mountPath: /var/lib/kubelet/device-plugins
         volumes:
           - name: device-plugin
             hostPath:
               path: /var/lib/kubelet/device-plugins
         nodeSelector:
           beta.kubernetes.io/os: linux
           accelerator: nvidia
   ```

1. 現在使用 kubectl apply 命令建立 DaemonSet。 **nvidia 裝置-外掛程式 ds.yaml**必須是工作目錄中，當您執行下列命令：

   ```
   kubectl apply -f nvidia-device-plugin-ds.yaml
   ```

## <a name="deploy-the-big-data-cluster"></a>部署巨量資料叢集

若要部署 SQL Server 2019 巨量資料叢集 （預覽） 支援的 Gpu，您必須從特定的 docker 登錄和儲存機制部署。 具體來說，您可以使用不同的值**DOCKER_REGISTRY**， **DOCKER_REPOSITORY**， **DOCKER_USERNAME**， **DOCKER_PASSWORD**，並**DOCKER_EMAIL**。 下列各節提供有關如何設定環境變數的範例。 使用 Windows 或 Linux 區段根據平台的用戶端用來部署巨量資料叢集。

### <a name="windows"></a>視窗

   1. 使用命令提示字元 視窗 (非 PowerShell)，設定下列環境變數。 請勿使用引號括住的值。

      ```cmd
      SET ACCEPT_EULA=yes
      SET CLUSTER_PLATFORM=aks

      SET CONTROLLER_USERNAME=<controller_admin_name - can be anything>
      SET CONTROLLER_PASSWORD=<controller_admin_password - can be anything, password complexity compliant>
      SET KNOX_PASSWORD=<knox_password - can be anything, password complexity compliant>
      SET MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instance, password complexity compliant>

      SET DOCKER_REGISTRY=marinchcreus3.azurecr.io
      SET DOCKER_REPOSITORY=ctp23-8-0-61-gpu
      SET DOCKER_USERNAME=<your username, gpu-specific credentials provided by Microsoft>
      SET DOCKER_PASSWORD=<your password, gpu-specific credentials provided by Microsoft>
      SET DOCKER_EMAIL=<your email address>
      SET DOCKER_PRIVATE_REGISTRY=1
      SET STORAGE_SIZE=10Gi
      ```

   1. 部署巨量資料叢集：

      ```cmd
      mssqlctl cluster create --name gpubigdatacluster
      ```

### <a name="linux"></a>Linux

   1. 初始化下列環境變數。 在 bash 中，您可以使用用引號括住每個值。

      ```bash
      export ACCEPT_EULA=yes
      export CLUSTER_PLATFORM="aks"

      export CONTROLLER_USERNAME="<controller_admin_name - can be anything>"
      export CONTROLLER_PASSWORD="<controller_admin_password - can be anything, password complexity compliant>"
      export KNOX_PASSWORD="<knox_password - can be anything, password complexity compliant>"
      export MSSQL_SA_PASSWORD="<sa_password_of_master_sql_instance, password complexity compliant>"

      export DOCKER_REGISTRY="marinchcreus3.azurecr.io"
      export DOCKER_REPOSITORY="ctp23-8-0-61-gpu"
      export DOCKER_USERNAME="<your username, gpu-specific credentials provided by Microsoft>"
      export DOCKER_PASSWORD="<your password, gpu-specific credentials provided by Microsoft>"
      export DOCKER_EMAIL="<your email address>"
      export DOCKER_PRIVATE_REGISTRY="1"
      export STORAGE_SIZE="10Gi"
      ```

   1. 部署巨量資料叢集：

      ```bash
      mssqlctl cluster create --name gpubigdatacluster
      ```

## <a name="run-the-tensorflow-example"></a>執行 TensorFlow 範例

下列兩個範例 notebook 會示範定型兩個影像分類模型適用於 GPU 使用 TensorFlow 的 Spark 叢集的單一節點上。

| 下載 notebook | 描述 |
|---|---|
| [**tf-cuda8.ipynb**](https://aka.ms/AA4jdgd) | 會使用 8 CUDA、 CUDNN 6 和 TensorFlow 1.4.0。  |
| [**tf-cuda9.ipynb**](https://aka.ms/AA4ixzr) | 會使用 9 CUDA、 CUDNN 7 和 TensorFlow 1.12.0。 |

將適當的記事本檔案到本機電腦，然後開啟，並在 Azure 資料 Studio 中使用的 PySpark3 核心中執行它。 除非您有較舊版本的 CUDA 或 TensorFlow 的特定需求，選擇 [CUDA 9/CUDNN 7/TensorFlow 1.12.0]。 如需如何搭配使用 notebook 和巨量資料叢集的詳細資訊，請參閱[如何在 SQL Server 2019 預覽中使用 notebook](notebooks-guidance.md)。

> [!NOTE]
> 請注意，notebook 會將軟體安裝在系統位置。 這可能是因為目前執行中的 notebook，以在 CTP 2.3 中的根權限。

安裝 NVIDIA GPU 的程式庫和之後 TensorFlow 適用於 GPU，notebook 會列出可用的 GPU 裝置。 然後他們符合，並評估 TensorFlow 模型可辨識手寫數字使用 MNIST 資料集。 檢查可用磁碟空間之後, 下載的人員，並執行中的 CIFAR 10 影像分類範例[ https://github.com/tensorflow/models.git ](https://github.com/tensorflow/models.git)。 藉由在具有不同的 Gpu 叢集上執行 CIFAR 10 範例，您可以觀察速度提升提供 GPU 可用在 Azure 中的每個層代。

## <a name="clean-up-resources"></a>清除資源

若要刪除巨量資料叢集，請使用下列命令：

```
mssqlctl cluster delete --name gpubigdatacluster
```

前一個命令不會移除 AKS 叢集。 若要刪除 AKS 叢集與它相關聯的資源，請使用下列命令：

```azurecli
az group delete -n sqlbigdatagroupgpu
```

## <a name="next-steps"></a>後續步驟

如需有關 SQL Server 2019 巨量資料叢集 （預覽） 的詳細資訊，請參閱 <<c0> [ 什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)。