---
title: "複寫記錄讀取器代理程式 | Microsoft Docs"
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
  - "記錄讀取器代理程式, 可執行檔"
  - "記錄讀取器代理程式, 參數參考"
  - "代理程式 [SQL Server 複寫], 記錄讀取器代理程式"
  - "命令提示字元 [SQL Server 複寫]"
ms.assetid: 5487b645-d99b-454c-8bd2-aff470709a0e
caps.latest.revision: 51
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 51
---
# 複寫記錄讀取器代理程式
  「複寫記錄讀取器代理程式」是一個可執行檔，它會監視針對異動複寫所設定之每個資料庫的交易記錄，並將標示要複寫的交易從交易記錄複製到散發資料庫中。  
  
> [!NOTE]  
>  您可以使用任何順序來指定參數。 沒有指定選擇性參數時，系統就會使用以預設代理程式設定檔為基礎的預先定義值。  
  
## 語法  
  
```  
  
logread [-?]   
-Publisher server_name[\instance_name]   
-PublisherDB publisher_database   
[-Continuous]  
[-DefinitionFile def_path_and_file_name]  
[-Distributor server_name[\instance_name]]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1]]  
[-EncryptionLevel [0|1|2]]  
[-ExtendedEventConfigFile configuration_path_and_file_name]  
[-HistoryVerboseLevel [0|1|2]]  
[-KeepAliveMessageInterval keep_alive_message_interval_seconds]  
[-LoginTimeOut login_time_out_seconds]  
[-LogScanThreshold scan_threshold]  
[-MaxCmdsInTran number_of_commands]  
[-MessageInterval message_interval]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2|3|4]]  
[-PacketSize packet_size]  
[-PollingInterval polling_interval]  
[-ProfileName profile_name]   
[-PublisherFailoverPartner server_name[\instance_name] ]  
[-PublisherSecurityMode [0|1]]  
[-PublisherLogin publisher_login]  
[-PublisherPassword publisher_password]   
[-QueryTimeOut query_time_out_seconds]  
[-ReadBatchSize number_of_transactions]   
[-ReadBatchThreshold read_batch_threshold]  
[-RecoverFromDataErrors]  
```  
  
