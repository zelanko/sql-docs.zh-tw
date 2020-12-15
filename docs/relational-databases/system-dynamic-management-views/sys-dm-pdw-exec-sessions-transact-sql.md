---
description: 'sys.dm_pdw_exec_sessions (Transact-sql) '
title: sys.dm_pdw_exec_sessions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/22/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31c262b3-7e4d-44c4-af71-aaef0fd1a980
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 1e5fc3af931460de84dde4467b803226dcd6d431
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482559"
---
# <a name="sysdm_pdw_exec_sessions-transact-sql"></a>sys.dm_pdw_exec_sessions (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  保存設備上目前或最近開啟之所有會話的相關資訊。 它會針對每個會話列出一個資料列。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|session_id|**nvarchar(32)**|目前查詢的識別碼或最後一個查詢執行 (如果會話已結束，而且查詢是在終止) 時執行。 此視圖的索引鍵。|在系統中的所有會話之間是唯一的。|  
|status|**Nvarchar (10)**|針對目前的會話，識別會話目前為作用中或閒置中。 針對過去的會話，會話狀態可能會顯示 [已關閉] 或 [已終止] (如果已強制關閉會話) 。|「作用中」、「已關閉」、「閒置」、「已終止」|  
|request_id|**nvarchar(32)**|目前查詢或上次查詢執行的識別碼。|系統中的所有要求都是唯一的。 如果未執行，則為 Null。|  
|security_id|**varbinary(85)**|執行會話之主體的安全識別碼。||  
|login_name|**nvarchar(128)**|執行會話之主體的登入名稱。|符合使用者命名慣例的任何字串。|  
|login_time|**datetime**|使用者登入的日期和時間，以及建立此會話的日期和時間。|目前時間之前的有效 **日期時間** 。|  
|query_count|**int**|捕捉自從建立之後，已執行的查詢/requeststhis 會話數目。|大於或等於0。|  
|is_transactional|**bit**|捕捉會話目前是否在交易內。|0表示自動認可，1代表交易式。|  
|client_id|**nvarchar(255)**|捕獲會話的用戶端資訊。|任何有效的字串。|  
|app_name|**nvarchar(255)**|捕捉在連接程式中選擇性設定的應用程式名稱資訊。|任何有效的字串。|  
|sql_spid|**int**|SPID 的識別碼。 使用 `session_id` 此會話。 使用資料 `sql_spid` 行聯結至 **sys.dm_pdw_nodes_exec_sessions**。<br /><br /> 警告：此資料行包含已關閉的 spid。 **\* \* \* \***||  
  
 如需此視圖所保留之最大資料列的相關資訊，請參閱「 [容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 」主題中的「中繼資料」一節。  
  
## <a name="permissions"></a>權限  
 需要 `VIEW SERVER STATE` 權限。  
  
## <a name="see-also"></a>另請參閱  
 [Azure Synapse Analytics 和平行處理資料倉儲動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
