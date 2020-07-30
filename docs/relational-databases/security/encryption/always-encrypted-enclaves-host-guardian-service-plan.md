---
title: 規劃主機守護者服務證明
description: 針對 SQL Server 具有安全記憶體保護區的 Always Encrypted 規劃主機守護者服務證明。
ms.custom: ''
ms.date: 10/12/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: rpsqrd
ms.author: ryanpu
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 425fdeb973918744b4aeab423629939a2a84f97a
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411373"
---
# <a name="plan-for-host-guardian-service-attestation"></a>規劃主機守護者服務證明

[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

當您使用[具有安全記憶體保護區的 Always Encrypted](always-encrypted-enclaves.md) 時，請確定用戶端應用程式正在與 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 處理序中可信任的記憶體保護區通訊。 針對虛擬化型安全性 (VBS) 記憶體保護區，此需求包括同時驗證記憶體保護區內的程式碼有效，且裝載 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 的電腦值得信任。 遠端證明藉由引進協力廠商來驗證 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 電腦的身分識別 (或設定) 來達到此目標。 在 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 可以使用記憶體保護區執行查詢之前，必須提供其作業環境的相關資訊給證明服務，以取得健康情況憑證。 此健康情況憑證接著會傳送到用戶端，然後由用戶端透過證明服務獨立驗證其真確性。 一旦用戶端信任健康情況憑證，就能確定正在與可信任的 VBS 記憶體保護區通訊，並接著發出使用該記憶體保護區的查詢。

Windows Server 2019 中主機守護者服務 (HGS) 角色為具有 VBS 記憶體保護區的 Always Encrypted 提供遠端證明功能。
本文將引導您完成部署前的決策和需求，以使用具有 VBS 記憶體保護區的 Always Encrypted 和 HGS 證明。

## <a name="architecture-overview"></a>架構概觀

主機守護者服務 (HGS) 是在 Windows Server 2019 上執行的叢集 Web 服務。
在一般部署中，會有 1-3 部 HGS 伺服器、至少一部執行 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 的電腦，以及一部執行用戶端應用程式或工具 (例如 SQL Server Management Studio) 的電腦。
由於 HGS 負責判斷哪些執行 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 的電腦值得信任，因此需要與所保護的 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 執行個體進行實體和邏輯隔離。
如果可以存取 HGS 和 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 電腦的系統管理員相同，則可能將證明服務設定為允許惡意電腦執行 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]，以便入侵 VBS 記憶體保護區。

### <a name="hgs-domain"></a>HGS 網域

HGS 安裝程式會自動為 HGS 伺服器、容錯移轉叢集資源和系統管理員帳戶建立新的 Active Directory 網域。

執行 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 的電腦不需要加入網域，但如果已加入，則應該與 HGS 伺服器所使用的網域不同。

### <a name="high-availability"></a>高可用性

