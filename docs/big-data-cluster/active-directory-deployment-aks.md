---
title: 在 Azure Kubernetes Service (AKS) 上以 Active Directory 部署
titleSuffix: SQL Server Big Data Cluster
description: 說明如何在 Azure Kubernetes Service (AKS) 上，以 AD 模式部署 SQL Server 巨量資料叢集的概念和規劃資訊。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 11/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3f6b3ce5f6a594e5be385ee1f7ea7d1c03c1f92a
ms.sourcegitcommit: 0f484f32709a414f05562bbaafeca9a9fc57c9ed
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632936"
---
# <a name="deploy-sql-server-big-data-clusters-in-ad-mode-on-azure-kubernetes-services-aks"></a>在 Azure Kubernetes Service (AKS) 上以 AD 模式部署 SQL Server 巨量資料叢集

SQL Server 巨量資料叢集支援 [Active Directory (AD) 部署模式](deploy-active-directory.md)，以進行 **身分識別與存取管理 (IAM)** 。 因為 SQL Server 不支援 Microsoft 身分識別平台廣泛支援的業界標準通訊協定 (例如 OAuth 2.0 和 OpenID Connect)，所以 **Azure Kubernetes Service (AKS)** 的 IAM 一直充滿挑戰性。  

本文說明如何在 [Azure Kubernetes Service (AKS)](/azure/aks/intro-kubernetes) 中部署時，以 AD 模式部署巨量資料叢集 (BDC)。 

## <a name="architecture-topologies"></a>架構拓撲

**Active Directory Domain Services (AD DS)** 在 Azure 虛擬機器 (VM) 上執行的方式會與在許多內部部署執行個體[相同](/windows-server/identity/ad-ds/deploy/virtual-dc/adds-on-azure-vm)。  在 Azure 中升級新的網域控制站之後，設定虛擬網路的主要和次要 DNS 伺服器，將任何內部部署 DNS 伺服器降級為第三個或之後的伺服器。 AD 驗證可讓 Linux 上已加入網域的用戶端，使用其網域認證和 Kerberos 通訊協定[向 SQL Server 進行驗證](../linux/sql-server-linux-active-directory-auth-overview.md)。

有幾種方式可以在 AKS 中以 AD 模式部署 BDC。  本文介紹兩種方法，可讓您更輕鬆地實作及整合現有的企業級架構：

* **將您的內部部署 Active Directory 網域擴充至 Azure。** 此方法[允許 Active Directory 環境](/azure/architecture/reference-architectures/identity/adds-extend-domain)在 Azure 上使用 Active Directory Domain Services (AD DS) 提供分散式驗證服務。 您會複寫內部部署 Active Directory Domain Services (AD DS)，以降低將驗證要求從雲端傳回內部部署 AD DS 所造成的延遲。 此解決方案的一般使用案例是，當應用程式部分裝載於內部部署且部分裝載於 Azure 中，而您的驗證要求需要來回移動時。

   [在此參考架構中](https://github.com/mspnp/identity-reference-architectures/tree/master/adds-extend-domain)了解如何逐步部署這個解決方案。

* **將 Active Directory Domain Services (AD DS) 資源樹系延伸到 Azure。** 在此架構中，您會在 Azure 中建立內部部署 AD 樹系所信任的新網域。 此架構顯示[從 Azure 中網域到內部部署樹系的單向信任](/azure/architecture/reference-architectures/identity/adds-forest)。

   信任可讓內部部署使用者存取 Azure 中的網域資源。 [在此參考架構中](https://github.com/mspnp/identity-reference-architectures/tree/master/adds-forest)了解如何逐步部署這個解決方案。

上述的參考架構可讓您建立登陸區域，其中包含要從頭開始部署的所有資源，或根據現有架構的任何其他因應措施。 除了這些參考架構以外，您還應該在 AKS 叢集中，將 BDC 部署到保留在目標 VNet 或對等互連 VNet 中的個別子網路上。

下圖代表一般的架構：

:::image type="content" source="media/active-directory-deployment-aks/ad-in-aks-diagram.png" alt-text="具有 AD 和 SQL Server 巨量資料叢集的 AKS 叢集":::

## <a name="recommendations"></a>建議

下列建議適用於 AKS 上以 AD 模式進行的大部分 BDC 部署。 每個元件中都會提及可用的選項，以提供與企業級架構更緊密整合的指引。

### <a name="networking-recommendations"></a>網路功能的建議

可以使用一些主要元件將您的內部部署環境連線到 Azure：

* **Azure VPN 閘道**：VPN 閘道是特定的虛擬網路閘道類型，可透過公用網際網路在 Azure 虛擬網路與內部部署位置之間傳送加密流量。 您將同時使用 Azure 虛擬網路閘道和本機虛擬網路閘道。 如需設定方式的詳細資訊，請參閱[什麼是 VPN 閘道](/azure/vpn-gateway/vpn-gateway-about-vpngateways)。
* **Azure ExpressRoute**：ExpressRoute 連線不會經過公用網際網路，相較於透過網際網路的一般連線，其提供了更高的安全性、可靠性和速度，以及更低的延遲。 選擇的連線選項將會影響解決方案的延遲、效能及 SLA 等級 (視 SKU 而定)。 如需特定資訊，請參閱[關於 ExpressRoute 虛擬網路閘道](/azure/expressroute/expressroute-about-virtual-network-gateways)。

大部分的客戶都使用跳躍箱或 [Azure Bastion](/azure/bastion/bastion-overview) 來存取其他 Azure 基礎結構。 **Azure Private Link** 可讓您透過虛擬網路中的私人端點安全地存取各項 Azure PaaS 服務，包括此案例中的 AKS，以及其他 Azure 裝載的服務。 虛擬網路與服務間的流量會透過 Microsoft 骨幹網路周遊，以降低資料公開到公用網際網路的風險。 您也可以在虛擬網路中建立自己的 Private Link 服務，並私下提供給您的客戶。

### <a name="active-directory-and-azure-recommendation"></a>Active Directory 與 Azure 建議

內部部署 AD DS 會儲存使用者帳戶的相關資訊，並讓相同網路上的其他授權使用者，透過驗證與安全性界限中所含使用者、電腦、應用程式或其他資源建立關聯的身分識別，存取這項資訊。 在大部分的混合式案例中，使用者驗證會透過內部部署 AD DS 環境的 VPN 閘道或 ExpressRoute 連線來執行。  

如果是以 AD 模式進行的 BDC 部署，[整合內部部署 Active Directory 與 Azure](/azure/architecture/reference-architectures/identity/) 的解決方案必須具備下列必要條件：

* [AD 帳戶具有特定權限](active-directory-prerequisites.md)，可在內部部署 Active Directory 中所提供的組織單位 (OU) 內建立使用者、群組及電腦帳戶。
* 用來[解析內部 DNS](active-directory-dns-reconciliation.md) 的 DNS 伺服器。 其必須同時包含 DNS 伺服器中，使用此網域內名稱的 **A (正向對應)** 和 **PTR (反向對應) 記錄**。 請指定 BDC 部署設定檔中的網域 DNS 設定。  

## <a name="next-steps"></a>後續步驟

[教學課程：在 Azure Kubernetes Service (AKS) 上以 AD 模式部署 SQL Server 巨量資料叢集](active-directory-deployment-aks-tutorial.md)
