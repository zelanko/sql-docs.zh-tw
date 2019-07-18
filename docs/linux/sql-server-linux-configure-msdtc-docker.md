---
title: 如何使用 Docker 上的 SQL Server 的分散式的交易
description: 這篇文章說明如何使用 Linux 上設定 MSDTC 的 Dprovides 逐步解說。
author: VanMSFT
ms.author: vanto
ms.date: 09/25/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: fab3934a86994b3c4a0d7d7ecfc7768f65660023
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077685"
---
# <a name="how-to-use-distributed-transactions-with-sql-server-on-docker"></a>如何使用 Docker 上的 SQL Server 的分散式的交易

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章說明如何設定分散式交易在 Docker 上的 SQL Server Linux 容器。

從 SQL Server 2019 preview 開始，容器映像支援 Microsoft Distributed Transaction Coordinator (MSDTC) 所需的分散式交易。 若要了解 MSDTC 的通訊需求，請參閱[如何在 Linux 上設定 Microsoft Distributed Transaction Coordinator (MSDTC)](sql-server-linux-configure-msdtc.md)。 這篇文章說明的特殊需求和案例相關的 SQL Server Docker 容器。

## <a name="configuration"></a>組態

若要啟用 MSDTC 交易，docker 容器中的，您必須設定兩個新的環境變數：

- **MSSQL_RPC_PORT**: RPC 端點對應程式服務繫結，而且會接聽的 TCP 連接埠。  
- **MSSQL_DTC_TCP_PORT**: 連接埠 MSDTC 服務設定為接聽。

### <a name="pull-and-run"></a>提取及執行

下列範例示範如何使用這些環境變數來提取，並執行單一的 SQL Server 容器，設定 msdtc。 這可讓它的任何主機上的任何應用程式進行通訊。

```bash
docker run \
   -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' \
   -e 'MSSQL_RPC_PORT=135' -e 'MSSQL_DTC_TCP_PORT=51000' \
   -p 51433:1433 -p 135:135 -p 51000:51000  \
   -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

> [!IMPORTANT]
> 前一個命令只適用於 Linux 上執行的 Docker。 Windows 上的 Docker，Windows 主機已經會接聽連接埠 135。 您可以移除`-p 135:135`docker on Windows，但它的參數有幾項限制。 產生的容器就不會用於分散式交易涉及的主應用程式;它可以參與只在主機上的 docker 容器之間的分散式交易。

這個命令中， **RPC 端點對應程式**服務已經繫結至連接埠 135，而**MSDTC**已繫結至連接埠 51000 docker 的虛擬網路內的服務。 SQL Server TDS 通訊是 docker 的虛擬網路內的通訊埠 1433年。 外部公開這些連接埠為 TDS 連接埠 51433、 RPC 端點對應程式通訊埠 135 和 MSDTC 連接埠 51000 的主機。

> [!NOTE]
> 相同的主機和容器上的 RPC 端點對應程式和 MSDTC 連接埠沒有。 因此 RPC 端點對應程式的連接埠已設定要在容器上的 135，它可能可以對應到連接埠 13501 或任何其他可用的連接埠上的主機伺服器。

## <a name="configure-the-firewall"></a>設定防火牆

若要進行通訊，透過主應用程式，您也必須設定防火牆容器在主機伺服器上。 連接埠的開啟所有防火牆，docker 容器會公開為外部通訊。 在上述範例中，這會是連接埠 135、 51433 和 51000。 這些是主機本身上的連接埠以及不將其對應到容器中的連接埠。 因此，如果 RPC 端點對應程式連接埠 51000 容器的已對應至主機連接埠 51001，然後連接埠 51001 (不 51000) 應該與主機通訊的防火牆中開啟。  

下列範例示範如何在 Ubuntu 上建立這些規則。

```bash
sudo ufw allow from any to any port 51433 proto tcp
sudo ufw allow from any to any port 51000 proto tcp
sudo ufw allow from any to any port 135 proto tcp
```

下列範例會示範如何進行上 Red Hat Enterprise Linux (RHEL):

```bash
sudo firewall-cmd --zone=public --add-port=51999/tcp --permanent
sudo firewall-cmd --zone=public --add-port=51433/tcp --permanent
sudo firewall-cmd --zone=public --add-port=135/tcp --permanent
sudo firewall-cmd --reload
```

## <a name="configure-port-routing-on-the-host"></a>設定主機上的連接埠路由

在上述範例中，因為單一 Docker 容器對應到主機上的連接埠 135 的 RPC 連接埠 135 與主機的分散式的交易現在應該運作而不進一步設定。 請注意，它可以直接使用連接埠 135，在容器中，因為使用提高的權限，在容器中執行的 SQL Server。 For SQL Server 容器之外，必須使用不同的暫時連接埠及通訊埠 135 的流量便會路由到該連接埠。

不過，如果您未決定對應的容器連接埠 135 以不同的連接埠，在主機上，例如 13500，然後您必須設定連接埠路由主機上。 這可讓要參與分散式交易與主應用程式和其他外部伺服器的 docker 容器。 如需詳細資訊，請參閱 <<c0> [ 設定的連接埠路由](sql-server-linux-configure-msdtc.md#configure-port-routing)。

## <a name="next-steps"></a>後續步驟

如需更多有關 Linux MSDTC 的詳細資訊，請[如何在 Linux 上設定 Microsoft Distributed Transaction Coordinator (MSDTC)](sql-server-linux-configure-msdtc.md)。
