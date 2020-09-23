---
title: 在 Azure Kubernetes Service (AKS) 私人叢集中管理巨量資料叢集 (BDC)
titleSuffix: SQL Server Big Data Cluster
description: 了解如何在 Azure Kubernetes Service (AKS) 私人叢集中管理 SQL Server 巨量資料叢集。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 08/20/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 442f5def7e1378b750460cfc6860e780b1dcfd80
ms.sourcegitcommit: fe5dedb2a43516450696b754e6fafac9f5fdf3cf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/31/2020
ms.locfileid: "89202210"
---
# <a name="manage-big-data-cluster-in-aks-private-cluster"></a>在 AKS 私人叢集中管理巨量資料叢集

此文章說明如何使用在 Azure 中部署的 SQL Server 巨量資料叢集 (BDC) 來管理 Azure Kubernetes Service (AKS) 私人叢集。

如[建立私人叢集](/azure/aks/private-clusters/)中所述，AKS 私人叢集 API 伺服器端點沒有公用 IP 位址。 若要管理 API 伺服器，請使用可存取 AKS 叢集之 Azure 虛擬網路 (VNet) 的 VM。

## <a name="azure-vm---same-vnet"></a>Azure VM - 相同的 VNet

最簡單的方法是在與 AKS 叢集相同的 VNet 中部署 Azure VM。

1. 在與您的 AKS 叢集相同的 VNET 中部署 Azure VM。 這有時稱為 *jumpbox*。
1. 連線到該 VM，並[安裝 SQL Server 2019 巨量資料工具](deployment-guidance.md#install-sql-server-2019-big-data-tools)。

基於安全性目的，您可以針對 API 伺服器授權的 IP 範圍使用 AKS 功能，以限制對 API 伺服器的存取 (在 AKS 控制平面上)。 有限的存取允許特定的 IP 位址，例如 jumpbox VM 或管理 VM，或一群開發人員的 IP 位址範圍，以及防火牆公用前端 IP 位址。

## <a name="other-options"></a>其他選項

使用 jumpbox 的替代方案包括：

* 在不同的網路中使用 VM，並設定連到 VNet 的[虛擬網路對等互連](/azure/virtual-network/virtual-network-peering-overview)。

* [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) 或 [VPN 閘道](/azure/vpn-gateway/vpn-gateway-about-vpngateways)連線。

   [用來連線到私人叢集的選項](/azure/aks/private-clusters#options-for-connecting-to-the-private-cluster)會討論上述每一種方法。

* 如果您的服務是在 [Azure Standard Load Balancer](/azure/aks/load-balancer-standard) 後方執行，則可以針對 [Azure Private Link](/azure/private-link/private-link-service-overview#limitations) 加以啟用。 使用 Azure Private Link，您可以啟用來自其他 Azure VNet 的私人存取。

* 在混合式案例中，您也可以設定 [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) 或 [VPN 閘道](/azure/vpn-gateway/vpn-gateway-about-vpngateways)連線。

## <a name="next-steps"></a>後續步驟

[使用 Azure Data Studio 連線到 SQL Server 巨量資料叢集](connect-to-big-data-cluster.md)