---
title: 在 Azure Kubernetes Service (AKS) 私人叢集中部署 BDC
titleSuffix: SQL Server Big Data Cluster
description: 了解如何使用具有進階網路功能 (CNI) 的 Azure Kubernetes Service (AKS) 私人叢集，部署 SQL Server 巨量資料叢集。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 08/20/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4a55d7f6c9c55891f8d1a7bf97d8834c9df4a796
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/01/2020
ms.locfileid: "89283117"
---
# <a name="deploy-bdc-in-azure-kubernetes-service-aks-private-cluster"></a>在 Azure Kubernetes Service (AKS) 私人叢集中部署 BDC

此文章說明如何在 Azure Kubernetes Service (AKS) 私人叢集上部署的 SQL Server 巨量資料叢集。 此組態支援在企業網路環境中限制公用 IP 位址的使用。

私人部署提供下列優點：

* 限制公用 IP 位址的使用
* 應用程式伺服器和叢集節點集區之間的網路流量僅保留在私人網路上
* 適用於強制輸出流量以符合特定需求的自訂設定

此文章示範如何使用 AKS 私人叢集來限制公用 IP 位址的使用，同時套用個別的安全性字串。

## <a name="deploy-private-bdc-cluster-with-aks-private-cluster"></a>使用 AKS 私人叢集部署私人 BDC 叢集

若要開始使用，請建立 [AKS 私人叢集](/azure/aks/private-clusters)，以確保 API 伺服器與節點集區之間的網路流量僅保留在私人網路上。 控制平面或 API 伺服器在 AKS 私人叢集中具有內部 IP 位址。

此節示範如何在具有進階網路功能 (CNI) 的 Azure Kubernetes Service (AKS) 私人叢集中部署 BDC 叢集。

## <a name="create-a-private-aks-cluster-with-advanced-networking"></a>建立具有進階網路功能的私人 AKS 叢集

```console

export REGION_NAME=<your Azure region >
export RESOURCE_GROUP=< your resource group name >
export SUBNET_NAME=aks-subnet
export VNET_NAME=bdc-vnet
export AKS_NAME=< your aks private cluster name >
 
az group create -n $RESOURCE_GROUP -l $REGION_NAME
 
az network vnet create \
    --resource-group $RESOURCE_GROUP \
    --location $REGION_NAME \
    --name $VNET_NAME \
    --address-prefixes 10.0.0.0/8 \
    --subnet-name $SUBNET_NAME \
    --subnet-prefix 10.1.0.0/16
 

SUBNET_ID=$(az network vnet subnet show \
    --resource-group $RESOURCE_GROUP \
    --vnet-name $VNET_NAME \
    --name $SUBNET_NAME \
    --query id -o tsv)
 
echo $SUBNET_ID
## will be displayed something similar as the following: 
/subscriptions/xxxx-xxxx-xxx-xxxx-xxxxxxxx/resourceGroups/your-bdc-rg/providers/Microsoft.Network/virtualNetworks/your-aks-vnet/subnets/your-aks-subnet
```

### <a name="create-aks-private-cluster-with-advanced-networking-cni"></a>建立具有進階網路功能 (CNI) 的 AKS 私人叢集

為能夠繼續進行下一個步驟，您必須佈建具有已啟用私人叢集功能的 Standard Load Balancer 的 AKS 叢集。 您的命令將如下所示： 

```console
az aks create \
    --resource-group $RESOURCE_GROUP \
    --name $AKS_NAME \
    --load-balancer-sku standard \
    --enable-private-cluster \
    --network-plugin azure \
    --vnet-subnet-id $SUBNET_ID \
    --docker-bridge-address 172.17.0.1/16 \
    --dns-service-ip 10.2.0.10 \
    --service-cidr 10.2.0.0/24 \
    --node-vm-size Standard_D13_v2 \
    --node-count 2 \
    --generate-ssh-keys
```

成功部署之後，您可以移至 `<MC_yourakscluster>` 資源群組，而且您會發現 `kube-apiserver` 是私人端點。 如需範例，請參閱下一節。

## <a name="connect-to-an-aks-cluster"></a>連線至 AKS 叢集

```console
az aks get-credentials -n $AKS_NAME -g $RESOURCE_GROUP
```

## <a name="build-big-data-cluster-bdc-deployment-profile"></a>建置巨量資料叢集 (BDC) 部署設定檔

連線到 AKS 叢集之後，您可以開始部署 BDC，而且您可以準備環境變數並起始部署： 

```console
azdata bdc config init --source aks-dev-test --target private-bdc-aks --force
```

產生並設定 BDC 自訂部署設定檔：

```console
azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.docker.imageTag=2019-CU6-ubuntu-16.04"
azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.storage.data.className=default"
azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.storage.logs.className=default"

azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.endpoints[1].serviceType=NodePort"

azdata bdc config replace -c private-bdc-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -c private-bdc-aks/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -c private-bdc-aks/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].serviceType=NodePort"
```

## <a name="deploy-private-sql-server-big-data-cluster-with-ha"></a>部署具有 HA 的 SQL Server 巨量資料叢集

如果您要[部署具有高可用性 (HA) 的 SQL Server 巨量資料叢集 (SQL-BDC)](deployment-high-availability.md)，您將會使用部署 `aks-dev-test-ha` 部署設定檔。 成功部署之後，您可以使用相同的 `kubectl get svc` 命令，而且您將會看到建立了額外的 `master-secondary-svc` 服務。 您需要將 `ServiceType` 設定為 `NodePort`。 其他步驟將與上一節所提及的步驟類似。

下列範例會將 `ServiceType` 設定為 `NodePort`：

```console
azdata bdc config replace -c private-bdc-aks /bdc.json -j "$.spec.resources.master.spec.endpoints[1].serviceType=NodePort"
```

## <a name="deploy-bdc-in-aks-private-cluster"></a>在 AKS 私人叢集中部署 BDC

```console
export AZDATA_USERNAME=<your bdcadmin username>
export AZDATA_PASSWORD=< your bdcadmin password>

azdata bdc create --config-profile private-bdc-aks --accept-eula yes
```

## <a name="check-deployment-status"></a>檢查部署狀態

部署將需要幾分鐘的時間，而且您可以使用下列命令檢查部署狀態： 

```console
kubectl get pods -n mssql-cluster -w
```

## <a name="check-the-service-status"></a>檢查服務狀態

使用下列命令檢查服務。 確認這些服務全都狀況良好，且沒有任何外部 IP：

```console
kubectl get services -n mssql-cluster
```

請參閱如何[在 AKS 私人叢集中管理 BDC](private-manage.md)，然後下一個步驟是[連線到 BDC 叢集](connect-to-big-data-cluster.md)。

請參閱 [GitHub 上的 SQL Server 範例存放庫](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/private-aks) \(英文\)，以取得適用於此案例的自動化指令碼。

## <a name="next-steps"></a>後續步驟

[管理私人叢集](private-manage.md)

[限制私人 BDC 叢集的輸出流量](private-restrict-egress-traffic.md)

[使用 Azure Data Studio 連線到 SQL Server 巨量資料叢集](connect-to-big-data-cluster.md)
