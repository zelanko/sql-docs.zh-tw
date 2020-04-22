---
title: 複寫記錄讀取器代理程式 | Microsoft Docs
ms.custom: ''
ms.date: 10/29/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Log Reader Agent, executables
- Log Reader Agent, parameter reference
- agents [SQL Server replication], Log Reader Agent
- command prompt [SQL Server replication]
ms.assetid: 5487b645-d99b-454c-8bd2-aff470709a0e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 58ff313686f1f37643068a28d4e30ac93eddd2ce
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528202"
---
# <a name="replication-log-reader-agent"></a>複寫記錄讀取器代理程式
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  「複寫記錄讀取器代理程式」是一個可執行檔，它會監視針對異動複寫所設定之每個資料庫的交易記錄，並將標示要複寫的交易從交易記錄複製到散發資料庫中。  
  
> [!NOTE]  
>  您可以使用任何順序來指定參數。 沒有指定選擇性參數時，系統就會使用以預設代理程式設定檔為基礎的預先定義值。  
  
## <a name="syntax"></a>語法  
  
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
  
## <a name="arguments"></a>引數  
 **-?**  
 顯示使用資訊。  
  
 **-Publisher** _server_name_[ **\\** _instance_name_]  
 這是發行者的名稱。 請針對該伺服器上的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設執行個體指定 *server_name*。 請針對該伺服器上 _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設執行個體指定 server_name。  
  
 **-PublisherDB** _publisher_database_  
 這是發行者資料庫的名稱。  
  
 **-Continuous**  
 指定代理程式是否會嘗試持續輪詢複寫的交易。 如果您指定了這個參數，代理程式就會以輪詢間隔輪詢來源的複寫交易，即使沒有任何交易暫止也一樣。  
  
 **-DefinitionFile** _def_path_and_file_name_  
 這是代理程式定義檔的路徑。 代理程式定義檔包含代理程式的命令列引數。 此檔案的內容會剖析為可執行檔。 請使用雙引號 (") 來指定包含任意字元的引數值。  
  
 **-Distributor** _server_name_[ **\\** _instance_name_]  
 這是散發者的名稱。 請針對該伺服器上的 *預設執行個體指定* server_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 請針對該伺服器上 _server_name_ **\\** _instance_name_ instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設執行個體指定 server_name。  
  
 **-DistributorLogin** _distributor_login_  
 這是散發者登入名稱。  
  
 **-DistributorPassword** _distributor_password_  
 這是散發者密碼。  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 指定散發者的安全性模式。 值為 **0** 表示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證模式 (預設值)，而值為 **1** 則表示 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 驗證模式。  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 這是建立連線時，佇列讀取器代理程式所使用的傳輸層安全性 (TLS) (先前稱為安全通訊端層 (SSL)) 加密層級。  
  
|EncryptionLevel 值|描述|  
|---------------------------|-----------------|  
|**0**|指定不使用 TLS。|  
|**1**|指定要使用 TLS，但是代理程式不會驗證 TLS/SSL 伺服器憑證是否由受信任的簽發者簽署。|  
|**2**|指定要使用 TLS，而且憑證會經過驗證。|  

 > [!NOTE]  
 >  定義的 TLS/SSL 憑證必須包含 SQL Server 的完整網域名稱才會有效。 為了讓代理程式能在將 -EncryptionLevel 設定為 2 時成功連線，請在本機 SQL Server 上建立別名。 ‘Alias Name’ 參數應為伺服器名稱，且應將 ‘Server’ 參數設為 SQL Server 的完整名稱。
 
 如需詳細資訊，請參閱[檢視及修改複寫安全性設定](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
 **-ExtendedEventConfigFile** _configuration_path_and_file_name_  
 指定擴充的事件 XML 組態檔的路徑和檔案名稱。 擴充的事件組態檔可讓您設定工作階段以及啟用事件追蹤。  
  
 **-HistoryVerboseLevel** [ **0**| **1**| **2**]  
 指定在記錄讀取器作業期間記錄的記錄量。  您可以透過選取 1，盡量減少記錄作業的效能影響。  
  
|HistoryVerboseLevel 值|描述|  
|-------------------------------|-----------------|  
|**0**||  
|**1**|預設值。 一律更新相同狀態的上一個記錄訊息 (啟動、進度、成功等等)。 如果沒有任何具有相同狀態的上一筆記錄存在，便插入新的記錄。|  
|**2**|除非記錄用於閒置訊息或長時間執行作業訊息等事件 (在此情況下，更新之前的記錄)，否則便插入新的記錄。|  
  
 **-KeepAliveMessageInterval** _keep_alive_message_interval_seconds_  
 這是記錄執行緒檢查是否有任何現有的連接正在等候伺服器回應之前的秒數。 執行長時間執行的批次時，您可以減少這個值，避免檢查代理程式將記錄讀取器代理程式標示為有疑問。 預設為 300 秒。  
  
 **-LoginTimeOut** _login_time_out_seconds_  
 這是登入逾時之前的秒數。預設為 15 秒。  
  
 **-LogScanThreshold** _scan_threshold_  
 僅供內部使用。  
  
 **-MaxCmdsInTran** _number_of_commands_  
 指定當記錄讀取器將命令寫入散發資料庫時，分組到某交易內的最大陳述式數目。 使用此參數可讓記錄讀取器代理程式和散發代理程式在「訂閱者」端套用命令時，於「發行者」端將大型交易 (由許多命令組成) 分割成幾個較小的交易。 指定此參數可以降低「散發者」的競爭，並減少「發行者」和「訂閱者」之間的延遲。 因為原始交易是以較小的單位來套用，所以「訂閱者」在原始交易結束之前可以存取大量的邏輯「發行者」交易資料列，打破了嚴格的交易不可部份完成性。 預設值為 **0**，保留「發行者」的交易界限。  
  
> [!NOTE]
>  非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行集會忽略這個參數。 如需詳細資訊，請參閱＜ [Performance Tuning for Oracle Publishers](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)＞中的「設定交易集作業」一節。  
  
 **-MessageInterval** _message_interval_  
 這是用於記錄的時間間隔。 在記錄上一個記錄事件之後，如果到達 **MessageInterval** 值，系統就會記錄記錄事件。  
  
 如果來源沒有任何複寫的交易可用，代理程式就會回報無交易訊息給散發者。 這個選項會指定回報另一個無交易訊息之前等候的時間長度。 在先前處理複寫的交易之後，當代理程式偵測到來源沒有任何交易可用時，代理程式一律會回報無交易訊息。 預設值是 60 秒。  
  
 **-Output** _output_path_and_file_name_  
 這是代理程式輸出檔的路徑。 如果未提供檔案名稱，輸出將傳送至主控台。 如果指定的檔案名稱存在，輸出就會附加至該檔案。  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2** | **3** | **4** ]  
 指定輸出是否應該詳細。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|僅列印錯誤訊息。|  
|**1**|列印所有代理程式進度報表訊息。|  
|**2** (預設值)|列印所有錯誤訊息和代理程式進度報表訊息。|  
|**3**|列印每個複寫命令中的前 100 個位元組。|  
|**4**|列印所有複寫指令。|  
  
 進行偵錯時，值 2-4 很有用。  
  
 **-PacketSize** _packet_size_  
 這是封包大小 (以位元組為單位)。 預設值是 4096 (位元組)。  
  
 **-PollingInterval** _polling_interval_  
 這是針對複寫交易查詢記錄的頻率 (以秒為單位)。 預設值是 5 秒。  
  
 **-ProfileName** _profile_name_  
 指定要用於代理程式參數的代理程式設定檔。 如果 **ProfileName** 為 NULL，就會停用代理程式設定檔。 如果沒有指定 **ProfileName** ，就會使用該代理程式類型的預設設定檔。 如需資訊，請參閱[複寫代理程式設定檔](../../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
 **-PublisherFailoverPartner** _server_name_[ **\\** _instance_name_]  
 指定參與具有發行集資料庫之資料庫鏡像工作階段的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉夥伴執行個體。 如需詳細資訊，請參閱 [資料庫鏡像和複寫 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)。  
  
 **-PublisherSecurityMode** [ **0**| **1**]  
 指定發行者的安全性模式。 值為 **0** 表示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證 (預設值)，而值為 **1** 則表示 Windows 驗證模式。  
  
 **-PublisherLogin** _publisher_login_  
 這是發行者登入名稱。  
  
 **-PublisherPassword** _publisher_password_  
 這是發行者密碼。  
  
 **-QueryTimeOut** _query_time_out_seconds_  
 這是查詢逾時之前的秒數。預設值是 1800 秒。  
  
 **-ReadBatchSize** _number_of_transactions_  
 這是每個處理週期中從發行資料庫的交易記錄所讀取出最大交易數目，預設值為 500，最大值是 10000。 代理程式將繼續以批次方式讀取交易，直到從記錄中讀取所有交易為止。 這個參數不支援 Oracle 發行者。  
  
 **-ReadBatchThreshold** _number_of_commands_  
 這是要從交易記錄中讀取的複寫命令數目，然後散發代理程式便將這些命令發送至訂閱者。 預設值是 0。 如果沒有指定這個參數，記錄讀取器代理程式將讀取至記錄結尾或 **-ReadBatchSize** (交易數目) 中指定的數目。  
  
 **-RecoverFromDataErrors**  
 指定當記錄讀取器代理程式在非 SQL Server 發行者發行的資料行資料中遇到錯誤時，它會繼續執行。 根據預設，這類錯誤會導致記錄讀取器代理程式失敗。 當您使用 **-RecoverFromDataErrors**時，錯誤的資料行資料就會複寫成 NULL 或適當的非 Null 值，而且系統會在 [MSlogreader_history](../../../relational-databases/system-tables/mslogreader-history-transact-sql.md) 資料表中記錄警告訊息。 這個參數僅支援 Oracle 發行者。  
  
## <a name="remarks"></a>備註  
  
> [!IMPORTANT]  
>  如果您將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 安裝成在本機系統帳戶而非網域使用者帳戶 (預設值) 底下執行，這項服務就只能存取本機電腦。 如果在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 底下執行的記錄讀取器代理程式設定為使用 Windows 驗證模式，當它登入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]時，記錄讀取器代理程式就會失敗。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設設定為  驗證。 如需有關變更安全性帳戶的詳細資訊，請參閱＜ [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)＞。  
  
 若要啟動記錄讀取器代理程式，請從命令提示字元執行 **logread.exe** 。 如需詳細資訊，請參閱[複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
## <a name="change-history"></a>變更記錄  
  
|更新的內容|  
|---------------------|  
| 已加入 -ExtendedEventConfigFile 參數。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫代理程式管理](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