HGS 功能會自動安裝和設定容錯移轉叢集。
在生產環境中，建議使用三部 HGS 伺服器以獲得高可用性。 如需叢集仲裁判斷方式及替代設定 (包括具有外部見證的兩個節點叢集) 的詳細資料，請參閱[容錯移轉叢集文件](https://docs.microsoft.com/windows-server/failover-clustering/manage-cluster-quorum)。

HGS 節點之間不需要共用存放裝置。 證明資料庫的複本會儲存在每部 HGS 伺服器上，並由叢集服務透過網路自動複寫。

### <a name="network-connectivity"></a>網路連線

SQL 用戶端和 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 都必須能夠透過 HTTP 與 HGS 通訊。
使用 TLS 憑證設定 HGS，以加密 SQL 用戶端與 HGS 之間的所有通訊，以及 SQL Server 和 HGS 之間的所有通訊。
這項設定有助於防止攔截式攻擊，並確保您會與正確的 HGS 伺服器通訊。

HGS 伺服器需要在叢集中的每個節點之間進行連線，以確保證明服務資料庫保持同步。容錯移轉叢集最佳做法是連接一個網路上的 HGS 節點進行叢集通訊，並使用不同的網路讓其他用戶端與 HGS 通訊。

### <a name="attestation-modes"></a>證明模式

當執行 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 的電腦嘗試使用 HGS 進行證明時，會先詢問 HGS 應該如何證明。
HGS 支援兩種證明模式，可搭配 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 使用：

| 證明模式 | 說明 |
| ---------------- | ------- |
| TPM | 信賴平台模組 (TPM) 證明提供有關使用 HGS 進行電腦身分識別和完整性證明的最強保證。 執行 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 的電腦必須已安裝 TPM 2.0 版。 每個 TPM 晶片都包含唯一且固定的身分識別 (簽署金鑰)，可用來識別特定電腦。 TPM 也會測量電腦的開機程序，並將安全性敏感測量雜湊儲存在作業系統可讀取但無法修改的平台控制暫存器 (PCR) 中。 在證明期間會使用這些測量來提供密碼編譯證明，以證實電腦是在其所宣告的安全性設定中。 |
| 主機金鑰 | 主機金鑰證明是較簡單的證明形式，只會使用非對稱金鑰組來驗證電腦的身分識別。 私密金鑰會儲存在執行 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 的電腦上，而公開金鑰則提供給 HGS。 不會測量電腦的安全性設定，且執行 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 的電腦上也不需要 TPM 2.0 晶片。 請務必保護安裝在 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 電腦上的私密金鑰，因為取得此金鑰的任何人都可以模擬合法的 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 電腦及在 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 內執行的 VBS 記憶體保護區。 |

一般來說，以下是我們的建議：

- 針對**實體生產伺服器**，建議使用 TPM 證明來取得它所提供的其他保證。
- 針對**虛擬生產伺服器**，建議使用主機金鑰證明，因為大部分的虛擬機器都沒有虛擬 TPM 或安全開機。 如果您使用增強安全性的 VM (例如[內部部署受防護的 VM](https://aka.ms/shieldedvms))，您可以選擇使用 TPM 模式。 在所有虛擬化部署中，證明程序只會分析您的 VM 環境，而不是 VM 底下的虛擬化平台。
- 針對**開發/測試案例**，建議使用主機金鑰證明，因為它較容易設定。

### <a name="trust-model"></a>信任模型

在 VBS 記憶體保護區信任模型中，加密的查詢和資料會在以軟體為基礎記憶體保護區中進行評估，以保護免於遭受來自主機 OS 的攻擊。
此記憶體保護區的存取權會受到 Hypervisor 的保護，其保護方式就像是同一部電腦上執行的兩部虛擬機器無法相互存取記憶體一樣。
為了讓用戶端信任其正在與合法的 VBS 執行個體通訊，您必須使用 TPM 型證明在 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 電腦上建立硬體根信任。
開機程序期間所擷取 TPM 測量包含 VBS 執行個體的唯一識別金鑰，以確保健康情況憑證只在該確切電腦上有效。
此外，當執行 VBS 的電腦上可以使用 TPM 時，VBS 識別金鑰的私密部分會受到 TPM 的保護，以防止任何人嘗試模擬該 VBS 執行個體。

TPM 證明需要安全開機，以確保 UEFI 載入 Microsoft 簽署的合法開機載入器，且不會有 Rootkit 攔截 Hypervisor 開機程序。
此外，預設必須有 IOMMU 裝置，以確保具有直接記憶體存取的任何硬體裝置都無法檢查或修改記憶體保護區記憶體。

這些保護措施全都假設執行 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 的電腦是實體電腦。
如果您將執行 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 的電腦虛擬化，則無法再保證 VM 的記憶體不會受 Hypervisor 或 Hypervisor 管理員檢查。例如，Hypervisor 管理員可以傾印 VM 的記憶體，並取得記憶體保護區中查詢和資料的純文字版本存取權。
同樣地，即使 VM 具有虛擬 TPM，也只能測量 VM 作業系統和開機環境的狀態和完整性。
無法測量控制 VM 的 Hypervisor 狀態。

不過，即使 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 已虛擬化，記憶體保護區還是會受到保護，以免於遭受來自 VM 作業系統內部的攻擊。
如果您信任 Hypervisor 或雲端提供者，且主要是擔心資料庫管理員和 OS 管理員對敏感性資料的攻擊，則虛擬化 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 可能會符合您的需求。

同樣地，在執行 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 的電腦上未安裝 TPM 2.0 模組的情況下，或在安全性不重要的開發/測試案例中，主機金鑰證明仍然非常有用。
您仍然可以使用上述的許多安全性功能 (包括安全開機和 TPM 1.2 模組)，以進一步保護 VBS 和整體作業系統。
但由於 HGS 無法驗證電腦是否真的使用主機金鑰證明來啟用這些設定，因此用戶端無法確定主機是否真的使用所有可用保護措施。

## <a name="prerequisites"></a>Prerequisites

### <a name="hgs-server-prerequisites"></a>HGS 伺服器先決條件

執行主機守護者服務角色的電腦應符合下列需求：

| 元件 | 需求 |
| --------- | ----------- |
| 作業系統 | Windows Server 2019 Standard 或 Datacenter Edition |
| CPU | 2 核心 (最小值)，4 核心 (建議) |
| RAM | 8 GB (最小值) |
| NIC | 建議使用 2 個使用靜態 IP 的 NIC (1 個用於叢集流量，1 個用於 HGS 服務) |

由於需要加密和解密的動作數目，因此 HGS 是受限於 CPU 的角色。
使用搭載密碼編譯加速功能的新式處理器將會改善 HGS 效能。
證明資料的儲存空間需求很小，每個唯一電腦證明的範圍介於 10 KB 到 1 MB 之間。

在您開始之前，請勿將 HGS 電腦加入網域。

### <a name="ssnoversion-md-computer-prerequisites"></a>[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 電腦先決條件

執行 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 的電腦必須同時符合[安裝 SQL Server 的需求](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)和 [Hyper-V 硬體需求](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/hyper-v-requirements#hardware-requirements)。

這些需求包括：

- [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] 或更新版本
- Windows 10 企業版 1809 版或更新版本；或 Windows Server 2019 Datacenter Edition。 其他版本的 Windows 10 和 Windows Server 不支援使用 HGS 進行證明。
- 虛擬化技術的 CPU 支援：
  - 搭載延伸分頁表的 Intel VT-x。
  - 搭載快速虛擬化索引處理的 AMD-V。
  - 如果您是在 VM 中執行 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]，則 Hypervisor 和實體 CPU 必須提供巢狀虛擬化功能。 如需在 VM 中執行 VBS 記憶體保護區時的保證資訊，請參閱[＜信任模型＞](#trust-model)一節。
    - 在 Hyper-V 2016 或更新版本上，[於 VM 處理器上啟用巢狀虛擬化延伸模組](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization#configure-nested-virtualization)。
    - 在 Azure 中，選取支援巢狀虛擬化的 VM 大小。 所有 v3 系列 VM 都支援巢狀虛擬化，例如 Dv3 與 Ev3。 請參閱[建立可使用巢狀功能的 Azure VM](/azure/virtual-machines/windows/nested-virtualization#create-a-nesting-capable-azure-vm) \(部分機器翻譯\)。
    - 在 VMWare vSphere 6.7 或更新版本上，針對 VM 啟用虛擬化型安全性支援，如 [VMware 文件](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.vm_admin.doc/GUID-C2E78F3E-9DE2-44DB-9B0A-11440800AADD.html) \(英文\) 所述。
    - 其他 Hypervisor 和公用雲端可能還支援啟用具有 VBS 記憶體保護區的 Always Encrypted 巢狀虛擬化功能。 如需相容性和設定指示，請參閱虛擬化解決方案文件。
- 如果打算使用 TPM 證明，您必須備妥 TPM 2.0 rev 1.16 晶片，以在伺服器中使用。 目前，HGS 證明無法搭配 TPM 2.0 rev 1.38 晶片使用。 此外，TPM 必須具備有效的簽署金鑰憑證。

## <a name="devtest-environment-considerations"></a>開發/測試環境考量

如果您在開發或測試環境中使用具有 VBS 記憶體保護區的 Always Encrypted，且執行 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 的電腦不需要高可用性或強式保護，您可以進行下列任何或所有讓步來簡化部署：

- 只部署一個 HGS 節點。 即使 HGS 安裝容錯移轉叢集，但如果高可用性並不重要，您就不需要新增其他節點。
- 使用主機金鑰模式而不是 TPM 模式，以獲得更簡單的設定體驗。
- 將 HGS 和/或 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 虛擬化以節省實體資源。
- 執行 SSMS 或其他工具，以在與 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 相同電腦上設定具有安全記憶體保護區的 Always Encrypted。 這會將資料行主要金鑰保留在與 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 相同電腦上，因此請勿在生產環境中執行這項操作。

## <a name="next-steps"></a>後續步驟

- [部署 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]](./always-encrypted-enclaves-host-guardian-service-deploy.md) 的主機守護者服務
