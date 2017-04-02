---
title: "Integration Services (SSIS) 相應放大背景工作 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 480a3f3d-9a79-4a02-81e5-7d27afd756c4
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Integration Services (SSIS) 相應放大背景工作
相應放大背景工作執行 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] 相應放大背景工作服務，從相應放大主機提取執行工作，並使用 ISServerExec.exe 在本機執行封裝。

## <a name="configure-sql-server-integration-services-scale-out-worker-service"></a>設定 SQL Server Integration Services 相應放大背景工作服務
相應放大背景工作服務可以使用 \<磁碟機\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config 檔案設定。 更新組態檔後必須重新啟動服務。
    


組態  |Description  |預設值  
---------|---------|---------
DisplayName|相應放大背景工作的顯示名稱。 **[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1 不使用。**|電腦名稱         
Description|相應放大背景工作的描述。 **[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1 不使用。**|Empty         
MasterEndpoint|要連接到相應放大主機的端點。|在相應放大背景工作安裝期間設定的端點         
MasterHttpsCertThumbprint|驗證相應放大主機所使用的用戶端 SSL 憑證指紋|在相應放大背景工作安裝期間指定的用戶端憑證指紋。          
WorkerHttpsCertThumbprint|相應放大主機驗證相應放大背景工作所使用的憑證指紋。|在相應放大背景工作安裝期間自動建立並安裝的憑證指紋          
StoreLocation|背景工作憑證的儲存位置。|LocalMachine       
StoreName|背景工作憑證所在的存放區名稱。|My         
AgentHeartbeatInterval|相應放大背景工作的活動訊號間隔。|00:01:00         
TaskHeartbeatInterval|相應放大背景工作報告工作狀態的間隔。|00:00:10         
HeartbeatErrorTollerance|在最後一個成功的工作活動訊號時段後，如果收到活動訊號的錯誤回應，便會終止工作。|00:10:00      
TaskRequestMaxCPU|相應放大背景工作要求工作的 CPU 上限。 **[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1 不使用。**|70.0         
TaskRequestMinMemory|相應放大背景工作要求工作的記憶體 MB 下限。 **[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1 不使用。**|100.0         
MaxTaskCount|相應放大背景工作可以保留的最大工作數目。|10         
LeaseInternval|相應放大背景工作保留的工作租用間隔。|00:01:00         
TasksRootFolder|工作記錄檔的資料夾。 如果值是空的，就會使用 \<磁碟機\>:\Users\\*[帳戶]*\AppData\Local\SSIS\Cluster\Tasks 資料夾路徑。 [帳戶] 是執行相應放大背景工作服務的帳戶。 預設的帳戶是 SSISScaleOutWorker140。|Empty         
TaskLogLevel|相應放大背景工作的工作記錄層級。 (詳細資訊 0x01，資訊 0x02，警告 0x04，錯誤 0x08，進度 0x10，嚴重錯誤 0x20，稽核 0x40)|126 (Information,Warning,Error,Progress,CriticalError,Audit)     
TaskLogSegment|工作記錄檔的時間範圍。|00:00:00         
TaskLogEnabled|指定是否啟用工作記錄檔。|true         
ExecutionLogCacheFolder|用以快取封裝執行記錄檔的資料夾。 如果值是空的，就會使用 \<磁碟機\>:\Users\\*[帳戶]*\AppData\Local\SSIS\Cluster\Agent\ELogCache 資料夾路徑。 [帳戶] 是執行相應放大背景工作服務的帳戶。 預設的帳戶是 SSISScaleOutWorker140。|Empty         
ExecutionLogMaxBufferLogCount|記憶體中一個執行記錄檔緩衝的最大快取執行記錄檔數目。|10000        
ExecutionLogMaxInMemoryBufferCount|執行記錄檔的記憶體中的最大執行記錄檔緩衝數目。|10         
ExecutionLogRetryCount|執行記錄失敗時的重試次數。|3         
AgentId|相應放大背景工作的背景工作代理程式識別碼|自動產生        



## <a name="view-scale-out-worker-log"></a>檢視相應放大背景工作記錄檔
相應放大背景工作服務的記錄檔位於 \<磁碟機\>:\Users\\*[帳戶]*\AppData\Local\SSIS\Cluster\Agent 資料夾路徑。

各個工作的記錄檔位置由 TasksRootFolder 設定在 WorkerSettings.config 檔案中。 如未指定，則記錄檔位於 \<磁碟機\>:\Users\\*[帳戶]*\AppData\Local\SSIS\Cluster\Tasks 資料夾路徑。 

*[帳戶]* 資料夾是執行相應放大背景工作服務的帳戶。 預設的帳戶是 SSISScaleOutWorker140。
    