---
title: 設定多重子網路可用性群組與 FCI (Linux)
description: 了解如何在 Linux 上，針對 SQL Server 設定多個子網路 Always On 可用性群組和容錯移轉叢集執行個體 (FCI)。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/01/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: af017cf5d36075fdba6de31aa841e980cc20e175
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "76911010"
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>設定多個子網路 Always On 可用性群組和容錯移轉叢集執行個體

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

當 Always On 可用性群組 (AG) 或容錯移轉叢集執行個體 (FCI) 跨越一個以上的網站時，每個網站通常會有自己的網路。 這通常表示每個網站都有自己的 IP 位址。 例如，網站 A 的位址開頭為 192.168.1.*x*，網站 B 的位址開頭為 192.168.2.*x*，其中 *x* 是伺服器唯一的 IP 位址部分。 如果網路層沒有適當的路由，這些伺服器將無法互相通訊。 有兩種方式可以處理這種情況：設定網路來橋接兩個不同的子網路 (稱為 VLAN)，或設定子網路之間的路由。

## <a name="vlan-based-solution"></a>VLAN 型解決方案
 
**必要條件**：針對 VLAN 型的解決方案，參與 AG 或 FCI 的每部伺服器都需要兩張網路卡 (NIC) 以提供適當可用性 (雙重連階埠 NIC 會是實體伺服器上的單一失敗點)，以便在其原生子網路和 VLAN 上指派 IP 位址。 這是網路需求之外的附加項目，例如 iSCSI 也需要自己的網路。

針對 AG 或 FCI 建立的 IP 位址是在 VLAN 上完成。 在下列範例中，VLAN 具有 192.168.3.*x* 的子網路；因此，針對 AG 或 FCI 所建立的 IP 位址是 192.168.3.104。 不需要設定任何額外項目，因為已有單一 IP 位址指派給 AG 或 FCI。

![](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>使用 Pacemaker 設定

在 Windows 的世界中，Windows Server 容錯移轉叢集 (WSFC) 可原生支援多個子網路，並透過對 IP 位址的 OR 相依性來處理多個 IP 位址。 在 Linux 上則沒有 OR 相依性，但有一種方法可以使用 Pacemaker 以原生方式實現適當的多個子網路，如下所示。 若要進行此操作，您無法僅使用一般的 Pacemaker 命令列來修改資源。 您需要修改叢集資訊基底 (CIB)。 CIB 是具有 Pacemaker 設定的 XML 檔案。

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

    其中 *filename* 是您想要呼叫 CIB 的名稱。

2.  編輯已產生的檔案。 尋找 `<resources>` 區段。 您會看到針對 AG 或 FCI 所建立的各種資源。 尋找與 IP 位址建立關聯的資源。 新增 `<instance attributes>` 區段，其中包含第二個 IP 位址的資訊，該位址位於現有的 IP 位置之上或之下，但在 `<operations>` 之前。 其類似於下列語法：

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    其中 *NameForAttribute* 是此屬性的唯一名稱，*Score* 是指派給屬性的數字 (必須高於主要子網路)，*RuleName* 是規則的名稱，*ExpressionName* 是運算式的名稱，*NodeNameInSubnet2* 是另一個子網路中的節點名稱，*NameForSecondIP* 是與第二個 IP 位址建立關聯的名稱，*IPAddress* 是第二個子網路的 IP 位址，*NameForSecondIPNetmask* 是與網路遮罩建立關聯的名稱，*Netmask* 是第二個子網路的網路遮罩。
    
    下列為範例。
    
    ```xml
    <instance attributes id="Node3-2nd-IP" score="2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node" attribute="\#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet-2" name="ip" value="192.168.2.102"/>
        <nvpair id="Netmask-For-IP2" name="cidr\_netmask" value="24" />
    </instance attributes>
    ```

3.  匯入已修改的 CIB 並重新設定 Pacemaker。

    **RHEL/Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    其中 *filename* 是 CIB 檔案的名稱，包含已修改的 IP 位址資訊。

### <a name="check-and-verify-failover"></a>檢查並驗證容錯移轉

1.  成功套用已更新設定的 CIB 之後，請 Ping 與 Pacemaker 中 IP 位址資源建立關聯的 DNS 名稱。 其應該會反映與其目前裝載 AG 或 FCI 之子網路建立關聯的 IP 位址。
2.  將 AG 或 FCI 容錯回復至另一個子網路。
3.  在 AG 或 FCI 完全上線之後，請 Ping 與 IP 位址建立關聯的 DNS 名稱。 其應該會反映第二個子網路中的 IP 位址。
4.  如有需要，將 AG 或 FCI 容錯回復至原始子網路。
