---
title: 設定適用於 SQL Server 2019 巨量資料叢集部署的 Azure Kubernetes 服務 |Microsoft Docs
description: 了解如何設定適用於 SQL Server 2019 巨量資料叢集 （預覽） 部署的 Azure Kubernetes Service (AKS)。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 07ee0ac0db742eca9a55decfcd78cb76b75e0160
ms.sourcegitcommit: cb73d60db8df15bf929ca17c1576cf1c4dca1780
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2018
ms.locfileid: "51221654"
---
# <a name="configure-azure-kubernetes-service-for-sql-server-2019-preview-deployments"></a>設定 Azure Kubernetes Service 來進行 SQL Server 2019 （預覽） 部署

本文說明如何設定適用於 SQL Server 2019 巨量資料叢集 （預覽） 部署的 Azure Kubernetes Service (AKS)。 

AKS 可讓您更輕鬆地建立、 設定及管理預先設定的虛擬機器的叢集使用來執行容器化應用程式的 Kubernetes 叢集。 這可讓您使用現有技能，或運用大量且不斷成長的社群專業知識，來部署和管理 Microsoft Azure 上的容器型應用程式。

這篇文章說明部署 Kubernetes AKS 使用 Azure CLI 上的步驟。 如果您沒有 Azure 訂用帳戶，請在您開始前建立免費帳戶。

> [!TIP] 
> 部署 AKS 和 SQL Server 的巨量資料叢集的範例 python 指令碼，請參閱[部署巨量資料叢集的 Azure Kubernetes Service (AKS) 上的 SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks)。

## <a name="prerequisites"></a>先決條件

- AKS 環境，以獲得最佳的體驗，同時驗證的基本案例，我們建議至少三個代理程式 （除了主機） 中的 Vm 具有至少 4 個 Vcpu 和 32 GB 的記憶體，每個。 Azure 基礎結構提供多個 Vm 的大小選項，請參閱 <<c0> [ 此處](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sizes)針對您打算要部署的區域中選取項目。
  
- 本節中，您必須執行 Azure CLI 2.0.4 版或更新版本。 如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)。 執行`az --version`以尋找版本，如有需要。

- 安裝[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)版本 1.10 伺服器和用戶端的最少。 如果您想要安裝 kubectl 用戶端上的特定版本，請參閱[安裝 kubectl 二進位透過 curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl)。 您必須使用 AKS，`--kubernetes-version`參數來指定預設值不同的版本。

> [!NOTE]
請注意，用戶端/伺服器版本也就是扭曲支援是 + /-1 的次要版本。 Kubernetes 文件中指出，「 用戶端應該扭曲有一個以上的次要版本，在主機上，但可能會導致主要由最多一個次要版本。 比方說，v1.3 主要應該使用 v1.1、 v1.2 和 v1.3 節點，並應該使用 v1.2、 v1.3 和 v1.4 用戶端。 」 如需詳細資訊，請參閱 < [Kubernetes 支援的版本和元件扭曲](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew)。

另請注意，`az aks kubernetes install-cli`都會安裝 kubectl 用戶端版本較低，需要的 1.10。 請遵循上述指示安裝 kubectl 用戶端的正確版本。

## <a name="create-a-resource-group"></a>建立資源群組

Azure 資源群組是在哪一項 Azure 資源部署與管理的邏輯群組。 下列步驟登入 Azure，並建立 AKS 叢集的資源群組。

> [!TIP]
> 如果您使用的 Windows，使用 PowerShell，如接下來的步驟。

1. 在命令提示字元中，執行下列命令，並遵循提示來登入您的 Azure 訂用帳戶：

    ```bash
    az login
    ```

1. 如果您有多個訂用帳戶，您可以執行下列命令來檢視您所有的訂閱：

   ```bash
   az account list
   ```

1. 如果您想要將變更為不同的訂用帳戶，您可以執行此命令：

   ```bash
   az account set --subscription <subscription id>
   ```

1. 建立的資源群組**az 群組建立**命令。 下列範例會建立名為的資源群組`sqlbigdatagroup`在`westus2`位置。

   ```bash
   az group create --name sqlbigdatagroup --location westus2
   ```

## <a name="create-a-kubernetes-cluster"></a>建立 Kubernetes 叢集

1. 在與 AKS 建立 Kubernetes 叢集[az aks 建立](https://docs.microsoft.com/cli/azure/aks)命令。 下列範例會建立名為 Kubernetes 叢集*kubcluster*使用一個 Linux 主要節點和兩個 Linux 代理程式節點。 請確定您在先前各節中使用的相同資源群組中建立 AKS 叢集。

    ```bash
   az aks create --name kubcluster \
    --resource-group sqlbigdatagroup \
    --generate-ssh-keys \
    --node-vm-size Standard_E4s_v3 \
    --node-count 3 \
    --kubernetes-version 1.10.8
    ```

    您可以增加或減少預設代理程式計數，藉由變更`--node-count <n>`其中`<n>`是您想要有代理程式節點數目。

    幾分鐘之後，此命令會完成，並傳回 JSON 格式化叢集的相關資訊。

1. 儲存 JSON 輸出以供稍後使用前一個命令。

## <a name="connect-to-the-cluster"></a>連線到叢集

1. 若要設定 kubectl 來連線到 Kubernetes 叢集，請執行[az aks get-credentials 來取得認證](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials)命令。 此步驟中下載憑證，並設定 kubectl CLI 來使用它們。

   ```bash
   az aks get-credentials --resource-group=sqlbigdatagroup --name kubcluster
   ```

1. 若要驗證您的叢集連線，請使用[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)命令來傳回叢集節點的清單。  下列範例顯示輸出時有 1 部主機，以及 3 個代理程式節點。

   ```bash
   kubectl get nodes
   ```

## <a name="next-steps"></a>後續步驟

這篇文章中的步驟會設定在 AKS 中 Kubernetes 叢集。 下一個步驟是將 SQL Server 2019 巨量資料部署到叢集。

[快速入門： 部署 Azure Kubernetes Service (AKS) 上的 SQL Server 巨量資料叢集](quickstart-big-data-cluster-deploy.md)