## 引數  
 **-?**  
 顯示使用方式資訊。  
  
 **-發行者** *server_name*[**\\***instance_name*]  
 這是發行者的名稱。 指定 *server_name* 預設執行個體 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 該伺服器上。 指定 *server_name***\\***instance_name* 的具名執行個體 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 該伺服器上。  
  
 **-PublisherDB** *publisher_database*  
 這是發行者資料庫的名稱。  
  
 **-Continuous**  
 指定代理程式是否會嘗試持續輪詢複寫的交易。 如果您指定了這個參數，代理程式就會以輪詢間隔輪詢來源的複寫交易，即使沒有任何交易暫止也一樣。  
  
 **-DefinitionFile** *def_path_and_file_name*  
 這是代理程式定義檔的路徑。 代理程式定義檔包含代理程式的命令列引數。 此檔案的內容會剖析為可執行檔。 請使用雙引號 (") 來指定包含任意字元的引數值。  
  
 **-Distributor** *server_name*[**\\***instance_name*]  
 這是散發者的名稱。 指定 *server_name* 預設執行個體 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 該伺服器上。 指定 *server_name***\\***instance_name* 的具名執行個體 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 該伺服器上。  
  
 **-DistributorLogin** *distributor_login*  
 這是散發者登入名稱。  
  
 **-DistributorPassword** *distributor_password*  
 這是散發者密碼。  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 指定散發者的安全性模式。 值為 **0** 指出 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證模式 （預設值），而值為 **1** 指出 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 驗證模式。  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 這是建立連接時，記錄讀取器代理程式所使用的安全通訊端層 (SSL) 加密層級。  
  
|EncryptionLevel 值|說明|  
|---------------------------|-----------------|  
|**0**|指定不使用 SSL。|  
|**1**|指定要使用 SSL，但是代理程式不會驗證 SSL 伺服器憑證是否由受信任的簽發者簽署。|  
|**2**|指定要使用 SSL，而且憑證會經過驗證。|  
  
 如需詳細資訊，請參閱 [安全性概觀與 #40。複寫 & #41;](../../../relational-databases/replication/security/security-overview-replication.md)。  
  
 **-ExtendedEventConfigFile** *configuration_path_and_file_name*  
 指定擴充的事件 XML 組態檔的路徑和檔案名稱。 擴充的事件組態檔可讓您設定工作階段以及啟用事件追蹤。  
  
 **-HistoryVerboseLevel** [ **0**| **1**| **2**]  
 指定在記錄讀取器作業期間記錄的記錄量。 您可以透過選取 1，盡量減少記錄作業的效能影響。  
  
|HistoryVerboseLevel 值|說明|  
|-------------------------------|-----------------|  
|**0**||  
|**1**|預設值。 一律更新相同狀態的上一個記錄訊息 (啟動、進度、成功等等)。 如果沒有任何具有相同狀態的上一筆記錄存在，便插入新的記錄。|  
|**2**|除非記錄用於閒置訊息或長時間執行作業訊息等事件 (在此情況下，更新之前的記錄)，否則便插入新的記錄。|  
  
 **-KeepAliveMessageInterval** *keep_alive_message_interval_seconds*  
 這是記錄執行緒檢查是否有任何現有的連接正在等候伺服器回應之前的秒數。 執行長時間執行的批次時，您可以減少這個值，避免檢查代理程式將記錄讀取器代理程式標示為有疑問。 預設值是 300 秒。  
  
 **-LoginTimeOut** *login_time_out_seconds*  
 這是登入逾時之前的秒數。 預設為 15 秒。  
  
 **-LogScanThreshold** *scan_threshold*  
 僅供內部使用。  
  
 **-MaxCmdsInTran** *number_of_commands*  
 指定當記錄讀取器將命令寫入散發資料庫時，分組到某交易內的最大陳述式數目。 使用此參數可讓記錄讀取器代理程式和散發代理程式在「訂閱者」端套用命令時，於「發行者」端將大型交易 (由許多命令組成) 分割成幾個較小的交易。 指定此參數可以降低「散發者」的競爭，並減少「發行者」和「訂閱者」之間的延遲。 因為原始交易是以較小的單位來套用，所以「訂閱者」在原始交易結束之前可以存取大量的邏輯「發行者」交易資料列，打破了嚴格的交易不可部份完成性。 預設值是 **0**, ，保留 「 發行者 」 端的交易界限。  
  
> [!NOTE]  
>  非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行集會忽略這個參數。 如需詳細資訊，請參閱 「 設定交易集作業 」 一節中 [效能微調 Oracle 發行者](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)。  
  
 **-MessageInterval** *message_interval*  
 這是用於記錄的時間間隔。 記錄記錄事件時 **MessageInterval** 記錄最後一個記錄事件之後，到達值。  
  
 如果來源沒有任何複寫的交易可用，代理程式就會回報無交易訊息給散發者。 這個選項會指定回報另一個無交易訊息之前等候的時間長度。 在先前處理複寫的交易之後，當代理程式偵測到來源沒有任何交易可用時，代理程式一律會回報無交易訊息。 預設值是 60 秒。  
  
 **-輸出** *output_path_and_file_name*  
 這是代理程式輸出檔的路徑。 如果未提供檔案名稱，輸出將傳送至主控台。 如果指定的檔案名稱存在，輸出就會附加至該檔案。  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2** | **3** | **4** ]  
 指定輸出是否應該詳細。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|僅列印錯誤訊息。|  
|**1**|列印所有代理程式進度報表訊息。|  
|**2** （預設值）|列印所有錯誤訊息和代理程式進度報表訊息。|  
|**3**|列印每個複寫命令中的前 100 個位元組。|  
|**4**|列印所有複寫指令。|  
  
 進行偵錯時，值 2-4 很有用。  
  
 **-PacketSize** *packet_size*  
 這是封包大小 (以位元組為單位)。 預設值是 4096 (位元組)。  
  
 **-PollingInterval** *polling_interval*  
 這是針對複寫交易查詢記錄的頻率 (以秒為單位)。 預設值是 5 秒。  
  
 **-ProfileName** *profile_name*  
 指定要用於代理程式參數的代理程式設定檔。 **ProfileName** 如果  為 NULL，就會停用代理程式設定檔。 **ProfileName** 如果沒有指定 ，就會使用該代理程式類型的預設設定檔。 如需資訊，請參閱 [複寫代理程式設定檔](../../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
 **-PublisherFailoverPartner** *server_name*[**\\***instance_name*]  
 指定參與具有發行集資料庫之資料庫鏡像工作階段的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉夥伴執行個體。 如需詳細資訊，請參閱 [資料庫鏡像和複寫 & #40。SQL Server & #41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)。  
  
 **-PublisherSecurityMode** [ **0**| **1**]  
 指定發行者的安全性模式。 值為 **0** 指出 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證 （預設值），而值為 **1** 表示 Windows 驗證模式。  
  
 **-PublisherLogin** *publisher_login*  
 這是發行者登入名稱。  
  
 **-PublisherPassword** *publisher_password*  
 這是發行者密碼。  
  
 **-QueryTimeOut** *query_time_out_seconds*  
 這是查詢逾時之前的秒數。 預設值是 1800 秒。  
  
 **-ReadBatchSize** *number_of_transactions*  
 這是每個處理循環中從發行資料庫之交易記錄讀取出的最大交易數目，預設值為 500。 代理程式將繼續以批次方式讀取交易，直到從記錄中讀取所有交易為止。 這個參數不支援 Oracle 發行者。  
  
 **-ReadBatchThreshold** *number_of_commands*  
 這是要從交易記錄中讀取的複寫命令數目，然後散發代理程式便將這些命令發送至訂閱者。 預設值是 0。 如果未指定此參數，記錄讀取器代理程式會讀取到記錄檔的結尾，或是在指定的數字 **-ReadBatchSize** （交易的數目）。  
  
 **-RecoverFromDataErrors**  
 指定當記錄讀取器代理程式在非 SQL Server 發行者發行的資料行資料中遇到錯誤時，它會繼續執行。 根據預設，這類錯誤會導致記錄讀取器代理程式失敗。 當您使用 **-RecoverFromDataErrors**, 、 錯誤的資料行資料會複寫為 NULL 或適當的非 null 值和警告訊息會記錄到 [MSlogreader_history](../../../relational-databases/system-tables/mslogreader-history-transact-sql.md) 資料表。 這個參數僅支援 Oracle 發行者。  
  
## 備註  
  
> [!IMPORTANT]  
>  如果您將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 安裝成在本機系統帳戶而非網域使用者帳戶 (預設值) 底下執行，這項服務就只能存取本機電腦。 如果在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 底下執行的記錄讀取器代理程式設定為使用 Windows 驗證模式，當它登入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時，記錄讀取器代理程式就會失敗。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設設定為  驗證。 如需變更安全性帳戶的詳細資訊，請參閱 [檢視和修改複寫安全性設定](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
 若要啟動記錄讀取器代理程式，請執行 **logread.exe** 從命令提示字元。 如需資訊，請參閱 [複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
## 變更記錄  
  
|更新的內容|  
|---------------------|  
|加入 **-ExtendedEventConfigFile** 參數。|  
  
## 另請參閱  
 [複寫代理程式管理](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  