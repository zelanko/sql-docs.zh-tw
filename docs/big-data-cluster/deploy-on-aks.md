---
title: 設定 Azure Kubernetes Service
titleSuffix: SQL Server big data clusters
description: 瞭解如何設定部署的[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] Azure Kubernetes Service (AKS)。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b33ef15bd6a47bcd2a475f608197a1566bb030b0
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652389"
---
# <a name="configure-azure-kubernetes-service-for-sql-server-big-data-cluster-deployments"></a>針對 SQL Server 巨量資料叢集部署設定 Azure Kubernetes Service

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何設定部署的[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] Azure Kubernetes Service (AKS)。

AKS 可讓使用者輕鬆地建立、設定及管理已預先設定 Kubernetes 叢集的虛擬機器叢集，以執行容器化的應用程式。 這可讓您使用自己現有的技能，或是運用大量且不斷成長的社群專業知識，來在 Microsoft Azure 上部署及管理容器型應用程式。

此文章說明使用 Azure CLI 在 AKS 上部署 Kubernetes 的步驟。 如果您沒有 Azure 訂用帳戶，請在開始前先建立免費帳戶。

> [!TIP]
> 您也可以透過單一步驟編寫部署 AKS 和巨量資料叢集的指令碼。 如需詳細資訊，請參閱如何在 [Python 指令碼](quickstart-big-data-cluster-deploy.md)或 Azure Data Studio [筆記本](deploy-notebooks.md)中執行此動作。

## <a name="prerequisites"></a>必要條件

- [部署 SQL Server 2019 巨量資料工具](deploy-big-data-tools.md)：
   - **Kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
   - **Azure CLI**

- 1\.10 版或更新版本的 Kubernetes 伺服器。 針對 AKS，您必須使用 `--kubernetes-version` 參數來指定與預設版本不同的版本。

- 若要在 AKS 上驗證基本案例時取得最佳體驗，請使用：
   - 8 個 vCPU (跨所有節點)
   - 32 GB 的記憶體 (每個 VM)
   - 24 個或更多的已連接磁碟 (跨所有節點)

   > [!TIP]
   > Azure 基礎結構對 VM 提供多個大小選項；請參閱[這裡](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) \(部分機器翻譯\) 以取得適用於您目標部署區域的選項。

## <a name="create-a-resource-group"></a>建立資源群組

Azure 資源群組是部署及管理 Azure 資源所在的邏輯群組。 下列步驟會登入 Azure 並針對 AKS 叢集建立資源群組。

1. 在命令提示字元中執行下列命令，然後遵循提示以登入您的 Azure 訂用帳戶：

    ```azurecli
    az login
    ```

1. 如果您有多個訂用帳戶，則可以執行下列命令來檢視所有訂用帳戶：

   ```azurecli
   az account list
   ```

1. 如果您想要變更為不同的訂用帳戶，請執行此命令：

   ```azurecli
   az account set --subscription <subscription id>
   ```

1. 使用 **az group create** 命令來建立資源群組。 下列範例會在 `westus2` 位置建立名為 `sqlbdcgroup` 的資源群組。

   ```azurecli
   az group create --name sqlbdcgroup --location westus2
   ```

## <a name="verify-available-kubernetes-versions"></a>確認可用的 Kubernetes 版本

使用最新可用的 Kubernetes 版本。 最新可用版本會取決於您將叢集部署到的位置。 下列命令會傳回特定位置的可用 Kubernetes 版本。

在您執行命令之前，請更新指令碼。 將 `<Azure data center>` 取代為叢集的位置。

   **bash**

   ```bash
   az aks get-versions \
   --location <Azure data center> \
   --query orchestrators \
   --o table
   ```

   **PowerShell**

   ```powershell
   az aks get-versions `
   --location <Azure data center> `
   --query orchestrators `
   --o table
   ```

選擇適用於叢集的最新可用版本。 記錄版本號碼。 您將會在下一個步驟中使用它。

## <a name="create-a-kubernetes-cluster"></a>建立 Kubernetes 叢集

1. 使用 [az aks create](https://docs.microsoft.com/cli/azure/aks) \(英文\) 命令在 AKS 中建立 Kubernetes 叢集。 下列範例會建立名為 *kubcluster* 的 Kubernetes 叢集，其具有大小為 **Standard_L8s** 的單一 Linux 代理程式節點。

   在您執行程式碼之前，請將 `<version number>` 取代為您在上一個步驟中識別的版本號碼。

   確定您是在和先前小節中相同的資源群組中建立 AKS 叢集。

   **bash：**

   ```bash
   az aks create --name kubcluster \
   --resource-group sqlbdcgroup \
   --generate-ssh-keys \
   --node-vm-size Standard_L8s \
   --node-count 1 \
   --kubernetes-version <version number>
   ```

   **PowerShell：**

   ```powershell
   az aks create --name kubcluster `
   --resource-group sqlbdcgroup `
   --generate-ssh-keys `
   --node-vm-size Standard_L8s `
   --node-count 1 `
   --kubernetes-version <version number>
   ```

   您可以透過變更 `--node-count <n>` 來增加或減少 Kubernetes 代理程式節點的數目，其中 `<n>` 是您想要使用的代理程式節點數目。 這並不包含主要 Kubernetes 節點，其是由 AKS 在幕後管理。 基於評估目的，上述範例只會使用單一節點。

   在數分鐘之後，該命令會完成並傳回關於節點的 JSON 格式資料。

   > [!TIP]
   > 如果您在 AKS 中建立叢集時遇到任何錯誤，請參閱此文章的[疑難排解小節](#troubleshoot)。

1. 儲存上一個命令的 JSON 輸出以供稍後使用。

## <a name="connect-to-the-cluster"></a>連線到叢集

1. 若要設定 kubectl 以連線到您的 Kubernetes 叢集，請執行 [az aks get-credentials](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials) \(英文\) 命令。 此步驟會下載認證，並設定 kubectl CLI 以使用它們。

   ```azurecli
   az aks get-credentials --resource-group=sqlbdcgroup --name kubcluster
   ```

1. 若要驗證針對您叢集的連線，請使用 [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) \(英文\) 命令來傳回叢集節點的清單。  下列範例會顯示當您具有 1 個主要節點和 3 個代理程式節點時的輸出。

   ```bash
   kubectl get nodes
   ```

## <a id="troubleshoot"></a> 疑難排解

如果您在使用上述命令建立 Azure Kubernetes Service 時遇到任何問題，請嘗試下列解決方法：

- 確定您已安裝[最新版本的 Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)。
- 使用不同的資源群組和叢集名稱來嘗試相同的步驟。

## <a name="next-steps"></a>後續步驟

此文章中的步驟已在 AKS 中設定 Kubernetes 叢集。 下一步是在 AKS Kubernetes 叢集上部署 SQL Server 2019 巨量資料叢集。 如需如何部署巨量資料叢集的詳細資訊，請參閱下列文章：

[如何在 Kubernetes [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]上部署](deployment-guidance.md)
