---
title: SQL Server 可用性群組設定為向外延展讀取 on Linux |Microsoft 文件
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 02/14/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
ms.openlocfilehash: dfe38445a76606543b184b60c3b1d37fbde64547
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="configure-a-sql-server-availability-group-for-read-scale-on-linux"></a>SQL Server 可用性群組設定為向外延展讀取 on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

您可以在 Linux 上設定 SQL Server Alwayson 上可用性群組 (AG) 的向外延展讀取工作負載。 有兩種類型的 Ag 的架構。 高可用性架構會使用叢集管理員來提供改良的業務續航力。 此架構也可以包含向外延展讀取的複本。 若要建立高可用性架構，請參閱[設定 SQL Server Alwayson 可用性群組在 Linux 上的高可用性](sql-server-linux-availability-group-configure-ha.md)。 其他架構支援僅為向外延展讀取工作負載。 本文說明如何建立不含向外延展讀取工作負載的叢集管理員 AG。 此架構提供的向外延展讀取只。 它並不提供高可用性。

>[!NOTE]
>可用性群組與`CLUSTER_TYPE = NONE`可以包含在不同的作業系統平台上裝載的複本。 它無法支援高可用性。 

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>建立 AG

建立 AG。 Set `CLUSTER_TYPE = NONE`. 此外，設定每個複本`FAILOVER_MODE = NONE`。 用戶端應用程式以執行分析或報告工作負載可以直接連接到次要資料庫。 您也可以建立唯讀路由清單。 向前復原主要複本的連接讀取連線要求至每個次要複本以循環配置資源方式的路由清單。

下列的 TRANSACT-SQL 指令碼會建立名為 AG `ag1`。 指令碼會設定 AG 複本`SEEDING_MODE = AUTOMATIC`。 此設定會自動建立每個次要伺服器資料庫之後會新增到 AG, 的 SQL Server。 更新您的環境中的下列指令碼。 取代`<node1>`和`<node2>`裝載複本的 SQL Server 執行個體名稱的值。 取代`<5022>`值與您設定端點的通訊埠。 SQL Server 的主要複本上執行下列 TRANSACT-SQL 指令碼：

```SQL
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

### <a name="join-secondary-sql-servers-to-the-ag"></a>次要 SQL 伺服器加入 AG

下列的 TRANSACT-SQL 指令碼會將伺服器聯結至名為 AG `ag1`。 更新您的環境的指令碼。 每個 SQL Server 在次要複本上，執行下列的 TRANSACT-SQL 指令碼，以加入 AG:

```SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create post](../includes/ss-linux-cluster-availability-group-create-post.md)]

此 AG 不是高可用性組態。 如果您需要高可用性，請遵循指示[設定 Alwayson 可用性群組的 SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md)。 具體而言，建立與 AG `CLUSTER_TYPE=WSFC` （在 Windows) 或`CLUSTER_TYPE=EXTERNAL`（在 Linux)。 然後使用其中一個 Windows Server 的容錯移轉叢集 Windows 或 Linux 上的 Pacemaker 整合和叢集管理員。

## <a name="connect-to-read-only-secondary-replicas"></a>連接到唯讀次要複本

有兩種方式可連接到唯讀次要複本。 應用程式可以直接連接到裝載次要複本的 SQL Server 執行個體，並查詢資料庫。 他們也可以使用唯讀路由，這需要一個接聽程式。

* [可讀取次要複本](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)
* [唯讀路由](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-the-primary-replica-on-a-read-scale-availability-group"></a>容錯移轉的主要複本上的向外延展讀取可用性群組

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>後續的步驟

* [設定分散式的可用性群組](..\database-engine\availability-groups\windows\distributed-availability-groups-always-on-availability-groups.md)
* [深入了解可用性群組](..\database-engine\availability-groups\windows\overview-of-always-on-availability-groups-sql-server.md)
* [執行強制手動容錯移轉](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)

