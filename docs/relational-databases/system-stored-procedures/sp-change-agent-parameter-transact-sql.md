---
title: "sp_change_agent_parameter (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_change_agent_parameter_TSQL
- sp_change_agent_parameter
helpviewer_keywords:
- sp_change_agent_parameter
ms.assetid: f1fbecc7-e64f-405c-8067-6b38c1f3c0a0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8eb615a76b87152c437d3ecc5667262df4e0120c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="spchangeagentparameter-transact-sql"></a>sp_change_agent_parameter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  複寫代理程式設定檔的參數中所儲存的變更[MSagent_parameters](../../relational-databases/system-tables/msagent-parameters-transact-sql.md)系統資料表。 這個預存程序執行於在任何資料庫執行代理程式的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_change_agent_parameter [ @profile_id= ] profile_id, [ @parameter_name= ] 'parameter_name', [ @parameter_value= ] 'parameter_value'  
```  
  
## <a name="arguments"></a>引數  
 [  **@profile_id=**] *profile_id*，  
 這是設定檔的識別碼。 *profile_id*是**int**，沒有預設值。  
  
 [  **@parameter_name=**] **'***parameter_name***'**  
 這是參數的名稱。 *parameter_name*是**sysname**，沒有預設值。 系統設定檔可以變更的參數會隨著代理程式的類型而不同。 若要找出哪種類型的代理程式這*profile_id*表示，找出*profile_id*中的資料行**Msagent_profiles**資料表，並記下*agent_type*值。  
  
> [!NOTE]  
>  如果支援參數指定*agent_type*，但尚未定義代理程式設定檔中，則會傳回錯誤。 若要將參數加入代理程式設定檔必須執行[sp_add_agent_parameter](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)。  
  
 快照集代理程式 (*agent_type*=**1**)，如果在設定檔中定義，可以變更下列屬性：  
  
-   **70Subscribers**  
  
-   **BcpBatchSize**  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **MaxBcpThreads**  
  
-   **MaxNetworkOptimization**  
  
-   **輸出**  
  
-   **OutputVerboseLevel**  
  
-   **封包**  
  
-   **QueryTimeout**  
  
-   **StartQueueTimeout**  
  
-   **UsePerArticleContentsView**  
  
 記錄讀取器代理程式 (*agent_type*=**2**)，如果在設定檔中定義，可以變更下列屬性：  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **MessageInterval**  
  
-   **輸出**  
  
-   **OutputVerboseLevel**  
  
-   **封包**  
  
-   **PollingInterval**  
  
-   **QueryTimeout**  
  
-   **ReadBatchSize**  
  
-   **ReadBatchThreshold**  
  
 散發代理程式 」 (*agent_type*=**3**)，如果在設定檔中定義，可以變更下列屬性：  
  
-   **BcpBatchSize**  
  
-   **CommitBatchSize**  
  
-   **CommitBatchThreshold**  
  
-   **FileTransferType**  
  
-   **HistoryVerboseLevel**  
  
-   **KeepAliveMessageInterval**  
  
-   **LoginTimeout**  
  
-   **MaxBcpThreads**  
  
-   **MaxDeliveredTransactions**  
  
-   **MessageInterval**  
  
-   **輸出**  
  
-   **OutputVerboseLevel**  
  
-   **封包**  
  
-   **PollingInterval**  
  
-   **QueryTimeout**  
  
-   **QuotedIdentifier**  
  
-   **SkipErrors**  
  
-   **TransactionsPerHistory**  
  
 合併代理程式 」 (*agent_type*=**4**)，如果在設定檔中定義，可以變更下列屬性：  
  
-   **AltSnapshotFolder**  
  
-   **BcpBatchSize**  
  
-   **ChangesPerHistory**  
  
-   **DestThreads**  
  
-   **DownloadGenerationsPerBatch**  
  
-   **DownloadReadChangesPerBatch**  
  
-   **DownloadWriteChangesPerBatch**  
  
-   **DynamicSnapshotLocation**  
  
-   **ExchangeType**  
  
-   **FastRowCount**  
  
-   **FileTransferType**  
  
-   **GenerationChangeThreshold**  
  
-   **HistoryVerboseLevel**  
  
-   **InputMessageFile**  
  
-   **InteractiveResolution**  
  
-   **InterruptOnMessagePattern**  
  
-   **KeepAliveMessageInterval**  
  
-   **LoginTimeout**  
  
-   **MaxBcpThreads**  
  
-   **MaxDownloadChanges**  
  
-   **MaxUploadChanges**  
  
-   **MetadataRetentionCleanup**  
  
-   **NumDeadlockRetries**  
  
-   **輸出**  
  
-   **OutputMessageFile**  
  
-   **OutputVerboseLevel**  
  
-   **封包**  
  
-   **ParallelUploadDownload**  
  
-   **PauseOnMessagePattern**  
  
-   **PauseTime**  
  
-   **PollingInterval**  
  
-   **ProcessMessagesAtPublisher**  
  
-   **ProcessMessagesAtSubscriber**  
  
-   **QueryTimeout**  
  
-   **QueueSizeMultiplier**  
  
-   **SrcThreads**  
  
-   **StartQueueTimeout**  
  
-   **SyncToAlternate**  
  
-   **UploadGenerationsPerBatch**  
  
-   **UploadReadChangesPerBatch**  
  
-   **UploadWriteChangesPerBatch**  
  
-   **UseInprocLoader**  
  
-   **Validate**  
  
-   **ValidateInterval**  
  
 佇列讀取器代理程式 (*agent_type*=**9**)，如果在設定檔中定義，可以變更下列屬性：  
  
-   **HistoryVerboseLevel**  
  
-   **LoginTimeout**  
  
-   **輸出**  
  
-   **OutputVerboseLevel**  
  
-   **PollingInterval**  
  
-   **QueryTimeout**  
  
-   **ResolverState**  
  
-   **SQLQueueMode**  
  
 若要查看已為給定的設定檔定義的參數，執行**sp_help_agent_profile**並記下*profile_name*聯*profile_id*。 以適當*profile_id*，接下來執行**sp_help_agent_parameters**使用該*profile_id*若要查看與設定檔相關聯的參數。 可以在設定檔中加入參數，藉由執行[sp_add_agent_parameter](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)。  
  
 [  **@parameter_value=**] **'***parameter_value***'**  
 這是參數的新值。 *parameter_value*是**nvarchar （255)**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_change_agent_parameter**用於所有複寫類型。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_change_agent_parameter**。  
  
## <a name="see-also"></a>請參閱＜  
 [複寫代理程式設定檔](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [複寫記錄讀取器代理程式](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [複寫合併代理程式](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [複寫佇列讀取器代理程式](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)   
 [sp_add_agent_parameter &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_drop_agent_parameter &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_help_agent_parameter &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
