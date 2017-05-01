---
title: "CursorRecompile 事件類別 | Microsoft Docs"
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
- CursorRecompile event class
ms.assetid: ab351c50-eed4-493a-87ed-89ec10933477
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cb8545540abe4396d76f35d9c029f7b4afb3732e
ms.lasthandoff: 04/11/2017

---
# <a name="cursorrecompile-event-class"></a>CursorRecompile 事件類別
  **CursorRecompile** 事件類別描述在應用程式開發介面 (API) 資料指標中發生的資料指標重新編譯事件。 當 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 因為結構描述已變更而需重新編譯 Transact-SQL 資料指標時，就會發生資料指標重新編譯事件。  
  
 可將 **CursorRecompile** 事件類別包含在記錄資料指標效能的追蹤當中， 當追蹤包含 **CursorRecompile** 事件類別時，所造成的負擔量，是依追蹤期間針對資料庫使用資料指標的頻率而定。 如果大量使用資料指標，追蹤可能會明顯地妨礙效能。  
  
## <a name="cursorrecompile-event-class-data-columns"></a>CursorRecompile 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|**ClientProcessID**|**int**|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|**DatabaseID**|**int**|由 USE *database* 陳述式所指定的資料庫識別碼；如果沒有針對指定執行個體發出 USE *database*陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**DatabaseName**|**nvarchar**|正在執行使用者陳述式的資料庫名稱。|35|是|  
|**EventClass**|**int**|記錄的事件類型 = 75。|27|否|  
|**EventSequence**|**int**|**CursorRecompile** 事件類別在批次中的順序。|51|否|  
|**GroupID**|**int**|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|**HostName**|**nvarchar**|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|**LoginName**|**nvarchar**|使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\Username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|**LoginSid**|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 **sys.server_principals** 目錄檢視中找到此項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|**NTDomainName**|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|**NTUserName**|**nvarchar**|Windows 使用者名稱。|6|是|  
|**RequestID**|**int**|重新編譯資料指標的要求識別碼。|49|是|  
|**ServerName**|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|**SessionLoginName**|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 執行陳述式，則 **SessionLoginName** 將顯示 Login1 而 **LoginName** 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|**SPID**|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|**TransactionID**|**bigint**|由系統指派給交易的識別碼。|4|是|  
|**XactSequence**|**bigint**|描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
