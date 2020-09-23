---
title: 限制 Azure Kubernetes Service (AKS) 私人叢集中巨量資料叢集 (BDC) 叢集的連出流量
titleSuffix: SQL Server Big Data Clusters
description: 了解如何限制 Azure Kubernetes Service (AKS) 私人叢集中巨量資料叢集 (BDC) 叢集的連出流量。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 08/20/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 962e155b3b0b5906d36fa4d884be2af353cb25a9
ms.sourcegitcommit: 1126792200d3b26ad4c29be1f561cf36f2e82e13
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076604"
---
# <a name="restrict-egress-traffic-of-big-data-clusters-bdc-clusters-in-azure-kubernetes-service-aks-private-cluster"></a>限制 Azure Kubernetes Service (AKS) 私人叢集中巨量資料叢集 (BDC) 叢集的連出流量

AKS 預設會佈建要設定並用於輸出的標準 SKU 負載平衡器。 不過，如果不允許公用 IP 或輸出需要額外的躍點，則預設設定可能不符合所有案例的需求。 如果叢集不允許使用公用 IP，且位於網路虛擬設備 (NVA) 後方，請定義使用者定義的路由表。

根據預設，AKS 叢集具有不受限制的連出網際網路存取權，以供管理與操作之用。 AKS 叢集中的背景工作角色節點需要存取特定連接埠與完整網域名稱 (FQDN)，例如：

* 背景工作角色節點 OS 安全性更新，叢集必須從 Microsoft 容器登錄 (MCR) 提取基礎系統容器映像
* 已啟用 GPU 的 AKS 背景工作角色節點需要從 Nvidia 存取一些端點，才能安裝驅動程式
* 在客戶使用 AKS 工作搭配 Azure 服務，例如，適用於企業級合規性的 Azure 原則、Azure 監視 (含容器見解) 的案例中 
* 啟用開發人員空間及類似本質的更多案例

> [!NOTE]
> 目前，當您在 Azure Kubernetes Service (AKS) 私人叢集中部署 BDC 時，除了此文章中所提及的案例，沒有任何連入相依性，您可以在[控制 Azure Kubernetes Service (AKS) 中叢集節點的連出流量](/azure/aks/limit-egress-traffic)中找到所有連出相依性。

此文章涵蓋如何使用進階網路與 UDR (使用者定義的路由) 在 AKS 私人叢集中部署 BDC，及其與企業級網路環境的進一步整合。

## <a name="use-azure-firewall-to-restrict-egress-traffic"></a>使用 Azure 防火牆限制連出流量

Azure 防火牆提供 Azure Kubernetes Service `(AzureKubernetesService)` FQDN 標籤來簡化此設定。

