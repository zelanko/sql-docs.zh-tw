---
title: Audit Add Member to DB Role 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Audit Add Member to DB Role event class
ms.assetid: a5ac46b6-765b-4424-b6c7-4d5a1b898d65
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 673fa5941785f332893af3ea8f3630579d8a5741
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62761998"
---
# <a name="audit-add-member-to-db-role-event-class"></a>Audit Add Member to DB Role 事件類別
  每當資料庫角色中加入或移除登入時，就會發生**Audit Add Member TO DB role**事件類別。 這個事件類別是與 **sp_addrolemember**、 **sp_changegroup**及 **sp_droprolemember** 預存程序搭配使用。  
  
## <a name="audit-add-member-to-db-role-event-class-data-columns"></a>Audit Add Member to DB Role 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|建立 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|**ClientProcessID**|**int**|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|**DatabaseID**|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]如果在追蹤中捕捉到**ServerName**資料行，而且伺服器可供使用，則會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**DatabaseName**|**nvarchar**|角色成員資格遭修改的資料庫名稱。|35|是|  
|**DBUserName**|**nvarchar**|簽發者在資料庫中的使用者名稱。|40|是|  
|**EventClass**|**int**|事件類型 = 110。|27|否|  
|**EventSequence**|**int**|要求中的給定事件順序。|51|否|  
|**EventSubClass**|**int**|事件子類別的類型。<br /><br /> 1=加入<br /><br /> 2=卸除<br /><br /> 3=變更群組|21|是|  
|**HostName**|**nvarchar**|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|**LoginName**|**nvarchar**|使用者的登入名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|**LoginSid**|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在**server_principals**目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|**NTDomainName**|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|**NTUserName**|**nvarchar**|Windows 使用者名稱。|6|是|  
|**ObjectName**|**nvarchar**|正在參考之物件的名稱。|34|是|  
|**ObjectType**|**int**|代表參與事件之物件類型的值。 這個值對應于**sys.databases**目錄檢視中的類型資料行。 針對各值，請參閱 [ObjectType 追蹤事件資料行](objecttype-trace-event-column.md)。|28|是|  
|**OwnerName**|**nvarchar**|物件擁有者的資料庫使用者名稱。|37|是|  
|**RequestID**|**int**|包含陳述式之要求的識別碼。|49|是|  
|**RoleName**|**nvarchar**|啟用的應用程式角色的名稱。|38|是|  
|**ServerName**|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|**SessionLoginName**|**NVarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到，並以 Login2 的身分執行語句，**則 sessionloginname 將**會顯示 Login1，而**LoginName**會顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|**SPID**|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|「成功」 |**int**|1 = 成功。 0 = 失敗。 例如，值為 1 指出權限檢查成功，而值為 0 指出該檢查失敗。|23|是|  
|**TargetUserName**|**nvarchar**|其角色成員資格遭修改的使用者名稱。|39|是|  
|**TransactionID**|**Bigint**|由系統指派給交易的識別碼。|4|是|  
|**XactSequence**|**Bigint**|用來描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [sp_addrolemember &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)   
 [sp_droprolemember &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql)  
  
  
