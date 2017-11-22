---
title: "設定分散式的可用性群組 (Alwayson 可用性群組) | Microsoft Docs"
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f7c7acc5-a350-4a17-95e1-e689c78a0900
caps.latest.revision: "28"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3e122b8b8aba89b971407c43c35715a387a687e1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="configure-distributed-availability-group"></a>設定分散式的可用性群組  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

若要建立分散式的可用性群組，您必須在每個 Windows Server 容錯移轉叢集 (WSFC) 上建立可用性群組與接聽程式。 隨後您再將這些可用性群組合併成分散式的可用性群組。 下列步驟提供 TRANSACT-SQL 中的基本範例。 本範例未涵蓋關於建立可用性群組與接聽程式的所有詳細資料，而僅著重探討與其相關的重要需求。 

如需分散式可用性群組的技術概觀，請參閱[分散式可用性群組](distributed-availability-groups.md)。   

## <a name="prerequisites"></a>必要條件

### <a name="set-the-endpoint-listeners-to-listen-to-all-ip-addresses"></a>設定端點接聽程式來接聽所有 IP 位址

請確定端點可以在分散式可用性群組的不同可用性群組之間進行通訊。 如果一個可用性群組設定為端點上的特定網路，分散式的可用性群組不會正常運作。 在分散式可用性群組中裝載複本的每部伺服器上，將接聽程式設定為 `LISTENER_IP = ALL`。 

#### <a name="create-a-listener-to-listen-to-all-ip-addresses"></a>建立接聽所有 IP 位址的接聽程式

例如，下列指令碼會在 TCP 通訊埠 5022 上建立接聽程式端點，接聽所有 IP 位址。  

```sql
CREATE ENDPOINT [aodns-hadr] 
    STATE=STARTED
    AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)
FOR DATA_MIRRORING (
   ROLE = ALL, 
   AUTHENTICATION = WINDOWS NEGOTIATE,
   ENCRYPTION = REQUIRED ALGORITHM AES
)
GO
```

#### <a name="alter-a-listener-to-listen-to-all-ip-addresses"></a>將接聽程式改變為接聽所有 IP 位址

例如，下列指令碼會變更接聽程式端點，接聽所有 IP 位址。  

```sql
ALTER ENDPOINT [aodns-hadr] 
    AS TCP (LISTENER_IP = ALL)
GO
```

## <a name="create-first-availability-group"></a>建立第一個可用性群組

### <a name="create-the-primary-availability-group-on-the-first-cluster"></a>在第一個叢集上建立主要可用性群組  
在第一個 WSFC 上建立可用性群組。   在此範例中，會針對資料庫 `ag1` 將可用性群組命名為 `db1`。      
  
```sql  
CREATE AVAILABILITY GROUP [ag1]   
FOR DATABASE db1   
REPLICA ON N'server1' WITH (ENDPOINT_URL = N'TCP://server1.contoso.com:5022',  
    FAILOVER_MODE = AUTOMATIC,  
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC),   
N'server2' WITH (ENDPOINT_URL = N'TCP://server2.contoso.com:5022',   
    FAILOVER_MODE = AUTOMATIC,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC);   
GO  
  
```  
  
>[!NOTE]
>上一個範例係採用直接植入，並針對複本與分散式可用性群組將 **SEEDING_MODE** 設為 **AUTOMATIC** 。 這個組態會將次要複本與次要可用性群組設定成自動填入，無須手動備份和還原主要資料庫。  
  
### <a name="join-the-secondary-replicas-to-the-primary-availability-group"></a>將次要複本聯結至主要可用性群組  
任何次要複本皆必須透過 **JOIN** 選項，聯結至具 **ALTER AVAILABILITY GROUP** 的可用性群組。 本範例採用直接植入，因此您還必須透過  **GRANT CREATE ANY DATABASE** 選項呼叫 **ALTER AVAILABILITY GROUP** 。 此設定可讓可用性群組建立資料庫，並開始自動從主要複本將其植入。  
  
在此範例中，系統會在次要複本 `server2`執行下列命令，以聯結 `ag1` 可用性群組。 接著會允許可用性群組在次要複本上建立資料庫。  
  
```sql  
ALTER AVAILABILITY GROUP [ag1] JOIN   
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE  
GO  
```  

