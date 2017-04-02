---
title: "複寫快照集代理程式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "快照集代理程式, 可執行檔"
  - "代理程式 [SQL Server 複寫], 快照集代理程式"
  - "命令提示字元 [SQL Server 複寫]"
  - "快照集代理程式, 參數參考"
ms.assetid: 2028ba45-4436-47ed-bf79-7c957766ea04
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# 複寫快照集代理程式
  「複寫快照集代理程式」是一個可執行檔，它會準備包含已發行資料表與資料庫物件之結構描述及資料的快照集檔案、將這些檔案儲存在快照集資料夾內，然後記錄散發資料庫中的同步處理作業。  
  
> [!NOTE]  
>  您可以使用任何順序來指定參數。  
  
## 語法  
  
```  
  
snapshot [ -?]   
-Publisher server_name[\instance_name]   
-Publication publication_name   
[-70Subscribers]   
[-BcpBatchSize bcp_batch_size]  
[-DefinitionFile def_path_and_file_name]  
[-Distributor server_name[\instance_name]]  
[-DistributorDeadlockPriority [-1|0|1] ]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1] ]  
[-DynamicFilterHostName dynamic_filter_host_name]  
[-DynamicFilterLogin dynamic_filter_login]  
[-DynamicSnapshotLocation dynamic_snapshot_location]   
[-EncryptionLevel [0|1|2]]  
[-FieldDelimiter field_delimiter]  
[-HistoryVerboseLevel [0|1|2|3] ]  
[-HRBcpBlocks number_of_blocks ]  
[-HRBcpBlockSize block_size ]  
[-HRBcpDynamicBlocks ]  
[-KeepAliveMessageInterval keep_alive_interval]  
[-LoginTimeOut login_time_out_seconds]  
[-MaxBcpThreads number_of_threads ]  
[-MaxNetworkOptimization [0|1]]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2] ]  
[-PacketSize packet_size]  
[-ProfileName profile_name]  
[-PublisherDB publisher_database]  
[-PublisherDeadlockPriority [-1|0|1] ]  
[-PublisherFailoverPartner server_name[\instance_name] ]  
[-PublisherLogin publisher_login]  
[-PublisherPassword publisher_password]   
[-PublisherSecurityMode [0|1] ]  
[-QueryTimeOut query_time_out_seconds]  
[-ReplicationType [1|2] ]  
[-RowDelimiter row_delimiter]  
[-StartQueueTimeout start_queue_timeout_seconds]  
[-UsePerArticleContentsView use_per_article_contents_view]  
```  
  
