---
title: "設定 SQL Server on Linux 讀取的向外延展可用性群組 |Microsoft 文件"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 06/14/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: cf249ff8e6d2e82d1cf413bdec0272e3796b72cb
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="configure-read-scale-out-availability-group-for-sql-server-on-linux"></a>設定 SQL Server on Linux 讀取的向外延展可用性群組

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

您可以設定為讀取的向外延展可用性群組的 SQL Server on Linux。 有兩個可用性群組的架構。 A*高可用性*架構會使用 「 叢集管理員提供改進的業務續航力。 此架構也可以包含唯讀的相應放大複本。 若要建立高可用性架構，請參閱[設定 Alwayson 可用性群組的 SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md)。

本文件說明如何建立*讀取的向外延展*沒有叢集管理員的可用性群組。 這個架構只提供讀取的向外延展只。 它不提供高可用性。

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-availability-group"></a>建立可用性群組

建立可用性群組。 Set `CLUSTER_TYPE = NONE`. 此外，設定每個複本`FAILOVER_MODE = NONE`。 用戶端應用程式以執行分析或報告工作負載可以直接連接到次要資料庫。 您也可以建立唯讀路由清單。 向前復原主要複本的連接讀取連線要求至每個次要複本以循環配置資源方式的路由清單。

下列的 TRANSACT-SQL 指令碼會建立可用性群組名稱`ag1`。 指令碼會設定可用性群組複本隨著`SEEDING_MODE = AUTOMATIC`。 此設定會自動於加入至可用性群組之後，每個次要伺服器上建立資料庫的 SQL Server。 更新您的環境中的下列指令碼。 取代`**<node1>**`和`**<node2>**`裝載複本的 SQL Server 執行個體名稱的值。 取代`**<5022>**`與您設定端點的通訊埠。 SQL Server 的主要複本上執行下列 TRANSACT-SQL:

```Transact-SQL
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

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

這不是高可用性組態，如果您需要高可用性，請依照下列指示[設定 Alwayson 可用性群組的 SQL Server on Linux](sql-server-linux-availability-group-configure-ha.md)。 具體而言，建立在可用性群組`CLUSTER_TYPE=WSFC`（在 Windows) 或`CLUSTER_TYPE=EXTERNAL`（在 Linux)，並使用叢集管理員的 Windows 上的 WSFC，或是在 Linux 上 Pacemaker 整合。

## <a name="connect-to-read-only-secondary-replicas"></a>連接到唯讀次要複本

有兩種方式可連接到唯讀次要複本。 應用程式可以直接連接到裝載次要複本的 SQL Server 執行個體，並查詢資料庫，或者可以使用唯讀路由。 唯讀路由要求的接聽程式。

[可讀取次要複本](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)

[唯讀路由](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-primary-replica-on-read-scale-out-availability-group"></a>容錯移轉主要複本上讀取的向外延展可用性群組

每個可用性群組有一個主要複本。 主要複本允許讀取和寫入。 若要變更是主要的複本，您可以容錯移轉。 在可用性群組中的高可用性，叢集管理員 會自動容錯移轉程序中。 在讀取的向外延展可用性群組中，容錯移轉程序是手動。 有兩種方式，容錯移轉中讀取的標尺的可用性群組的主要複本。

- 強制手動容錯移轉，會遺失資料

- 手動容錯移轉不會遺失資料

### <a name="forced-fail-over-with-data-loss"></a>強制的容錯移轉會遺失資料

並非主要複本，而且無法復原時，請使用這個方法。 您可以尋找在遺失資料的強制容錯移轉的詳細資訊[執行強制手動容錯移轉](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)。

若要強制容錯移轉，會遺失資料，連接到裝載目標次要複本的 SQL 執行個體並執行：
```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

### <a name="manual-fail-over-without-data-loss"></a>手動容錯移轉不會遺失資料

這個方法時使用的主要複本可以使用，但您需要暫時或永久地變更組態，然後變更 SQL Server 執行個體裝載主要複本。 之前發出手動容錯移轉，請確定目標次要複本是最新狀態，使得沒有任何潛在資料遺失。 

下列步驟描述如何手動容錯移轉不會遺失資料：

1. 請在目標次要複本的同步認可。

   ```Transact-SQL
   ALTER AVAILABILITY GROUP [ag1] MODIFY REPLICA ON N'**<node2>*' WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```
1. 更新`required_synchronized_secondaries_to_commit`設為 1。

   此設定可確保每個使用中交易認可至主要複本和至少一個同步次要複本。 可用性群組已準備好要容錯移轉 synchronization_state_desc 同步處理時，sequence_number 是在相同的兩個主要和目標次要複本。 執行此查詢來檢查：

   ```Transact-SQL
   SELECT ag.name, 
      drs.database_id, 
      drs.group_id, 
      drs.replica_id, 
      drs.synchronization_state_desc, 
      ag.sequence_number
   FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
   WHERE drs.group_id = ag.group_id; 
   ```

1. 降級至次要複本的主要複本。 主要複本降級之後，它會處於唯讀狀態。 在裝載主要複本更新角色到次要資料庫的 SQL 執行個體上執行此命令：

   ```Transact-SQL
   ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY); 
   ```

1. 升級為主要的目標次要複本。 

   ```Transact-SQL
   ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```  

   > [!NOTE] 
   > 若要刪除可用性群組使用[DROP AVAILABILITY GROUP](https://docs.microsoft.com/en-us/sql/t-sql/statements/drop-availability-group-transact-sql)。 使用 CLUSTER_TYPE NONE 或外部建立可用性群組，命令對於可用性群組的所有複本組件上執行。

## <a name="next-steps"></a>後續的步驟

[設定分散式的可用性群組](..\database-engine\availability-groups\windows\distributed-availability-groups-always-on-availability-groups.md)

[深入了解可用性群組](..\database-engine\availability-groups\windows\overview-of-always-on-availability-groups-sql-server.md)


