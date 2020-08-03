---
title: 複寫合併代理程式 | Microsoft Docs
description: 複寫合併代理程式會向訂閱者套用資料庫資料表中保存的初始快照集，合併累加資料變更，然後協調衝突。
ms.custom: ''
ms.date: 10/29/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Merge Agent, executables
- Merge Agent, parameter reference
- agents [SQL Server replication], Merge Agent
- command prompt [SQL Server replication]
ms.assetid: fe1e7f60-b0c8-45e9-a5e8-4fedfa73d7ea
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4f65282964494ba1fdb160b1e755922a60ad80d8
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394983"
---
# <a name="replication-merge-agent"></a>Replication Merge Agent
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  「複寫合併代理程式」是一個公用程式可執行檔，它會將資料庫資料表中保存的初始快照集套用至「訂閱者」。 此外，它也會合併建立初始快照集之後在「發行者」端發生的累加資料變更，並根據您設定的規則或使用您建立的自訂解析程式來調解衝突。  
  
> [!NOTE]  
>  您可以使用任何順序來指定參數。 沒有指定選擇性參數時，系統就會使用本機電腦上預先定義登錄設定的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
replmerg [-?]   
-Publisher server_name[\instance_name]  
-PublisherDB publisher_database  
-Publication publication  
-Subscriber server_name[\instance_name]  
-SubscriberDB subscriber_database  
[-AltSnapshotFolder alt_snapshot_folder_path]  
[-Continuous]  
[-DefinitionFile def_path_and_file_name]  
[-DestThreads number_of_destination_threads]  
[-Distributor server_name[\instance_name]]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1]]  
[-DownloadGenerationsPerBatch download_generations_per_batch]  
[-DownloadReadChangesPerBatch download_read_changes_per_batch]  
[-DownloadWriteChangesPerBatch download_write_changes_per_batch]  
[-DynamicSnapshotLocation dynamic_snapshot_location]  
[-EncryptionLevel [0|1|2]]  
[-ExchangeType [1|2|3]]  
[-FastRowCount [0|1]]  
[-FileTransferType [0|1]]  
[-ForceConvergenceLevel [0|1|2 (Publisher|Subscriber|Both)]]  
[-FtpAddress ftp_address]  
[-FtpPassword ftp_password]  
[-FtpPort ftp_port]  
[-FtpUserNameftp_user_name]  
[-HistoryVerboseLevel [0|1|2|3]]  
[-Hostname host_name]  
[-InteractiveResolution [0|1]]  
[-InternetLogin internet_login]  
[-InternetPassword internet_password]  
[-InternetProxyLogin internet_proxy_login]  
[–InternetProxyPassword internet_proxy_password]  
[-InternetProxyServer internet_proxy_server]  
[-InternetSecurityMode [0|1]]  
[-InternetTimeout internet_timeout]  
[-InternetURL internet_url]  
[-KeepAliveMessageInterval keep_alive_message_interval_seconds]  
[-LoginTimeOut login_time_out_seconds]  
[-MakeGenerationInterval make_generation_interval_seconds]  
[-MaxBcpThreads number_of_threads]  
[-MaxDownloadChanges number_of_download_changes]  
[-MaxUploadChanges number_of_upload_changes]  
[-MetadataRetentionCleanup [0|1]]  
[-Output]  
[-OutputVerboseLevel [0|1|2]]  
[-ParallelUploadDownload [0|1]]  
[-PacketSize packet_size]   
[-PollingInterval polling_interval]  
[-ProfileName profile_name]  
[-PublisherFailoverPartner server_name[\instance_name] ]  
[-PublisherLogin publisher_login]  
[-PublisherPassword publisher_password]  
[-PublisherSecurityMode [0|1]]  
[-QueryTimeOut query_time_out_seconds]  
[-SrcThreads number_of_source_threads]  
[-StartQueueTimeout start_queue_timeout_seconds]  
[-SubscriberConflictClean [0|1]]  
[-SubscriberDatabasePath subscriber_path]  
[-SubscriberDBAddOption [0|1|2|3]]  
[-SubscriberLogin subscriber_login]  
[-SubscriberPassword subscriber_password   
[-SubscriberSecurityMode [0|1]]  
[-SubscriberType [0|1|2|3|4|5|6|7|8|9]]  
[-SubscriptionType [0|1|2]]  
[-SyncToAlternate [0|1]]  
[-T [101|102]]  
[-UploadGenerationsPerBatch upload_generations_per_batch]  
[-UploadReadChangesPerBatch upload_read_changes_per_batch]  
[-UploadWriteChangesPerBatch upload_write_changes_per_batch]  
[-UseInprocLoader]  
[-Validate [0|1|2|3]]  
[-ValidateInterval validate_interval]  
```  
  
## <a name="arguments"></a>引數  
 **-?**  
 列印所有可用的參數。  
  
 **-Publisher** _server_name_[ **\\** _instance_name_]  
 這是發行者的名稱。 請針對該伺服器上的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設執行個體指定 *server_name*。 請針對該伺服器上 _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設執行個體指定 server_name。  
  
 **-PublisherDB** _publisher_database_  
 這是發行者資料庫的名稱。  
  
 **-Publication** _publication_  
 這是發行集的名稱。 只有在發行集設定成隨時都有快照供新的訂閱或重新初始化的訂閱使用時，這個參數才有效。  
  
 **-Subscriber** _server_name_[ **\\** _instance_name_]  
 這是訂閱者的名稱。 請針對該伺服器上的 *預設執行個體指定* server_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 請針對該伺服器上 _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設執行個體指定 server_name。  
  
 **-SubscriberDB** _subscriber_database_  
 這是訂閱者資料庫的名稱。  
  
 **-AltSnapshotFolder** _alt_snapshot_folder_path_  
 這是包含訂閱之初始快照集的資料夾路徑。  
  
 **-Continuous**  
 指定代理程式是否會嘗試持續輪詢複寫的交易。 如果您指定了這個參數，代理程式就會以輪詢間隔輪詢來源的複寫交易，即使沒有任何交易暫止也一樣。  
  
 **-DestThreads** _number_of_destination_threads_  
 指定合併代理程式在目的地套用變更所用的目的地執行緒數目。 在上傳期間，目的地是發行者，而在下載期間，目的地則是訂閱者。 預設值為 4。  
  
 **-DefinitionFile** _def_path_and_file_name_  
 這是代理程式定義檔的路徑。 代理程式定義檔包含代理程式的命令提示字元引數。 此檔案的內容會剖析為可執行檔。 請使用雙引號 (") 來指定包含任意字元的引數值。  
  
 **-Distributor** _server_name_[ **\\** _instance_name_]  
 這是散發者的名稱。 請針對該伺服器上的 *預設執行個體指定* server_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 請針對該伺服器上 _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設執行個體指定 server_name。 若為散發者 (發送) 散發，此名稱就會預設為本機電腦上 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設執行個體的名稱。  
  
 **-DistributorLogin** _distributor_login_  
 這是散發者登入名稱。  
  
 **-DistributorPassword** _distributor_password_  
 這是散發者密碼。  
  
 **-DistributorSecurityMode** [ **0**\| **1**]  
 指定散發者的安全性模式。 值為 **0** 表示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證模式 (預設值)，而值為 **1** 則表示 Windows 驗證模式。  
  
 **-DownloadGenerationsPerBatch** _download_generations_per_batch_  
 這是將變更從發行者下載至訂閱者時，要在單一批次中處理的層代數目。 層代會定義為每個發行項的邏輯變更群組。 可靠通訊連結的預設值為 100。 不可靠通訊連結的預設值為 10。  
  
 **-DownloadReadChangesPerBatch** _download_read_changes_per_batch_  
 這是將變更從發行者下載至訂閱者時，要在單一批次中讀取的變更數目。 預設值為 100。  
  
 **-DownloadWriteChangesPerBatch** _download_write_changes_per_batch_  
 這是將變更從發行者下載至訂閱者時，要在單一批次中套用的變更數目。 預設值為 100。  
  
 **-DynamicSnapshotLocation** _dynamic_snapshot_location_  
 這是當發行集使用數化資料列篩選器時，已篩選資料快照集檔案的位置。  
  
 **-EncryptionLevel** [ **0** \| **1** \| **2** ]  
 這是建立連線時，合併代理程式所使用的傳輸層安全性 (TLS) (先前稱為安全通訊端層 (SSL)) 加密層級。  
  
|EncryptionLevel 值|描述|  
|---------------------------|-----------------|  
|**0**|指定不使用 TLS。|  
|**1**|指定要使用 TLS，但是代理程式不會驗證 TLS/SSL 伺服器憑證是否由受信任的簽發者簽署。|  
|**2**|指定要使用 TLS，而且憑證會經過驗證。|  

 > [!NOTE]  
 >  定義的 TLS/SSL 憑證必須包含 SQL Server 的完整網域名稱才會有效。 為了讓代理程式能在將 -EncryptionLevel 設定為 2 時成功連線，請在本機 SQL Server 上建立別名。 ‘Alias Name’ 參數應為伺服器名稱，且應將 ‘Server’ 參數設為 SQL Server 的完整名稱。

 如需詳細資訊，請參閱[檢視及修改複寫安全性設定](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
 **-ExchangeType** [ **1**\| **2**\| **3**]  
> [!WARNING]
>  [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)] 若要限制上傳，請改用 **sp_addmergearticle** 的 **\@subscriber_upload_options**。  
  
 指定同步處理期間資料交換的類型，它可以是下列其中一個值：  
  
|ExchangeType 值|描述|  
|------------------------|-----------------|  
|**1**|代理程式應該將資料變更從訂閱者上傳至發行者。|  
|**2**|代理程式應該將資料變更從發行者下載至訂閱者。|  
|**3** (預設)|代理程式應該先將資料變更從訂閱者上傳至發行者，然後再將資料變更從發行者下載至訂閱者。 您必須使用這個選項搭配 Web 同步處理。|  
  
 僅限下載的發行項可讓您控制發行集中個別發行項的同步處理行為，而且它們可以改善效能。 如需詳細資訊，請參閱[使用僅限下載的發行項最佳化合併式複寫效能](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
  
 如果使用 **ExchangeType** 將合併式複寫的上傳和下載階段分成不同的工作階段，您必須先將 **ExchangeType** 設定為 1 來執行合併代理程式，然後將此值設定為 2 再次執行合併代理程式。 如果無法使用這兩個參數執行合併代理程式，將會導致中繼資料遭到刪除，而且您將必須重新初始化訂閱 (沒有上傳)。  
  
 **-FastRowCount** [**0**\|**1**]  
 指定應該針對資料列計數驗證使用哪一種資料列計數計算方法。 值為 **1** (預設值) 表示快速方法。 值為 **0** 則表示完整資料列計數方法。  
  
 **-FileTransferType** [**0**\|**1**]  
 指定檔案傳輸類型。 值為 **0** 表示 UNC (通用命名慣例)，而值為 1 則表示 FTP (檔案傳輸通訊協定)。  
  
 **-ForceConvergenceLevel** [**0**\|**1**\|**2** ( **Publisher**\| **Subscriber**\| **Both**)]  
 指定合併代理程式應該使用的聚合層級，而且可以是下列其中一個值。  
  
|ForceConvergenceLevel 值|描述|  
|---------------------------------|-----------------|  
|**0** (預設)|預設值。 執行標準合併，但不進行其他聚合。|  
|**1**|針對所有層代強制執行聚合。|  
|**2**|針對所有層代強制執行聚合並更正損毀的歷程。 指定這個值時，指定應該修正歷程的位置：發行者、訂閱者或發行者與訂閱者兩者。|  
  
 **-FtpAddress** _ftp_address_  
 這是散發者之 FTP 服務的網路位址。 沒有指定這個參數時，系統就會使用 **Distributor** 。  
  
 **-FtpPassword** _ftp_password_  
 這是用來連接到 FTP 服務的使用者密碼。  
  
 **-FtpPort** _ftp_port_  
 這是散發者的 FTP 服務通訊埠編號。 沒有指定這個參數時，系統就會使用 FTP 服務的預設通訊埠編號 (21)。  
  
 **-FtpUserName** _ftp_user_name_  
 這是用來連接到 FTP 服務的使用者名稱。 沒有指定這個參數時，系統就會使用 anonymous。  
  
 **-HistoryVerboseLevel** [**1**\|**2**\|**3**]  
 指定在合併作業期間記錄的記錄量。 您可以透過選取 **1**，盡量減少記錄作業對效能造成的影響。  
  
|HistoryVerboseLevel 值|描述|  
|-------------------------------|-----------------|  
|**0**|記錄最終代理程式狀態訊息、最終工作階段詳細資料，以及任何錯誤。|  
|**1**|除了最終代理程式狀態訊息、最終工作階段詳細資料以及任何錯誤以外，記錄每個工作階段狀態的累加工作階段詳細資料，包括完成百分比。|  
|**2**|預設值。 除了最終代理程式狀態訊息、最終工作階段詳細資料以及任何錯誤以外，記錄每個工作階段狀態的累加工作階段詳細資料和發行項層級工作階段詳細資料，包括完成百分比。 此外，系統也會記錄代理程式狀態訊息。|  
|**3**|與 **-HistoryVerboseLevel** = **2**相同，但是系統會記錄更多代理程式進度訊息。|  
  
 **-Hostname** _host_name_  
 這是本機電腦的網路名稱。 預設值為本機電腦名稱。  
  
 **-InteractiveResolution** [**0**\|**1**]  
 指定在同步處理期間發生衝突時，是否要使用互動式衝突解決方案。 預設值為 **0**，表示不使用互動式衝突解決方案。  
  
 **-InternetLogin** _internet_login_  
 指定連接至需要驗證之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Replication Listener ISAPI DLL 時使用的登入名稱。  
  
 **-InternetPassword** _internet_password_  
 指定連接至需要驗證之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Replication Listener ISAPI DLL 時使用的密碼。  
  
 **-InternetProxyLogin**  *internet_proxy_login*  
 指定連接至需要驗證之 Proxy 伺服器 (定義於 *internet_proxy_server*) 時使用的登入名稱。  
  
 **–InternetProxyPassword**  *internet_proxy_password*  
 指定連接至需要驗證之 Proxy 伺服器 (定義於 *internet_proxy_server*) 時使用的密碼。  
  
 **-InternetProxyServer**  *internet_proxy_server*  
 指定要在存取 *internet_url*中指定之 HTTP 資源時使用的 Proxy 伺服器。  
  
 **-InternetSecurityMode** [**0**\|**1**]  
 指定在 Web 同步處理期間，連接至 Web 伺服器時使用的 IIS 安全性模式。 值為 **0** 表示基本驗證，而值為 **1** 則表示 Windows 整合式驗證 (預設值)。  
  
 **-InternetTimeout** _internet_timeout_  
 這是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Replication Listener ISAPI DLL 的連接逾時之前的秒數。  
  
 **-InternetURL** _internet_url_  
 指定用來連接至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Replication Listener ISAPI DLL 的 URL。 您必須指定這個屬性。  
  
 **-KeepAliveMessageInterval** _keep_alive_message_interval_seconds_  
 這是記錄執行緒檢查是否有任何現有的連接正在等候伺服器回應之前的秒數。 執行長時間執行的批次時，您可以減少這個值，避免檢查代理程式將合併代理程式標示為有疑問。 預設值是 **300** 秒。  
  
 **-LoginTimeOut** _login_time_out_seconds_  
 這是登入逾時之前的秒數。 預設值為 15 秒。  
  
 **-MakeGenerationInterval** _make_generation_interval_seconds_  
 這是建立層代或變更批次之間等待的秒數，以便下載到用戶端。 預設值為 **1** 秒。  
  
 Makegeneration 是準備將發行者變更下載到訂閱者的程序，而且在它下載期間可能是效能瓶頸。 如果 makegeneration 程序已經在 **-MakeGenerationInterval**指定的間隔內執行，則會略過目前同步處理工作階段的程序。 這有助於進行並行同步處理，而且在訂閱者不想要下載變更時特別實用。  
  
 **-MaxBcpThreads** _number_of_threads_  
 指定可用平行方式執行的大量複製作業數目。 同時存在之執行緒和 ODBC 連接的最大數目是 **MaxBcpThreads** 或發行集資料庫之系統資料表 **sysmergeschemachange** 中顯示的大量複製要求數目的較小者。 **MaxBcpThreads** 必須具有大於 0 的值而且沒有硬式編碼的上限。 預設為 **1**。  
  
 **-MaxDownloadChanges** _number_of_download_changes_  
 指定應該從發行者下載至訂閱者的最大變更資料列數目。 所下載的資料列數目可能會高於指定的最大值，因為：系統會處理完整的層代，而且平行目的地執行緒可能會執行，其中每個執行緒在第一次傳遞時至少會處理 100 項變更。 根據預設，系統會傳送準備下載的所有變更。  
  
 **-MaxUploadChanges** _number_of_upload_changes_  
 指定應該從訂閱者上傳至發行者的最大變更資料列數目。 所上傳的資料列數目可能會高於指定的最大值，因為：系統會處理完整的層代，而且平行目的地執行緒可能會執行，其中每個執行緒在第一次傳遞時至少會處理 100 項變更。 根據預設，系統會傳送準備上傳的所有變更。  
  
 **-MetadataRetentionCleanup** [**0**\|**1**]  
 指定是否應該根據發行集保留週期，從 [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)、 [MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md)、 [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)、 [MSmerge_past_partition_mappings](../../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)和 [MSmerge_current_partition_mappings](../../../relational-databases/system-tables/msmerge-current-partition-mappings.md) 中移除中繼資料。 預設值為 **1**，表示應該進行清除。 值為 **0** 則表示不應該自動進行清除。  
  
 **-Output** _output_path_and_file_name_  
 這是代理程式輸出檔的路徑。 如果未提供檔案名稱，輸出將傳送至主控台。 如果指定的檔案名稱存在，輸出就會附加至該檔案。  
  
 **-OutputVerboseLevel** [**0**\|**1**\|**2**]  
 指定輸出是否應該詳細。 如果詳細資訊層級為 0，系統就只會列印錯誤訊息。 如果詳細資訊層級為 **1**，系統就會列印所有進度報表訊息。 如果詳細資訊層級為 2 (預設值)，系統就會列印所有錯誤訊息和進度報表訊息 (可用於偵錯)。  
  
 **-ParallelUploadDownload** [**0**\|**1**]  
 指定合併代理程式是否應該以平行方式處理上傳至發行者的變更以及下載至訂閱者的變更，而且這個參數在具有高網路頻寬的高容量環境中很有用。 如果 **ParallelUploadDownload** 是 **1**，就會啟用平行處理。  
  
 **-PacketSize**  
 這是封包大小 (以位元組為單位)。 預設值是 4096 (位元組)。  
  
 **-PollingInterval** _polling_interval_  
 這是針對資料變更查詢發行者或訂閱者的頻率 (以秒為單位)。 預設值是 60 秒。  
  
 **-ProfileName** _profile_name_  
 指定要用於代理程式參數的代理程式設定檔。 如果 **ProfileName** 為 NULL，就會停用代理程式設定檔。 如果沒有指定 **ProfileName** ，就會使用該代理程式類型的預設設定檔。 如需資訊，請參閱[複寫代理程式設定檔](../../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
 **-PublisherFailoverPartner** _server_name_[ **\\** _instance_name_]  
 指定參與具有發行集資料庫之資料庫鏡像工作階段的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉夥伴執行個體。 如需詳細資訊，請參閱 [資料庫鏡像和複寫 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)。  
  
 **-PublisherLogin** _publisher_login_  
 這是發行者登入名稱。 如果 **PublisherSecurityMode** 是 **0** (代表 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證)，您就必須指定這個參數。  
  
 **-PublisherPassword** _publisher_password_  
 這是發行者密碼。 如果 **PublisherSecurityMode** 是 **0** (代表 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證)，您就必須指定這個參數。  
  
 **-PublisherSecurityMode** [**0**\|**1**]  
 指定發行者的安全性模式。 值為 **0** 表示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證 (預設值)，而值為 **1** 則表示 Windows 驗證模式。  
  
 **-QueryTimeOut** _query_time_out_seconds_  
 這是查詢逾時之前的秒數。預設為 300 秒。 此外，當這個值大於 1800 時，合併代理程式也會使用 **QueryTimeout** 的值來決定等候資料分割快照集產生的時間長度。  
  
 **-SrcThreads** _number_of_source_threads_  
 指定合併代理程式從來源列舉變更所用的來源執行緒數目。 在上傳期間，來源是訂閱者，而在下載期間，來源則是發行者。 預設為 **3**。  
  
 **-StartQueueTimeout** _start_queue_timeout_seconds_  
 這是當執行中並行合併處理序數目到達 **sp_addmergepublication** 的 **\@max_concurrent_merge** 屬性所設定的限制時，合併代理程式等候的最大秒數。 如果已到達最大秒數而且合併代理程式仍然等候中，它就會結束。 值為 0 表示代理程式會永遠等候，不過您可以取消它。  
  
 **-SubscriberDatabasePath** _subscriber_database_path_  
 如果 **SubscriberType** 是 **2** (允許連接至沒有 ODBC 資料來源名稱 (DSN) 的 Jet 資料庫)，這就是 Jet 資料庫 (.mdb 檔) 的名稱。  
  
 **-SubscriberDBAddOption** [**0**\| **1**\| **2**\| **3**]  
 指定現有的訂閱者資料庫是否存在。  
  
|SubscriberDBAddOption 值|描述|  
|---------------------------------|-----------------|  
|**0**|使用現有的資料庫 (預設值)。|  
|**1**|建立新的空白訂閱者資料庫。|  
|**2**|建立新的資料庫並將它附加至指定的檔案。|  
|**3**|建立新的資料庫、附加該資料庫，然後啟用可能存在檔案中的所有訂閱。|  
  
> [!NOTE]  
>  當您使用 **2** 和 **3**值時，就必須在 **SubscriberDatabasePath** 選項中指定訂閱者的資料庫路徑。  
  
 **-SubscriberLogin** _subscriber_login_  
 這是訂閱者登入名稱。 如果 **SubscriberSecurityMode** 是 **0** (代表 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證)，您就必須指定這個參數。  
  
 **-SubscriberPassword** _subscriber_password_  
 這是訂閱者密碼。 如果 **SubscriberSecurityMode** 是 **0** (代表 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證)，您就必須指定這個參數。  
  
 **-SubscriberSecurityMode** [ **0**\| **1**]  
 指定訂閱者的安全性模式。 值為 **0** 表示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證 (預設值)，而值為 **1** 則表示 Windows 驗證模式。  
  
 **-SubscriberConflictClean** [ **0**\| **1**]  
 是否要在同步處理過程中清除訂閱者端的衝突資料表。值為 **1** 表示要清除訂閱者端的衝突資料表。 這個參數只能用於具有分散式衝突記錄之發行集的訂閱。  
  
 **-SubscriberType** [ **0**\| **1**\| **3**\| **4**\| **5**\| **6**\| **7**\| **8**]  
 指定由合併代理程式所使用的訂閱者連接類型。 只有預設值 **0** 支援這個參數。  
  
 **-SubscriptionType**[ **0**\| **1**\| **2**]  
 指定散發的訂閱類型。 值為 **0** 表示發送訂閱 (預設值)、值為 **1** 表示提取訂閱，而值為 **2** 則表示匿名訂閱。  
  
 **-SyncToAlternate** [ **0\|1**]  
 指定合併代理程式是否會在訂閱者與替代發行者之間進行同步處理。 值為 **1** 表示它是替代發行者。 預設為 **0**。  
 
 **-T** [**101\|102**]  
 為合併代理程式啟用額外功能的追蹤旗標。 值 **101** 會啟用額外的詳細資訊記錄資訊，以協助判斷合併式複寫同步處理程序的每個步驟所花費時間。 值 **102** 會寫入與追蹤旗標 **101** 相同的統計資料，但改為寫入到 <Distribution server>..msmerge_history 資料表。 當您使用追蹤旗標 101 時，請使用 `-output` 和 `-outputverboselevel` 參數來啟用合併代理程式記錄。  例如，將下列參數新增至合併代理程式，然後重新啟動代理程式：`-T 101, -output, -outputverboselevel`。 
 
 **-UploadGenerationsPerBatch** _upload_generations_per_batch_  
 這是將變更從訂閱者上傳至發行者時，要在單一批次中處理的層代數目。 層代會定義為每個發行項的邏輯變更群組。 可靠通訊連結的預設值為 **100**。 不可靠通訊連結的預設值為 **1**。  
  
 **-UploadReadChangesPerBatch** _upload_read_changes_per_batch_  
 這是將變更從訂閱者上傳至發行者時，要在單一批次中讀取的變更數目。 預設為 **100**。  
  
 **-UploadWriteChangesPerBatch** _upload_write_changes_per_batch_  
 這是將變更從訂閱者上傳至發行者時，要在單一批次中套用的變更數目。 預設為 **100**。  
  
 **-UseInprocLoader**  
 將快照集檔案套用至訂閱者時，讓合併代理程式使用 BULK INSERT 命令，藉以改善初始快照集的效能。 這個參數已被取代，因為它與 XML 資料類型不相容。 如果您不複寫 XML 資料，則可使用這個參數。 這個參數無法搭配字元模式快照集使用。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 如果您使用這個參數，位於訂閱者端的  服務帳戶就必須擁有快照集 .bcp 資料檔案所在目錄的讀取權限。 沒有使用這個參數時，代理程式所載入的 ODBC 驅動程式就會從這些檔案中讀取，因此不會使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務帳戶的安全性內容。  
  
 **-Validate** [**0**\|**1**\|**2**\|**3**]  
 指定是否應該在合併工作階段結束時完成驗證，而且如果是的話，應該完成哪一種驗證。 值 **3** 是建議值。  
  
|Validate 值|描述|  
|--------------------|-----------------|  
|**0** (預設)|不驗證。|  
|**1**|僅驗證資料列計數。|  
|**2**|資料列計數及總和檢查碼驗證。|  
|**3**|資料列計數及二進位總和檢查碼驗證。|  
  
> [!NOTE]  
>  如果「訂閱者」與「發行者」端的資料類型不同，則使用二進位總和檢查碼或總和檢查碼的驗證可能會誤報失敗。 如需詳細資訊，請參閱[驗證複寫的資料](../../../relational-databases/replication/validate-data-at-the-subscriber.md)中的＜資料驗證的考量＞一節。  
  
 **-ValidateInterval** _validate_interval_  
 這是在連續模式下驗證訂閱的頻率。 預設值是 **60** 分鐘。  
  
## <a name="remarks"></a>備註  
  
> [!IMPORTANT]  
>  如果您已將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 安裝成在本機系統帳戶而非網域使用者帳戶 (預設值) 底下執行，這項服務就只能存取本機電腦。 如果在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 底下執行的合併代理程式設定為使用 Windows 驗證模式，當它登入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]時，合併代理程式就會失敗。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設設定為  驗證。  
  
 若要啟動合併代理程式，請從命令提示字元執行 **replmerg.exe** 。 如需詳細資訊，請參閱＜ [複寫代理程式可執行檔](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)＞。  
  
 ### <a name="troubleshooting-merge-agent-performance"></a>針對合併代理程式效能進行疑難排解 
 在連續模式執行時，不會移除目前工作階段的合併代理程式記錄。 長時間執行的代理程式會在合併記錄資料表中產生可能會影響效能的大量項目。 若要解決這個問題，請切換到排程模式或是繼續使用連續模式，但是要建立專門作業來定期重新啟動合併代理程式，或是減少記錄層級的詳細資訊來減少資料列數，這樣會降低效能影響。  
 
  在某些情況下，複寫合併代理程式可能會需要很長的時間來複寫變更。 若要判斷合併式複寫同步處理程序的哪一個步驟需要花費最多時間，請使用追蹤旗標 101 搭配合併代理程式記錄。 若要這樣做，請針對合併代理程式參數使用下列參數，然後重新啟動代理程式：   <br/>-T 101   <br/>-output   <br/>-outputverboselevel

此外，如果您必須將統計資料寫入 <Distribution server>..msmerge_history 資料表中，請使用追蹤旗標 -T 102。
  
## <a name="see-also"></a>另請參閱  
 [複寫代理程式管理](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