## 引數  
 **-?**  
 列印所有可用的參數。  
  
 **-發行者**  *server_name*[**\\***instance_name*]    
 這是發行者的名稱。 指定的預設執行個體的 server_name [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 該伺服器上。 指定 *server_name***\\***instance_name* 的具名執行個體 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 該伺服器上。  
  
 **-發行集** *發行集*  
 這是發行集的名稱。 只有在發行集設定成隨時都有快照供新的訂閱或重新初始化的訂閱使用時，這個參數才有效。  
  
 **-70Subscribers**  
 如果執行的任何 「 訂閱者 」 必須使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 7.0 版。  
  
 **-BcpBatchSize** *bcp*_ *批次*\_ *大小*  
 這是要在大量複製作業中傳送的資料列數目。  執行 **bcp in** 作業時，批次大小就是要在單一交易中傳送至伺服器的資料列數目，而且它也是「散發代理程式」記錄 bcp 進度訊息之前必須傳送的資料列數目。 執行時 **bcp out** 使用固定批次大小 1000年的作業。 值為 0 表示沒有記錄任何訊息。  
  
 **-DefinitionFile** *def_path_and_file_name*  
 這是代理程式定義檔的路徑。 代理程式定義檔包含代理程式的命令列引數。 此檔案的內容會剖析為可執行檔。 請使用雙引號 (") 來指定包含任意字元的引數值。  
  
 **-Distributor** *server_name*[**\\***instance_name*]  
 這是散發者的名稱。 指定 *server_name* 預設執行個體 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 該伺服器上。 指定 *server_name***\\***instance_name* 的具名執行個體 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 該伺服器上。  
  
 **-DistributorDeadlockPriority** [**-1**|**0**|**1**]  
 這是發生死結時散發者之快照集代理程式連接的優先權。 指定這個參數的目的是為了解決快照集產生期間，快照集代理程式與使用者應用程式之間可能會發生的死結。  
  
|DistributorDeadlockPriority 值|描述|  
|---------------------------------------|-----------------|  
|**-1**|在散發者端發生死結時，快照集代理程式以外的應用程式擁有優先權。|  
|**0** （預設值）|未指派優先權。|  
|**1**|在散發者端發生死結時，快照集代理程式擁有優先權。|  
  
 **-DistributorLogin** *distributor_login*  
 這是連接至使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證的散發者時，系統所使用的登入。  
  
 **-DistributorPassword** *distributor_password*  
 這是連接至使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證的散發者時，系統所使用的密碼。 。  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 指定散發者的安全性模式。 值為 **0** 指出 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證模式 （預設值），而值為 **1** 表示 Windows 驗證模式。  
  
 **-DynamicFilterHostName** *dynamic_filter_host_name*  
 用來設定的值 [HOST_NAME & #40。TRANSACT-SQL & #41;](../../../t-sql/functions/host-name-transact-sql.md) 在篩選時動態快照集建立。 例如，如果了子集篩選子句 `rep_id = HOST_NAME()` 指定發行項，而且您將設定 **DynamicFilterHostName** 屬性"FBJones"，然後再呼叫 「 合併代理程式僅資料列具有"FBJones" **rep_id** 將複寫資料行。  
  
 **-DynamicFilterLogin** *dynamic_filter_login*  
 用來設定的值 [SUSER_SNAME & #40。TRANSACT-SQL & #41;](../../../t-sql/functions/suser-sname-transact-sql.md)在篩選時動態快照集建立。 例如，如果了子集篩選子句 `user_id = SUSER_SNAME()` 指定發行項，並將 **DynamicFilterLogin** 屬性為"rsmith"，然後再呼叫 **執行** 方法 **Dynamicfilterlogin** 物件時，只有具有"rsmith"的資料列 **user_id** 快照集將包含資料行。  
  
 **-DynamicSnapshotLocation** *dynamic_snapshot_location*  
 這是應該產生動態快照集的位置。  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 這是建立連接時，快照集代理程式所使用的安全通訊端層 (SSL) 加密層級。  
  
|EncryptionLevel 值|說明|  
|---------------------------|-----------------|  
|**0**|指定不使用 SSL。|  
|**1**|指定要使用 SSL，但是代理程式不會驗證 SSL 伺服器憑證是否由受信任的簽發者簽署。|  
|**2**|指定要使用 SSL，而且憑證會經過驗證。|  
  
 如需詳細資訊，請參閱 [安全性概觀與 #40。複寫 & #41;](../../../relational-databases/replication/security/security-overview-replication.md)。  
  
 **-F** *field_delimiter*  
 這是在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大量複製資料檔案中標示欄位結尾的字元或字元序列。 預設值為 \n\<x$3>\n。  
  
 **-HistoryVerboseLevel** [ **1**| **2**| **3**]  
 指定在快照集作業期間記錄的記錄量。 您可以藉由選取記錄效能的影響降至最低 **1**。  
  
|HistoryVerboseLevel 值|說明|  
|-------------------------------|-----------------|  
|**0**|進度訊息會寫入主控台或輸出檔中。 但是，記錄不會記錄在散發資料庫中。|  
|**1**|一律更新相同狀態的上一個記錄訊息 (啟動、進度、成功等等)。 如果沒有任何具有相同狀態的上一筆記錄存在，便插入新的記錄。|  
|**2** （預設值）|除非記錄用於閒置訊息或長時間執行作業訊息等事件 (在此情況下，更新之前的記錄)，否則便插入新的記錄。|  
|**3**|除非記錄用於閒置訊息，否則一律插入新的記錄。|  
  
 **-HRBcpBlocks** *number_of_blocks*  
 是的數字 **bcp** 器和讀取器執行緒之間排入佇列的資料區塊。 預設值是 50。 **HRBcpBlocks** 只能搭配 Oracle 發行集。  
  
> [!NOTE]  
>  這個參數用於效能微調 **bcp** 從 Oracle 發行者 」 的效能。  
  
 -**HRBcpBlockSize***block_size*  
 是 (kb) 的大小，每個 **bcp** 資料區塊。 預設值為 64 KB。 **HRBcpBlocks** 只能搭配 Oracle 發行集。  
  
> [!NOTE]  
>  這個參數用於效能微調 **bcp** 從 Oracle 發行者 」 的效能。  
  
 **-HRBcpDynamicBlocks**  
 是是否每個大小 **bcp** 資料區塊可以動態地成長。 **HRBcpBlocks** 只能搭配 Oracle 發行集。  
  
> [!NOTE]  
>  這個參數用於效能微調 **bcp** 從 Oracle 發行者 」 的效能。  
  
 **-KeepAliveMessageInterval** *keep_alive_interval*  
 是一段時間，以秒為單位，快照集代理程式 」 正在等候後端訊息 」 的記錄之前 [MSsnapshot_history](../../../relational-databases/system-tables/mssnapshot-history-transact-sql.md) 資料表。 預設值為 300 秒。  
  
 **-LoginTimeOut** *login_time_out_seconds*  
 這是登入逾時之前的秒數。  預設值為 15 秒。  
  
 **-MaxBcpThreads** *number_of_threads*  
 指定可用平行方式執行的大量複製作業數目。 **MaxBcpThreads** 同時存在之執行緒和 ODBC 連接的最大數目是  或散發資料庫之同步處理交易中顯示的大量複製要求數目的較小者。 **MaxBcpThreads** 值必須是大於 **0** 而且沒有硬式編碼的上限。 預設值是 **1**。  
  
 \- **MaxNetworkOptimization** [ **0**| **1**]  
 這是指無關的刪除動作是否會傳送至訂閱者。 無關的刪除動作是針對不屬於訂閱者資料分割的資料列傳送至訂閱者的 DELETE 命令。 雖然無關的刪除動作不會影響資料完整性或聚合，但是它們可能會產生不必要的網路流量。 預設值的 **MaxNetworkOptimization** 是 **0**。 設定 **MaxNetworkOptimization** 至 **1** 藉此減少無關刪除的機會降低網路流量並擴大網路最佳化。 此參數設定為 **1** 亦可增加的中繼資料的儲存體，並導致效能降低在 「 發行者 」，如果有多個聯結篩選和複雜子集篩選層級。 您應該仔細評估複寫拓撲，並設定 **MaxNetworkOptimization** 至 **1** 才無關刪除的網路流量過高。  
  
> [!NOTE]  
>  此參數設定為 **1** 適合只有當合併式發行集的同步處理最佳化選項設定為 **true** ( **@keep_partition_changes** 參數 [sp_addmergepublication & #40;Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md))。  
  
 **-輸出** *output_path_and_file_name*  
 這是代理程式輸出檔的路徑。 如果未提供檔案名稱，輸出將傳送至主控台。 如果指定的檔案名稱存在，輸出就會附加至該檔案。  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 指定輸出是否應該詳細。  
  
|OutputVerboseLevel 值|描述|  
|------------------------------|-----------------|  
|**0**|僅列印錯誤訊息。|  
|**1** （預設值）|列印所有進度報表訊息 (預設值)。|  
|**2**|列印所有錯誤訊息和進度報表訊息 (可用於偵錯)。|  
  
 **-PacketSize** *packet_size*  
 這是快照集代理程式連接至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時所使用的封包大小 (以位元組為單位)。 預設值為 8192 個位元組。  
  
> [!NOTE]  
>  除非確信有助於提升效能，否則請勿變更封包大小。 對於大部分應用程式而言，預設封包大小是最適當的大小。  
  
 **-ProfileName** *profile_name*  
 指定要用於代理程式參數的代理程式設定檔。 **ProfileName** 如果  為 NULL，就會停用代理程式設定檔。 **ProfileName** 如果沒有指定 ，就會使用該代理程式類型的預設設定檔。 如需資訊，請參閱 [複寫代理程式設定檔](../../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
 **-PublisherDB** *publisher_database*  
 這是發行集資料庫的名稱。 *這個參數不支援 Oracle 發行者*。  
  
 **-PublisherDeadlockPriority** [**-1**|**0**|**1**]  
 這是發生死結時發行者之快照集代理程式連接的優先權。 指定這個參數的目的是為了解決快照集產生期間，快照集代理程式與使用者應用程式之間可能會發生的死結。  
  
|PublisherDeadlockPriority 值|描述|  
|-------------------------------------|-----------------|  
|**-1**|在發行者端發生死結時，快照集代理程式以外的應用程式擁有優先權。|  
|**0** （預設值）|未指派優先權。|  
|**1**|在發行者端發生死結時，快照集代理程式擁有優先權。|  
  
 **-PublisherFailoverPartner** *server_name*[**\\***instance_name*]  
 指定參與具有發行集資料庫之資料庫鏡像工作階段的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉夥伴執行個體。 如需詳細資訊，請參閱 [資料庫鏡像和複寫 & #40。SQL Server & #41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)。  
  
 **-PublisherLogin** *publisher_login*  
 這是連接至使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證的發行者時，系統所使用的登入。  
  
 **-PublisherPassword**  *publisher_password*  
 這是連接至使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證的發行者時，系統所使用的密碼。 。  
  
 **-PublisherSecurityMode** [ **0**| **1**]  
 指定發行者的安全性模式。 值為 **0** 指出 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證 （預設值），而值為 **1** 表示 Windows 驗證模式。  
  
 **-QueryTimeOut** *query_time_out_seconds*  
 這是查詢逾時之前的秒數。 預設值是 1800 秒。  
  
 **-ReplicationType** [ **1**| **2**]  
 指定複寫的類型。 值為 **1** 表示交易式複寫，而值的 **2** 表示合併式複寫。  
  
 **-RowDelimiter** *row_delimiter*  
 這是在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大量複製資料檔案中標示資料列結尾的字元或字元序列。 預設值為 \n\<,@g>\n。  
  
 **-StartQueueTimeout** *start_queue_timeout_seconds*  
 是的快照集代理程式時執行的並行動態快照集處理序數目會在所設定的限制所等待的秒數上限 **@max_concurrent_dynamic_snapshots** 屬性 [sp_addmergepublication & #40;TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 如果已到達最大秒數而且快照集代理程式仍然等候中，它就會結束。 值為 0 表示代理程式會永遠等候，不過您可以取消它。  
  
 \- **UsePerArticleContentsView** *use_per_article_contents_view*  
 這個參數已被取代，而且是為了回溯相容性才提供支援。  
  
## 備註  
  
> [!IMPORTANT]  
>  如果您已將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 安裝成在本機系統帳戶而非網域使用者帳戶 (預設值) 底下執行，這項服務就只能存取本機電腦。 如果在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 底下執行的快照集代理程式設定為使用 Windows 驗證模式，當它登入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時，快照集代理程式就會失敗。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設設定為  驗證。  
  
 若要啟動快照集代理程式，請執行 **snapshot.exe** 從命令提示字元。 如需資訊，請參閱 [複寫代理程式可執行檔](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
## 另請參閱  
 [複寫代理程式管理](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  