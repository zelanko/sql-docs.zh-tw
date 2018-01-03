---
title: "sys.dm_hadr_auto_page_repair (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_hadr_auto_page_repair_TSQL
- sys.dm_hadr_auto_page_repair
- sys.dm_hadr_auto_page_repair_TSQL
- dm_hadr_auto_page_repair
dev_langs: TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- automatic page repair
- sys.dm_hadr_auto_page_repair dynamic management view
ms.assetid: d7840adf-4a1b-41ac-bc94-102c07ad1c79
caps.latest.revision: "8"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1ec6bf44d2628247af4d132cf06aadd30a19ceaf
ms.sourcegitcommit: 6e016a4ffd28b09456008f40ff88aef3d911c7ba
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2017
---
# <a name="sysdmhadrautopagerepair-transact-sql"></a>sys.dm_hadr_auto_page_repair (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  針對可用性複本上的任何可用性資料庫進行的每個自動修復頁面嘗試行為，各傳回一個資料列，該可用性複本是針對伺服器執行個體的任何可用性群組所裝載。 這個檢視包含在給定之主要或次要資料庫上進行最新自動修復頁面嘗試行為的資料列，而且每個資料庫最多 100 個資料列。 一旦資料庫到達上限時，下一個自動修復頁面嘗試行為的資料列就會取代其中一個現有的項目。
  
  下表定義各資料欄的意義：  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|這個資料列所對應的資料庫識別碼。|  
|**file_id**|**int**|頁面所在之檔案的識別碼。|  
|**page_id**|**bigint**|檔案中頁面的識別碼。|  
|**error_type**|**int**|錯誤的類型。 其值可能是：<br /><br /> **-**1 = 所有硬體 823 錯誤<br /><br /> 1 = 824 錯誤的總和檢查碼或損毀的頁 （例如，頁面識別碼不正確） 以外的錯誤<br /><br /> 2 = 總和檢查碼錯誤<br /><br /> 3 = 頁面損毀|  
|**page_status**|**int**|修復頁面嘗試行為的狀態：<br /><br /> 2 = 已將夥伴的要求排入佇列。<br /><br /> 3 = 要求已傳送給夥伴。<br /><br /> 4 = 已將自動修復頁面 (從夥伴收到的回應) 排入佇列。<br /><br /> 5 = 自動修復頁面成功，而且頁面應該可用。<br /><br /> 6 = 無法修復。 這表示在進行修復頁面嘗試行為時發生錯誤，因為該頁面在夥伴上也損毀、夥伴已中斷連線，或者發生網路問題。 這種狀態並非終端狀態。如果頁面上再次遇到損毀情況，就會再次向夥伴要求此頁面。|  
|**modification_time**|**datetime**|上次變更頁面狀態的時間。|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="see-also"></a>請參閱  
 [自動修復頁面 &#40;可用性群組：資料庫鏡像&#41;](../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [suspect_pages &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
 [管理 suspect_pages 資料表 &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  