如需有關此標籤的完整資訊，請參閱[使用 Azure 防火牆限制連出流量](/azure/aks/limit-egress-traffic#restrict-egress-traffic-using-azure-firewall)。

下圖顯示 AKS 私人叢集上的流量限制方式。 

:::image type="content" source="media/private-cluster-restrict-egress-traffic/aks-azure-firewall-egress.png" alt-text="AKS 私人叢集防火牆連出流量":::

使用 Azure 防火牆設定基本架構：

1. 建立資源群組與 VNet
2. 建立並設定 Azure 防火牆
3. 建立使用者定義的路由表
4. 設定防火牆規則
5. 建立服務主體 (SP)
6. 建立 AKS 私人叢集
7. 建立 BDC 部署設定檔
8. 部署 BDC

下列步驟提供詳細資料。

## <a name="create-the-resource-group-and-vnet"></a>建立資源群組與 VNet

1. 定義一組用於建立資源的環境變數。

   ```console
   export REGION_NAME=<region>
   export RESOURCE_GROUP=private-bdc-aksudr-rg
   export SUBNET_NAME=aks-subnet
   export VNET_NAME=bdc-vnet
   export AKS_NAME=bdcaksprivatecluster
   ```

1. 建立資源群組

   ```azurecli
   az group create -n $RESOURCE_GROUP -l $REGION_NAME
   ```

1. 建立 VNET

   ```azurecli
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
   ```

## <a name="create-and-set-up-azure-firewall"></a>建立並設定 Azure 防火牆

1. 定義一組用於建立資源的環境變數。

   ```console
   export FWNAME=bdcaksazfw
   export FWPUBIP=$FWNAME-ip
   export FWIPCONFIG_NAME=$FWNAME-config

   az extension add --name azure-firewall
   ```

1. 為防火牆建立專用子網路

   > [!NOTE]
   > 您無法在建立後變更防火牆名稱

   ```azurecli
   az network vnet subnet create \
     --resource-group $RESOURCE_GROUP \
     --vnet-name $VNET_NAME \
     --name AzureFirewallSubnet \
     --address-prefix 10.3.0.0/24

    az network firewall create -g $RESOURCE_GROUP -n $FWNAME -l $REGION_NAME --enable-dns-proxy true

    az network public-ip create -g $RESOURCE_GROUP -n $FWPUBIP -l $REGION_NAME --sku "Standard"

    az network firewall ip-config create -g $RESOURCE_GROUP -f $FWNAME -n $FWIPCONFIG_NAME --public-ip-address $FWPUBIP --vnet-name $VNET_NAME
   ```

根據預設，Azure 會自動在 Azure 子網路、虛擬網路與內部部署網路之間路由傳送流量。 

## <a name="create-user-defined-route-table"></a>建立使用者定義的路由表

建立具有可連到 Azure 防火牆之躍點的使用者定義的路由表 (UDR)。

```azurecli

export SUBID= <your Azure subscription ID>
export FWROUTE_TABLE_NAME=bdcaks-rt
export FWROUTE_NAME=bdcaksroute
export FWROUTE_NAME_INTERNET=bdcaksrouteinet

export FWPUBLIC_IP=$(az network public-ip show -g $RESOURCE_GROUP -n $FWPUBIP --query "ipAddress" -o tsv)
export FWPRIVATE_IP=$(az network firewall show -g $RESOURCE_GROUP -n $FWNAME --query "ipConfigurations[0].privateIpAddress" -o tsv)

# Create UDR and add a route for Azure Firewall

az network route-table create -g $RESOURCE_GROUP --name $FWROUTE_TABLE_NAME

az network route-table route create -g $RESOURCE_GROUP --name $FWROUTE_NAME --route-table-name $FWROUTE_TABLE_NAME --address-prefix 0.0.0.0/0 --next-hop-type VirtualAppliance --next-hop-ip-address $FWPRIVATE_IP --subscription $SUBID

az network route-table route create -g $RESOURCE_GROUP --name $FWROUTE_NAME_INTERNET --route-table-name $FWROUTE_TABLE_NAME --address-prefix $FWPUBLIC_IP/32 --next-hop-type Internet
```

## <a name="set-up-firewall-rules"></a>設定防火牆規則 

```azurecli
# Add FW Network Rules

az network firewall network-rule create -g $RESOURCE_GROUP -f $FWNAME --collection-name 'aksfwnr' -n 'apiudp' --protocols 'UDP' --source-addresses '*' --destination-addresses "AzureCloud.$REGION_NAME" --destination-ports 1194 --action allow --priority 100
az network firewall network-rule create -g $RESOURCE_GROUP -f $FWNAME --collection-name 'aksfwnr' -n 'apitcp' --protocols 'TCP' --source-addresses '*' --destination-addresses "AzureCloud.$REGION_NAME" --destination-ports 9000
az network firewall network-rule create -g $RESOURCE_GROUP -f $FWNAME --collection-name 'aksfwnr' -n 'time' --protocols 'UDP' --source-addresses '*' --destination-fqdns 'ntp.ubuntu.com' --destination-ports 123

# Add FW Application Rules

az network firewall application-rule create -g $RESOURCE_GROUP -f $FWNAME --collection-name 'aksfwar' -n 'fqdn' --source-addresses '*' --protocols 'http=80' 'https=443' --fqdn-tags "AzureKubernetesService" --action allow --priority 100
```

您可以使用下列命令將使用者定義的路由表 (UDR) 與先前部署 BDC 的 AKS 叢集產生關聯：

```azurecli
az network vnet subnet update -g $RESOURCE_GROUP --vnet-name $VNET_NAME --name $SUBNET_NAME --route-table $FWROUTE_TABLE_NAME
```

## <a name="create--configure-service-principal-sp"></a>建立並設定服務主體 (SP)

在此步驟中，您需要建立服務主體，並指派虛擬網路的權限。

請參閱下列範例： 

```azurecli
# Create SP and Assign Permission to Virtual Network

az ad sp create-for-rbac -n "bdcaks-sp" --skip-assignment

APPID=<your service principal ID >
PASSWORD=< your service principal password >
VNETID=$(az network vnet show -g $RESOURCE_GROUP --name $VNET_NAME --query id -o tsv)

# Assign SP Permission to VNET

az role assignment create --assignee $APPID --scope $VNETID --role "Network Contributor"


RTID=$(az network route-table show -g $RESOURCE_GROUP -n $FWROUTE_TABLE_NAME --query id -o tsv)
az role assignment create --assignee $APPID --scope $RTID --role "Network Contributor"
```

## <a name="create-aks-cluster"></a>建立 AKS 叢集

接著，使用 `userDefinedRouting` 作為輸出類型，建立 AKS 叢集。

```azurecli
az aks create \
    --resource-group $RESOURCE_GROUP \
    --location $REGION_NAME \
    --name $AKS_NAME \
    --load-balancer-sku standard \
    --outbound-type userDefinedRouting \
    --enable-private-cluster \
    --network-plugin azure \
    --vnet-subnet-id $SUBNET_ID \
    --docker-bridge-address 172.17.0.1/16 \
    --dns-service-ip 10.2.0.10 \
    --service-cidr 10.2.0.0/24 \
    --service-principal $APPID \
    --client-secret $PASSWORD \
    --node-vm-size Standard_D13_v2 \
    --node-count 2 \
    --generate-ssh-keys
```

## <a name="build-big-data-cluster-bdc-deployment-profile"></a>建置巨量資料叢集 (BDC) 部署設定檔

您可以使用自訂設定檔建立 BDC 叢集： 

```console
azdata bdc config init --source aks-dev-test --target private-bdc-aks --force
```

## <a name="generate-and-config-bdc-custom-deployment-profile"></a>產生並設定 BDC 自訂部署設定檔： 
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

## <a name="deploy-bdc-in-aks-private-cluster"></a>在 AKS 私人叢集中部署 BDC

```console
export AZDATA_USERNAME=<your bdcadmin username>
export AZDATA_PASSWORD=< your bdcadmin password>

azdata bdc create --config-profile private-bdc-aks --accept-eula yes
```

## <a name="use-third-party-firewall-instead-of-azure-firewall"></a>使用第三方防火牆，而不是 Azure 防火牆

使用第三方防火牆限制使用 AKS 私人叢集部署 BDC 時的連出流量。 如需範例，請參閱 [Azure Marketplace 防火牆](https://azuremarketplace.microsoft.com/marketplace/apps?search=firewall&page=1)。 第三方防火牆可在具有更符合規範之設定的私人部署解決方案中使用。 防火牆應該提供下列網路規則：

* 所有 [AKS 叢集的必要連出網路規則與 FQDN](/azure/aks/limit-egress-traffic#required-outbound-network-rules-and-fqdns-for-aks-clusters) 以及所有萬用字元 HTTP/HTTPS 端點與相依性，這些可能會根據限定詞的數目與您的實際需求而隨著您的 AKS 叢集有所不同。
* [這裡](/azure/aks/limit-egress-traffic#azure-global-required-network-rules)所提及的 Azure 全球必要網路規則/FQDN/應用程式規則。
* [這裡](/azure/aks/limit-egress-traffic#optional-recommended-fqdn--application-rules-for-aks-clusters)所提及的 AKS 叢集的選用建議 FQDN/應用程式規則。 

請確認如何[在 AKS 私人叢集中管理 BDC](private-manage.md)，然後下一個步驟是[連線到 BDC 叢集](connect-to-big-data-cluster.md)。

請參閱 [GitHub 上的 SQL Server 範例存放庫](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/private-aks)中適用於此案例的自動化指令碼。

## <a name="next-steps"></a>後續步驟

[在 AKS 私人叢集中管理巨量資料叢集](private-manage.md)

[使用 Azure Data Studio 連線到 SQL Server 巨量資料叢集](connect-to-big-data-cluster.md)
