---
title: "OLEDB QueryInterface 事件類別 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLEDB QueryInterface event class
ms.assetid: f54c9ef9-3add-497c-a09b-42c4ce3c623d
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b47d42e3d8de99ad7dc4fc508c2af42a745ca704
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="oledb-queryinterface-event-class"></a>OLEDB QueryInterface 事件類別
  **OLEDB QueryInterface** 事件類別會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 對分散式查詢和遠端預存程序發出 OLE DB **QueryInterface** 呼叫時發生。 將這個事件類別納入追蹤，追蹤會監視與分散式查詢和遠端預存程序相關聯的問題。  
  
 納入 **OLEDB QueryInterface** 事件類別時，負擔量會比較高。 如果這類事件時常發生，追蹤可能會嚴重妨礙效能。 若要減輕所造成的負擔，此事件類別請限用於追蹤對特定問題的短期監視。  
  
## <a name="oledb-queryinterface-event-class-data-columns"></a>OLEDB QueryInterface 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|ClientProcessID|**int**|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|**nvarchar**|正在執行使用者陳述式的資料庫名稱。|35|是|  
|有效期間|**bigint**|完成 OLE DB QueryInterface 事件的時間長度。|13|否|  
|EndTime|**datetime**|事件結束的時間。|15|是|  
|錯誤|**int**|給定事件的錯誤號碼。 通常這是存放在 **sys.messages** 目錄檢視中的錯誤號碼。|31|是|  
|EventClass|**int**|事件類型 = 120。|27|否|  
|EventSequence|**int**|批次中 OLE DB 事件類別的順序。|51|否|  
|EventSubClass|**int**|0=正在啟動<br /><br /> 1=已完成|21|否|  
|GroupID|**int**|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|HostName|**nvarchar**|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IsSystem|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|LinkedServerName|**nvarchar**|連結伺服器的名稱。|45|是|  
|LoginName|**nvarchar**|使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|LoginSid|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|MethodName|**nvarchar**|呼叫方法的名稱。|47|否|  
|NTDomainName|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|**nvarchar**|Windows 使用者名稱。|6|是|  
|ProviderName|**nvarchar**|OLE DB 提供者的名稱。|46|是|  
|RequestID|**int**|包含陳述式之要求的識別碼。|49|是|  
|SessionLoginName|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 執行陳述式，則 **SessionLoginName** 將顯示 Login1 而 **LoginName** 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|StartTime|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|**nvarchar**|在 OLE DB 呼叫中傳送與接收的參數。|1|否|  
|TransactionID|**bigint**|由系統指派給交易的識別碼。|4|是|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Transact-SQL 中的 OLE Automation 物件](../../relational-databases/stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  
