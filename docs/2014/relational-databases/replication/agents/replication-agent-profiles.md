---
title: 複寫代理程式設定檔 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Distribution Agent, profiles
- replication [SQL Server], agents and profiles
- replication agent profiles [SQL Server]
- Merge Agent, profiles
- agents [SQL Server replication], profiles
- Queue Reader Agent, profiles
- profiles [SQL Server], replication agents
- Snapshot Agent, profiles
- Log Reader Agent, profiles
ms.assetid: 0e980725-e42f-4283-94cb-d8a6dba5df62
caps.latest.revision: 43
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f17c7ae974704ba42ad4653f1f560497f7bd9061
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134154"
---
# <a name="replication-agent-profiles"></a>複寫代理程式設定檔
  設定複寫時，會在散發者上安裝一組代理程式設定檔。 代理程式設定檔包含一組參數，代理程式每次執行時都會使用這組參數：每個代理程式在啟動過程中都會登入散發者，並查詢其設定檔內的參數。 針對使用 Web 同步處理的合併訂閱，會下載設定檔並儲存於「訂閱者」。 如果設定檔變更，則「訂閱者」中的設定檔會在下一次「合併代理程式」執行時更新。 如需有關 Web 同步處理的詳細資訊，請參閱＜ [Web Synchronization for Merge Replication](../web-synchronization-for-merge-replication.md)＞。  
  
 複寫為每個代理程式提供預設的設定檔，並為記錄讀取代理程式、散發代理程式及合併代理程式提供其他預先定義的設定檔。 除了提供的設定檔之外，您也可以建立適合自己的應用程式需求的設定檔。 代理程式設定檔可讓您輕易變更關聯該設定檔的所有代理程式的關鍵參數。 例如，若有 20 個「快照集代理程式」，且必須變更其查詢逾時值 ( **-QueryTimeout** 參數)，則可以更新「快照集代理程式」所用的設定檔，則該類型的所有代理程式都會在下次執行時自動開始使用新值。  
  
 代理程式的不同執行個體也可以具有不同的設定檔。 例如，透過撥號連接來連接「發行者」和「散發者」的「合併代理程式」，可能會藉由使用 **慢速連結** 設定檔使用一組更適合慢速通訊連結的參數。  
  
> [!NOTE]  
>  如果您在命令列上指定代理程式參數的值，則該值會覆寫針對代理程式設定檔中同名參數設定的值。  
  
 **使用及修改代理程式設定檔**  
  
-   [處理複寫代理程式設定檔](replication-agent-profiles.md)  
  
## <a name="snapshot-agent-profiles"></a>快照集代理程式設定檔  
 下表顯示於「快照集代理程式」的預設設定檔中定義的參數。 如需這些參數的詳細資訊，請參閱＜ [Replication Snapshot Agent](replication-snapshot-agent.md)＞。  
  
||預設|  
|-|-------------|  
|**-BcpBatchSize**|100000|  
|**-HistoryVerboseLevel**|2|  
|**-LoginTimeout**|15|  
|**-QueryTimeout**|1800|  
  
## <a name="log-reader-agent-profiles"></a>記錄讀取器代理程式設定檔  
 下表顯示於「記錄讀取器代理程式」的設定檔中定義的參數。 資料表中的每一個資料行代表一個具名設定檔。 如需這些參數的詳細資訊，請參閱＜ [Replication Log Reader Agent](replication-log-reader-agent.md)＞。  
  
||預設|詳細資訊記錄|  
|-|-------------|---------------------|  
|**-HistoryVerboseLevel**|@shouldalert|2|  
|**-LoginTimeout**|15|15|  
|**-LogScanThreshold**|500000|500000|  
|**-PollingInterval**|5|5|  
|**-QueryTimeout**|1800|1800|  
|**-ReadBatchSize**|500|500|  
  
## <a name="distribution-agent-profiles"></a>散發代理程式設定檔  
 下表顯示於「散發代理程式」的設定檔中定義的參數。 資料表中的每一個資料行代表一個具名設定檔。 如需這些參數的詳細資訊，請參閱＜ [Replication Distribution Agent](replication-distribution-agent.md)＞。  
  
