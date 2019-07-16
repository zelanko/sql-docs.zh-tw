---
title: 在 Linux 上設定多個子網路 Always On 可用性群組和容錯移轉叢集執行個體
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/01/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 2fc848c30af32e5ff2a81ebadf4378b75ff5a521
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077593"
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>設定子網路的多個 Always On 可用性群組和容錯移轉叢集執行個體

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

當 Alwayson 可用性群組 (AG) 或容錯移轉叢集執行個體 (FCI) 跨越多個站台的每個站台通常都有它自己的網路。 這通常表示每個網站有它自己的 IP 位址。 比方說，站台 A 的位址會以 192.168.1 開始。*x*且站台 B 位址開頭 192.168.2。*x*，其中*x*是對伺服器是唯一的 IP 位址的一部分。 而不需要某種形式的路由在網路層中，這些伺服器將無法彼此通訊。 有兩種方式來處理此案例： 設定網路的橋接兩個不同的子網路，又稱為 VLAN，或設定子網路之間的路由。

## <a name="vlan-based-solution"></a>VLAN 為基礎的解決方案
 
**必要條件**:VLAN 架構的解決方案，參與 AG 或 FCI 的每一部伺服器需要兩張網路卡 (Nic)，以取得適當可用性 （雙重連接埠 NIC 會是單一實體伺服器上的失敗點），以便它可以將指派其原生的子網路，以及一個上的 IP 位址在 VLAN。 這是任何其他網路需求，例如 iSCSI，也需要它自己的網路之外。

AG 或 FCI 的 IP 位址建立 VLAN 上執行。 在下列範例中，VLAN 有 192.168.3 的子網路。*x*，因此建立 AG 或 FCI 的 IP 位址是 192.168.3.104。 其他不需要設定，因為沒有單一 IP 位址指派給 FCI 的 AG。

![](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>設定 pacemaker

在 Windows 世界中，Windows Server 容錯移轉叢集 (WSFC)，以原生方式支援多個子網路，並會處理透過 IP 位址上 OR 相依性的多個 IP 位址。 在 Linux 上，沒有 OR 相依性，但是沒有原生 pacemaker，達到適當的多重子網路的方式如下所示。 您無法直接修改資源使用一般的 Pacemaker 命令列來這樣做。 您需要修改叢集資訊基底 (CIB)。 CIB 是 Pacemaker 組態 XML 檔案。

![](./media/sql-server-linux-configure-multiple-subnet/image2.png)

### <a name="update-the-cib"></a>更新 CIB

1.  匯出 CIB。

    **Red Hat Enterprise Linux (RHEL) 和 Ubuntu**

    ```bash
    sudo pcs cluster cib <filename>
    ```

    **SUSE Linux Enterprise Server (SLES)**

    ```bash
    sudo cibadmin -Q > <filename>
    ```

    何處*filename*是您想要呼叫 CIB 的名稱。

2.  編輯所產生的檔案。 尋找`<resources>`一節。 您會看到所建立的 AG 或 FCI 的各種資源。 找出相關聯的 IP 位址。 新增`<instance attributes>`區段取代為高於或低於現有的帳戶，第二個 IP 位址的資訊之前`<operations>`。 它會類似於下列語法：

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    何處*NameForAttribute*是唯一的名稱，這個屬性，如*分數*是指派給屬性，必須是高於主要子網路，數字*RuleName*的規則，名稱*ExpressionName*是運算式的名稱*NodeNameInSubnet2*是另一個子網路，在節點名稱*NameForSecondIP*是名稱的第二個 IP 位址，與相關聯*IPAddress*是第二個子網路，IP 位址*NameForSecondIPNetmask*是與網路遮罩，相關聯的名稱和*Netmask*是第二個子網路的網路遮罩。
    
    以下顯示的範例。
    
    ```xml
    <instance attributes id="Node3-2nd-IP" score="2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node" attribute="\#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet-2" name="ip" value="192.168.2.102"/>
        <nvpair id="Netmask-For-IP2" name="cidr\_netmask" value="24" />
    </instance attributes>
    ```

3.  匯入修改過的 CIB 並重新設定 Pacemaker。

    **RHEL/Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    何處*filename*是修改過的 IP 位址資訊 CIB 檔案的名稱。

### <a name="check-and-verify-failover"></a>請檢查並確認容錯移轉

1.  CIB 順利套用更新的設定之後，ping pacemaker 的 IP 位址資源相關聯的 DNS 名稱。 它應該會反映目前裝載的 AG 或 FCI 的子網路相關聯的 IP 位址。
2.  無法另一個子網路 FCI 的 AG。
3.  AG 或 FCI 完全上線後，偵測相關聯的 IP 位址的 DNS 名稱。 它應該會反映在第二個子網路的 IP 位址。
4.  如有需要，請回到原始的子網路中失敗的 AG 或 FCI。
