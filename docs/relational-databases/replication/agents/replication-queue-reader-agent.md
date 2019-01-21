---
title: 複寫佇列讀取器代理程式 | Microsoft Docs
ms.custom: ''
ms.date: 10/29/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], Queue Reader Agent
- command prompt [SQL Server replication]
- Queue Reader Agent, parameter reference
- Queue Reader Agent, executables
ms.assetid: 8e227793-11f6-47c6-99dc-ffc282f5d4bf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 81cdc720a23c402a493776c9fba7c0da6c119e60
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54126888"
---
# <a name="replication-queue-reader-agent"></a>複寫佇列讀取器代理程式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  「複寫佇列讀取器代理程式」是一個可執行檔，它會讀取儲存在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 佇列或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Message Queue 中的訊息，然後將這些訊息套用至發行者。 佇列讀取器代理程式可搭配允許佇列更新的快照式和交易式發行集使用。  
  
> [!NOTE]  
>  您可以使用任何順序來指定參數。 沒有指定選擇性參數時，系統就會使用以預設代理程式設定檔為基礎的預先定義值。  
  
## <a name="syntax"></a>語法  
  
```  
  
qrdrsvc [-?]  
[-Continuous]  
[-DefinitionFile definition_file]  
[-Distributor server_name[\instance_name]]  
[-DistributionDB distribution_database]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1]]  
[-EncryptionLevel [0|1|2]]  
[-HistoryVerboseLevel [0|1|2|3]]  
[-LoginTimeOut login_time_out_seconds]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2]]  
[-PollingInterval polling_interval]  
[-PublisherFailoverPartner server_name[\instance_name] ]  
[-ProfileName agent_profile_name]  
[-QueryTimeOut query_time_out_seconds]  
[-ResolverState [1|2|3]]  
```  
  
## <a name="arguments"></a>引數  
 **-?**  
 顯示使用方式資訊。  
  
 **-Continuous**  
 指定代理程式是否會嘗試連續處理佇列的交易。 如果您指定了這個參數，代理程式就會繼續執行，即使所有訂閱者都沒有任何佇列交易暫止也一樣。  
  
 **-DefinitionFile** _def_path_and_file_name_  
 這是代理程式定義檔的路徑。 代理程式定義檔包含代理程式的命令列引數。 此檔案的內容會剖析為可執行檔。 請使用雙引號 (") 來指定包含任意字元的引數值。  
  
 **-Distributor** _server_name_[**\\**_instance_name_]  
 這是散發者的名稱。 請針對該伺服器上的 *預設執行個體指定* server_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 請針對該伺服器上的 *server_name*\\*instance_name* instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 如果沒有指定這個參數，此名稱就會預設為本機電腦上 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設執行個體的名稱。  
  
 **-DistributionDB** _distribution_database_  
 這是散發資料庫。  
  
 **-DistributorLogin** _distributor_login_  
 這是散發者登入名稱。  
  
 **-DistributorPassword** _distributor_password_  
 這是散發者密碼。  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 指定散發者的安全性模式。 值為 **0** 表示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證模式 (預設值)，而值為 **1** 則表示 Windows 驗證模式。  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 這是建立連接時，佇列讀取器代理程式所使用的安全通訊端層 (SSL) 加密層級。  
  
|EncryptionLevel 值|Description|  
|---------------------------|-----------------|  
|**0**|指定不使用 SSL。|  
|**1**|指定要使用 SSL，但是代理程式不會驗證 SSL 伺服器憑證是否由受信任的簽發者簽署。|  
|**2**|指定要使用 SSL，而且憑證會經過驗證。|  

 > [!NOTE]  
 >  定義的 SSL 憑證必須包含 SQL Server 的完整網域名稱才會有效。 為了讓代理程式能在將 -EncryptionLevel 設定為 2 時成功連線，請在本機 SQL Server 上建立別名。 ‘Alias Name’ 參數應為伺服器名稱，且應將 ‘Server’ 參數設為 SQL Server 的完整名稱。
  
 如需詳細資訊，請參閱[檢視及修改複寫安全性設定](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
 **-HistoryVerboseLevel** [ **0**| **1**| **2**| **3**]  
 指定在佇列讀取器作業期間記錄的記錄量。 您可以透過選取 **1**，盡量減少記錄作業對效能造成的影響。  
  
|HistoryVerboseLevel 值|Description|  
|-------------------------------|-----------------|  
|**0**|無記錄 (不建議使用)。|  
|**1**|預設值。 一律更新相同狀態的上一個記錄訊息 (啟動、進度、成功等等)。 如果沒有任何具有相同狀態的上一筆記錄存在，便插入新的記錄。|  
|**2**|插入新的記錄，包括閒置訊息或長時間執行作業訊息。|  
|**3**|插入新的記錄，包括可用於疑難排解的其他詳細資料。|  
  
 **-LoginTimeOut** _login_time_out_seconds_  
 這是登入逾時之前的秒數。預設為 15 秒。  
  
 **-Output** _output_path_and_file_name_  
 這是代理程式輸出檔的路徑。 如果未提供檔案名稱，輸出將傳送至主控台。 如果指定的檔案名稱存在，輸出就會附加至該檔案。  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 指定輸出是否應該詳細。 如果詳細資訊層級為 0，系統就只會列印錯誤訊息。 如果詳細資訊層級為 1，系統就會列印所有進度報表訊息。  如果詳細資訊層級為 2 (預設值)，系統就會列印所有錯誤訊息和進度報表訊息 (可用於偵錯)。  
  
 **-PollingInterval** _polling_interval_  
 這僅與使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 架構佇列的更新訂閱有關。 指定針對暫止佇列交易輪詢 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 佇列的頻率 (以秒為單位)。 此值可介於 0 與 240 秒之間。 預設值是 5 秒。  
  
 **-PublisherFailoverPartner** _server_name_[**\\**_instance_name_]  
 指定參與具有發行集資料庫之資料庫鏡像工作階段的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉夥伴執行個體。 如需詳細資訊，請參閱[資料庫鏡像和複寫 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)。  
  
 **-ProfileName** _agent_profile_name_  
 這是將一組預設值提供給代理程式所用之代理程式設定檔的名稱。 如需詳細資訊，請參閱[複寫代理程式設定檔](../../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
 **-QueryTimeOut** _query_time_out_seconds_  
 這是查詢逾時之前的秒數。預設值是 1800 秒。  
  
 **-ResolverState** [ **1**| **2**| **3**]  
 指定解決佇列更新衝突的方式。 值為 **1** 表示發行者在衝突中獲勝，而且目前的衝突佇列交易將在發行者和原始更新訂閱者上回復。後續佇列交易的處理將繼續進行。 值為 **2** 表示訂閱者在衝突中獲勝，而且佇列交易將覆寫發行者的值。 值為 **3** 表示任何衝突將導致訂閱者重新初始化。發行者在衝突中獲勝、後續佇列交易的處理將結束，而且訂閱將重新初始化。 交易式發行集的預設設定為 **1** ，而快照式發行集的預設設定為 **3** 。  
  
## <a name="remarks"></a>Remarks  
 若要啟動佇列讀取器代理程式，請從命令提示字元執行 **qrdrsvc.exe** 。 如需詳細資訊，請參閱＜ [複寫代理程式可執行檔](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [複寫代理程式管理](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  
