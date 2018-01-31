---
title: "SQL Server Integration Services (SSIS) Scale Out 主機 | Microsoft Docs"
ms.description: This article describes the Scale Out Master component of SSIS Scale Out
ms.custom: 
ms.date: 12/19/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 
author: haoqian
ms.author: haoqian
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0cd80620f668e87eba8a77f1ac6a9e5faa2378da
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="integration-services-ssis-scale-out-worker"></a>Integration Services (SSIS) 相應放大背景工作

Scale Out Worker 會執行 Scale Out Worker 服務，以從 Scale Out Master 提取執行工作。 然後，背景工作會使用 `ISServerExec.exe` 在本機執行套件。

## <a name="configure-the-scale-out-worker-service"></a>設定 Scale Out Worker 服務
您可以使用 ` \<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config` 檔案來設定 Scale Out Worker 服務。 更新設定檔之後，必須重新啟動服務。

組態  |描述  |預設值  
---------|---------|---------
DisplayName|相應放大背景工作的顯示名稱。 **未在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017 中使用。**|電腦名稱         
描述|相應放大背景工作的描述。 **未在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017 中使用。**|Empty         
MasterEndpoint|要連接到相應放大主機的端點。|在相應放大背景工作安裝期間設定的端點         
MasterHttpsCertThumbprint|驗證相應放大主機所使用的用戶端 SSL 憑證指紋|在相應放大背景工作安裝期間指定的用戶端憑證指紋。          
WorkerHttpsCertThumbprint|相應放大主機驗證相應放大背景工作所使用的憑證指紋。|在相應放大背景工作安裝期間自動建立並安裝的憑證指紋          
StoreLocation|背景工作憑證的儲存位置。|LocalMachine       
StoreName|背景工作憑證所在的存放區名稱。|My         
AgentHeartbeatInterval|相應放大背景工作的活動訊號間隔。|00:01:00         
TaskHeartbeatInterval|相應放大背景工作報告工作狀態的間隔。|00:00:10         
HeartbeatErrorTollerance|在最後一個成功的工作活動訊號時段後，如果收到活動訊號的錯誤回應，便會終止工作。|00:10:00      
TaskRequestMaxCPU|相應放大背景工作要求工作的 CPU 上限。 **未在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017 中使用。**|70.0         
TaskRequestMinMemory|相應放大背景工作要求工作的記憶體 MB 下限。 **未在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017 中使用。**|100.0         
MaxTaskCount|相應放大背景工作可以保留的最大工作數目。|10         
LeaseInternval|相應放大背景工作保留的工作租用間隔。|00:01:00         
TasksRootFolder|工作記錄檔的資料夾。 如果值空白，則會使用 `\<drive\>:\Users\[account]\AppData\Local\SSIS\Cluster\Tasks` 資料夾路徑。 [帳戶] 是執行相應放大背景工作服務的帳戶。 預設的帳戶是 SSISScaleOutWorker140。|Empty         
TaskLogLevel|相應放大背景工作的工作記錄層級。 (詳細資訊 0x01，資訊 0x02，警告 0x04，錯誤 0x08，進度 0x10，嚴重錯誤 0x20，稽核 0x40)|126 (資訊，警告，錯誤，進度，嚴重錯誤，稽核)     
TaskLogSegment|工作記錄檔的時間範圍。|00:00:00         
TaskLogEnabled|指定是否啟用工作記錄檔。|true         
ExecutionLogCacheFolder|用以快取封裝執行記錄檔的資料夾。 如果值空白，則會使用 ` \<drive\>:\Users\[account]\AppData\Local\SSIS\Cluster\Agent\ELogCache` 資料夾路徑。 [帳戶] 是執行相應放大背景工作服務的帳戶。 預設的帳戶是 SSISScaleOutWorker140。|Empty         
ExecutionLogMaxBufferLogCount|記憶體中一個執行記錄檔緩衝的最大快取執行記錄檔數目。|10000        
ExecutionLogMaxInMemoryBufferCount|執行記錄檔的記憶體中的最大執行記錄檔緩衝數目。|10         
ExecutionLogRetryCount|執行記錄失敗時的重試次數。|3
ExecutionLogRetryTimeout|執行記錄失敗時的重試逾時。 如果達到 ExecutionLogRetryTimeout，則會忽略 ExecutionLogRetryCount。 |7.00:00:00 (7 天)        
AgentId|Scale Out Worker 的背景工作代理程式識別碼|自動產生    
||||    

## <a name="view-the-scale-out-worker-log"></a>檢視 Scale Out Worker 記錄
Scale Out Worker 服務的記錄檔位於 `\<drive\>:\Users\\[account]\AppData\Local\SSIS\ScaleOut\Agent` 資料夾中。

每個個別工作的記錄位置都是設定在 `WorkerSettings.config` 檔案的 `TasksRootFolder` 中。 如果未指定值，則記錄位於 `\<drive\>:\Users\\[account]\AppData\Local\SSIS\ScaleOut\Tasks` 資料夾中。 

*[account]* 參數是執行 Scale Out Worker 服務的帳戶。 帳戶預設為 `SSISScaleOutWorker140`。

## <a name="next-steps"></a>後續步驟
[Integration Services (SSIS) Scale Out Master](integration-services-ssis-scale-out-master.md)
