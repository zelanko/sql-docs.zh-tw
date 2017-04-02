---
title: "分散式可用性群組 (AlwaysOn 可用性群組) | Microsoft Docs"
ms.custom: ""
ms.date: "08/30/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f7c7acc5-a350-4a17-95e1-e689c78a0900
caps.latest.revision: 28
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 28
---
# 分散式可用性群組 (AlwaysOn 可用性群組)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  您可使用分散式可用性群組，將位於不同 Windows Server 容錯移轉叢集 (WSFC) 的兩個可用性群組建立關聯。 分散式可用性群組的主要用途之一，即是針對主要網站地理位置與 DR 網站分散的災害復原用途。 您想要將資料持續覆寫至 DR 網站，但不希望 DR 網站發生潛在的網路問題或狀況致使拖慢主要網站運作效能。  
  
 下列圖表說明分散式可用性群組的架構。  
  
 ![AlwaysOn Distributed Availability Groups](../../../database-engine/availability-groups/windows/media/alwayson-distributed-availability-groups.png "AlwaysOn Distributed Availability Groups")  
  
 在上圖中，有兩個不同的 Windows Server 容錯移轉叢集 (WFSC 1 和 WFSC 2)。 每個叢集皆有具相符資料庫設定的專屬可用性群組。 您可將分散式可用性群組視為是「針對可用性群組的可用性群組」。 在此範例中，AG 1 會成為主要可用性群組。 針對主要複本、AG 1 執行所有的插入和更新動作，然後再複寫至其次要複本。 不過，系統亦會將全體網路的變更一次複寫至 WSFC 2 上的次要可用性群組。 AG 2 可用性群組會將這些變更複寫至其次要複本。  
  
> [!IMPORTANT]  
>  在兩個可用性群組之間建立分散式可用性群組關係時，次要可用性群組會自動變為唯讀。 您只能針對主要可用性群組的主要複本 (在本範例中為 AG 1 的主要複本)，執行更新和插入動作。  
  
 位於單一 Windows Server 容錯移轉叢集的可用性群組，其分散式可用性群組差異如下：  
  
-   每個 WSFC 會維護專屬的仲裁模式以及節點投票設定。 這表示次要 WSFC 的健全狀況不會影響主要 WSFC。  
  
-   系統會透過網路將資料一次傳送至次要 WSFC，然後再於該叢集內部執行複寫。 在單一 WSFC，資料會個別傳送至每個複本。 針對地理位置分散的次要網站，分散式可用性群組可提供更優異的運作效率。  
  
-   主要與次要叢集上的作業系統版本可能有所不同。 在單一 WSFC 中，所有伺服器皆必須位於相同版本的作業系統上。 這可能會使用採輪流更新/升級作業系統方式的分散式可用性群組。  
  
-   主要與次要可用性群組必須具有相同的資料庫設定。  
  
-   不支援自動容錯移轉至次要可用性群組。  
  
## 建立分散式可用性群組  
 若要建立分散式可用性群組，您必須在每個 WSFC 上建立可用性群組與接聽程式。 隨後您再將其整合為分散式可用性群組。 下列步驟提供 TRANSACT-SQL 中的基本範例。 本範例未涵蓋關於建立可用性群組與接聽程式的所有詳細資訊，而僅著重探討與其相關的重要需求。  
  
### 在第一個叢集上建立主要可用性群組  
 在第一個 WSFC 上建立可用性群組。   在此範例中，會針對資料庫 `ag1` 將可用性群組命名為 `db1`。  
  
