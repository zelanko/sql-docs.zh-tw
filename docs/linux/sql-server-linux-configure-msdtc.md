---
title: 如何在 Linux 上設定 MSDTC
description: 此文章提供在 Linux 上設定 MSDTC 的逐步解說。
author: VanMSFT
ms.author: vanto
ms.date: 08/01/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: a39e0a743053db694efc2d0e8176e659d7e376d1
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68995871"
---
# <a name="how-to-configure-the-microsoft-distributed-transaction-coordinator-msdtc-on-linux"></a>如何在 Linux 上設定 Microsoft Distributed Transaction Coordinator (MSDTC)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

此文章說明如何在 Linux 上設定 Microsoft 分散式交易協調器 (MSDTC)。

> [!NOTE]
> 從累積更新 16 開始，SQL Server 2017 就支援 Linux 上的 MSDTC。

## <a name="overview"></a>概觀

在 Linux 上的 SQL Server 啟用分散式交易時，會藉由在 SQL Server 內導入 MSDTC 和 RPC 端點對應程式功能來啟用。 根據預設，RPC 端點對應程序會在連接埠 135 上接聽傳入的 RPC 要求，並向遠端要求提供已註冊的元件資訊。 遠端要求可以使用端點對應程式傳回的資訊來與已註冊的 RPC 元件 (例如 MSDTC 服務) 進行通訊。 程序必須要有超級使用者權限，才能繫結至 Linux 上的已知連接埠 (小於 1024 的連接埠)。 為了避免以根權限啟動 SQL Server 來進行 RPC 端點對應程式程序，系統管理員必須使用 iptables 來建立「網路位址轉譯」，以將連接埠 135 上的流量路由傳送至 SQL Server 的 RPC 端點對應程序。

MSDTC 針對 mssql-conf 公用程式使用兩個設定參數：

| mssql-conf 設定 | 描述 |
|---|---|
| **network.rpcport** | RPC 端點對應程式所繫結的 TCP 連接埠。 |
| **distributedtransaction.servertcpport** | MSDTC 伺服器所接聽的連接埠。 如果未設定，MSDTC 服務會在服務重新啟動時使用隨機的暫時連接埠，且防火牆例外將必須重新設定，以確保 MSDTC 服務可以繼續進行通訊。 |

如需有關這些設定及其他相關 MSDTC 設定的詳細資訊，請參閱[使用 mssql-conf 工具設定 Linux 上的 SQL Server](sql-server-linux-configure-mssql-conf.md)。

## <a name="supported-msdtc-configurations"></a>支援的 MSDTC 設定

以下是支援的 MSDTC 設定：

- 適用於 ODBC 提供者之針對 Linux 上 SQL Server 的 OLE-TX 分散式交易。

