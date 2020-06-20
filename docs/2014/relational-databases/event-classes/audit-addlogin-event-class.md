---
title: Audit Addlogin 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Audit Addlogin event class
ms.assetid: 6e0633dc-889e-49ef-bace-3c50958db2dd
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2d14f0992c76934088a7bccf6d2b5a05b2db57ec
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053460"
---
# <a name="audit-addlogin-event-class"></a>Audit Addlogin 事件類別
  當新增或移除   登入時，就會發生 [!INCLUDE[msCoName](../../includes/msconame-md.md)]Audit Addlogin[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件類別。  
  
 在新增登入時如果還有設定其他屬性，例如預設資料庫，您可在這個事件的 **TextData** 資料行中找到這些屬性的相關資訊。 如果在新增登入時設定了這些屬性，就不會發生 **Audit Login Change Property** 事件。  
  
 這個稽核事件適用於 **sp_addlogin** 和 **sp_droplogin** 預存程序。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的未來版本可能會移除這個事件類別。 建議您改用 **Audit Server Principal Management** 事件類別。  
  
## <a name="audit-addlogin-event-class-data-columns"></a>Audit Addlogin 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|**ClientProcessID**|**int**|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|**DatabaseID**|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**DatabaseName**|**nvarchar**|正在執行使用者陳述式的資料庫名稱。|35|是|  
|**EventClass**|**int**|事件類型 = 104。|27|否|  
|**EventSequence**|**int**|要求中的給定事件順序。|51|否|  
|**EventSubClass**|**int**|事件子類別的類型。<br /><br /> 1=加入<br /><br /> 2=卸除|21|是|  
|**HostName**|**nvarchar**|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|**LoginName**|**nvarchar**|使用者的登入名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|**LoginSid**|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 **sys.server_principals** 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|**NTDomainName**|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|**NTUserName**|**nvarchar**|Windows 使用者名稱。|6|是|  
|**RequestID**|**int**|包含陳述式之要求的識別碼。|49|是|  
|**ServerName**|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|**SessionLoginName**|**Nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 執行陳述式，則 **SessionLoginName** 將顯示 Login1 而 **LoginName** 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|**SPID**|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|「成功」 |**int**|1 = 成功。 0 = 失敗。 例如，值為 1 表示權限檢查成功，值為 0 表示該檢查失敗。|23|是|  
|**TargetLoginName**|**nvarchar**|要加入或卸除的登入名稱。|42|是|  
|**TargetLoginSid**|**image**|目標登入的安全性識別碼 (SID) (若以參數傳遞的話)。|43|是|  
|**TransactionID**|**bigint**|由系統指派給交易的識別碼。|4|是|  
|**XactSequence**|**bigint**|用來描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Audit Login Change Property 事件類別](audit-login-change-property-event-class.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql)   
 [sp_droplogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droplogin-transact-sql)   
 [Audit Server Principal Management 事件類別](audit-server-principal-management-event-class.md)  
  
  
