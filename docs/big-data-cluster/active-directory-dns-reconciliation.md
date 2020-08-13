---
title: 巨量資料叢集部署中的 Active Directory 與 Kubernetes DNS 協調
description: 管理巨量資料叢集存取
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/06/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 411d713734db080b036a98bd18b0618326dbd70f
ms.sourcegitcommit: dacd9b6f90e6772a778a3235fb69412662572d02
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2020
ms.locfileid: "86279424"
---
# <a name="active-directory-and-kubernetes-dns-reconciliation-in-big-data-clusters-deployments"></a>巨量資料叢集部署中的 Active Directory 與 Kubernetes DNS 協調

本文描述在部署巨量資料叢集 (BDC) 時處理 Active Directory 整合的一些挑戰和解決方案。

## <a name="overview"></a>概觀

在沒有 Active Directory 整合的情況下部署巨量資料叢集時，我們會依賴 [Kubernetes CoreDNS](https://kubernetes.io/docs/tasks/administer-cluster/coredns/) 服務來進行內部 DNS 解析。 Kubernetes 使用內部網域，例如 `<namespace>.svc.cluster.local`。 其會使用此網域中的名稱，在 DNS 伺服器中建立 A (正向對應) 和 PTR (反向對應) 記錄。

不過，啟用 Active Directory 模式時，新網域即會出現一組自己的 DNS 伺服器。 在內部名稱解析期間，這可能會導致不確定要使用哪組 DNS 伺服器進行正向和反向對應。

## <a name="challenges"></a>挑戰

* 當部署新的 Kubernetes Pod 時，必須在這兩組 DNS 伺服器中新增 DNS 項目。 Kubernetes 會負責在其 CoreDNS 中記錄項目，但 BDC 部署工作流程會負責在 Active Directory 網域控制站 DNS 伺服器中新增所需的項目。 同樣地，刪除 BDC 叢集之後，工作流程必須確保移除這些項目。
* Active Directory DNS 伺服器位於 Kubernetes 叢集外部。 但 BDC 在 Kubernetes 內有自己的 IP 空間，且無法為外部 DNS 伺服器中的 IP 空間建立記錄，因為在叢集界限外看不到此 IP 空間。
* 當 Kubernetes 叢集中發生容錯移轉事件時，也必須更新 AD DNS 伺服器中的記錄。
* 除了 Pod 名稱之外，也必須透過 AD 網域名稱查閱來定址 Kubernetes 服務名稱。 這會在 Active Directory DNS 中帶來額外的挑戰，因為一個服務名稱可能會對應至多個 Pod IP 位址。
* 組織的 Active Directory DNS 伺服器中記錄更新傳播和複寫延遲可能很明顯，並超過 BDC 管理工作流程的控制。 這可能會在部署和容錯移轉時立即影響 BDC 功能。 相反地，Kubernetes CoreDNS 因其位置而更快速且有效率。

## <a name="solution"></a>解決方法

為了解決上述挑戰，在 BDC 中實作的解決方案包含在 BDC 命名空間內所管理新內部 CoreDNS 服務。 這是 BDC 命名空間中 Pod 為了進行名稱解析所連絡的唯一 DNS 服務。 多個網域的複雜性會隱藏在新 CoreDNS 服務後方。

例如，在下列圖表中，Pod 使用 BDC CoreDNS 伺服器來解析名稱。 Pod 不會直接與 Kubernetes CoreDNS 伺服器或 AD DNS 伺服器互動。 

:::image type="content" source="media/active-directory-dns-reconciliation/bdc-ad-dns-reconciliation.png" alt-text="Pod 連線到其所屬命名空間中的 CoreDNS 伺服器":::

以下是一些實作詳細資料，其說明此設計如何在 BDC 中運作：

### <a name="centralized-management-of-multiple-domains"></a>集中管理多個網域

名稱查閱所發生的複雜性，會以集中方式保持隱藏在內部 DNS 服務後方。 這可避免將多個網域的管理負擔放在個別 Pod 上，並可簡化設計。

### <a name="no-records-for-internal-pods-in-external-dns-servers"></a>外部 DNS 伺服器中沒有內部 Pod 的記錄

由於此設計原則，BDC 將不需要在外部 DNS 伺服器其 Kubernetes IP 空間中建立及管理 Pod 的 A 和 PTR 記錄。

### <a name="no-duplication-of-records"></a>不重複記錄

內部 DNS 記錄位於多個位置。 這些記錄的唯一儲存位置是 Kubernetes CoreDNS。 BDC 內部 CoreDNS 會執行計算重寫，並將 DNS 查詢轉送至 Kubernetes CoreDNS。

### <a name="computational-rewriting"></a>計算重寫

由於 BDC 不會儲存任何記錄，因此 BDC 會負責將名稱具有 AD 網域的傳入正向對應查詢，轉譯為具有 Kubernetes 網域的名稱，並將此查詢轉送至 Kubernetes CoreDNS。
例如，`compute-0-0.contoso.local` 的傳入查詢會重寫至 `compute-0-0.compute-0-svc.contoso.svc.cluster.local`，且此要求會轉送至 Kubernetes CoreDNS。
在反向對應的情況下，要求會使用相同的內部 IP 轉送至 Kubernetes CoreDNS，並從該處將回應重寫為 AD 網域名稱，再回應給用戶端。

### <a name="simplicity-in-pod-configurations"></a>簡單的 Pod 設定

由於所有 BDC Pod 的 /etc/resolv.conf 中只會參考內部 BDC CoreDNS，因此這會簡化 Pod 中的網路檢視。 複雜性會改為隱藏在內部 CoreDNS 中。

### <a name="static-and-reliable-ip-address-for-dns-service"></a>DNS 服務的靜態和可靠 IP 位址

BDC 所部署 CoreDNS 服務會有註冊的靜態內部 IP，其可從所有 Pod 存取。 這可確保 /etc/resolv.conf 中的值不需要更新。

### <a name="service-load-balance-management-is-retained-by-kubernetes"></a>服務負載平衡管理會維持由 Kubernetes 進行

當服務 (而不是個別 Pod) 進行查閱時，仍會進入 Kubernetes CoreDNS，因此 BDC 不會負責為 AD 網域特別實作負載平衡。

例如，如果正向對應要求是針對 `compute-0-svc.contoso.local`，則會將其重寫至 ` compute-0-svc.contoso.svc.cluster`.local。 此要求會轉送至 Kubernetes CoreDNS，並在此進行負載平衡。 回應會是多個計算集區執行個體 (Pod 複本) 其中一個的 IP 位址。

### <a name="scalability"></a>延展性

由於 BDC 不會儲存任何記錄，因此可調整內部 BDC CoreDNS，而不需要在多個複本之間保留狀態和複寫記錄。 如果 DNS 記錄會儲存在 BDC 中，則在所有 Pod 之間複寫狀態也必須處理 BDC。

### <a name="externally-visible-service-entries-stay-in-ad-dns"></a>外部可見的服務項目會保留在 AD DNS 中

針對必須提供 Kubernetes 叢集外部用戶端存取的服務端點，則會在部署 BDC 時，於 AD DNS 伺服器中建立 DNS 項目。 使用者會輸入要透過部署組態設定檔註冊的 DNS 名稱。

### <a name="self-deprovisioning"></a>自我取消佈建

刪除 BDC 之後，不需要在取消佈建叢集時執行任何其他動態工作來刪除 DNS 項目。 遠端 Active Directory DNS 中唯一需要清除的項目是外部服務項目，且其數目是固定的。 內部 DNS 項目會自動隨叢集移除。

## <a name="next-steps"></a>後續步驟

- [以 Active Directory 模式部署 SQL Server 巨量資料叢集](deploy-active-directory.md)
- [以 Active Directory 模式管理巨量資料叢集存取](active-directory-objects.md)
- [在相同的 Active Directory 網域中部署多個 SQL Server 巨量資料叢集](active-directory-deployment-background.md)