```tsql  
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
  
 請注意，此範例係採用直接植入，並針對複本與分散式可用性群組將 **SEEDING_MODE** 設為 **AUTOMATIC**。 這表示一旦建立次要複本與次要可用性群組，其即會自動填入而無須手動備份和還原主要資料庫。  
  
### 將次要複本聯結至主要可用性群組  
 任何次要複本皆必須透過 **JOIN** 選項，聯結至具 **ALTER AVAILABILITY GROUP** 的可用性群組。 本範例採用直接植入，因此您還必須透過  **GRANT CREATE ANY DATABASE** 選項呼叫 **ALTER AVAILABILITY GROUP** 。 這可讓可用性群組建立資料庫，並開始自動從主要複本將其植入。  
  
 在此範例中，系統會在次要複本 `server2`執行下列命令，以聯結 `ag1` 可用性群組。 接著會允許可用性群組在次要複本上建立資料庫。  
  
```tsql  
ALTER AVAILABILITY GROUP [ag1] JOIN   
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE  
GO  
```  
  
### 建立主要可用性群組的接聽程式  
 接下來要在第一個 WSFC 上建立主要可用性群組。 在此範例中，接聽程式會命名為 `ag1-listener`。 如需建立接聽程式的詳細指示，請參閱[建立或設定可用性群組接聽程式 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)。  
  
```  
ALTER AVAILABILITY GROUP [ag1]    
    ADD LISTENER 'ag1-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
### 在第二個叢集上建立次要可用性群組  
 接著在第二個 WSFC 上，建立第二個可用性群組 `ag2`。 在此案例中未指定資料庫，因為其會從主要可用性群組自動植入。  
  
```tsql  
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
>  請注意，次要可用性群組必須使用相同的資料庫鏡像端點 (在本範例中為通訊埠 5022)。 否則在執行本機容錯移轉後將會停止複寫。  
  
### 將次要複本聯結至次要可用性群組  
 在此範例中，系統會在次要複本 `server4`執行下列命令，以聯結 `ag2` 可用性群組。 接著會允許可用性群組在次要複本上建立資料庫，以支援直接植入。  
  
```tsql  
ALTER AVAILABILITY GROUP [ag2] JOIN   
ALTER AVAILABILITY GROUP [ag2] GRANT CREATE ANY DATABASE  
GO  
```  
  
### 建立次要可用性群組的接聽程式  
 接下來要在第二個 WSFC 上建立次要可用性群組。 在此範例中，接聽程式會命名為 `ag2-listener`。 如需建立接聽程式的詳細指示，請參閱[建立或設定可用性群組接聽程式 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)。  
  
```  
ALTER AVAILABILITY GROUP [ag2]    
    ADD LISTENER 'ag2-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
### 在第一個叢集上建立分散式可用性群組  
 在第一個 WSFC 上，建立分散式可用性群組 (在此範例中名為 `distributedag`)。 使用 **CREATE AVAILABILITY GROUP** 命令搭配 **DISTRIBUTED** 選項。 **AVAILABILITY GROUP ON** 參數會指定成員可用性群組 `ag1` 和 `ag2`。  
  
```tsql  
CREATE AVAILABILITY GROUP [distributedag]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO   
```  
  
> [!NOTE]  
>  **LISTENER_URL** 會指定每個可用性群組的接聽程式，以及可用性群組的資料庫鏡像端點。 在此範例中，其為通訊埠 `5022` (非用於建立接聽程式的通訊埠 `60173`)。  
  
### 在第二個叢集上聯結分散式可用性群組  
 然後在第二個 WSFC 上聯結分散式可用性群組。  
  
```tsql  
ALTER AVAILABILITY GROUP [distributedag]   
   JOIN   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO  
```  

  
## 容錯移轉至次要可用性群組  
 目前僅支援手動容錯移轉。 下列 Transact-SQL 陳述式會針對名為 `distributedag` 的分散式可用性群組，強制執行容錯移轉：  


1. 將次要可用性群組的可用性模式設定為同步認可。 
    
      ```tsql  
      ALTER AVAILABILITY GROUP [distributedag] 
      MODIFY 
      AVAILABILITY GROUP ON
      'ag1' WITH  
         ( 
          LISTENER_URL = 'tcp://ag1-listener:5022',  
          AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = MANUAL, 
          SEEDING_MODE = MANUAL 
          ), 
      'ag2' WITH  
        ( 
        LISTENER_URL = 'tcp://ag2-listener:5022', 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
        FAILOVER_MODE = MANUAL, 
        SEEDING_MODE = MANUAL 
        );  
       
      ```  
  
