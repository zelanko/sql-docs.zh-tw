---
title: Object:Altered 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Object:Altered event class
ms.assetid: f94e3b59-ff2f-4d8d-8479-e85ce5b3483e
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d491fb1b7dd799f8b831ed3cdd5846e7656398ba
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43060030"
---
# <a name="objectaltered-event-class"></a>Object:Altered 事件類別
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Object:Altered 事件類別指出物件已遭到改變，例如被 ALTER INDEX、ALTER TABLE 或 ALTER DATABASE 陳述式改變。 這個事件類別可用來判別物件是否已被改變，例如被 ODBC 應用程式改變，此應用程式經常會建立暫存的預存程序。  
  
 Object:Altered 事件類別一定會產生兩個事件。 第一個事件指出 Begin 階段。 第二個事件指出 Rollback 或 Commit 階段。  
  
 藉由監視 LoginName 和 NTUserName 資料行，您可以判別是誰在建立、刪除或改變物件。  
  
## <a name="objectaltered-event-class-data-columns"></a>Object:Altered 事件類別資料行  
  
|資料行名稱|資料類型|Description|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|ClientProcessID|**int**|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 如果在追蹤中擷取 ServerName 資料行，則會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|**nvarchar**|正在執行使用者陳述式的資料庫名稱。|35|是|  
|EventClass|**int**|事件類型 = 164。|27|否|  
|EventSequence|**int**|要求中的給定事件順序。|51|否|  
|EventSubClass|**int**|事件子類別的類型。<br /><br /> 0=開始<br /><br /> 1=認可<br /><br /> 2=回復|21|是|  
|GroupID|**int**|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|HostName|**nvarchar**|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IndexID|**int**|事件所影響之物件的索引識別碼。 若要判斷物件的索引識別碼，請使用 sys.indexes 目錄檢視的 index_id 資料行。|24|是|  
|IntegerData|**int**|與 Begin 事件對應的事件序號。 只有 Commit 或 Rollback 類型的事件 子類別有此資料行。|25|是|  
|IsSystem|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，NULL = 使用者。|60|是|  
|LoginName|**nvarchar**|使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|LoginSid|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|NTDomainName|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|**nvarchar**|Windows 使用者名稱。|6|是|  
|ObjectID|**int**|系統指派給物件的識別碼。|22|是|  
|ObjectID2|**bigint**|資料分割函數識別碼 (資料分割結構描述改變時)、佇列識別碼 (服務改變時)，或集合結構描述識別碼 (Schema ID) (XML 結構描述改變時)。|56|是|  
|ObjectName|**nvarchar**|正在參考之物件的名稱。|34|是|  
|ObjectType|**int**|代表參與事件之物件類型的值。 這個值會對應到 sy.sobjects 目錄檢視中的類型資料行。 如需各值，請參閱 [ObjectType 追蹤事件資料行](../../relational-databases/event-classes/objecttype-trace-event-column.md)。|28|是|  
|RequestID|**int**|陳述式所在批次要求的識別碼。|49|是|  
|ServerName|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|SessionLoginName|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|StartTime|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|TransactionID|**bigint**|由系統指派給交易的識別碼。|4|是|  
|XactSequence|**bigint**|描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
