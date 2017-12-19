---
title: "Plan Guide Unsuccessful 事件類別 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: event-classes
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Plan Guide Unsuccessful event class
ms.assetid: ef9759f8-5613-4884-9257-86b609313f69
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: be69d14358de068a3799823e575df8ea9033531e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="plan-guide-unsuccessful-event-class"></a>Plan Guide Unsuccessful 事件類別
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Plan Guide Unsuccessful 事件類別指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法針對包含計畫指南的查詢或批次產生執行計畫。 而且，系統將不會使用此計畫指南來編譯計畫。 當下列條件成立時，就會引發此事件：  
  
-   計畫指南定義中的批次/模組符合正在執行的批次。  
  
-   計畫指南定義中的查詢符合正在執行的查詢。  
  
-   計畫指南定義中的提示 (包括 USE PLAN 提示) 沒有成功套用至查詢或批次。 也就是說，已編譯的查詢計畫無法接受指定的提示，而且系統將不會使用此計畫指南來編譯計畫。  
  
 無效的計畫指南可能會導致引發此事件。 請使用 [sys.fn_validate_plan_guide](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md) 函數來驗證查詢或批次所使用的計畫指南，然後更正此函數所回報的錯誤。  
  
 這個事件包含在 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 微調範本中。  
  
## <a name="plan-guide-unsuccessful-event-class-data-columns"></a>Plan Guide Unsuccessful 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|ClientProcessID|**int**|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 如果在追蹤中擷取 ServerName 資料行，則會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|**nvarchar**|正在執行使用者陳述式的資料庫名稱。|35|是|  
|EventClass|**int**|事件類型 = 218。|27|否|  
|EventSequence|**int**|要求中之特定事件的順序。|51|否|  
|HostName|**nvarchar**|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IsSystem|**int**|指出事件是發生在系統處理序或使用者處理序：1 = 系統，0 = 使用者。|60|是|  
|LoginName|**nvarchar**|使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN [!INCLUDE[msCoName](../../includes/msconame-md.md)] username\\*格式的*Windows 登入認證)。|11|是|  
|LoginSid|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 或 [sys.sql_logins](../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md) 目錄檢視中找到此資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|NTDomainName|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|**nvarchar**|Windows 使用者名稱。|6|是|  
|ObjectID|**int**|套用計畫指南時正在編譯之模組的物件識別碼。 如果計畫指南沒有套用至模組，這個資料行就會設定為 NULL。|22|是|  
|RequestID|**int**|包含陳述式之要求的識別碼。|49|是|  
|ServerName|**nvarchar**|所追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|SessionLoginName|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|StartTime|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|**ntext**|計畫指南的名稱。|1|是|  
|TransactionID|**bigint**|由系統指派給交易的識別碼。|4|是|  
|XactSequence|**bigint**|描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [Plan Guide Successful 事件類別](../../relational-databases/event-classes/plan-guide-successful-event-class.md)   
 [擴充事件](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sys.fn_validate_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
  
