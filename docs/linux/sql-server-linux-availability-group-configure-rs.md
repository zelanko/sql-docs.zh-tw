---
title: "設定向外延展讀取可用性群組的 SQL Server on Linux |Microsoft 文件"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 10/20/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.openlocfilehash: bd3fa34a4fbfe40dfe184f7d5cf0e1f64372c8f2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="configure-read-scale-availability-group-for-sql-server-on-linux"></a>設定向外延展讀取可用性群組的 SQL Server on Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

您可以設定為向外延展讀取可用性群組的 SQL Server on Linux。 有兩個可用性群組的架構。 A*高可用性*架構會使用 「 叢集管理員提供改進的業務續航力。 此架構也可以包含向外延展讀取的複本。 若要建立高可用性架構，請參閱[設定 Alwayson 可用性群組的 SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md)。

本文件說明如何建立*向外延展讀取*沒有叢集管理員的可用性群組。 這個架構只提供的向外延展讀取只。 它不提供高可用性。

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-availability-group"></a>建立可用性群組

建立可用性群組。 Set `CLUSTER_TYPE = NONE`. 此外，設定每個複本`FAILOVER_MODE = NONE`。 用戶端應用程式以執行分析或報告工作負載可以直接連接到次要資料庫。 您也可以建立唯讀路由清單。 向前復原主要複本的連接讀取連線要求至每個次要複本以循環配置資源方式的路由清單。

下列的 TRANSACT-SQL 指令碼會建立可用性群組名稱`ag1`。 指令碼會設定可用性群組複本隨著`SEEDING_MODE = AUTOMATIC`。 此設定會自動於加入至可用性群組之後，每個次要伺服器上建立資料庫的 SQL Server。 更新您的環境中的下列指令碼。 取代`**<node1>**`和`**<node2>**`裝載複本的 SQL Server 執行個體名稱的值。 取代`**<5022>**`與您設定端點的通訊埠。 SQL Server 的主要複本上執行下列 TRANSACT-SQL:

```SQL
CREATE AVAILABILITY GROUP [ag1]
    WITH (CLUSTER_TYPE = NONE)
    FOR REPLICA ON
        N'**<node1>**' WITH (
            ENDPOINT_URL = N'tcp://**<node1>:**<5022>**',
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
                    SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
        N'**<node2>**' WITH ( 
            ENDPOINT_URL = N'tcp://**<node2>**:**<5022>**', 
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
            SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            );
        
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

### <a name="join-secondary-sql-servers-to-the-availability-group"></a>聯結至可用性群組的次要 SQL Server

下列的 TRANSACT-SQL 指令碼會將伺服器聯結至可用性群組`ag1`。 更新您的環境的指令碼。 每個 SQL Server 在次要複本上，執行下列 TRANSACT-SQL 來聯結可用性群組。

```SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

這不是高可用性組態，如果您需要高可用性，請依照下列指示[設定 Alwayson 可用性群組的 SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md)。 具體而言，建立在可用性群組`CLUSTER_TYPE=WSFC`（在 Windows) 或`CLUSTER_TYPE=EXTERNAL`（在 Linux)，並使用叢集管理員的 Windows 上的 WSFC，或是在 Linux 上 Pacemaker 整合。

## <a name="connect-to-read-only-secondary-replicas"></a>連接到唯讀次要複本

有兩種方式可連接到唯讀次要複本。 應用程式可以直接連接到裝載次要複本的 SQL Server 執行個體，並查詢資料庫，或者可以使用唯讀路由。 唯讀路由要求的接聽程式。

[可讀取次要複本](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)

[唯讀路由](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-primary-replica-on-read-scale-availability-group"></a>容錯移轉向外延展讀取可用性群組主要複本

[!INCLUDE[Force Failover](../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>後續的步驟

[設定分散式可用性群組](..\database-engine\availability-groups\windows\distributed-availability-groups-always-on-availability-groups.md)

[深入了解可用性群組](..\database-engine\availability-groups\windows\overview-of-always-on-availability-groups-sql-server.md)

[執行強制手動容錯移轉](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)。

