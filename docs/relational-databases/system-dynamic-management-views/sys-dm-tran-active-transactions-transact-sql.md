---
title: sys.dm_tran_active_transactions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_active_transactions
- sys.dm_tran_active_transactions_TSQL
- dm_tran_active_transactions_TSQL
- dm_tran_active_transactions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_active_transactions dynamic management view
ms.assetid: 154ad6ae-5455-4ed2-b014-e443abe2c6ee
caps.latest.revision: 39
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5aedf9cc79bb389d6920cc736c3f30b319368b07
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmtranactivetransactions-transact-sql"></a>sys.dm_tran_active_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之交易的資訊。  
  
> [!NOTE]  
>  若要呼叫從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_tran_active_transactions**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|transaction_id|**bigint**|執行個體層級 (而非資料庫層級) 的交易識別碼。 它只有在一個執行個體的所有資料庫才是唯一的，在所有的伺服器執行個體則不是。|  
|name|**nvarchar(32)**|交易名稱。 如果交易被標示出來，而且標示的名稱取代了交易名稱，這個值便會被覆寫。|  
|transaction_begin_time|**datetime**|交易啟動的時間。|  
|transaction_type|**int**|交易的類型。<br /><br /> 1 = 讀取/寫入交易<br /><br /> 2 = 唯讀交易<br /><br /> 3 = 系統交易<br /><br /> 4 = 分散式交易|  
|transaction_uow|**uniqueidentifier**|分散式交易的交易工作單位 (UOW) 識別碼。 MS DTC 是以 UOW 識別碼來使用分散式交易。|  
|transaction_state|**int**|0 = 交易尚未完全初始化。<br /><br /> 1 = 交易已經初始化，但尚未啟動。<br /><br /> 2 = 交易在作用中。<br /><br /> 3 = 交易已經結束。 它只用於唯讀交易。<br /><br /> 4 = 認可處理序已經在分散式交易上起始。 它只用於分散式交易。 分散式交易仍在作用中，但無法再做進一步的處理。<br /><br /> 5 = 交易是在已準備的狀態，正在等候解析。<br /><br /> 6 = 已認可交易。<br /><br /> 7 = 正在回復交易。<br /><br /> 8 = 已回復交易。|  
|transaction_status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|transaction_status2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|dtc_state|**int**|**適用於**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (初始版本至[目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299659))。<br /><br /> 1 = ACTIVE<br /><br /> 2 = PREPARED<br /><br /> 3 = COMMITTED<br /><br /> 4 = ABORTED<br /><br /> 5 = RECOVERED|  
|dtc_status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|dtc_isolation_level|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|filestream_transaction_id|**varbinary(128)**|**適用於**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (初始版本至[目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299659))。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|pdw_node_id|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此發行版本上的節點識別碼。|  
  
## <a name="permissions"></a>Permissions

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_tran_session_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)   
 [sys.dm_tran_database_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)   
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [交易相關的動態管理檢視和函數 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


