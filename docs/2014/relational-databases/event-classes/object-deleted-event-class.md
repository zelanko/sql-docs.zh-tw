---
title: Object:Deleted 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
topic_type:
- apiref
helpviewer_keywords:
- Object:Deleted event class
ms.assetid: d4db32bc-972d-4429-809a-a62047c33e79
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c3878a6432a35e0749b37da1e7a6e4b330f12eea
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037489"
---
# <a name="objectdeleted-event-class"></a>Object:Deleted 事件類別
  Object:Deleted 事件類別指出物件已刪除，例如，被 DROP INDEX 和 DROP TABLE 陳述式所刪除。 此事件類別可以用來判斷物件是否已遭刪除，例如，由通常建立暫存預存程序的 ODBC 應用程式刪除。  
  
 除了監視 Objects 事件類別，您還可以監視 LoginName 和 NTUserName 預設資料行，以判斷建立、刪除或存取物件的使用者名稱。  
  
## <a name="objectdeleted-event-class-data-columns"></a>Object:Deleted 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|ClientProcessID|`int`|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|`int`|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 如果在追蹤中擷取 ServerName 資料行，則會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|`nvarchar`|正在執行使用者陳述式的資料庫名稱。|35|是|  
|EventClass|`int`|事件類型 = 47。|27|否|  
|EventSequence|`int`|要求中的給定事件順序。|51|否|  
|EventSubClass|`int`|事件子類別的類型。<br /><br /> 0=開始<br /><br /> 1=認可<br /><br /> 2=回復|21|是|  
|GroupID|`int`|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|HostName|`nvarchar`|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IndexID|`int`|事件所影響之物件的索引識別碼。 若要判斷物件的索引識別碼，請使用 sys.indexes 目錄檢視的 index_id 資料行。|24|是|  
|IntegerData|`int`|這是一個整數值，會隨著追蹤所擷取的事件類別而不同。|25|是|  
|IsSystem|`int`|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|LoginName|`nvarchar`|使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|LoginSid|`image`|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|NTDomainName|`nvarchar`|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|`nvarchar`|Windows 使用者名稱。|6|是|  
|ObjectID|`int`|系統指派給物件的識別碼。|22|是|  
|ObjectID2|`bigint`|相關物件或實體的識別碼。|56|是|  
|ObjectName|`nvarchar`|正在參考之物件的名稱。|34|是|  
|ObjectType|`int`|代表參與事件之物件類型的值。 此值對應至 sys.objects 中的類型資料行。 如需各值，請參閱 [ObjectType 追蹤事件資料行](objecttype-trace-event-column.md)。|28|是|  
|RequestID|`int`|包含陳述式之要求的識別碼。|49|是|  
|ServerName|`nvarchar`|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|SessionLoginName|`nvarchar`|引發工作階段的使用者登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|`int`|事件發生所在之工作階段的識別碼。|12|是|  
|StartTime|`datetime`|事件啟動的時間 (如果有的話)。|14|是|  
|TransactionID|`bigint`|由系統指派給交易的識別碼。|4|是|  
|XactSequence|`bigint`|用來描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
