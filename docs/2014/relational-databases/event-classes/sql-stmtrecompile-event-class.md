---
title: SQL:StmtRecompile 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SQL:StmtRecompile event class
ms.assetid: 3a134751-3e93-4fe8-bf22-1e0561189293
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 237838d4d9780c6180adebcae264949b10af94e9
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52804050"
---
# <a name="sqlstmtrecompile-event-class"></a>SQL:StmtRecompile 事件類別
  SQL:StmtRecompile 事件類別表示所有批次類型造成的陳述式層級重新編譯：預存程序、觸發程序、特定批次及查詢。 使用 sp_executesql、動態 SQL、Prepare 方法、Execute 方法或類似介面可以提交查詢。 應該使用 SQL:StmtRecompile 事件類別來取代 SP:Recompile 事件類別。  
  
## <a name="sqlstmtrecompile-event-class-data-columns"></a>SQL:StmtRecompile 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|建立 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|ClientProcessID|`int`|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|`int`|執行預存程序之資料庫的識別碼。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|`nvarchar`|執行預存程序之資料庫的名稱。|35|是|  
|EventSequence|`int`|要求內的事件順序。|51|否|  
|EventSubClass|`int`|描述重新編譯的原因：<br /><br /> 1 = 結構描述已變更<br /><br /> 2 = 統計資料已變更<br /><br /> 3 = 延遲編譯<br /><br /> 4 = Set 選項已變更<br /><br /> 5 = Temp 資料表已變更<br /><br /> 6 = 遠端資料列集已變更<br /><br /> 7 = For Browse 權限已變更<br /><br /> 8 = 查詢通知環境已變更<br /><br /> 9 = 資料分割檢視已變更<br /><br /> 10 = 資料指標選項已變更<br /><br /> 11 = 已要求選項 (重新編譯)|21|是|  
|GroupID|`int`|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|HostName|`nvarchar`|提交此陳述式的用戶端正在執行的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IntegerData2|`int`|預存程序或批次內造成重新編譯之陳述式的結束位移。 如果陳述式是其批次中的最後一個陳述式，則結束位移為 -1。|55|是|  
|IsSystem|`int`|指出事件是發生在系統處理序或使用者處理序。<br /><br /> 1 = 系統<br /><br /> 0 = 使用者|60|是|  
|LineNumber|`int`|此陳述式在批次內的序號 (如果適用的話)。|5|是|  
|LoginName|`nvarchar`|提交此批次的登入名稱。|11|是|  
|LoginSid|`image`|目前登入的使用者之安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|NestLevel|`int`|預存程序呼叫的巢狀層級。 例如，my_proc_a 預存程序會呼叫 my_proc_b。 在此情況下，my_proc_a 的 NestLevel 是 1，my_proc_b 的 NestLevel 是 2。|29|是|  
|NTDomainName|`nvarchar`|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|`nvarchar`|已連接使用者的 Windows 使用者名稱。|6|是|  
|ObjectID|`int`|物件的系統指派識別碼，此物件包含造成重新編譯的陳述式。 此物件可能是預存程序、觸發程序或使用者自訂函數。 對於特定批次或備妥的 SQL 而言，ObjectID 和 ObjectName 會傳回 NULL 值。|22|是|  
|ObjectName|`nvarchar`|ObjectID 所識別的物件名稱。|34|是|  
|ObjectType|`int`|代表參與事件之物件類型的值。 如需詳細資訊，請參閱 [ObjectType 追蹤事件資料行](objecttype-trace-event-column.md)。|28|是|  
|Offset|`int`|預存程序或批次內造成重新編譯之陳述式的起始位移。|61|是|  
|RequestID|`int`|包含陳述式之要求的識別碼。|49|是|  
|ServerName|`nvarchar`|被追蹤的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名稱。|26|否|  
|SessionLoginName|`nvarchar`|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|`int`|連接的伺服器處理序識別碼。|12|是|  
|SqlHandle|`varbinary`|這是一個 64 位元雜湊，以隨選查詢的文字或 SQL 物件的資料庫和物件識別碼為基礎。 這個值可以傳給 sys.dm_exec_sql_text()，以便擷取相關聯的 SQL 文字。|63|否|  
|StartTime|`datetime`|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|`ntext`|重新編譯的 Transact-SQL 陳述式文字。|1|是|  
|TransactionID|`bigint`|由系統指派給交易的識別碼。|4|是|  
|XactSequence|`bigint`|描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [SP:Recompile 事件類別](sp-recompile-event-class.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
