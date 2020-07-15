---
title: 複寫快照集代理程式 | Microsoft Docs
description: 在 SQL Server 中，複寫快照集代理程式會準備快照集檔案、將這些檔案儲存在資料夾中，以及記錄散發資料庫中的同步處理作業。
ms.custom: ''
ms.date: 10/29/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Snapshot Agent, executables
- agents [SQL Server replication], Snapshot Agent
- command prompt [SQL Server replication]
- Snapshot Agent, parameter reference
ms.assetid: 2028ba45-4436-47ed-bf79-7c957766ea04
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 7132154bcb61e84d052891c200589cf157b31f65
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730224"
---
# <a name="replication-snapshot-agent"></a>複寫快照集代理程式
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../../includes/applies-to-version/sql-asdb.md)]
  「複寫快照集代理程式」是一個可執行檔，它會準備包含已發行資料表與資料庫物件之結構描述及資料的快照集檔案、將這些檔案儲存在快照集資料夾內，然後記錄散發資料庫中的同步處理作業。  
  
> [!NOTE]  
>  - 您可以使用任何順序來指定參數。  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="syntax"></a>語法  
  
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
[-PrefetchTables [0|1] ]  
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
  
## <a name="arguments"></a>引數  
 **-?**  
 列印所有可用的參數。  
  
 **-Publisher**  _server_name_[ **\\** _instance\_name_]  
 這是發行者的名稱。 請針對該伺服器上的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設執行個體指定 server_name。 請針對該伺服器上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 具名執行個體指定 _server\_name_ **\\** _instance\_name_。  
  
 **-Publication** _publication_  
 這是發行集的名稱。 只有在發行集設定成隨時都有快照供新的訂閱或重新初始化的訂閱使用時，這個參數才有效。  
  
 **-70Subscribers**  
 如果有任何訂閱者正在執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 7.0 版，您就必須使用這個參數。  
  
 **-BcpBatchSize** _bcp_\_ *batch*\_ *size*  
 這是要在大量複製作業中傳送的資料列數目。 執行 **bcp in** 作業時，批次大小就是要在單一交易中傳送至伺服器的資料列數目，而且它也是「散發代理程式」記錄 **bcp** 進度訊息之前必須傳送的資料列數目。 執行 **bcp out** 作業時，系統會使用固定批次大小 1000。 值為 0 表示沒有記錄任何訊息。  
  
 **-DefinitionFile** _def_path_and_file_name_  
 這是代理程式定義檔的路徑。 代理程式定義檔包含代理程式的命令列引數。 此檔案的內容會剖析為可執行檔。 請使用雙引號 (") 來指定包含任意字元的引數值。  
  
 **-Distributor** _server_name_[ **\\** _instance\_name_]  
 這是散發者的名稱。 請針對該伺服器上的 *預設執行個體指定* server_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 請針對該伺服器上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 具名執行個體指定 _server\_name_ **\\** _instance\_name_。  
  
 **-DistributorDeadlockPriority** [ **-1**|**0**|**1**]  
 這是發生死結時散發者之快照集代理程式連接的優先權。 指定這個參數的目的是為了解決快照集產生期間，快照集代理程式與使用者應用程式之間可能會發生的死結。  
  
|DistributorDeadlockPriority 值|描述|  
|---------------------------------------|-----------------|  
|**-1**|在散發者端發生死結時，快照集代理程式以外的應用程式擁有優先權。|  
|**0** (預設值)|未指派優先權。|  
|**1**|在散發者端發生死結時，快照集代理程式擁有優先權。|  
  
 **-DistributorLogin** _distributor_login_  
 這是連接至使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證的散發者時，系統所使用的登入。  
  
 **-DistributorPassword** _distributor_password_  
 這是連接至使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證的散發者時，系統所使用的密碼。 。  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 指定散發者的安全性模式。 值為 **0** 表示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證模式 (預設值)，而值為 **1** 則表示 Windows 驗證模式。  
  
 **-DynamicFilterHostName** _dynamic_filter_host_name_  
 這是建立動態快照集時，用來進行篩選所設定的 [HOST_NAME &#40;Transact-SQL&#41;](../../../t-sql/functions/host-name-transact-sql.md) 值。 例如，如果已針對發行項指定了子集篩選子句 `rep_id = HOST_NAME()` ，而且您在呼叫「合併代理程式」之前將 **DynamicFilterHostName** 屬性設定為 "FBJones"，系統就只會複寫 **rep_id** 資料行中具有 "FBJones" 的資料列。  
  
 **-DynamicFilterLogin** _dynamic_filter_login_  
 這是建立動態快照集時，用來進行篩選所設定的 [SUSER_SNAME &#40;Transact-SQL&#41;](../../../t-sql/functions/suser-sname-transact-sql.md) 值。 例如，如果已針對發行項指定了子集篩選子句 `user_id = SUSER_SNAME()` ，而且您在呼叫 **SQLSnapshot** 物件的 **Run** 方法之前將 **DynamicFilterLogin** 屬性設定為 "rsmith"，就只有 **user_id** 資料行中具有 "rsmith" 的資料列會加入快照集中。  
  
 **-DynamicSnapshotLocation** _dynamic_snapshot_location_  
 這是應該產生動態快照集的位置。  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 這是建立連線時，快照集代理程式所使用的傳輸層安全性 (TLS) (先前稱為安全通訊端層 (SSL)) 加密層級。  
  
|EncryptionLevel 值|描述|  
|---------------------------|-----------------|  
|**0**|指定不使用 TLS。|  
|**1**|指定要使用 TLS，但是代理程式不會驗證 TLS/SSL 伺服器憑證是否由受信任的簽發者簽署。|  
|**2**|指定要使用 TLS，而且憑證會經過驗證。|  

 > [!NOTE]  
 >  定義的 TLS/SSL 憑證必須包含 SQL Server 的完整網域名稱才會有效。 為了讓代理程式能在將 -EncryptionLevel 設定為 2 時成功連線，請在本機 SQL Server 上建立別名。 ‘Alias Name’ 參數應為伺服器名稱，且應將 ‘Server’ 參數設為 SQL Server 的完整名稱。
  
 如需詳細資訊，請參閱[檢視及修改複寫安全性設定](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
 **-FieldDelimiter** _field_delimiter_  
 這是在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大量複製資料檔案中標示欄位結尾的字元或字元序列。 預設為 \n\<x$3>\n。  
  
 **-HistoryVerboseLevel** [ **1**| **2**| **3**]  
 指定在快照集作業期間記錄的記錄量。 您可以透過選取 **1**，盡量減少記錄作業對效能造成的影響。  
  
|HistoryVerboseLevel 值|描述|  
|-------------------------------|-----------------|  
|**0**|進度訊息會寫入主控台或輸出檔中。 但是，記錄不會記錄在散發資料庫中。|  
|**1**|一律更新相同狀態的上一個記錄訊息 (啟動、進度、成功等等)。 如果沒有任何具有相同狀態的上一筆記錄存在，便插入新的記錄。|  
|**2** (預設值)|除非記錄用於閒置訊息或長時間執行作業訊息等事件 (在此情況下，更新之前的記錄)，否則便插入新的記錄。|  
|**3**|除非記錄用於閒置訊息，否則一律插入新的記錄。|  
  
 **-HRBcpBlocks** _number_of_blocks_  
 這是在寫入器與讀取器執行緒之間排入佇列的 **bcp** 資料區塊數目。 預設值是 50。 **HRBcpBlocks** 只能搭配 Oracle 發行集使用。  
  
> [!NOTE]  
>  這個參數是用於從 Oracle 發行者進行 **bcp** 效能的效能微調。  
  
 -**HRBcpBlockSize**_block\_size_  
 這是每個 **bcp** 資料區塊的大小 (以 KB 為單位)。 預設值為 64 KB。 **HRBcpBlocks** 只能搭配 Oracle 發行集使用。  
  
> [!NOTE]  
>  這個參數是用於從 Oracle 發行者進行 **bcp** 效能的效能微調。  
  
 **-HRBcpDynamicBlocks**  
 這是指每個 **bcp** 資料區塊的大小是否可以動態地成長。 **HRBcpBlocks** 只能搭配 Oracle 發行集使用。  
  
> [!NOTE]  
>  這個參數是用於從 Oracle 發行者進行 **bcp** 效能的效能微調。  
  
 **-KeepAliveMessageInterval** _keep_alive_interval_  
 這是將「正在等候後端訊息」記錄至 [MSsnapshot_history](../../../relational-databases/system-tables/mssnapshot-history-transact-sql.md) 資料表之前，快照集代理程式等候的時間量 (以秒為單位)。 預設值為 300 秒。  
  
 **-LoginTimeOut** _login_time_out_seconds_  
 這是登入逾時之前的秒數。 預設值為 15 秒。  
  
 **-MaxBcpThreads** _number_of_threads_  
 指定可用平行方式執行的大量複製作業數目。 同時存在之執行緒和 ODBC 連接的最大數目是 **MaxBcpThreads** 或散發資料庫之同步處理交易中顯示的大量複製要求數目的較小者。 **MaxBcpThreads** 必須具有大於 **0** 的值而且沒有硬式編碼的上限。 預設值為處理器數目的兩倍。  
  
 \- **MaxNetworkOptimization** [ **0**| **1**]  
 這是指無關的刪除動作是否會傳送至訂閱者。 無關的刪除動作是針對不屬於訂閱者資料分割的資料列傳送至訂閱者的 DELETE 命令。 雖然無關的刪除動作不會影響資料完整性或聚合，但是它們可能會產生不必要的網路流量。 **MaxNetworkOptimization** 的預設值為 **0**。 將 **MaxNetworkOptimization** 設定為 **1** 會盡可能減少無關刪除動作的機會，因而縮減網路流量並擴大網路最佳化。 如果聯結篩選和複雜子集篩選的多重層級存在，將這個參數設定為 **1** 也可能會增加中繼資料的儲存體，而且導致發行者端的效能降低。 您應該仔細地評估複寫拓撲，並且只有在無關刪除動作的網路流量高得無法接受，才將 **MaxNetworkOptimization** 設定為 **1** 。  
  
> [!NOTE]
>  只有當合併式發行集之同步處理最佳化選項設定為 **true** ([sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 的 `@keep_partition_changes**` 參數) 時，將這個參數設定為 **1** 才有用。  
  
 **-Output** _output_path_and_file_name_  
 這是代理程式輸出檔的路徑。 如果未提供檔案名稱，輸出將傳送至主控台。 如果指定的檔案名稱存在，輸出就會附加至該檔案。  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 指定輸出是否應該詳細。  
  
|OutputVerboseLevel 值|描述|  
|------------------------------|-----------------|  
|**0**|僅列印錯誤訊息。|  
|**1** (預設值)|列印所有進度報表訊息 (預設值)。|  
|**2**|列印所有錯誤訊息和進度報表訊息 (可用於偵錯)。|  
  
 **-PacketSize** _packet_size_  
 這是快照集代理程式連接至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]時所使用的封包大小 (以位元組為單位)。 預設值為 8192 個位元組。  
  
> [!NOTE]  
>  除非確信有助於提升效能，否則請勿變更封包大小。 對於大部分應用程式而言，預設封包大小是最適當的大小。  

**-PrefetchTables** [ **0**| **1**]  
 指定是否要預先擷取並快取資料表物件的選擇性參數。  預設行為是根據內部計算，使用 SMO 元件預先擷取特調資料表內容。  此參數在 SMO 預先擷取作業花非常長時間執行的情況下很實用。 若未使用此參數，會在執行階段根據已新增為要發佈之發行項的資料表百分比來制訂決策。  
  
|OutputVerboseLevel 值|描述|  
|------------------------------|-----------------|  
|**0**|SMO 元件的「呼叫以預先擷取」方法已停用。|  
|**1**|「快照集代理程式」將會呼叫預先擷取方法以使用 SMO 快取某些資料表內容|  

 **-ProfileName** _profile_name_  
 指定要用於代理程式參數的代理程式設定檔。 如果 **ProfileName** 為 NULL，就會停用代理程式設定檔。 如果沒有指定 **ProfileName** ，就會使用該代理程式類型的預設設定檔。 如需資訊，請參閱[複寫代理程式設定檔](../../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
 **-PublisherDB** _publisher_database_  
 這是發行集資料庫的名稱。 *這個參數不支援 Oracle 發行者*。  
  
 **-PublisherDeadlockPriority** [ **-1**|**0**|**1**]  
 這是發生死結時發行者之快照集代理程式連接的優先權。 指定這個參數的目的是為了解決快照集產生期間，快照集代理程式與使用者應用程式之間可能會發生的死結。  
  
|PublisherDeadlockPriority 值|描述|  
|-------------------------------------|-----------------|  
|**-1**|在發行者端發生死結時，快照集代理程式以外的應用程式擁有優先權。|  
|**0** (預設值)|未指派優先權。|  
|**1**|在發行者端發生死結時，快照集代理程式擁有優先權。|  
  
 **-PublisherFailoverPartner** _server_name_[ **\\** _instance\_name_]  
 指定參與具有發行集資料庫之資料庫鏡像工作階段的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉夥伴執行個體。 如需詳細資訊，請參閱 [資料庫鏡像和複寫 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)。  
  
 **-PublisherLogin** _publisher_login_  
 這是連接至使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證的發行者時，系統所使用的登入。  
  
 **-PublisherPassword**  _publisher_password_  
 這是連接至使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證的發行者時，系統所使用的密碼。 。  
  
 **-PublisherSecurityMode** [ **0**| **1**]  
 指定發行者的安全性模式。 值為 **0** 表示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證 (預設值)，而值為 **1** 則表示 Windows 驗證模式。  
  
 **-QueryTimeOut** _query_time_out_seconds_  
 這是查詢逾時之前的秒數。預設值是 1800 秒。  
  
 **-ReplicationType** [ **1**| **2**]  
 指定複寫的類型。 值為 **1** 表示異動複寫，而值為 **2** 則表示合併式複寫。  
  
 **-RowDelimiter** _row_delimiter_  
 這是在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大量複製資料檔案中標示資料列結尾的字元或字元序列。 預設為 \n\<,@g>\n。  
  
 **-StartQueueTimeout** _start_queue_timeout_seconds_  
 這是當執行中並行動態快照集處理序數目到達 [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) 的 `@max_concurrent_dynamic_snapshots` 屬性所設定限制時，快照集代理程式等候的最大秒數。 如果已到達最大秒數而且快照集代理程式仍然等候中，它就會結束。 值為 0 表示代理程式會永遠等候，不過您可以取消它。  
  
 \- **UsePerArticleContentsView** _use_per_article_contents_view_  
 這個參數已被取代，而且是為了回溯相容性才提供支援。  
  
## <a name="remarks"></a>備註  
  
> [!IMPORTANT]  
>  如果您已將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 安裝成在本機系統帳戶而非網域使用者帳戶 (預設值) 底下執行，這項服務就只能存取本機電腦。 如果在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 底下執行的快照集代理程式設定為使用 Windows 驗證模式，當它登入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]時，快照集代理程式就會失敗。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設設定為  驗證。  
  
 若要啟動快照集代理程式，請從命令提示字元執行 **snapshot.exe** 。 如需詳細資訊，請參閱＜ [複寫代理程式可執行檔](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [複寫代理程式管理](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
