---
title: sys.databases dm_os_dispatcher_pools （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_dispatcher_pools_TSQL
- dm_os_dispatcher_pools
- sys.dm_os_dispatcher_pools
- sys.dm_os_dispatcher_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], views
- sys.dm_os_dispatcher_pools DMV
ms.assetid: b9edbc83-c6bc-4753-9bb5-a454cfe7d6bf
author: stevestein
ms.author: sstein
ms.openlocfilehash: cf8e1700f51f808811a1f5a61f86777547c9cb65
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68265846"
---
# <a name="sysdm_os_dispatcher_pools-transact-sql"></a>sys.dm_os_dispatcher_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回有關工作階段發送器集區的資訊。 發送器集區是系統元件用來執行背景處理的執行緒集區。  
  
> [!NOTE]  
>  若要從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]呼叫此，請使用**dm_pdw_nodes_os_dispatcher_pools**的名稱。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|dispatcher_pool_address|**varbinary(8)**|發送器集區的位址。 dispatcher_pool_address 是唯一的。 不可為 Null。|  
|type|**nvarchar(256)**|發送器集區的類型。 不可為 Null。 發送器集區的類型有兩種：<br /><br /> DISP_POOL_XE_ENGINE<br /><br /> DISP_POOL_XE_SESSION<br /><br /> 查詢 DMV 以取得完整清單|  
|NAME|**nvarchar(256)**|發送器集區的名稱。 不可為 Null。|  
|dispatcher_count|**int**|使用中發送器執行緒的數目。 不可為 Null。|  
|dispatcher_ideal_count|**int**|發送器集區可以成長來使用的發送器執行緒數目。 不可為 Null。|  
|dispatcher_timeout_ms|**int**|發送器在結束之前等候新工作的時間 (以毫秒為單位)。 不可為 Null。|  
|dispatcher_waiting_count|**int**|閒置發送器執行緒的數目。 不可為 Null。|  
|queue_length|**int**|等候要由發送器集區所處理的工作項目數。 不可為 Null。|  
|pdw_node_id|**int**|**適用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此散發所在節點的識別碼。|  
  
## <a name="permissions"></a>權限

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上， `VIEW SERVER STATE`需要許可權。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高階層級上， `VIEW DATABASE STATE`需要資料庫的許可權。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] [標準] 和 [基本] 層上，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。   

## <a name="see-also"></a>另請參閱  
  
  


