---
title: SP:Recompile 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SP:Recompile event class
ms.assetid: 526c8eae-a07b-4d0e-b91e-8e537835d77d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 156d1ab718e88afb7ddb66b4270884065b4e6574
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68064958"
---
# <a name="sprecompile-event-class"></a>SP:Recompile 事件類別
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  SP:Recompile 事件類別表示有某個預存程序、觸發程序或使用者自訂函數已重新編譯。 這個事件類別報告的重新編譯會在陳述式層級發生。  
  
 若要追蹤陳述式層級的重新編譯，建議使用 SQL:StmtRecompile 事件類別。 SP:Recompile 事件類別已被取代。 如需詳細資訊，請參閱 [SQL:StmtRecompile 事件類別](../../relational-databases/event-classes/sql-stmtrecompile-event-class.md)。  
  
## <a name="sprecompile-event-class-data-columns"></a>SP:Recompile 事件類別資料行  
  
|資料行名稱|**Data type**|描述|資料行識別碼|可篩選|  
|----------------------|-------------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|建立 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體連線的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|ClientProcessID|**int**|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|**int**|執行預存程序之資料庫的識別碼。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|**nvarchar**|執行預存程序之資料庫的名稱。|35|是|  
|EventClass|**int**|事件類型 = 37。|27|否|  
|EventSequence|**int**|要求中之給定事件的順序。|51|否|  
|EventSubClass|**int**|事件子類別的類型。 指出重新編譯的原因。<br /><br /> 1 = 結構描述已變更<br /><br /> 2 = 統計資料已變更<br /><br /> 3 = 重新編譯 DNR<br /><br /> 4 = Set 選項已變更<br /><br /> 5 = Temp 資料表已變更<br /><br /> 6 = 遠端資料列集已變更<br /><br /> 7 = For Browse 權限已變更<br /><br /> 8 = 查詢通知環境已變更<br /><br /> 9 = MPI 檢視已變更<br /><br /> 10 = 資料指標選項已變更<br /><br /> 11 = With Recompile 選項|21|是|  
|GroupID|**int**|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|HostName|**nvarchar**|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IntegerData2|**int**|預存程序或批次內造成重新編譯之陳述式的結束位移。 如果陳述式是其批次中的最後一個陳述式，則結束位移為 -1。|55|是|  
|IsSystem|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|LoginName|**nvarchar**|使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|LoginSid|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|NestLevel|**int**|預存程序的巢狀層級。|29|是|  
|NTDomainName|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|**nvarchar**|Windows 使用者名稱。|6|是|  
|ObjectID|**int**|系統指派的預存程序識別碼。|22|是|  
|ObjectName|**nvarchar**|觸發重新編譯之物件的名稱。|34|是|  
|ObjectType|**int**|代表參與事件之物件類型的值。 如需詳細資訊，請參閱 [ObjectType 追蹤事件資料行](../../relational-databases/event-classes/objecttype-trace-event-column.md)。|28|是|  
|Offset|**int**|預存程序或批次內造成重新編譯之陳述式的起始位移。|61|是|  
|RequestID|**int**|包含陳述式之要求的識別碼。|49|是|  
|ServerName|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|SessionLoginName|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|SqlHandle|**varbinary**|這是一個 64 位元雜湊，以隨選查詢的文字或 SQL 物件的資料庫和物件識別碼為基礎。 這個值可以傳給 sys.dm_exec_sql_text()，以便擷取相關聯的 SQL 文字。|63|是|  
|StartTime|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|**ntext**|造成陳述式層級重新編譯的 Transact-SQL 陳述式文字。|1|是|  
|TransactionID|**bigint**|由系統指派給交易的識別碼。|4|是|  
|XactSequence|**bigint**|用來描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [SQL:StmtRecompile 事件類別](../../relational-databases/event-classes/sql-stmtrecompile-event-class.md)  
  
  
