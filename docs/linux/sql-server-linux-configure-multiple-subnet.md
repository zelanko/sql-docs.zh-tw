---
title: "在 Linux 上設定多重子網路 Alwayson 可用性群組和容錯移轉叢集執行個體 |Microsoft 文件"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/1/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: df5182d374e41b68fe35333c6e4ab59714d8241d
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2018
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>設定多重子網路 Alwayson 可用性群組和容錯移轉叢集執行個體

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

當一律在可用性群組 (AG) 或容錯移轉叢集執行個體 (FCI) 跨越一個以上的站台的每個站台通常都有它自己的網路。 這通常表示每個站台有它自己的 IP 位址。 例如，網站 A 的位址 192.168.1 的開頭。*x*和站台 B 位址開頭 192.168.2。*x*，其中*x*是伺服器的唯一的 IP 位址的一部分。 沒有某種路由在網路層的位置，這些伺服器將無法與對方進行通訊。 有兩種方式處理這種狀況： 設定網路等兩個不同的子網路，又稱為 VLAN，或設定子網路間路由。

## <a name="vlan-based-solution"></a>VLAN 為基礎的解決方案
 
**必要條件**： 為 VLAN 架構的解決方案，參與 AG 或 FCI 的每個伺服器需要兩張網路卡 (Nic) （NIC 的雙連接埠會是單一實體伺服器上的失敗點） 的正常可用性，以便將其指派的 IP 位址上其原生的子網路，以及其中一個 vlan。 這是除了任何其他網路的需求，例如 iSCSI，也需要自己的網路。

AG 或 FCI 的 IP 位址建立 VLAN 上執行。 在下列範例中，VLAN 有 192.168.3 的子網路。*x*，因此建立 AG 或 FCI 的 IP 位址是 192.168.3.104。 其他不需要設定，因為沒有單一的 IP 位址指派給 AG 或 FCI。

![](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>Pacemaker 組態

在 Windows 世界中，Windows Server 容錯移轉叢集 (WSFC) 原生支援多個子網路，並會處理透過 IP 位址的 OR 相依性的多個 IP 位址。 在 Linux 上沒有 OR 相依性，但是沒有 Pacemaker，與原生達到適當的多重子網路的方式如下所示。 您無法只使用標準 Pacemaker 命令列來修改資源。 您需要修改叢集資訊基底 (CIB)。 CIB 是 Pacemaker 組態 XML 檔案。

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

    其中*filename*是您想要呼叫 CIB 的名稱。

2.  編輯產生的檔案。 尋找`<resources>`> 一節。 您會看到所建立的 AG 或 FCI 的各種資源。 找出相關聯的 IP 位址。 新增`<instance attributes>`前一節的上方或下方，現有的第二個 IP 位址資訊`<operations>`。 它看起來像下列語法：

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    其中*NameForAttribute*是唯一的名稱，這個屬性，*分數*是指派給屬性，必須高於主要子網路，數字*RuleName*規則名稱*ExpressionName*是運算式的名稱*NodeNameInSubnet2*是其他子網路中的節點名稱*NameForSecondIP*是第二個 IP 位址，相關聯的名稱*IPAddress*是，第二個的子網路的 IP 位址*NameForSecondIPNetmask*網路遮罩，相關聯的名稱和*網路遮罩*是第二個子網路的網路遮罩。
    
    以下顯示範例。
    
    ```xml
    <instance attributes id="Node3-2nd-IP" score="2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node" attribute="\#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet-2" name="ip" value="192.168.2.102"/>
        <nvpair id="Netmask-For-IP2" name="cidr\_netmask" value="24" />
    </instance attributes>
    ```

3.  匯入已修改的 CIB，並重新設定 Pacemaker。

    **RHEL/Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    其中*filename* CIB 檔案已修改的 IP 位址資訊的名稱。

### <a name="check-and-verify-failover"></a>請檢查並確認容錯移轉

1.  已成功套用 CIB 與更新的組態之後，ping Pacemaker 中的 IP 位址資源相關聯的 DNS 名稱。 它應該會反映目前裝載的 AG 或 FCI 的子網路相關聯的 IP 位址。
2.  無法其他子網路 FCI 的 AG。
3.  AG 或 FCI 完全上線後，ping DNS 名稱相關聯的 IP 位址。 它應該會反映在第二個子網路的 IP 位址。
4.  如有需要，請回到原始的子網路失敗 AG 或 FCI。
