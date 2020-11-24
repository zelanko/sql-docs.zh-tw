---
title: 在 Azure Kubernetes Service (AKS) 上以 Active Directory 部署 - 教學課程
titleSuffix: SQL Server Big Data Cluster
description: 了解如何在 Azure Kubernetes Service (AKS) 上以 AD 模式部署 SQL Server 巨量資料叢集。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 11/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b24a83e1647b0e32aff3ce19ad69a0fdc9405b0e
ms.sourcegitcommit: 0f484f32709a414f05562bbaafeca9a9fc57c9ed
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632931"
---
# <a name="tutorial-deploy-sql-server-big-data-clusters-in-ad-mode-on-azure-kubernetes-services-aks"></a>教學課程：在 Azure Kubernetes Service (AKS) 上以 AD 模式部署 SQL Server 巨量資料叢集

本文說明如何使用參考架構以 Active Directory 驗證模式部署 SQL Server 巨量資料叢集 (BDC)。 此參考架構可將您的內部部署 Active Directory Domain Services (AD DS) 延伸到 Azure。 您可以從 [Azure 架構中心](https://github.com/mspnp/identity-reference-architectures/tree/master/adds-extend-domain)使用 [Azure 建置組塊](https://github.com/mspnp/template-building-blocks/wiki/Install-Azure-Building-Blocks)進行部署。

## <a name="prerequisites"></a>Prerequisites

在部署 SQL Server 巨量資料叢集之前，您必須：

* 存取 Azure VM 進行管理。 此 VM 需要存取您將部署 BDC 的 Azure 虛擬網路 (VNet)。 其必須位於相同的 VNet 上，或位於[對等互連的 VNet](/azure/virtual-network/virtual-network-manage-peering) 上。
* 在管理 VM 上[安裝巨量資料工具](deploy-big-data-tools.md)。
* 準備在您的內部部署 AD 控制器中以 [Active Directory 驗證模式](active-directory-prerequisites.md)部署叢集。

## <a name="create-aks-subnet"></a>建立 AKS 子網路

1. 設定環境變數

   ```console
   export REGION_NAME=< your Azure Region >
   export RESOURCE_GROUP=<your resource group >
   export SUBNET_NAME=aks-subnet
   export VNet_NAME= adds-vnet
   export AKS_NAME= <your aks cluster name>
   ```

1. 建立 AKS 子網路

   ```console
   SUBNET_ID=$(az network vnet subnet show \
    --resource-group $RESOURCE_GROUP \
    --vnet-name $VNet_NAME \
    --name $SUBNET_NAME \
    --query id -o tsv)
   ```

下列螢幕擷取畫面顯示如何規劃位於架構中 VNet 的子網路。

:::image type="content" source="media/active-directory-deployment-aks/ad-in-aks-diagram.png" alt-text="具有 AD 和 SQL Server 巨量資料叢集的 AKS 叢集":::

## <a name="create-an-aks-private-cluster"></a>建立 AKS 私人叢集

您可以使用下列命令來部署 AKS 私人叢集。 如果不需要私人叢集，請在命令中移除 `--enable-private-cluster` 參數。 如需任何其他需求的詳細資訊，請參閱[如何部署 Azure Kubernetes 叢集 (AKS)](/azure/aks/tutorial-kubernetes-deploy-cluster)。

```azurecli
az aks create \
    --resource-group $RESOURCE_GROUP \
    --name $AKS_NAME \
    --load-balancer-sku standard \
    --enable-private-cluster \
    --network-plugin azure \
    --vnet-subnet-id $SUBNET_ID \
    --docker-bridge-address 172.17.0.1/16 \
    --dns-service-ip 10.3.0.10 \
    --service-cidr 10.3.0.0/24 \
    --node-vm-size Standard_D13_v2 \
    --node-count 2 \
    --generate-ssh-keys
```

部署 AKS 叢集之後，請[連線到 AKS 叢集](/azure/aks/tutorial-kubernetes-deploy-cluster#connect-to-cluster-using-kubectl)。

## <a name="verify-reverse-dns-entry-for-domain-controller"></a>確認網域控制站的反向 DNS 項目

在 AKS 叢集中以 AD 模式啟動 BDC 部署之前，請確認網域控制站本身已在 DNS 伺服器中同時註冊 **A 記錄** 和 **PTR 記錄** (反向 DNS 項目)。

若要確認這項設定，請執行 `nslookup` 命令，或執行 [PowerShell 指令碼](troubleshoot-ad-reverse-lookup-zone.md)，以確認是否已設定反向 DNS 項目 (PTR 記錄)。

## <a name="create-bdc-deployment-profile"></a>建立 BDC 部署設定檔

下列命令會建立一個部署設定檔：

```console
azdata bdc config init --source kubeadm-prod  --target bdc-ad-aks
```

使用下列命令來設定部署設定檔的參數。

### <a name="controljson"></a>control.json

```console
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.storage.data.className=default"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.storage.logs.className=default"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.endpoints[1].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.endpoints[0].dnsName=controller.contoso.com"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.endpoints[1].dnsName=proxys.contoso.com"

# security settings 
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=com"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.dnsIpAddresses=[\"192.168.0.4\"]"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.domainControllerFullyQualifiedDns=[\"ad1.contoso.com\"]"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.domainDnsName=contoso.com"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.clusterUsers=[\"bdcusersgroup\"]"
```

### <a name="bdcjson"></a>bdc.json

```console
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[0].dnsName=master.contoso.com"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[1].dnsName=mastersec.contoso.com"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[1].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].dnsName=gateway.contoso.com"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].dnsName=approxy.contoso.com"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].serviceType=NodePort"
```

## <a name="initiate-deployment"></a>起始部署

下列命令會起始 BDC 部署：

```console
azdata bdc create --config-profile bdc-ad-aks --accept-eula yes
```

## <a name="next-steps"></a>後續步驟

[使用 Azure Data Studio 連線到 SQL Server 巨量資料叢集](connect-to-big-data-cluster.md)

[教學課程：將範例資料載入 SQL Server 巨量資料叢集](tutorial-load-sample-data.md)