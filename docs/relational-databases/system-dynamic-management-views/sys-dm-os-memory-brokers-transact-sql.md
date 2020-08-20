---
description: sys.dm_os_memory_brokers (Transact-SQL)
title: sys. dm_os_memory_brokers (Transact-sql) |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: edf0cd2ad0dae2acc6c89be4942c753d33d4c46d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454890"
---
# <a name="sysdm_os_memory_brokers-transact-sql"></a>sys.dm_os_memory_brokers (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部的配置會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體管理員。 從 **sys. dm_os_process_memory** 和內部計數器追蹤進程記憶體計數器之間的差異，可能表示記憶體空間中的外部元件記憶體使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 記憶體 Broker 會根據目前的使用量和預計的使用量，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的各種元件之間，公平地散發記憶體配置。 記憶體 Broker 不會執行配置。 它們只會追蹤配置來計算散發。  
  
 下表提供有關記憶體 Broker 的資訊。  
  
> [!NOTE]  
>  若要從或呼叫這個 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ，請使用名稱 **sys. dm_pdw_nodes_os_memory_brokers**。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**pool_id**|**int**|如果與資源管理員集區相關聯，則是資源集區的識別碼。|  
|**memory_broker_type**|**nvarchar(60)**|記憶體 Broker 的類型。 目前有三種類型的記憶體代理程式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，如下所列及其說明。<br /><br /> **MEMORYBROKER_FOR_CACHE** ：配置給快取物件使用的記憶體 (不是緩衝集區快取) 。<br /><br /> **MEMORYBROKER_FOR_STEAL** ：從緩衝集區遭竊的記憶體。 在目前的擁有者釋放這種記憶體前，其他元件無法重複使用它。<br /><br /> **MEMORYBROKER_FOR_RESERVE** ：保留給目前正在執行之要求使用的記憶體。|  
|**allocations_kb**|**bigint**|已經配置給此類型 Broker 的記憶體數量 (以 KB 為單位)。|  
|**allocations_kb_per_sec**|**bigint**|每秒的記憶體配置率 (以 KB 為單位)。 對於記憶體取消配置，這個值可以是負值。|  
|**predicted_allocations_kb**|**bigint**|預測 Broker 所配置的記憶體數量。 這是以記憶體使用量模式為基礎。|  
|**target_allocations_kb**|**bigint**|根據目前的設定與記憶體使用率模式所建議的配置記憶體數量 (以 KB 為單位)。 此 Broker 應該成長或壓縮到這個數量。|  
|**future_allocations_kb**|**bigint**|將會在下幾秒鐘內完成的預計配置數量 (以 KB 為單位)。|  
|**overall_limit_kb**|**bigint**|訊息代理程式可以配置的最大記憶體數量（以 kb (KB) ）。|  
|**last_notification**|**nvarchar(60)**|根據目前的設定與使用量模式所建議的記憶體使用量。 下列是有效值：<br /><br /> grow<br /><br /> shrink<br /><br /> 穩定|  
|**pdw_node_id**|**int**|**適用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此散發所在之節點的識別碼。|  
  
## <a name="permissions"></a>權限  

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 許可權。   
在進階層中 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] ，需要 `VIEW DATABASE STATE` 資料庫中的許可權。 在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 標準和基本層中，需要  **伺服器管理員** 或 **Azure Active Directory 系統管理員** 帳戶。   
  
## <a name="see-also"></a>另請參閱  

  [SQL Server 作業系統相關的動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


