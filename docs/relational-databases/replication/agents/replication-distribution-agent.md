---
title: 複寫散發代理程式 | Microsoft Docs
ms.custom: ''
ms.date: 02/23/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Distribution Agent, executables
- agents [SQL Server replication], Distribution Agent
- Distribution Agent, parameter reference
- command prompt [SQL Server replication]
ms.assetid: 7b4fd480-9eaf-40dd-9a07-77301e44e2ac
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1864abc0cfa12e0b7ea60f5e080d372b9b50d989
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47790286"
---
# <a name="replication-distribution-agent"></a>複寫散發代理程式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  「複寫散發代理程式」是一個可執行檔，它會將快照集 (快照式複寫與異動複寫) 和散發資料庫資料表中保存的交易 (異動複寫) 移動至位於「訂閱者」端的目的地資料表。  
  
> [!NOTE]  
>  您可以使用任何順序來指定參數。 沒有指定選擇性參數時，系統就會使用本機電腦上預先定義登錄設定的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
distrib [-?]  
-Publisher server_name[\instance_name]  
-PublisherDB publisher_database  
-Subscriber server_name[\instance_name]  
-SubscriberDB subscriber_database   
[-AltSnapshotFolder alt_snapshot_folder_path]   
[-BcpBatchSize bcp_batch_size]  
[-CommitBatchSize commit_batch_size]  
[-CommitBatchThreshold commit_batch_threshold]  
[-Continuous]  
[-DefinitionFile def_path_and_file_name]  
[-Distributor distributor]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1]]  
[-EncryptionLevel [0|1|2]]  
[-ErrorFile error_path_and_file_name]  
[-ExtendedEventConfigFile configuration_path_and_file_name]  
[-FileTransferType [0|1]]  
[-FtpAddress ftp_address]  
[-FtpPassword ftp_password]   
[-FtpPort ftp_port]  
[-FtpUserName ftp_user_name]  
[-HistoryVerboseLevel [0|1|2|3]]  
[-Hostname host_name]  
[-KeepAliveMessageInterval keep_alive_message_interval_seconds]  
[-LoginTimeOut login_time_out_seconds]  
[-MaxBcpThreads]  
[-MaxDeliveredTransactions number_of_transactions]  
[-MessageInterval message_interval]  
[-OledbStreamThreshold oledb_stream_threshold]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2]]  
[-PacketSize packet_size]  
[-PollingInterval polling_interval]  
[-ProfileName profile_name]  
[-Publication publication]  
[-QueryTimeOut query_time_out_seconds]  
[-QuotedIdentifier quoted_identifier]  
[-SkipErrors native_error_id [:...n]]  
[-SubscriberDatabasePath subscriber_path]  
[-SubscriberLogin subscriber_login]  
[-SubscriberPassword subscriber_password]  
[-SubscriberSecurityMode [0|1]]  
[-SubscriberType [0|1|3]]  
[-SubscriptionStreams [1|2|...64]]  
[-SubscriptionTableName subscription_table]  
[-SubscriptionType [0|1|2]]  
[-TransactionsPerHistory [0|1|...10000]]  
[-UseDTS]  
[-UseInprocLoader]  
[-UseOledbStreaming]  
```  
  
## <a name="arguments"></a>引數  
 **-?**  
 列印所有可用的參數。  
  
 **-Publisher** *server_name*[**\\***i**nstance_name*]  
 這是發行者的名稱。 請針對該伺服器上的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設執行個體指定 <伺服器名稱>。 請針對該伺服器上的 *server_name***\\***instance_name* instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
 **-PublisherDB** *publisher_database*  
 這是發行者資料庫的名稱。  
  
 **-Subscriber** *server_name*[**\\***instance_name*]  
 這是訂閱者的名稱。 請針對該伺服器上的 *預設執行個體指定* server_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 請針對該伺服器上的 *server_name***\\***instance_name* instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
 **-SubscriberDB** *subscriber_database*  
 這是訂閱者資料庫的名稱。  
  
 **-AltSnapshotFolder** *alt_snapshot_folder_path*  
 這是包含訂閱之初始快照集的資料夾路徑。  
  
 **-BcpBatchSize** *bcp_batch_size*  
 這是要在大量複製作業中傳送的資料列數目。  執行 **bcp in** 作業時，批次大小就是要在單一交易中傳送至伺服器的資料列數目，而且它也是「散發代理程式」記錄 bcp 進度訊息之前必須傳送的資料列數目。 執行 **bcp out** 作業時，系統會使用固定批次大小 **1000** 。  
  
 **-CommitBatchSize** *commit_batch_size*  
 這是發出 COMMIT 陳述式之前，要發送至訂閱者的交易數目。 預設值為 100。  
  
 **-CommitBatchThreshold**  *commit_batch_threshold*  
 這是發出 COMMIT 陳述式之前，要發送至訂閱者的複寫命令數目。 預設值是 1000。  
  
 **-Continuous**  
 指定代理程式是否會嘗試持續輪詢複寫的交易。 如果您指定了這個參數，代理程式就會以輪詢間隔輪詢來源的複寫交易，即使沒有任何交易暫止也一樣。  
  
 **-DefinitionFile** *def_path_and_file_name*  
 這是代理程式定義檔的路徑。 代理程式定義檔包含代理程式的命令提示字元引數。 此檔案的內容會剖析為可執行檔。 請使用雙引號 (") 來指定包含任意字元的引數值。  
  
 **-Distributor** *distributor*  
 這是散發者的名稱。 若為散發者 (發送) 散發，此名稱會預設為本機散發者的名稱。  
  
 **-DistributorLogin** *distributor_login*  
 這是散發者登入名稱。  
  
 **-DistributorPassword** *distributor_password*  
 這是散發者密碼。  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 指定散發者的安全性模式。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 值為 0 表示  驗證模式，而值為 1 則表示 Windows 驗證模式 (預設值)。  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 這是建立連接時，散發代理程式所使用的安全通訊端層 (SSL) 加密層級。  
  
|EncryptionLevel 值|Description|  
|---------------------------|-----------------|  
|**0**|指定不使用 SSL。|  
|**1**|指定要使用 SSL，但是代理程式不會驗證 SSL 伺服器憑證是否由受信任的簽發者簽署。|  
|**2**|指定要使用 SSL，而且憑證會經過驗證。|  
  
 如需詳細資訊，請參閱[安全性概觀 &#40;複寫&#41;](../../../relational-databases/replication/security/security-overview-replication.md)。  
  
 **-ErrorFile** *error_path_and_file_name*  
 這是由散發代理程式產生之錯誤檔的路徑和檔案名稱。 此檔案是在「訂閱者」端套用複寫交易時於發生故障處產生的；「發行者」或「散發者」端發生的錯誤將不記錄在此檔案中。 此檔案包含失敗的複寫交易和相關的錯誤訊息。 如果未指定，錯誤檔將在散發代理程式的目前目錄中產生。 錯誤檔的名稱是含有 .err 副檔名的散發代理程式名稱。 如果指定的檔案名稱存在，錯誤訊息就會附加至該檔案。 這個參數最多可以有 256 個 Unicode 字元。  
  
 **-ExtendedEventConfigFile** *configuration_path_and_file_name*  
 指定擴充的事件 XML 組態檔的路徑和檔案名稱。 擴充的事件組態檔可讓您設定工作階段以及啟用事件追蹤。  
  
 **-FileTransferType** [ **0**| **1**]  
 指定檔案傳輸類型。  值為 **0** 表示 UNC (通用命名慣例)，而值為 1 則表示 FTP (檔案傳輸通訊協定)。  
  
 **-FtpAddress** *ftp_address*  
 這是散發者之 FTP 服務的網路位址。  沒有指定這個參數時，系統就會使用 DistributorAddress。  如果沒有指定 **DistributorAddress** ，則會使用 Distributor。  
  
 **-FtpPassword** *ftp_password*  
 這是用來連接到 FTP 服務的使用者密碼。  
  
 **-FtpPort** *ftp_port*  
 這是散發者的 FTP 服務通訊埠編號。 沒有指定這個參數時，系統就會使用 FTP 服務的預設通訊埠編號 (21)。  
  
 **-FtpUserName**  *ftp_user_name*  
 這是用來連接到 FTP 服務的使用者名稱。  沒有指定這個參數時，系統就會使用 anonymous。  
  
 **-HistoryVerboseLevel** [ **0** | **1** | **2** | **3** ]  
 指定在散發作業期間記錄的記錄量。 您可以透過選取 1，盡量減少記錄作業的效能影響。  
  
|HistoryVerboseLevel 值|Description|  
|-------------------------------|-----------------|  
|**0**|進度訊息會寫入主控台或輸出檔中。 但是，記錄不會記錄在散發資料庫中。|  
|**1**|預設值。 一律更新相同狀態的上一個記錄訊息 (啟動、進度、成功等等)。 如果沒有任何具有相同狀態的上一筆記錄存在，便插入新的記錄。|  
|**2**|除非記錄用於閒置訊息或長時間執行作業訊息等事件 (在此情況下，更新之前的記錄)，否則便插入新的記錄。|  
|**3**|除非記錄用於閒置訊息，否則一律插入新的記錄。|  
  
 **-Hostname** *host_name*  
 這是連接到發行者時所用的主機名稱。 這個參數最多可以有 128 個 Unicode 字元。  
  
 **-KeepAliveMessageInterval** *keep_alive_message_interval_seconds*  
 這是記錄執行緒檢查是否有任何現有的連接正在等候伺服器回應之前的秒數。 執行長時間執行的批次時，您可以減少這個值，避免檢查代理程式將散發代理程式標示為有疑問。 預設值是 **300** 秒。  
  
 **-LoginTimeOut** *login_time_out_seconds*  
 這是登入逾時之前的秒數。 預設值為 15 秒。  
  
 **-MaxBcpThreads** *number_of_threads*  
 指定可用平行方式執行的大量複製作業數目。 同時存在之執行緒和 ODBC 連接的最大數目是 **MaxBcpThreads** 或散發資料庫之同步處理交易中顯示的大量複製要求數目的較小者。 **MaxBcpThreads** 必須具有大於 **0** 的值而且沒有硬式編碼的上限。  預設值為 **2**乘以處理器的數目，最大值是 8。 當使用並行快照集選項來套用在發行者端產生的快照集時，系統會使用單一執行緒，不論您針對 **MaxBcpThreads**指定的數目為何都一樣。  
  
 **-MaxDeliveredTransactions** *number_of_transactions*  
 這是在單一同步處理作業中套用至訂閱者的最大發送或提取交易數目。  值為 0 表示最大值是無限個交易。 訂閱者可以使用其他值來縮短從發行者提取之同步處理作業的持續時間。  
  
> [!NOTE]  
>  如果 -MaxDeliveredTransactions 和 -Continuous 都已指定，「散發代理程式」會傳遞指定的交易數目，然後停止 (即使已指定 -Continuous)。 作業完成之後，您必須重新啟動「散發代理程式」。  
  
 **-MessageInterval**  *message_interval*  
 這是用於記錄的時間間隔。 到達下列其中一個參數時，系統就會記錄記錄事件：  
  
-   記錄上一個歷程記錄事件之後，到達 **TransactionsPerHistory** 值。  
  
-   記錄上一個歷程記錄事件之後，到達 **MessageInterval** 值。  
  
 如果來源沒有任何複寫的交易可用，代理程式就會回報無交易訊息給散發者。 這個選項會指定回報另一個無交易訊息之前等候的時間長度。 在先前處理複寫的交易之後，當代理程式偵測到來源沒有任何交易可用時，代理程式一律會回報無交易訊息。 預設值是 60 秒。  
  
 **-OledbStreamThreshold** *oledb_stream_threshold*  
 指定二進位大型物件資料 (其中資料將繫結為資料流) 的大小下限 (以位元組為單位)。 您必須指定 **–UseOledbStreaming** 才能使用這個參數。 值的範圍在 400 至 1048576 個位元組之間，預設為 16384 個位元組。  
  
 **-Output** *output_path_and_file_name*  
 這是代理程式輸出檔的路徑。 如果未提供檔案名稱，輸出將傳送至主控台。 如果指定的檔案名稱存在，輸出就會附加至該檔案。  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 指定輸出是否應該詳細。 如果詳細資訊層級為 0，系統就只會列印錯誤訊息。 如果詳細資訊層級為 1，系統就會列印所有進度報表訊息。  如果詳細資訊層級為 2 (預設值)，系統就會列印所有錯誤訊息和進度報表訊息 (可用於偵錯)。  
  
 **-PacketSize** *packet_size*  
 這是封包大小 (以位元組為單位)。 預設值是 4096 (位元組)。  
  
 **-PollingInterval** *polling_interval*  
 這是針對複寫交易查詢散發資料庫的頻率 (以秒為單位)。 預設值是 5 秒。  
  
 **-ProfileName** *profile_name*  
 指定要用於代理程式參數的代理程式設定檔。 如果 **ProfileName** 為 NULL，就會停用代理程式設定檔。 如果沒有指定 **ProfileName** ，就會使用該代理程式類型的預設設定檔。 如需資訊，請參閱[複寫代理程式設定檔](../../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
 **-Publication**  *publication*  
 這是發行集的名稱。 只有在發行集設定成隨時都有快照供新的訂閱或重新初始化的訂閱使用時，這個參數才有效。  
  
 **-QueryTimeOut** *query_time_out_seconds*  
 這是查詢逾時之前的秒數。預設值是 1800 秒。  
  
 **-QuotedIdentifier** *quoted_identifier*  
 指定要使用的引號識別碼字元。 此值的第一個字元表示散發代理程式所使用的值。 如果使用了沒有任何值的 **QuotedIdentifier** ，散發代理程式就會使用空格。 如果未使用 **QuotedIdentifier** ，散發代理程式就會使用訂閱者所支援的任何引號識別項。  
  
 **-SkipErrors** *native_error_id* [**:***...n*]  
 這是冒號分隔的清單，其中指定了這個代理程式要忽略的錯誤號碼。  
  
 **-SubscriberDatabasePath** *subscriber_database_path*  
 如果 **SubscriberType** 是 **2** (允許連接至沒有 ODBC 資料來源名稱 (DSN) 的 Jet 資料庫)，這就是 Jet 資料庫 (.mdb 檔) 的名稱。  
  
 **-SubscriberLogin** *subscriber_login*  
 這是訂閱者登入名稱。 如果 **SubscriberSecurityMode** 是 **0** (代表 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證)，您就必須指定這個參數。  
  
 **-SubscriberPassword** *subscriber_password*  
 這是訂閱者密碼。 如果 **SubscriberSecurityMode** 是 **0** (代表 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證)，您就必須指定這個參數。  
  
 **-SubscriberSecurityMode** [ **0**| **1**]  
 指定訂閱者的安全性模式。  值為 0 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 表示  驗證，而值為 1 則表示 Windows 驗證模式 (預設值)。  
  
 **-SubscriberType** [ **0**| **1**| **3**]  
 指定由散發代理程式所使用的訂閱者連接類型。  
  
|SubscriberType 值|Description|  
|--------------------------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|  
|**1**|ODBC 資料來源|  
|**3**|OLE DB 資料來源|  
  
 **-SubscriptionStreams** [**0**|**1**|**2**|...**64**]  
 這是在維護許多使用單一執行緒時所提供的交易式特性時，每個散發代理程式可用來將變更批次並行套用在訂閱者上的連接數目。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 若為  發行者，就支援範圍在 1 至 64 之間的值。 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 只有當發行者或散發者在  或更新版本上執行時，才支援這個參數。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 這個參數不支援非  訂閱者或點對點訂閱，否則就必須為 0。  
  
> [!NOTE]  
>  如果有一個連接無法執行或認可，則所有連接都將中止目前批次，且代理程式將使用單一資料流重試失敗的批次。 在此重試階段完成之前，「訂閱者」端可能會出現暫時的交易不一致性。 成功認可失敗的批次後，「訂閱者」將返回交易一致性的狀態。  
  
> [!IMPORTANT]  
>  當您針對 **-SubscriptionStreams**指定 2 以上的值時，在訂閱者端收到交易的順序可能會與在發行者端建立交易的順序不同。 如果這個行為在同步處理期間導致條件約束違規，您就應該使用 NOT FOR REPLICATION 選項來停用同步處理期間的條件約束強制執行。 如需詳細資訊，請參閱[在同步處理期間控制觸發程序和條件約束的行為 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)。  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../../includes/tsql-md.md)]Subscriptionstreams 不適用於設定為傳遞  的發行項。 若要使用 subscriptionstreams，請改將發行項設定為傳遞預存程序呼叫。  
  
 **-SubscriptionTableName** *subscription_table*  
 這是在給定訂閱者端產生或使用之訂閱資料表的名稱。 未指定時，會使用 [MSreplication_subscriptions &#40;Transact-SQL&#41;](../../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) 資料表。 您可以針對不支援長檔名的資料庫管理系統 (DBMS) 使用這個選項。  
  
 **-SubscriptionType** [ **0**| **1**| **2**]  
 指定散發的訂閱類型。  值為 **0** 表示發送訂閱、值為 **1** 表示提取訂閱，而值為 2 則表示匿名訂閱。  
  
 **-TransactionsPerHistory** [ **0**| **1**|...**10000**]  
 指定記錄作業的交易間隔。 如果上一個記錄執行個體之後認可的交易數目大於這個選項，系統就會記錄記錄訊息。 預設值為 100。 **0** 值表示無限 **TransactionsPerHistory**。 See the preceding **–MessageInterval**parameter.  
  
 **-UseDTS**  
 必須針對允許資料轉換的發行集指定為參數。  
  
 **-UseInprocLoader**  
 將快照集檔案套用至訂閱者時，讓散發代理程式使用 BULK INSERT 命令，藉以改善初始快照集的效能。 這個參數已被取代，因為它與 XML 資料類型不相容。 如果您不複寫 XML 資料，則可使用這個參數。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 這個參數無法搭配字元模式快照集或非  訂閱者使用。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 如果您使用這個參數，位於訂閱者端的  服務帳戶就必須擁有快照集 .bcp 資料檔案所在目錄的讀取權限。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 沒有使用這個參數時，代理程式 (代表非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者) 或代理程式所載入的 ODBC 驅動程式 (代表 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者) 就會從這些檔案中讀取，因此不會使用  服務帳戶的安全性內容。  
  
 **-UseOledbStreaming**  
 指定這個參數時，可將二進位大型物件資料繫結成資料流。 您可以使用 **-OledbStreamThreshold** 來指定將使用的資料流大小 (以位元組為單位)。 **UseOledbStreaming** 預設為啟用。 **UseOledbStreaming** 會寫入 **C:\Program Files\Microsoft SQL Server\\<版本\>\COM** 資料夾。  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 如果您已將  Agent 安裝成在本機系統帳戶而非網域使用者帳戶 (預設值) 底下執行，這項服務就只能存取本機電腦。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 如果在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Agent 底下執行的散發代理程式設定為使用 Windows 驗證模式，當它登入  執行個體時，散發代理程式就會失敗。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設設定為  驗證。 [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)如需有關變更安全性帳戶的詳細資訊，請參閱＜＞。  
  
 若要啟動散發代理程式，請從命令提示字元執行 **distrib.exe** 。 如需詳細資訊，請參閱[複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
## <a name="change-history"></a>變更記錄  
  
|更新的內容|  
|---------------------|  
| 已加入 -ExtendedEventConfigFile 參數。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫代理程式管理](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
