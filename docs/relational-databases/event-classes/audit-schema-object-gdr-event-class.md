---
description: Audit Schema Object GDR 事件類別
title: Audit Schema Object GDR 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Audit Schema Object GDR event class
ms.assetid: a0187811-dc71-4792-a282-3bfe1ca90c21
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3c5403c4a42264c0d1ffeaf64bfd7c0d27525826
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97476289"
---
# <a name="audit-schema-object-gdr-event-class"></a>Audit Schema Object GDR 事件類別
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  每當 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的使用者對結構描述物件權限發出 GRANT、REVOKE 或 DENY 時，就會發生 **Audit Schema Object GDR** 事件類別。  
  
## <a name="audit-schema-object-gdr-event-class-data-columns"></a>Audit Schema Object GDR 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|**ClientProcessID**|**int**|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|**ColumnPermissions**|**int**|是否設定資料行權限的指標。 剖析陳述式文字以決定哪些權限套用至哪些資料行。 1=是，0=否。|44|是|  
|**DatabaseID**|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**DatabaseName**|**nvarchar**|正在執行使用者陳述式的資料庫名稱。|35|是|  
|**DBUserName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者名稱。|40|是|  
|**EventClass**|**int**|事件類型 = 103。|27|否|  
|**EventSequence**|**int**|要求中的給定事件順序。|51|否|  
|**EventSubClass**|**int**|事件子類別的類型。<br /><br /> 1=授與<br /><br /> 2=撤銷<br /><br /> 3=拒絕|21|是|  
|**HostName**|**nvarchar**|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|**LoginName**|**nvarchar**|使用者的登入名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|**LoginSid**|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 **sys.server_principals** 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|**NTDomainName**|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|**NTUserName**|**nvarchar**|Windows 使用者名稱。|6|是|  
|**ObjectName**|**nvarchar**|作為授與/撤銷/拒絕目標的物件名稱。|34|是|  
|**ObjectType**|**int**|代表參與事件之物件類型的值。 這個值會對應到 **sys.objects** 目錄檢視中的類型資料行。 針對各值，請參閱 [ObjectType 追蹤事件資料行](../../relational-databases/event-classes/objecttype-trace-event-column.md)。|28|是|  
|**OwnerName**|**nvarchar**|物件 (作為授與/撤銷/拒絕目標) 的物件擁有者的資料庫使用者名稱。|37|是|  
|**ParentName**|**nvarchar**|物件所在結構描述的名稱。|59|是|  
|**權限**|**bigint**|代表被檢查之權限類型的整數值。<br /><br /> 1=SELECT ALL<br /><br /> 2=UPDATE ALL<br /><br /> 4=REFERENCES ALL<br /><br /> 8=INSERT<br /><br /> 16=DELETE<br /><br /> 32=EXECUTE (僅程序)<br /><br /> 4096=SELECT ANY (至少一個資料行)<br /><br /> 8192=UPDATE ANY<br /><br /> 16384=REFERENCES ANY|19|是|  
|**RequestID**|**int**|包含陳述式之要求的識別碼。|49|是|  
|**ServerName**|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|**SessionLoginName**|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 執行陳述式，則 **SessionLoginName** 將顯示 Login1 而 **LoginName** 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|**SPID**|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|「成功」|**int**|1 = 成功。 0 = 失敗。 例如，值為 1 指出權限檢查成功，而值為 0 指出該檢查失敗。|23|是|  
|**TargetLoginName**|**nvarchar**|對於目標為登入的動作 (例如，加入新登入)，這是目標登入的名稱。|42|是|  
|**TargetLoginSid**|**image**|對於目標為登入的動作 (例如，加入新登入)，這是目標登入的安全性識別碼 (SID)。|43|是|  
|**TargetUserName**|**nvarchar**|對於目標為資料庫使用者的動作 (例如，授與使用者權限)，這是該使用者的名稱。|39|是|  
|**TextData**|**ntext**|與追蹤中所擷取的事件類別有關的文字值。|1|是|  
|**TransactionID**|**bigint**|由系統指派給交易的識別碼。|4|是|  
|**XactSequence**|**bigint**|用來描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)  
  
  
