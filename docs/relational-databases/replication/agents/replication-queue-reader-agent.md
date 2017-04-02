---
title: "複寫佇列讀取器代理程式 | Microsoft Docs"
ms.custom: ""
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "代理程式 [SQL Server 複寫], 佇列讀取器代理程式"
  - "命令提示字元 [SQL Server 複寫]"
  - "佇列讀取器代理程式, 參數參考"
  - "佇列讀取器代理程式, 可執行檔"
ms.assetid: 8e227793-11f6-47c6-99dc-ffc282f5d4bf
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 複寫佇列讀取器代理程式
  複寫佇列讀取器代理程式會讀取訊息儲存在可執行檔 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 佇列或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 訊息佇列，然後將這些訊息套用至 「 發行者 」。 佇列讀取器代理程式可搭配允許佇列更新的快照式和交易式發行集使用。  
  
> [!NOTE]  
>  您可以使用任何順序來指定參數。 沒有指定選擇性參數時，系統就會使用以預設代理程式設定檔為基礎的預先定義值。  
  
## 語法  
  
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
  
## 引數  
 **-?**  
 顯示使用方式資訊。  
  
 **-Continuous**  
 指定代理程式是否會嘗試連續處理佇列的交易。 如果您指定了這個參數，代理程式就會繼續執行，即使所有訂閱者都沒有任何佇列交易暫止也一樣。  
  
 **-DefinitionFile** *def_path_and_file_name*  
 這是代理程式定義檔的路徑。 代理程式定義檔包含代理程式的命令列引數。 此檔案的內容會剖析為可執行檔。 請使用雙引號 (") 來指定包含任意字元的引數值。  
  
 **-Distributor** *server_name*[**\\***instance_name*]  
 這是散發者的名稱。 指定 *server_name* 預設執行個體 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 該伺服器上。 指定 *server_name*\\*instance_name* 的具名執行個體 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 該伺服器上。 如果沒有指定這個參數，此名稱就會預設為本機電腦上 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設執行個體的名稱。  
  
 **-DistributionDB** *distribution_database*  
 這是散發資料庫。  
  
 **-DistributorLogin** *distributor_login*  
 這是散發者登入名稱。  
  
 **-DistributorPassword** *distributor_password*  
 這是散發者密碼。  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 指定散發者的安全性模式。 值為 **0** 指出 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證模式 （預設值），而值為 **1** 表示 Windows 驗證模式。  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 這是建立連接時，佇列讀取器代理程式所使用的安全通訊端層 (SSL) 加密層級。  
  
|EncryptionLevel 值|說明|  
|---------------------------|-----------------|  
|**0**|指定不使用 SSL。|  
|**1**|指定要使用 SSL，但是代理程式不會驗證 SSL 伺服器憑證是否由受信任的簽發者簽署。|  
|**2**|指定要使用 SSL，而且憑證會經過驗證。|  
  
 如需詳細資訊，請參閱 [安全性概觀與 #40。複寫 & #41;](../../../relational-databases/replication/security/security-overview-replication.md)。  
  
 **-HistoryVerboseLevel** [ **0**| **1**| **2**| **3**]  
 指定在佇列讀取器作業期間記錄的記錄量。 您可以藉由選取記錄效能的影響降至最低 **1**。  
  
|HistoryVerboseLevel 值|說明|  
|-------------------------------|-----------------|  
|**0**|無記錄 (不建議使用)。|  
|**1**|預設值。 一律更新相同狀態的上一個記錄訊息 (啟動、進度、成功等等)。 如果沒有任何具有相同狀態的上一筆記錄存在，便插入新的記錄。|  
|**2**|插入新的記錄，包括閒置訊息或長時間執行作業訊息。|  
|**3**|插入新的記錄，包括可用於疑難排解的其他詳細資料。|  
  
 **-LoginTimeOut** *login_time_out_seconds*  
 這是登入逾時之前的秒數。 預設為 15 秒。  
  
 **-輸出** *output_path_and_file_name*  
 這是代理程式輸出檔的路徑。 如果未提供檔案名稱，輸出將傳送至主控台。 如果指定的檔案名稱存在，輸出就會附加至該檔案。  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 指定輸出是否應該詳細。 如果詳細資訊層級為 0，系統就只會列印錯誤訊息。 如果詳細資訊層級為 1，系統就會列印所有進度報表訊息。 如果詳細資訊層級是 **2** （預設值），所有的錯誤訊息和進度報表訊息會印出，這是適用於偵錯。  
  
 **-PollingInterval** *polling_interval*  
 這僅與使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 架構佇列的更新訂閱有關。 指定針對暫止佇列交易輪詢 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 佇列的頻率 (以秒為單位)。 此值可介於 0 與 240 秒之間。 預設值是 5 秒。  
  
 **-PublisherFailoverPartner** *server_name*[**\\***instance_name*]  
 指定參與具有發行集資料庫之資料庫鏡像工作階段的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 容錯移轉夥伴執行個體。 如需詳細資訊，請參閱 [資料庫鏡像和複寫 & #40。SQL Server & #41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)。  
  
 **-ProfileName** *agent_profile_name*  
 這是將一組預設值提供給代理程式所用之代理程式設定檔的名稱。 如需資訊，請參閱 [複寫代理程式設定檔](../../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
 **-QueryTimeOut** *query_time_out_seconds*  
 這是查詢逾時之前的秒數。 預設值是 1800 秒。  
  
 **-ResolverState** [ **1**| **2**| **3**]  
 指定解決佇列更新衝突的方式。 值為 **1** 表示發行者優先衝突，而且目前的衝突佇列的交易將會回復在 「 發行者 」 和原始更新訂閱者上; 後續佇列交易的處理會繼續進行。 值為 **2** 表示訂閱者在衝突中獲勝，而且佇列的交易將會覆寫在 「 發行者 」 的值。 值為 **3** 指出任何衝突將導致訂閱者重新初始化，則為發行者在衝突中獲勝、 後續佇列交易的處理將會終止，且會重新初始化訂閱。 預設值是 **1** 交易式發行集和 **3** 快照式發行集。  
  
## 備註  
 若要啟動佇列讀取器代理程式，請執行 **qrdrsvc.exe** 從命令提示字元。 如需資訊，請參閱 [複寫代理程式可執行檔](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
## 另請參閱  
 [複寫代理程式管理](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  