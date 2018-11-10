---
title: 如何在 Linux 上設定 MSDTC |Microsoft Docs
description: 本文章提供在 Linux 上設定 MSDTC 的逐步解說。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: a06dfa03442cfbcff2f8815f9c946afbd9ff771c
ms.sourcegitcommit: a2be75158491535c9a59583c51890e3457dc75d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2018
ms.locfileid: "51269671"
---
# <a name="how-to-configure-the-microsoft-distributed-transaction-coordinator-msdtc-on-linux"></a>如何在 Linux 上設定 Microsoft Distributed Transaction Coordinator (MSDTC)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文說明如何在 Linux 上設定 Microsoft 分散式交易協調器 (MSTDC)。 Linux 上的 MSDTC 支援是在 SQL Server 2019 預覽引進。

## <a name="overview"></a>總覽

在 Linux 上的 SQL Server 上已啟用分散式的交易，藉由引進 SQL Server 內的 MSDTC 和 RPC 端點對應程式功能。 根據預設，RPC 端點對應程序會接聽內送 RPC 要求的連接埠 135，而且將會路由傳送至適當的元件 （例如 MSDTC 服務）。 處理程序需要繫結至已知的通訊埠 （連接埠號碼小於 1024年），在 Linux 上的進階使用者權限。 若要避免以 RPC 端點對應程式處理序的根權限啟動 SQL Server，系統管理員必須使用 iptables 來建立將流量路由傳送至 SQL Server 的 RPC 端點對應處理序的連接埠 135 的 NAT 轉譯。

SQL Server 2019 導入了 「 mssql conf 公用程式的兩個組態參數。

| mssql conf 設定 | 描述 |
|---|---|
| **network.rpcport** | RPC 端點對應程式處理序繫結至 TCP 連接埠。 |
| **network.servertcpport** | MSDTC 伺服器接聽連接埠。 如果未設定，MSDTC 服務會使用隨機的暫時連接埠在服務重新啟動時，及防火牆例外狀況將會需要重新設定，請確定 MSDTC 服務可以繼續通訊。 |

