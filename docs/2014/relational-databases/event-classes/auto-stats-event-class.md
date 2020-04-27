---
title: Auto Stats 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Auto Stats event class
ms.assetid: cd613fce-01e1-4d8f-86cc-7ffbf0759f9e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 354c2e39716dc0cfa215e4392945bf9aa5899da0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63012367"
---
# <a name="auto-stats-event-class"></a>Auto Stats 事件類別
  **Auto Stats** 事件類別表示索引和資料行統計資料已發生自動更新。  
  
## <a name="auto-stats-event-class-data-columns"></a>Auto Stats 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|**ClientProcessID**|**int**|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|**DatabaseID**|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**DatabaseName**|**nvarchar**|正在執行使用者陳述式的資料庫名稱。|35|是|  
|**期限**|**bigint**|事件所花費的時間量 (以百萬分之一秒為單位)。|13|是|  
|**EndTime**|**datetime**|事件結束的時間。|15|是|  
|**錯誤**|**int**|給定事件的錯誤號碼。 通常這是存放在 **sys.messages** 目錄檢視中的錯誤號碼。|31|是|  
|**EventClass**|**int**|事件類型 = 58。|27|否|  
|**EventSequence**|**int**|要求中的給定事件順序。|51|否|  
|**EventSubClass**|**int**|事件子類別的類型：<br /><br /> 1：同步建立/更新的統計資料;**TextData**資料行指出哪些是已建立或更新的統計資料。<br /><br /> 2：非同步統計資料更新；作業已佇列。<br /><br /> 3：非同步統計資料更新；作業開始。<br /><br /> 4：非同步統計資料更新；作業已完成。|21|是|  
|**GroupID**|**int**|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|**HostName**|**nvarchar**|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|**IndexID**|**int**|受事件影響之物件上的索引/統計資料項目識別碼。 若要判斷物件的索引識別碼，請使用 **sys.indexes** 目錄檢視的 **index_id** 資料行。|24|是|  
|**IntegerData**|**int**|已更新成功的統計資料集合數目。|25|是|  
|**IntegerData2**|**int**|作業序號。|55|是|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|**LoginName**|**nvarchar**|使用者的登入名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 Windows 登入認證)。|11|是|  
|**LoginSid**|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 **sys.server_principals** 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|**NTDomainName**|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|**NTUserName**|**nvarchar**|Windows 使用者名稱。|6|是|  
|**ObjectID**|**int**|系統指派給物件的識別碼。|22|是|  
|**RequestID**|**int**|包含陳述式之要求的識別碼。|49|是|  
|**ServerName**|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|**SessionLoginName**|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 執行陳述式，則 **SessionLoginName** 將顯示 Login1 而 **LoginName** 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|**SPID**|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|「成功」 |**int**|0 = 錯誤。<br /><br /> 1 = 成功。<br /><br /> 2 = 因伺服器調整流速而略過 (MSDE)。|23|是|  
|**TextData**|**ntext**|此資料行的內容需視統計資料是採同步更新 (**EventSubClass** 1) 或非同步更新 (**EventSubClass** 2、3 或 4) 而定：<br /><br /> 1：列出已更新/建立的統計資料<br /><br /> 2、3 或 4：NULL； **IndexID** 資料行中會填入已更新之統計資料的索引/統計資料識別碼。|1|是|  
|**TransactionID**|**bigint**|由系統指派給交易的識別碼。|4|是|  
|**類型**|**int**|作業類型。|57|是|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
