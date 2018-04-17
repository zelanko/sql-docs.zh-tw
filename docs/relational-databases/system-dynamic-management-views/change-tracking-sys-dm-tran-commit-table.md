---
title: sys.dm_tran_commit_table (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_tran_commit_table
- dm_tran_commit_table_TSQL
- sys.dm_tran_commit_table
- sys.dm_tran_commit_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_commit_table dynamic management view
ms.assetid: 732d23c5-1f6c-4e96-bc85-8f29b520cf0e
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7ef5171ec533bd912c14d3623a9c01e93d79edf2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="change-tracking---sysdmtrancommittable"></a>變更追蹤-sys.dm_tran_commit_table
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 變更追蹤所追蹤之資料表所認可的每個交易，各顯示一個資料列。 為了可支援性而提供的 sys.dm_tran_commit_table 管理檢視會公開交易相關的資訊，變更追蹤會將該資訊儲存在 sys.syscommittab 系統資料表內。 sys.syscommittab 資料表會提供從資料庫特有交易識別碼到交易的認可記錄序號 (LSN) 和認可時間戳記之間的有效率、持續性對應。 儲存在 sys.syscommittab 資料表中而且由這個管理檢視所公開的資料會根據設定變更追蹤時指定的保留週期進行清除。  
  
> [!NOTE]  
>  若要呼叫從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_tran_commit_table**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|commit_ts|**bigint**|單純遞增數字，當做每一筆認可之交易的資料庫特有時間戳記。|  
|xdes_id|**bigint**|交易之資料庫特有的內部識別碼。|  
|commit_lbn|**bigint**|包含交易之認可記錄檔記錄的記錄區塊數目。|  
|commit_csn|**bigint**|交易之執行個體特有的認可序號。|  
|commit_time|**smalldatetime**|認可交易的時間。|  
|pdw_node_id|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此發行版本上的節點識別碼。|  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [關於變更追蹤 &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)  
  
  