如需有關這些設定和其他相關的 MSDTC 設定的詳細資訊，請參閱 <<c0> [ 在 Linux 上使用 mssql-conf 工具的 設定 SQL Server](sql-server-linux-configure-mssql-conf.md#msdtc)。

## <a name="supported-msdtc-configurations"></a>支援的 MSDTC 設定

支援下列的 MSDTC 組態：

- OLE TX 分散式交易對 Linux 上的 SQL Server JDBC 和 ODBC 提供者。
- 針對 Linux 上使用 JDBC 的提供者的 SQL Server 的 XA 分散式交易。
- 在 連結的伺服器上的分散式的交易。

如為 MSDTC preview 的已知的問題和限制，請參閱 <<c0> [ 在 Linux 上的 SQL Server 2019 預覽的版本資訊](sql-server-linux-release-notes-2019.md#msdtc)。

## <a name="msdtc-configuration-steps"></a>MSDTC 組態步驟

有三個步驟，設定 MSDTC 的通訊和功能。 如果未進行必要的設定步驟，SQL Server 也不會啟用 MSDTC 功能。

- 設定**network.rpcport**並**distributedtransaction.servertcpport**使用 mssql 設定
- 設定防火牆允許通訊**rpcport**， **servertcpport**，和連接埠 135。
- 設定 Linux 伺服器的路由，以便在連接埠 135 的 RPC 通訊會重新導向至 SQL Server **network.rpcport**。

下列各節提供每個步驟的詳細的指示。

## <a name="configure-rpc-and-msdtc-ports"></a>設定 RPC 和 MSDTC 連接埠

首先，設定**network.rpcport**並**distributedtransaction.servertcpport**使用 mssql 設定

1. 若要設定使用 mssql conf **network.rpcport**值。 下列範例會將它設定為 13500。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport 13500
   ```

2. 設定**distributedtransaction.servertcpport**值。 下列範例會將它設定為 51999。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport 51999
   ```

3. 重新啟動 SQL Server。

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="configure-the-firewall"></a>設定防火牆

最後一個步驟是設定防火牆允許通訊**rpcport**， **servertcpport**，和連接埠 135。  這可讓 RPC 端點對應程序和 MSDTC 程序，與其他交易管理員和協調器外部通訊。 實際步驟取決於您的 Linux 散發套件和防火牆而異。 

下列範例示範如何在 Ubuntu 上建立這些規則。

```bash
sudo ufw allow from any to any port 51999 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

下列範例會示範如何進行上 Red Hat Enterprise Linux (RHEL):

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

請務必將防火牆設定之前設定的連接埠路由中下一節。 重新整理防火牆可以清除的連接埠路由規則，在某些情況下。

## <a name="configure-port-routing"></a>設定連接埠路由

設定 Linux 伺服器的路由表，以便在連接埠 135 的 RPC 通訊會重新導向至 SQL Server **network.rpcport**。 Iptable 規則可能不是保存在重新開機，因此下列命令也會提供在重新開機之後還原規則的指示。

1. 建立通訊埠 135 的路由規則。 在下列範例中，連接埠 135 會導向至 RPC 連接埠，13500 上, 一節中所定義。 取代`<ipaddress>`您伺服器的 IP 位址。

   ```bash
   iptables -t nat -A PREROUTING -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL  \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   iptables -t nat -A OUTPUT -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   ```

   `--comment RpcEndPointMapper`先前命令中的參數可協助管理這些規則在更新版本的命令。

2. 檢視您使用下列命令建立路由規則：

   ```bash
   iptables -S -t nat | grep "RpcEndPointMapper"
   ```

3. 將路由規則儲存到您的電腦上的檔案。

   ```bash
   iptables-save > /etc/iptables.conf
   ```

4. 若要在重新開機後，重新載入的規則，請新增下列命令，以`/etc/rc.local`（適用於 Ubuntu 或 RHEL） 或`/etc/init.d/after.local`（適用於 SLES):

   ```bash
   iptables-restore < /etc/iptables.conf
   ```

**Iptables 相關自定義儲存**並**iptables 相關自定義還原**命令提供基本機制來儲存和還原 iptables 相關自定義項目。 根據您的 Linux 散發套件，那里可能更進階或自動化的可用選項。 Ubuntu 上的替代方法是，例如**iptables 相關自定義持續**封裝，使持續性的項目。 或 Red Hat Enterprise linux，您可以使用 firewalld 服務 (透過防火牆 cmd 組態公用程式與-新增-向前-連接埠或類似的選項) 來建立持續性的連接埠轉送規則，而不是使用 iptables 相關自定義。

> [!IMPORTANT]
> 先前的步驟假設固定的 IP 位址。 如果您的 SQL Server 執行個體的 IP 位址有所變更 （因為手動操作或 DHCP），您必須移除並重新建立路由規則。 如果您需要重新建立或刪除現有的路由規則，您可以使用下列命令來移除舊`RpcEndPointMapper`規則：
> 
> ```bash
> iptables -S -t nat | grep "RpcEndPointMapper" | sed 's/^-A //' | while read rule; do iptables -t nat -D $rule; done
> ```

## <a name="verify"></a>Verify

此時，SQL Server 應該能夠參與分散式交易。 若要確認 SQL Server 正在接聽，請執行**netstat**命令 (如果您使用 RHEL，您可能必須先安裝**net 工具**封裝):

```bash
sudo netstat -tulpn | grep sqlservr
```

您應該會看到類似下面的輸出：

```bash
tcp 0 0 0.0.0.0:1433 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 127.0.0.1:1434 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 0.0.0.0:13500 0.0.0.0:* LISTEN 13911/sqlservr
tcp 0 0 0.0.0.0:51999 0.0.0.0:* LISTEN 13911/sqlservr
tcp6 0 0 :::1433 :::* LISTEN 13911/sqlservr
tcp6 0 0 ::1:1434 :::* LISTEN 13911/sqlservr
tcp6 0 0 :::13500 :::* LISTEN 13911/sqlservr
tcp6 0 0 :::51999 :::* LISTEN 13911/sqlservr
```

不過，重新啟動之後，SQL Server 不會啟動接聽**servertcpport**直到第一個分散式交易。 在此情況下，就不會看到第一個分散式交易，直到接聽連接埠 51999 在此範例中的 SQL Server。

## <a name="next-steps"></a>後續步驟

在 Linux 上 SQL Server 的相關資訊，請參閱[在 Linux 上的 SQL Server](sql-server-linux-overview.md)。
