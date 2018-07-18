---
title: 設定 SQL Server 可用性群組供 Windows 上的讀取縮放使用 | Microsoft Docs
description: ''
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.reviewer: ''
ms.date: 05/24/2018
ms.topic: conceptual
ms.prod: sql
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.openlocfilehash: 926e97d7aa6026946235d7abebdd5d3fd7023891
ms.sourcegitcommit: 9e83f308008c9e0da505a6064f652c638b8dfe76
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/13/2018
ms.locfileid: "35513003"
---
# <a name="configure-a-sql-server-availability-group-for-read-scale-on-windows"></a>設定 SQL Server 可用性群組供 Windows 上的讀取縮放使用

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

您可以設定 SQL Server AlwaysOn 可用性群組，供 Windows 上的讀取縮放工作負載使用。 可用性群組有兩種類型的架構：
* 高可用性結構，其使用叢集管理員來提供改善的商務持續性，並能夠包含可讀取的次要複本。 若要建立此高可用性結構，請參閱[在 Windows 上建立和設定可用性群組](creation-and-configuration-of-availability-groups-sql-server.md)。 
* 僅支援讀取縮放工作負載的結構。 

本文說明如何建立不使用叢集管理員的可用性群組，供讀取縮放工作負載使用。 此結構只會提供讀取級別。 它不會提供高可用性。

>[!NOTE]
>`CLUSTER_TYPE = NONE` 的可用性群組可包含裝載於各種作業系統平台上的複本。 它無法支援高可用性。 針對 Linux 作業系統，請參閱[設定 SQL Server 可用性群組供 Linux 上的讀取縮放使用](../../../linux/sql-server-linux-availability-group-configure-rs.md)。

[!INCLUDE [Create prerequisites](../../../includes/ss-availability-group-rs-prereq.md)]

## <a name="create-an-availability-group"></a>建立可用性群組

建立可用性群組。 設定 `CLUSTER_TYPE = NONE`。 此外，將每個複本設定為 `FAILOVER_MODE = NONE`。 執行分析或報告工作負載的用戶端應用程式可直接連線至次要資料庫。 您也可以建立唯讀路由清單。 連線到主要複本會從路由清單，以循環配置資源的方式將讀取連線要求轉送至每個次要複本。

下列 Transact-SQL 指令碼會建立名為 `ag1` 的可用性群組。 該指令碼會將可用性群組複本設定為 `SEEDING_MODE = AUTOMATIC`。 此設定會使 SQL Server 在將次要伺服器新增至可用性群組之後，在每個次要伺服器上自動建立資料庫。 

更新您環境中的下列指令碼。 將 `<node1>` 和 `<node2>` 值取代為裝載複本之 SQL Server 執行個體的名稱。 將 `<5022>` 值取代為您為端點設定的連接埠。 在 SQL Server 主要複本上，執行下列 TRANSACT-SQL 指令碼：

```sql
CREATE AVAILABILITY GROUP [ag1]
    WITH (CLUSTER_TYPE = NONE)
    FOR REPLICA ON
        N'<node1>' WITH (
            ENDPOINT_URL = N'tcp://<node1>:<5022>',
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
                    SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
        N'<node2>' WITH (
            ENDPOINT_URL = N'tcp://<node2>:<5022>',
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
            SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            );

ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

### <a name="join-secondary-sql-server-instances-to-the-availability-group"></a>將次要 SQL Server 執行個體加入可用性群組

下列 Transact-SQL 指令碼會將伺服器加入名為 `ag1` 的可用性群組。 更新您環境中的指令碼。 若要加入可用性群組，請在每個 SQL Server 次要複本上執行下列 Transact-SQL 指令碼：

```sql
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);

ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create post](../../../includes/ss-availability-group-rs-postactivity.md)]

這個可用性群組不是高可用性設定。 如果您需要高可用性，請遵循[為 Linux 上的 SQL Server 設定 AlwaysOn 可用性群組](../../../linux/sql-server-linux-availability-group-configure-ha.md)或[在 Windows 上建立和設定可用性群組](creation-and-configuration-of-availability-groups-sql-server.md)中的指示進行。

## <a name="connect-to-read-only-secondary-replicas"></a>連線到唯讀次要複本

您可以使用下列兩種方式之一連線至唯讀次要複本：
* 應用程式可以直接連線到裝載次要複本的 SQL Server 執行個體，並查詢資料庫。 如需詳細資訊，請參閱[可讀取的次要複本](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)。
* 應用程式也可以使用唯讀路由，這需要接聽程式。 如需詳細資訊，請參閱[唯讀路由](listeners-client-connectivity-application-failover.md#ConnectToSecondary)。

## <a name="fail-over-the-primary-replica-on-a-read-scale-availability-group"></a>容錯移轉讀取級別可用性群組上的主要複本

[!INCLUDE[Force failover](../../../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>後續步驟

* [設定分散式可用性群組](distributed-availability-groups-always-on-availability-groups.md)
* [深入了解可用性群組](overview-of-always-on-availability-groups-sql-server.md)
* [執行強制手動容錯移轉](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)
