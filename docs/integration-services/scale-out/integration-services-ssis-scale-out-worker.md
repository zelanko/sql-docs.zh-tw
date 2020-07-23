---
title: SQL Server Integration Services (SSIS) Scale Out 主機 | Microsoft Docs
description: 本文描述 SSIS Scale Out 的 Scale Out Master 元件
ms.custom: performance
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: b77fbcf909d534304bbaf2a27ca55daccb2a94c4
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918978"
---
# <a name="integration-services-ssis-scale-out-worker"></a>Integration Services (SSIS) 擴增背景工作

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]



Scale Out Worker 會執行 Scale Out Worker 服務，以從 Scale Out Master 提取執行工作。 然後，背景工作會使用 `ISServerExec.exe` 在本機執行套件。

## <a name="configure-the-scale-out-worker-service"></a>設定 Scale Out Worker 服務
您可以使用 `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config` 檔案來設定 Scale Out Worker 服務。 更新設定檔之後，必須重新啟動服務。

|組態  |描述  |預設值|
|---------|---------|---------|
|DisplayName|擴增背景工作的顯示名稱。 **未在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017 中使用。**|電腦名稱|
|描述|擴增背景工作的描述。 **未在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 2017 中使用。**|空白|
|MasterEndpoint|要連接到擴增主機的端點。|在擴增背景工作安裝期間設定的端點|
|MasterHttpsCertThumbprint|驗證擴增主機所使用的用戶端 TLS/SSL 憑證指紋|在擴增背景工作安裝期間指定的用戶端憑證指紋。|
|WorkerHttpsCertThumbprint|擴增主機驗證擴增背景工作所使用的憑證指紋。|在擴增背景工作安裝期間自動建立並安裝的憑證指紋|
|StoreLocation|背景工作憑證的儲存位置。|LocalMachine|
|StoreName|背景工作憑證所在的存放區名稱。|My|
|AgentHeartbeatInterval|擴增背景工作的活動訊號間隔。|00:01:00|
|TaskHeartbeatInterval|擴增背景工作報告工作狀態的間隔。|00:00:10|
|HeartbeatErrorTolerance|在最後一個成功的工作活動訊號時段後，如果收到活動訊號的錯誤回應，便會終止工作。|00:10:00|
|TaskRequestMaxCPU|擴增背景工作要求工作的 CPU 上限。|70.0|
|TaskRequestMinMemory|擴增背景工作要求工作的記憶體 MB 下限。|100.0|
|MaxTaskCount|擴增背景工作可以保留的最大工作數目。|10|
|LeaseInterval|擴增背景工作保留的工作租用間隔。|00:01:00|
|TasksRootFolder|工作記錄檔的資料夾。 如果值空白，則會使用 `\<drive\>:\Users\[account]\AppData\Local\SSIS\Cluster\Tasks` 資料夾路徑。 [帳戶] 是執行擴增背景工作服務的帳戶。 預設的帳戶是 SSISScaleOutWorker140。|空白|
|TaskLogLevel|擴增背景工作的工作記錄層級。 (詳細資訊 0x01，資訊 0x02，警告 0x04，錯誤 0x08，進度 0x10，嚴重錯誤 0x20，稽核 0x40)|126 (資訊，警告，錯誤，進度，嚴重錯誤，稽核)|
|TaskLogSegment|工作記錄檔的時間範圍。|00:00:00|
|TaskLogEnabled|指定是否啟用工作記錄檔。|true|
|ExecutionLogCacheFolder|用以快取封裝執行記錄檔的資料夾。 如果值空白，則會使用 `\<drive\>:\Users\[account]\AppData\Local\SSIS\Cluster\Agent\ELogCache` 資料夾路徑。 [帳戶] 是執行擴增背景工作服務的帳戶。 預設的帳戶是 SSISScaleOutWorker140。|空白|
|ExecutionLogMaxBufferLogCount|記憶體中一個執行記錄檔緩衝的最大快取執行記錄檔數目。|10000|
|ExecutionLogMaxInMemoryBufferCount|執行記錄檔的記憶體中的最大執行記錄檔緩衝數目。|10|
|ExecutionLogRetryCount|執行記錄失敗時的重試次數。|3|
|ExecutionLogRetryTimeout|執行記錄失敗時的重試逾時。 如果達到 ExecutionLogRetryTimeout，則會忽略 ExecutionLogRetryCount。 |7.00:00:00 (7 天)|
|AgentId|Scale Out Worker 的背景工作代理程式識別碼|自動產生|
||||    

## <a name="view-the-scale-out-worker-log"></a>檢視 Scale Out Worker 記錄
Scale Out Worker 服務的記錄檔位於 `\<drive\>:\Users\\[account]\AppData\Local\SSIS\ScaleOut\Agent` 資料夾中。

每個個別工作的記錄位置都是設定在 `WorkerSettings.config` 檔案的 `TasksRootFolder` 中。 如果未指定值，則記錄位於 `\<drive\>:\Users\\[account]\AppData\Local\SSIS\ScaleOut\Tasks` 資料夾中。 

*[account]* 參數是執行 Scale Out Worker 服務的帳戶。 帳戶預設為 `SSISScaleOutWorker140`。

## <a name="next-steps"></a>後續步驟
[Integration Services (SSIS) Scale Out Master](integration-services-ssis-scale-out-master.md)
