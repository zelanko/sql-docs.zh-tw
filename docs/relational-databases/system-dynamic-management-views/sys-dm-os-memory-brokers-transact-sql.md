---
title: sys.databases dm_os_memory_brokers （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_brokers
- dm_os_memory_brokers_TSQL
- sys.dm_os_memory_brokers_TSQL
- dm_os_memory_brokers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_brokers dynamic management view
ms.assetid: 48dd6ad9-0d36-4370-8a12-4921d0df4b86
author: stevestein
ms.author: sstein
ms.openlocfilehash: a8e131e2550ffa5078df5e284898ffe936128b7e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68265872"
---
# <a name="sysdm_os_memory_brokers-transact-sql"></a>sys.dm_os_memory_brokers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部的配置會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體管理員。 追蹤來自 sys.databases 的進程記憶體計數器之間的差異**dm_os_process_memory**和內部計數器，可以表示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]記憶體空間中外部元件的記憶體使用量。  
  
 記憶體 Broker 會根據目前的使用量和預計的使用量，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的各種元件之間，公平地散發記憶體配置。 記憶體 Broker 不會執行配置。 它們只會追蹤配置來計算散發。  
  
 下表提供有關記憶體 Broker 的資訊。  
  
> [!NOTE]  
>  若要從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]呼叫此，請使用**dm_pdw_nodes_os_memory_brokers**的名稱。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**pool_id**|**int**|如果與資源管理員集區相關聯，則是資源集區的識別碼。|  
|**memory_broker_type**|**Nvarchar （60）**|記憶體 Broker 的類型。 目前在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]有三種類型的記憶體代理程式，並列出其描述。<br /><br /> **MEMORYBROKER_FOR_CACHE** ：配置給快取物件使用的記憶體（不是緩衝集區快取）。<br /><br /> **MEMORYBROKER_FOR_STEAL** ：從緩衝集區遭竊的記憶體。 在目前的擁有者釋放這種記憶體前，其他元件無法重複使用它。<br /><br /> **MEMORYBROKER_FOR_RESERVE** ：保留供目前執行的要求使用的記憶體。|  
|**allocations_kb**|**Bigint**|已經配置給此類型 Broker 的記憶體數量 (以 KB 為單位)。|  
|**allocations_kb_per_sec**|**Bigint**|每秒的記憶體配置率 (以 KB 為單位)。 對於記憶體取消配置，這個值可以是負值。|  
|**predicted_allocations_kb**|**Bigint**|預測 Broker 所配置的記憶體數量。 這是以記憶體使用量模式為基礎。|  
|**target_allocations_kb**|**Bigint**|根據目前的設定與記憶體使用率模式所建議的配置記憶體數量 (以 KB 為單位)。 此 Broker 應該成長或壓縮到這個數量。|  
|**future_allocations_kb**|**Bigint**|將會在下幾秒鐘內完成的預計配置數量 (以 KB 為單位)。|  
|**overall_limit_kb**|**Bigint**|訊息代理程式可以配置的最大記憶體數量（以 kb 為單位）。|  
|**last_notification**|**Nvarchar （60）**|根據目前的設定與使用量模式所建議的記憶體使用量。 下列是有效值：<br /><br /> grow<br /><br /> shrink<br /><br /> stable|  
|**pdw_node_id**|**int**|**適用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此散發所在節點的識別碼。|  
  
## <a name="permissions"></a>權限  

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上， `VIEW SERVER STATE`需要許可權。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高階層級上， `VIEW DATABASE STATE`需要資料庫的許可權。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] [標準] 和 [基本] 層上，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。   
  
## <a name="see-also"></a>另請參閱  

  [SQL Server 作業系統相關的動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


