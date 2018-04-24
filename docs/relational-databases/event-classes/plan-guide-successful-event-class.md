---
title: Plan Guide Successful 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: event-classes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Plan Guide Successful event class
ms.assetid: fecfbb6c-56c9-4db4-84d3-00d6e338355a
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5a46c563ed506762f82fc52dd23c23d93e55ebe8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="plan-guide-successful-event-class"></a>Plan Guide Successful 事件類別
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Plan Guide Successful 事件類別會指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 成功針對包含計畫指南的查詢或批次產生了執行計畫。 當下列條件成立時，就會引發此事件：  
  
-   計畫指南定義中的批次或模組符合正在執行的批次或模組。  
  
-   計畫指南定義中的查詢符合正在執行的查詢。  
  
-   計畫指南定義中的提示 (包括 USE PLAN 提示) 已成功套用至查詢。 也就是說，已編譯的查詢計畫會接受指定的提示。  
  
## <a name="plan-guide-successful-event-class-data-columns"></a>Plan Guide Successful 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|ClientProcessID|**int**|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 如果在追蹤中擷取 ServerName 資料行，而且伺服器可供使用，則會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|**nvarchar**|正在執行使用者陳述式的資料庫名稱。|35|是|  
|EventClass|**int**|事件類型 = 214。|27|否|  
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
|TextData|**ntext**|計畫指南的名稱。|@shouldalert|是|  
|TransactionID|**bigint**|由系統指派給交易的識別碼。|4|是|  
|XactSequence|**bigint**|描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [Plan Guide Unsuccessful 事件類別](../../relational-databases/event-classes/plan-guide-unsuccessful-event-class.md)   
 [擴充事件](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
