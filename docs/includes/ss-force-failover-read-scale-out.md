---
title: SQL Server 可用性群組的強制容錯移轉
description: 叢集類型為 NONE 之可用性群組的強制容錯移轉
services: ''
author: MikeRayMSFT
ms.topic: include
ms.date: 02/05/2018
ms.author: mikeray
ms.custom: include file
ms.openlocfilehash: f5655e73481d830c848aea34c4a4f49613be0913
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
每個 AG 只有一個主要複本。 主要複本允許讀取和寫入。 若要變更作為主要的複本，您可以進行容錯移轉。 在高可用性的 AG 中，叢集管理員會自動化容錯移轉程序。 在叢集類型為 NONE 的 AG 中，容錯移轉程序是手動的。 

容錯移轉叢集類型為 NONE 之 AG 中的主要複本有兩種方式：

- 強制手動容錯移轉 (可能遺失資料)
- 手動容錯移轉 (不會遺失資料)

### <a name="forced-manual-failover-with-data-loss"></a>強制手動容錯移轉 (可能遺失資料)

當主要複本無法使用且無法復原時，請使用這個方法。 

若要強制容錯移轉 (可能遺失資料)，請連線到裝載目標次要複本的 SQL Server 執行個體並執行：

```SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

### <a name="manual-failover-without-data-loss"></a>手動容錯移轉 (不會遺失資料)

當主要複本可以使用，但您需要暫時或永久變更設定並變更裝載主要複本的 SQL Server 執行個體時，請使用這個方法。 發出手動容錯移轉之前，請確定目標次要複本是最新狀態，以免可能遺失資料。 

若要手動容錯移轉 (不會遺失資料)：

1. 將目標次要複本設為 `SYNCHRONOUS_COMMIT`。

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        MODIFY REPLICA ON N'<node2>' 
        WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```

2. 執行下列查詢，識別使用中交易已認可至主要複本及至少一個同步次要複本： 

   ```SQL
   SELECT ag.name, 
      drs.database_id, 
      drs.group_id, 
      drs.replica_id, 
      drs.synchronization_state_desc, 
      ag.sequence_number
   FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
   WHERE drs.group_id = ag.group_id; 
   ```

   當 `synchronization_state_desc` 為 `SYNCHRONIZED` 時，即會同步處理次要複本。

3. 將 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 更新為 1。

   下列指令碼會將名為 `ag1` 的 AG 上的 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 設為 1。 執行下列指令碼之前，請以您的 AG 名稱取代 `ag1`：

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = 1;
   ```

   這項設定可確保所有使用中交易都已認可至主要複本及至少一個同步次要複本。 

4. 將主要複本降階為次要複本。 主要複本降階之後，會處於唯讀狀態。 在裝載主要複本的 SQL Server 執行個體上執行此命令，將角色更新為 `SECONDARY`：

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET (ROLE = SECONDARY); 
   ```

5. 將目標次要複本升階為主要。 

   ```SQL
   ALTER AVAILABILITY GROUP ag1 FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```  

   > [!NOTE] 
   > 若要刪除 AG，請使用 [DROP AVAILABILITY GROUP](https://docs.microsoft.com/en-us/sql/t-sql/statements/drop-availability-group-transact-sql)。 針對以叢集類型 NONE 或 EXTERNAL 建立的 AG，必須在 AG 的所有複本組件上執行此命令。