>[!NOTE]
>當可用性群組在次要複本上建立資料庫時，它會將資料庫擁有者設成執行 `ALTER AVAILABILITY GROUP` 陳述式以授與建立任何資料庫權限的帳戶。 如需完整資訊，請參閱[授與可用性群組在次要複本上建立資料庫的權限](automatic-seeding-secondary-replicas.md#grantCreate)。
  
### <a name="create-a-listener-for-the-primary-availability-group"></a>建立主要可用性群組的接聽程式  

接下來要在第一個 WSFC 上建立主要可用性群組。 在此範例中，接聽程式會命名為 `ag1-listener`。 如需建立接聽程式的詳細指示，請參閱[建立或設定可用性群組接聽程式 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)。  
  
```sql
ALTER AVAILABILITY GROUP [ag1]    
    ADD LISTENER 'ag1-listener' ( 
        WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , 
        PORT = 60173);    
GO  
```  
  

## <a name="create-second-availability-group"></a>建立第二個可用性群組  
 接著在第二個 WSFC 上，建立第二個可用性群組 `ag2`。 在此案例中未指定資料庫，因為其會從主要可用性群組自動植入。  
  
```sql  
CREATE AVAILABILITY GROUP [ag2]   
FOR   
REPLICA ON N'server3' WITH (ENDPOINT_URL = N'TCP://server3.contoso.com:5022',   
    FAILOVER_MODE = MANUAL,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC),   
N'server4' WITH (ENDPOINT_URL = N'TCP://server4.contoso.com:5022',   
    FAILOVER_MODE = MANUAL,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC);   
GO  
```  
  
> [!NOTE]  
> 次要可用性群組必須使用相同的資料庫鏡像端點 (在本範例中為通訊埠 5022)。 否則在執行本機容錯移轉後將會停止複寫。  
  
### <a name="join-the-secondary-replicas-to-the-secondary-availability-group"></a>將次要複本聯結至次要可用性群組  
 在此範例中，系統會在次要複本 `server4`執行下列命令，以聯結 `ag2` 可用性群組。 接著會允許可用性群組在次要複本上建立資料庫，以支援直接植入。  
  
```sql  
ALTER AVAILABILITY GROUP [ag2] JOIN   
ALTER AVAILABILITY GROUP [ag2] GRANT CREATE ANY DATABASE  
GO  
```  
  
### <a name="create-a-listener-for--the-secondary-availability-group"></a>建立次要可用性群組的接聽程式  
 接下來要在第二個 WSFC 上建立次要可用性群組。 在此範例中，接聽程式會命名為 `ag2-listener`。 如需建立接聽程式的詳細指示，請參閱[建立或設定可用性群組接聽程式 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)。  
  
```  
ALTER AVAILABILITY GROUP [ag2]    
    ADD LISTENER 'ag2-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
## <a name="create-distributed-availability-group-on-first-cluster"></a>在第一個叢集上建立分散式可用性群組  
 在第一個 WSFC 上，建立分散式可用性群組 (在此範例中名為 `distributedag` )。 使用 **CREATE AVAILABILITY GROUP** 命令搭配 **DISTRIBUTED** 選項。 **AVAILABILITY GROUP ON** 參數會指定成員可用性群組 `ag1` 和 `ag2`。  
  
```sql  
CREATE AVAILABILITY GROUP [distributedag]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO   
```  
  
> [!NOTE]  
>  **LISTENER_URL** 會指定每個可用性群組的接聽程式，以及可用性群組的資料庫鏡像端點。 在此範例中，其為通訊埠 `5022` (非用於建立接聽程式的通訊埠 `60173` )。  
  
## <a name="join-distributed-availability-group-on-second-cluster"></a>將分散式可用性群組加入第二個叢集  
 然後在第二個 WSFC 上聯結分散式可用性群組。  
  
```sql  
ALTER AVAILABILITY GROUP [distributedag]   
   JOIN   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO  
```  

  
## <a name="failover"></a> 容錯移轉至次要可用性群組  
目前僅支援手動容錯移轉。 下列 Transact-SQL 陳述式會容錯移轉名為 `distributedag` 的分散式可用性群組：  


1. 將次要可用性群組的可用性模式設定為同步認可。 
    
      ```sql  
      ALTER AVAILABILITY GROUP [distributedag] 
      MODIFY 
      AVAILABILITY GROUP ON
      'ag1' WITH 
         ( 
          LISTENER_URL = 'tcp://ag1-listener.contoso.com:5022',  
          AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = MANUAL, 
          SEEDING_MODE = MANUAL 
          ), 
      'ag2' WITH  
        ( 
        LISTENER_URL = 'tcp://ag2-listener.contoso.com:5022', 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
        FAILOVER_MODE = MANUAL, 
        SEEDING_MODE = MANUAL 
        );  
       
      ```  
   >[!NOTE]
   >與一般可用性群組相似，分散式可用性群組中兩個可用性群組複本的同步處理狀態會取決於這兩個複本的可用性模式。 例如，若要發生同步認可，目前的主要可用性群組與次要可用性群組都必須設定成同步認可可用性模式。  


1. 等到分散式可用性群組的狀態變更為 `SYNCHRONIZED`。 在裝載主要可用性群組之主要複本的 SQL Server 上，執行下列查詢。 
    
      ```sql  
      SELECT ag.name
             , drs.database_id
             , drs.group_id
             , drs.replica_id
             , drs.synchronization_state_desc
             , drs.end_of_log_lsn 
        FROM sys.dm_hadr_database_replica_states drs,
        sys.availability_groups ag
          WHERE drs.group_id = ag.group_id;      
      ```  

    當可用性群組 **synchronization_state_desc** 成為 `SYNCHRONIZED`之後繼續進行。 如果 **synchronization_state_desc** 不是 `SYNCHRONIZED`，請每隔五秒執行命令一次，直到變更為止。 在 **synchronization_state_desc** = `SYNCHRONIZED`之前，請不要繼續進行。 

1. 在裝載主要可用性群組主要複本的 SQL Server 上，將分散式可用性群組角色設定為 `SECONDARY`。 

    ```sql
    ALTER AVAILABILITY GROUP distributedag SET (ROLE = SECONDARY); 
    ```  

    目前無法使用分散式可用性群組。

1. 測試容錯移轉整備。 執行下列查詢：

    ```sql
    SELECT ag.name, 
        drs.database_id, 
        drs.group_id, 
        drs.replica_id, 
        drs.synchronization_state_desc, 
        drs.end_of_log_lsn 
    FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
    WHERE drs.group_id = ag.group_id; 
    ```  
    當 **synchronization_state_desc** 為 `SYNCHRONIZED`，且兩個可用性群組的 **end_of_log_lsn** 皆相同時，可用性群組即準備好進行容錯移轉。 

1. 從主要可用性群組容錯移轉至次要可用性群組。 在裝載次要可用性群組之主要複本的 SQL Server 上，執行下列命令。 

    ```sql
    ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
    ```  

    在這個步驟之後，就可以使用分散式可用性群組。
      
完成上述步驟之後，分散式可用性群組就可以進行容錯移轉，而不會遺失任何資料。 如果可用性群組所橫跨的地理位置距離會造成延遲，請將可用性模式變更回 ASYNCHRONOUS_COMMIT。 
  
## <a name="remove-a-distributed-availability-group"></a>移除分散式可用性群組  
 下列 Transact-SQL 陳述式會移除名為 `distributedag`的分散式可用性群組：  
  
```sql  
DROP AVAILABILITY GROUP [distributedag]  
```  

## <a name="create-distributed-availability-group-on-failover-cluster-instances"></a>在容錯移轉叢集執行個體上建立分散式可用性群組

您可以使用容錯移轉叢集執行個體 (FCI) 上的可用性群組，建立分散式可用性群組。 在此情況下，您不需要可用性群組接聽程式。 請使用 FCI 執行個體之主要複本的虛擬網路名稱 (VNN)。 下列範例顯示稱為 SQLFCIDAG 的分散式可用性群組。 一個可用性群組為 SQLFCIAG。 SQLFCIAG 有兩個 FCI 複本。 主要 FCI 複本的 VNN 是 SQLFCIAG-1，而次要 FCI 複本的 VNN 是 SQLFCIAG-2。 分散式可用性群組也包含 SQLAG-DR，可用於災害復原。

![AlwaysOn 分散式可用性群組](../../../database-engine/availability-groups/windows/media/always-on-availability-group-distributed.png)

 
 
 下列 DDL 會建立此分散式可用性群組。 

```sql  
CREATE AVAILABILITY GROUP [SQLFCIDAG]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
  'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-1.contoso.com:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      ),   
  'SQLAG-DR' WITH    
       (   
         LISTENER_URL = 'tcp://SQLAG-DR.contoso.com:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      );   
```  

接聽程式 URL 會是主要 FCI 執行個體的 VNN。

## <a name="manually-fail-over-fci-in-distributed-availability-group"></a>手動容錯移轉分散式可用性群組中的 FCI

若要手動容錯移轉 FCI 可用性群組，請更新分散式可用性群組以反映接聽程式 URL 的變更。 例如，在 SQLFCIAG 的主要 AG 和次要 AG 上執行下列 DDL：

```sql  
ALTER AVAILABILITY GROUP [SQLFCIDAG]  
   MODIFY AVAILABILITY GROUP ON  
 'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-2.contoso.com:5022'
    )
```  
  
## <a name="next-steps"></a>後續的步驟

 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
