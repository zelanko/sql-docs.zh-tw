---
title: Audit Database Scope GDR 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Audit Database Scope GDR event class
ms.assetid: 1641a38a-ef24-46ce-b2f4-bf732858c771
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7f6ae55f3bdaef607d386926b52df276e95c4dc9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48089680"
---
# <a name="audit-database-scope-gdr-event-class"></a>Audit Database Scope GDR 事件類別
  每當  的任何使用者，對於授與資料庫權限的資料庫專有動作，對陳述式權限發出 GRANT、REVOKE 或 DENY 時，就會發生 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for database-only actions such as granting permissions on a database.  
  
## <a name="audit-database-scope-gdr-event-class-data-columns"></a>Audit Database Scope GDR 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|**ClientProcessID**|**int**|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供處理序識別碼，這個資料行就會擴展。|9|是|  
|**DatabaseID**|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**DatabaseName**|**nvarchar**|正在執行使用者陳述式的資料庫名稱。|35|是|  
|**DBUserName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者名稱。|40|是|  
|**EventClass**|**int**|事件類別 = 102。|27|否|  
|**EventSequence**|**int**|要求中的給定事件順序。|51|否|  
|**EventSubClass**|**int**|事件子類別的類型。<br /><br /> 1=授與<br /><br /> 2=撤銷<br /><br /> 3=拒絕|21|是|  
|**HostName**|**nvarchar**|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|**LoginName**|**nvarchar**|使用者的登入名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|**LoginSid**|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 **sys.server_principals** 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|**NTDomainName**|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|**NTUserName**|**nvarchar**|Windows 使用者名稱。|6|是|  
|**ObjectName**|**nvarchar**|正在參考之物件的名稱。|34|是|  
|**ObjectType**|**int**|代表參與事件之物件類型的值。 這個值會對應到 **sys.objects** 目錄檢視中的類型資料行。 如需各值，請參閱 [ObjectType 追蹤事件資料行](objecttype-trace-event-column.md)。|28|是|  
|**OwnerName**|**nvarchar**|物件擁有者的資料庫使用者名稱。|37|是|  
|**Permissions**|**bigint**|代表被檢查之權限類型的整數值。<br /><br /> 1=CREATE DATABASE<br /><br /> 2=CREATE TABLE<br /><br /> 4=CREATE PROCEDURE<br /><br /> 8=CREATE VIEW<br /><br /> 16=CREATE RULE<br /><br /> 32=CREATE DEFAULT<br /><br /> 64=BACKUP DATABASE<br /><br /> 128=BACKUP LOG<br /><br /> 256=BACKUP TABLE<br /><br /> 512=CREATE FUNCTION|19|是|  
|**RequestID**|**int**|包含陳述式之要求的識別碼。|49|是|  
|**ServerName**|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|**SessionLoginName**|**Nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 執行陳述式，則 **SessionLoginName** 將顯示 Login1 而 **LoginName** 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|**SPID**|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|**成功**|**int**|1 = 成功。 0 = 失敗。 例如，值為 1 指出權限檢查成功，而值為 0 指出該檢查失敗。|23|是|  
|**TargetLoginName**|**nvarchar**|對於目標為登入的動作 (例如，加入新登入)，這是目標登入的名稱。|42|是|  
|**TargetLoginSid**|**image**|對於目標為登入的動作 (例如，加入新登入)，這是目標登入的安全性識別碼 (SID)。|43|是|  
|**TargetUserName**|**nvarchar**|對於目標為資料庫使用者的動作 (例如，授與使用者權限)，這是該使用者的名稱。|39|是|  
|**TextData**|**ntext**|Grant/Revoke/Deny 陳述式的 SQL 文字。|1|是|  
|**TransactionID**|**bigint**|由系統指派給交易的識別碼。|4|是|  
|**XactSequence**|**bigint**|用來描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)   
 [REVOKE &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql)   
 [DENY &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-transact-sql)  
  
  
