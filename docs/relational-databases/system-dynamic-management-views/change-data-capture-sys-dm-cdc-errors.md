---
title: sys.dm_cdc_errors (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_cdc_errors_TSQL
- dm_cdc_errors
- sys.dm_cdc_errors
- sys.dm_cdc_errors_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cdc_errors dynamic management view
- change data capture [SQL Server], error reporting
ms.assetid: 898f2d76-9e63-45ef-94da-8034e86004ab
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 03e39dee1e8a04aa1222be9d5e477c7dd76895ad
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="change-data-capture---sysdmcdcerrors"></a>異動資料擷取-sys.dm_cdc_errors
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對在異動資料擷取記錄掃描工作階段期間遇到的每個錯誤，各傳回一個資料列。  
 
 
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|工作階段的識別碼。<br /><br /> 0 = 錯誤並非在記錄掃描工作階段中發生。|  
|**phase_number**|**int**|指出發生錯誤時工作階段所處階段的編號。 如需每個階段的說明，請參閱[sys.dm_cdc_log_scan_sessions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md).|  
|**entry_time**|**datetime**|記錄錯誤的日期和時間。 此值會對應到 SQL 錯誤記錄檔中的時間戳記。|  
|**error_number**|**int**|錯誤訊息的識別碼。|  
|**error_severity**|**int**|訊息的嚴重性層級，介於 1 至 25 之間。|  
|**error_state**|**int**|錯誤的狀態編號。|  
|**error_message**|**nvarchar(1024)**|錯誤的訊息文字。|  
|**start_lsn**|**nvarchar(23)**|發生錯誤時正在處理之資料列的起始 LSN 值。<br /><br /> 0 = 錯誤並非在記錄掃描工作階段中發生。|  
|**begin_lsn**|**nvarchar(23)**|發生錯誤時正在處理之交易的開頭 LSN 值。<br /><br /> 0 = 錯誤並非在記錄掃描工作階段中發生。|  
|**sequence_value**|**nvarchar(23)**|發生錯誤時正在處理之資料列的 LSN 值。<br /><br /> 0 = 錯誤並非在記錄掃描工作階段中發生。|  
  
## <a name="remarks"></a>備註  
 **sys.dm_cdc_errors**包含先前 32 個工作階段資訊時發生錯誤。  
  
## <a name="permissions"></a>Permissions  
 需要 VIEW DATABASE STATE 權限來查詢**sys.dm_cdc_errors**動態管理檢視。 如需動態管理檢視權限的相關詳細資訊，請參閱[動態管理檢視和函數 &#40;TRANSACT-SQL &#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_cdc_log_scan_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md)   
 [sys.dm_repl_traninfo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-repl-traninfo-transact-sql.md)  
  
  