||預設|詳細資訊記錄|Windows Synchronization Manager|資料一致性錯誤時仍然繼續|OLEDB 資料流的散發設定檔|  
|-|-------------|---------------------|-------------------------------------|-----------------------------------------|----------------------------------------------|  
|**-BcpBatchSize**|100000|100000|1000|100000|2147473647|  
|**-CommitBatchSize**|100|100|100|100|100|  
|**-CommitBatchThreshold**|1000|1000|1000|1000|1000|  
|**-HistoryVerboseLevel**|@shouldalert|2|@shouldalert|@shouldalert|@shouldalert|  
|**-KeepAliveMessageInterval**|300|300|300|300|300|  
|**-LoginTimeout**|15|15|15|15|15|  
|**-MaxBcpThreads**|@shouldalert|@shouldalert|@shouldalert|@shouldalert|@shouldalert|  
|**-MaxDeliveredTransactions**|0|0|0|0|0|  
|**-OledbStreamThreshold**|NULL|NULL|NULL|NULL|32768|  
|**-PacketSize**|NULL|NULL|NULL|NULL|32768|  
|**-PollingInterval**|5|5|5|5|5|  
|**-QueryTimeout**|1800|1800|1800|1800|1800|  
|**-SkipErrors**|NULL|NULL|NULL|**-SkipErrors** 2601:2627:20598|NULL|  
|**-TransactionsPerHistory**|100|100|100|100|100|  
|**-UseOledbStreaming**|NULL|NULL|NULL|NULL|**-UseOledbStreaming**|  
  
## <a name="merge-agent-profiles"></a>合併代理程式設定檔  
 下表顯示於「合併代理程式」的設定檔中定義的參數。 資料表中的每一個資料行代表一個具名設定檔。 如需這些參數的詳細資訊，請參閱＜ [Replication Merge Agent](replication-merge-agent.md)＞。  
  
||預設|詳細資訊記錄|Windows Synchronization Manager|資料列計數驗證|資料列計數與總和檢查碼驗證|慢速連結|高容量伺服器對伺服器|  
|-|-------------|---------------------|-------------------------------------|-------------------------|--------------------------------------|---------------|------------------------------------|  
|**-BcpBatchSize**|100000|100000|1000|100000|100000|100000|100000|  
|**-ChangesPerHistory**|100|50|50|100|100|100|1000|  
|**-DestThreads**|2|@shouldalert|@shouldalert|@shouldalert|@shouldalert|@shouldalert|4|  
|**-DownloadGenerationsPerBatch**|50|50|50|50|50|@shouldalert|500|  
|**-DownloadReadChangesPerBatch**|100|100|100|100|100|100|100|  
|**-DownloadWriteChangesPerBatch**|100|100|100|100|100|100|100|  
|**-FastRowCount**|@shouldalert|@shouldalert|@shouldalert|@shouldalert|@shouldalert|@shouldalert|@shouldalert|  
|**-HistoryVerboseLevel**|2|3|@shouldalert|@shouldalert|2|@shouldalert|2|  
|**-KeepAliveMessageInterval**|300|300|300|300|300|300|300|  
|**-LoginTimeout**|15|15|15|15|15|15|15|  
|**-MaxDownloadChanges**|0|0|0|0|0|0|0|  
|**-MaxUploadChanges**|0|0|0|0|0|0|0|  
|**-MetadataRetentionCleanup**|@shouldalert|@shouldalert|@shouldalert|@shouldalert|@shouldalert|@shouldalert|@shouldalert|  
|**-NumDeadlockRetries**|5|5|5|5|5|5|5|  
|**-ParallelUploadDownload**|NULL|NULL|NULL|NULL|NULL|NULL|@shouldalert|  
|**-PollingInterval**|60|60|60|60|60|60|60|  
|**-QueryTimeout**|300|300|300|300|300|300|600|  
|**-QueueSizeMultiplier**|NULL|NULL|NULL|NULL|NULL|NULL|5|  
|**-SrcThreads**|2|2|2|2|2|@shouldalert|3|  
|**-StartQueueTimeout**|0|0|0|0|0|0|0|  
|**-UploadGenerationsPerBatch**|50|50|50|50|50|@shouldalert|500|  
|**-UploadReadChangesPerBatch**|100|100|100|100|100|100|100|  
|**-UploadWriteChangesPerBatch**|100|100|100|100|100|100|100|  
|**-Validate**|0|0|0|@shouldalert|3|0|0|  
|**-ValidateInterval**|60|60|60|60|60|60|60|  
  
## <a name="queue-reader-agent-profiles"></a>佇列讀取器代理程式設定檔  
 下表顯示於「佇列讀取器代理程式」的預設設定檔中定義的參數。 如需這些參數的詳細資訊，請參閱＜ [Replication Queue Reader Agent](replication-queue-reader-agent.md)＞。  
  
||預設|  
|-|-------------|  
|**-HistoryVerboseLevel**|@shouldalert|  
|**-LoginTimeout**|15|  
|**-PollingInterval**|5|  
|**-QueryTimeout**|1800|  
  
## <a name="see-also"></a>另請參閱  
 [複寫代理程式管理](replication-agent-administration.md)   
 [檢視並修改複寫代理程式命令提示字元參數 &#40;SQL Server Management Studio&#41;](view-and-modify-replication-agent-command-prompt-parameters.md)   
 [Replication Agent Executables Concepts](../concepts/replication-agent-executables-concepts.md)  
  
  