- 使用 JDBC 和 ODBC 提供者之針對 Linux 上 SQL Server 的 XA 分散式交易。 針對要使用 ODBC 提供者來執行的 XA 交易，您必須使用 Microsoft ODBC Driver for SQL Server 17.3 版或更新版本。 如需詳細資訊，請參閱[了解 XA 交易](../connect/jdbc/understanding-xa-transactions.md#configuration-instructions)。

- 連結伺服器上的分散式交易。

## <a name="msdtc-configuration-steps"></a>MSDTC 設定步驟

設定 MSDTC 通訊和功能的步驟有三個。 如果未完成必要的設定步驟，SQL Server 將不會啟用 MSDTC 功能。

- 使用 mssql-conf 來設定 **network.rpcport** 和 **distributedtransaction.servertcpport**。
- 設定防火牆以允許在 **distributedtransaction.servertcpport** 和連接埠 135 上進行通訊。
- 設定 Linux 伺服器路由，以便將連接埠 135 上的 RPC 通訊重新導向到 SQL Server 的 **network.rpcport**。

下列各節提供每個步驟的詳細指示。

## <a name="configure-rpc-and-msdtc-ports"></a>設定 RPC 和 MSDTC 連接埠

首先，使用 mssql-conf 來設定 **network.rpcport** 和 **distributedtransaction.servertcpport**。 此步驟是 SQL Server 特定的步驟，所有支援的發行版本都通用。

1. 使用 mssql-conf 來設定 **network.rpcport** 值。 下列範例會將其設定為 13500。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set network.rpcport 13500
   ```

2. 設定 **distributedtransaction.servertcpport** 值。 下列範例會將其設定為 51999。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set distributedtransaction.servertcpport 51999
   ```

3. 重新啟動 SQL Server。

   ```bash
   sudo systemctl restart mssql-server
   ```

## <a name="configure-the-firewall"></a>設定防火牆

第二個步驟是設定防火牆以允許在 **servertcpport** 和連接埠 135 上進行通訊。  這可讓 RPC 端點對應程序和 MSDTC 程序與其他交易管理員和協調器進行外部通訊。 此操作的實際步驟將因 Linux 發行版本和防火牆而有所不同。 

下列範例說明如何在 **Ubuntu** 上建立這些規則。

```bash
sudo ufw allow from any to any port 51999 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

下列範例說明如何在 **Red Hat Enterprise Linux (RHEL)** 上進行此操作：

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

在下一節中，請務必先設定防火牆，再設定連接埠路由。 在某些情況下，重新整理防火牆可以清除連接埠路由規則。

## <a name="configure-port-routing"></a>設定連接埠路由

設定 Linux 伺服器路由表，以便將連接埠 135 上的 RPC 通訊重新導向到 SQL Server 的 **network.rpcport**。 不同發行版本上的連接埠轉送設定機制可能不同。 下列各節提供適用於 Ubuntu、SUS Enterprise Linux (SLES) 及 Red Hat Enterprise Linux (RHEL) 的指引。

### <a name="port-routing-in-ubuntu-and-sles"></a>Ubuntu 和 SLES 中的連接埠路由

Ubuntu 和 SLES 不使用 **firewalld** 服務，因此 **iptable** 規則是一個可達成連接埠路由的有效率機制。 **iptable** 規則在重新開機期間可能不會保存，因此下列命令也提供在重新開機後還原規則的指示。

1. 為連接埠 135 建立路由規則。 在下列範例中，連接埠 135 會導向到上一節中定義的 RPC 連接埠 13500。 請以您伺服器的 IP 位址取代 `<ipaddress>`。

   ```bash
   sudo iptables -t nat -A PREROUTING -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL  \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   sudo iptables -t nat -A OUTPUT -d <ip> -p tcp --dport 135 -m addrtype --dst-type LOCAL \
      -j DNAT --to-destination <ip>:13500 -m comment --comment RpcEndPointMapper
   ```

   先前命令中的 `--comment RpcEndPointMapper` 參數會在稍後的命令中協助管理這些規則。

2. 使用下列命令來檢視您建立的路由規則：

   ```bash
   sudo iptables -S -t nat | grep "RpcEndPointMapper"
   ```

3. 將路由規則儲存到您機器上的檔案中。

   ```bash
   sudo iptables-save > /etc/iptables.conf
   ```

4. 若要在重新開機後重新載入規則，請將下列命令新增至 `/etc/rc.local` (適用於 Ubuntu) 或 `/etc/init.d/after.local` (適用於 SLES)：

   ```bash
   iptables-restore < /etc/iptables.conf
   ```

   > [!NOTE]
   > 您必須具備超級使用者 (sudo) 權限，才能編輯 **rc.local** 或 **after.local** 檔案。

**iptables-save** 和 **iptables-restore** 命令以及 `rc.local`/`after.local` 啟動設定會提供一個基本機制來儲存和還原 iptables 項目。 視您的 Linux 發行版本而定，可能會有更進階或自動化的選項可供使用。 例如，Ubuntu 替代方案是 **iptables-persistent** 套件，此套件可讓項目變成永續性。

> [!IMPORTANT]
> 先前的步驟假設使用固定 IP 位址。 路由規則若是以 iptables 建立的，當 SQL Server 執行個體的 IP 位址發生變更 (因為手動介入或 DHCP) 時，您就必須移除並重新建立路由規則。 如果您必須重新建立或刪除現有的路由規則，您可以使用下列命令來移除舊的 `RpcEndPointMapper` 規則：
> 
> ```bash
> sudo iptables -S -t nat | grep "RpcEndPointMapper" | sed 's/^-A //' | while read rule; do iptables -t nat -D $rule; done
> ```

### <a name="port-routing-in-rhel"></a>RHEL 中的連接埠路由

在使用 **firewalld** 服務的發行版本 (例如 Red Hat Enterprise Linux) 上，可以使用該相同服務來開啟伺服器上的連接埠和進行內部連接埠轉送。 例如，在 Red Hat Enterprise Linux 上，您應該使用 **firewalld** 服務 (透過 **firewall-cmd** 設定公用程式搭配 `-add-forward-port` 或類似的選項) 來建立和管理永續性連接埠轉送規則，而不是使用 iptables。

```bash
sudo firewall-cmd --permanent --add-forward-port=port=135:proto=tcp:toport=13500
sudo firewall-cmd --reload
```

## <a name="verify"></a>Verify

此時，SQL Server 應該已能夠參與分散式交易。 若要確認 SQL Server 是否在進行接聽，請執行 **netstat** 命令 (如果您使用 RHEL，則可能必須先安裝 **net-tools** 套件)：

```bash
sudo netstat -tulpn | grep sqlservr
```

您應該會看到類似以下的輸出：

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

不過，在重新啟動之後，必須等到第一次分散式交易之後，SQL Server 才會開始在 **servertcpport** 上進行接聽。 在此情況下，於此範例中，您必須等到第一次分散式交易之後，才會看到 SQL Server 在連接埠 51999 上進行接聽。

## <a name="configure-authentication-on-rpc-communication-for-msdtc"></a>針對 MSDTC 設定 RPC 通訊上的驗證

Linux 上 SQL Server 的 MSDTC 預設不會在 RPC 通訊上使用驗證。 不過，當主機電腦已加入 Active Directory (AD) 網域時，便可以使用下列 **mssql-conf** 設定來設定讓 MSDTC 使用已驗證的 RPC 通訊：

| 設定 | 描述 |
|---|---|
| **distributedtransaction.allowonlysecurerpccalls**          | 針對分散式交易設定僅限安全的 RPC 呼叫。 預設值為 0。 |
| **distributedtransaction.fallbacktounsecurerpcifnecessary** | 針對分散式交易設定僅限安全性的 RPC 呼叫。 預設值為 0。 |
| **distributedtransaction.turnoffrpcsecurity**               | 針對分散式交易啟用或停用 RPC 安全性。 預設值為 0。 |

## <a name="additional-guidance"></a>其他指導方針

### <a name="active-directory"></a>Active Directory

如果 SQL Server 已註冊到 Active Directory (AD) 設定，Microsoft 建議在已啟用 RPC 的情況下使用 MSDTC。 如果 SQL Server 設定為使用 AD 驗證。則 MSDTC 預設會使用相互驗證 RPC 安全性。

### <a name="windows-and-linux"></a>Windows 與 Linux

如果 Windows 作業系統上的用戶端需要使用 Linux 上的 SQL Server 登錄到分散式交易，它必須具有下列最低版本的 Windows 作業系統：

| 作業系統 | 最小版本 | OS 組建 |
|---|---|---|
| [Windows Server](https://docs.microsoft.com/windows-server/get-started/windows-server-release-info) | 1903 | 18362.30.190401-1528 |
| [Windows 10](https://docs.microsoft.com/windows/release-information/) | 1903 | 18362.267 |

## <a name="next-steps"></a>後續步驟

如需 Linux 上 SQL Server 的詳細資訊，請參閱 [Linux 上的 SQL Server](sql-server-linux-overview.md)。
