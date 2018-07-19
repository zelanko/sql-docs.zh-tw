---
title: sys.dm_os_memory_brokers (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9799cc3ed5f33e1260c6d4b1907329a9a01b3ffc
ms.sourcegitcommit: 70882926439a63ab9d812809429c63040eb9a41b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36262332"
---
# <a name="sysdmosmemorybrokers-transact-sql"></a>sys.dm_os_memory_brokers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部的配置會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體管理員。 追蹤從處理序記憶體計數器之間的差異**sys.dm_os_process_memory**與內部計數器可以指出記憶體內外部元件的使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]記憶體空間。  
  
 記憶體 Broker 會根據目前的使用量和預計的使用量，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的各種元件之間，公平地散發記憶體配置。 記憶體 Broker 不會執行配置。 它們只會追蹤配置來計算散發。  
  
 下表提供有關記憶體 Broker 的資訊。  
  
> [!NOTE]  
>  若要呼叫從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_os_memory_brokers**。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**pool_id**|**int**|如果與資源管理員集區相關聯，則是資源集區的識別碼。|  
|**memory_broker_type**|**nvarchar(60)**|記憶體 Broker 的類型。 目前有三種記憶體 broker [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 列出以下與它們的描述。<br /><br /> **MEMORYBROKER_FOR_CACHE** ： 以供配置的記憶體快取物件 （緩衝集區快取）。<br /><br /> **MEMORYBROKER_FOR_STEAL** ： 從緩衝集區奪取的記憶體。 在目前的擁有者釋放這種記憶體前，其他元件無法重複使用它。<br /><br /> **MEMORYBROKER_FOR_RESERVE** ： 保留供未來使用的目前正在執行要求的記憶體。|  
|**allocations_kb**|**bigint**|已經配置給此類型 Broker 的記憶體數量 (以 KB 為單位)。|  
|**allocations_kb_per_sec**|**bigint**|每秒的記憶體配置率 (以 KB 為單位)。 對於記憶體取消配置，這個值可以是負值。|  
|**predicted_allocations_kb**|**bigint**|預測 Broker 所配置的記憶體數量。 這是以記憶體使用量模式為基礎。|  
|**target_allocations_kb**|**bigint**|根據目前的設定與記憶體使用率模式所建議的配置記憶體數量 (以 KB 為單位)。 此 Broker 應該成長或壓縮到這個數量。|  
|**future_allocations_kb**|**bigint**|將會在下幾秒鐘內完成的預計配置數量 (以 KB 為單位)。|  
|**overall_limit_kb**|**bigint**|Broker 可以配置的最大記憶體數量 (以 KB 為單位)。|  
|**last_notification**|**nvarchar(60)**|根據目前的設定與使用量模式所建議的記憶體使用量。 下列是有效值：<br /><br /> grow<br /><br /> shrink<br /><br /> stable|  
|**pdw_node_id**|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此發行版本上的節點識別碼。|  
  
## <a name="permissions"></a>Permissions  

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
  
## <a name="see-also"></a>另請參閱  

  [SQL Server 作業系統相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


