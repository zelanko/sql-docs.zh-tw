每個可用性群組只有一個主要複本。 主要複本允許讀取和寫入。 若要變更是主要的複本，您可以容錯移轉。 在高可用性的可用性群組中，叢集管理員會自動化容錯移轉程序。 在讀取級別可用性群組中，容錯移轉程序為手動。 

有兩種方式來容錯移轉中的向外延展讀取可用性群組的主要複本：

- 會遺失資料的強制手動容錯移轉
- 不會遺失資料的手動容錯移轉

### <a name="forced-manual-failover-with-data-loss"></a>會遺失資料的強制手動容錯移轉

當主要複本無法使用，而且無法復原，請使用這個方法。 

若要強制容錯移轉的資料遺失，連接到裝載目標次要複本並執行的 SQL Server 執行個體：

```SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

### <a name="manual-failover-without-data-loss"></a>不會遺失資料的手動容錯移轉

當主要複本可以使用，但您需要暫時或永久變更設定並變更裝載主要複本的 SQL Server 執行個體時，請使用這個方法。 當您發出手動容錯移轉之前，請確定目標次要複本是最新狀態以避免資料遺失。 

手動容錯移轉不會遺失資料：

1. 做為目標的次要複本`SYNCHRONOUS_COMMIT`。

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        MODIFY REPLICA ON N'**<node2>*' 
        WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```

2. 執行下列查詢來識別使用中交易被認可至主要複本和至少一個同步次要複本： 

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

3. 更新`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`設為 1。

   下列指令碼設定`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`設為 1 到可用性群組上名為`ag1`。 執行下列指令碼之前，取代`ag1`與可用性群組的名稱：

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = 1;
   ```

   此設定可確保每個使用中交易認可至主要複本和至少一個同步次要複本。 

4. 降級至次要複本的主要複本。 主要複本降級之後，它會處於唯讀狀態。 裝載更新至角色的主要複本的 SQL Server 執行個體上執行這個命令`SECONDARY`:

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET (ROLE = SECONDARY); 
   ```

5. 將目標次要複本升階為主要。 

   ```SQL
   ALTER AVAILABILITY GROUP ag1 FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```  

   > [!NOTE] 
   > 若要刪除可用性群組，請使用[DROP AVAILABILITY GROUP](https://docs.microsoft.com/en-us/sql/t-sql/statements/drop-availability-group-transact-sql)。 使用 CLUSTER_TYPE NONE 或外部建立可用性群組，必須在屬於可用性群組的所有複本上執行此命令。