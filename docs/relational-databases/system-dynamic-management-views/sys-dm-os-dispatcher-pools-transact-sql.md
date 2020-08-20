---
description: sys.dm_os_dispatcher_pools (Transact-SQL)
title: sys. dm_os_dispatcher_pools (Transact-sql) |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 768bf4dca3e42837218b49fe863ae45a3daf8630
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481930"
---
# <a name="sysdm_os_dispatcher_pools-transact-sql"></a>sys.dm_os_dispatcher_pools (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回有關工作階段發送器集區的資訊。 發送器集區是系統元件用來執行背景處理的執行緒集區。  
  
> [!NOTE]  
>  若要從或呼叫這個 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] ，請使用名稱 **sys. dm_pdw_nodes_os_dispatcher_pools**。  
  
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
|pdw_node_id|**int**|**適用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此散發所在之節點的識別碼。|  
  
## <a name="permissions"></a>權限

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 許可權。   
在進階層中 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] ，需要 `VIEW DATABASE STATE` 資料庫中的許可權。 在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 標準和基本層中，需要  **伺服器管理員** 或 **Azure Active Directory 系統管理員** 帳戶。   

## <a name="see-also"></a>另請參閱  
  
  