1. 等到分散式可用性群組的狀態變更為 `SYNCHRONIZED`。 在裝載主要可用性群組之主要複本的 SQL Server 上，執行下列查詢。 
    
      ```tsql  
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

    當可用性群組 **synchronization_state_desc** 成為 `SYNCHRONIZED` 之後繼續進行。 如果 **synchronization_state_desc** 不是 `SYNCHRONIZED`，請每隔五秒執行命令一次，直到變更為止。 在 **synchronization_state_desc** = `SYNCHRONIZED` 之前，請不要繼續進行。 

1. 在裝載主要可用性群組之主要複本的 SQL Server 上，將分散式可用性群組角色設定為 `SECONDARY`。 

      ```tsql
      ALTER AVAILABILITY GROUP distributedag SET (ROLE = SECONDARY); 
      ```  

    注意︰目前無法使用分散式可用性群組。

1. 測試容錯移轉整備。 執行下列查詢：

      ```tsql
      SELECT ag.name, 
             drs.database_id, 
             drs.group_id, 
             drs.replica_id, 
             drs.synchronization_state_desc, 
             drs.end_of_log_lsn 
      FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
      WHERE drs.group_id = ag.group_id; 
      ```  
    當 **synchronization_state_desc** 為 `SYNCHRONIZED`，且兩個可用性群組的 **end_of_log_lsn** 皆相同時，可用性群組便準備好進行容錯移轉。 

1. 從主要可用性群組容錯移轉至次要可用性群組。 在裝載次要可用性群組之主要複本的 SQL Server 上，執行下列命令。 

      ```tsql
      ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
      ```  
      注意︰在這個步驟之後，就可以使用分散式可用性群組。
      
完成上述步驟之後，分散式可用性群組就可以進行容錯移轉，而不會遺失任何資料。 如果可用性群組所橫跨的地理位置距離會造成延遲，Microsoft 建議將可用性模式變更回 ASYNCHRONOUS_COMMIT。 
  
## 移除分散式可用性群組  
 下列 Transact-SQL 陳述式會移除名為 `distributedag` 的分散式可用性群組：  
  
```tsql  
DROP AVAILABILITY GROUP [distributedag]  
```  

## 使用容錯移轉叢集執行個體建立分散式可用性群組

您可以使用容錯移轉叢集執行個體 (FCI) 上的可用性群組，建立分散式可用性群組。 在此情況下，您不需要可用性群組接聽程式。 請使用 FCI 執行個體之主要複本的虛擬網路名稱 (VNN)。 下列範例顯示稱為 SQLFCIDAG 的分散式可用性群組。 一個可用性群組為 SQLFCIAG。 SQLFCIAG 具有 2 個 FCI 複本。 主要 FCI 複本的 VNN 是 SQLFCIAG-1，而次要 FCI 複本的 VNN 是 SQLFCIAG-2。 分散式可用性群組也包含 SQLAG-DR，可用於災害復原。

![AlwaysOn 分散式可用性群組](../../../database-engine/availability-groups/windows/media/always-on-availability-group-distributed.png)

 
 
 下列 DDL 會建立此分散式可用性群組。 

```tsql  
CREATE AVAILABILITY GROUP [SQLFCIDAG]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
  'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-1:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      ),   
  'SQLAG-DR' WITH    
       (   
         LISTENER_URL = 'tcp://SQLAG-DR:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      );   
```  

請注意，接聽程式 URL 會是主要 FCI 執行個體的 VNN。

## 手動容錯移轉分散式可用性群組中的 FCI

若要手動容錯移轉 FCI 可用性群組，請更新分散式可用性群組以反映接聽程式 URL 的變更。 例如，在 SQLFCIAG 的主要 AG 和次要 AG 上執行下列 DDL：

```tsql  
ALTER AVAILABILITY GROUP [SQLFCIDAG]  
   MODIFY AVAILABILITY GROUP ON  
 'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-2:5022'
    )
```  
  
## 另請參閱  
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  