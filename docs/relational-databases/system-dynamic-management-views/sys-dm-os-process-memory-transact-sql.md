---
title: sys.dm_os_process_memory (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_process_memory_TSQL
- dm_os_process_memory_TSQL
- dm_os_process_memory
- sys.dm_os_process_memory
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_process_memory dynamic management view
ms.assetid: e838130c-95d4-4605-9e3b-eb0ab71cd250
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 21bde2847047df08e620e6ce64c3fe34f7993b6d
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmosprocessmemory-transact-sql"></a>sys.dm_os_process_memory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  大部分用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序空間的記憶體配置都是透過允許追蹤和說明這些配置的介面進行控制。 不過，記憶體配置可能會在略過內部記憶體管理常式的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 位址空間中進行。 其值是透過呼叫基底作業系統取得。 內部的方法無法操作[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 調整的情況針對鎖定或大型分頁配置除外。  
  
 指出記憶體大小的所有傳回值都會以 KB 為單位顯示。 資料行**total_virtual_address_space_reserved_kb**重複**virtual_memory_in_bytes**從**sys.dm_os_sys_info**。  
  
 下表提供處理位址空間的完整內容。  
  
> [!NOTE]  
>  若要呼叫從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_os_process_memory**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**physical_memory_in_use_kb**|**bigint**|指出處理工作集 (以 KB 為單位)，如作業系統所回報，以及使用大型分頁 API 所完成的追蹤配置。 不可為 Null。|  
|**large_page_allocations_kb**|**bigint**|指定使用大型分頁 API 所配置的實體記憶體。 不可為 Null。|  
|**locked_page_allocations_kb**|**bigint**|指定記憶體中鎖定的記憶體頁面。 不可為 Null。|  
|**total_virtual_address_space_kb**|**bigint**|指出虛擬位址空間之使用者模式部分的大小總計。 不可為 Null。|  
|**virtual_address_space_reserved_kb**|**bigint**|指出處理序所保留的虛擬位址空間的總數。 不可為 Null。|  
|**virtual_address_space_committed_kb**|**bigint**|指出已經認可或對應至實體頁面的已保留虛擬位址空間數量。 不可為 Null。|  
|**virtual_address_space_available_kb**|**bigint**|指出目前可用的虛擬位址空間數量。 不可為 Null。<br /><br /> **注意：**釋放小於可存在配置資料粒度的區域。 這些區域無法用於配置。|  
|**page_fault_count**|**bigint**|指出由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序所造成的分頁錯誤數目。 不可為 Null。|  
|**memory_utilization_percentage**|**int**|指定位於工作集之認可記憶體的百分比。 不可為 Null。|  
|**available_commit_limit_kb**|**bigint**|指出可供處理序認可的記憶體數量。 不可為 Null。|  
|**process_physical_memory_low**|**bit**|指出處理序正在回應實體記憶體不足的通知。 不可為 Null。|  
|**process_virtual_memory_low**|**bit**|指出偵測到虛擬記憶體不足的情況。 不可為 Null。|  
|**pdw_node_id**|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此發行版本上的節點識別碼。|  
  
## <a name="permissions"></a>Permissions  
 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]需要在伺服器上的 VIEW SERVER STATE 權限。  
  
在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server 作業系統相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


