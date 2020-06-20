---
title: CursorImplicitConversion 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- CursorImplicitConversion event class
ms.assetid: 44d12e23-146a-42e6-bb38-1f2f6a035bad
author: stevestein
ms.author: sstein
ms.openlocfilehash: 410ce293d126190971f3c463d5611761033f6c3c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85030180"
---
# <a name="cursorimplicitconversion-event-class"></a>CursorImplicitConversion 事件類別
  **CursorImplicitConversion** 事件類別描述應用程式開發介面 (API) 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料指標中所發生的資料指標隱含轉換事件。 當 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行的 Transact-SQL 陳述式不被所要求的伺服器資料指標類型支援時，就會發生資料指標隱含轉換事件。 此時 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會傳回一個錯誤訊息，指出資料指標類型已經變更。  
  
 可將 **CursorImplicitConversion** 事件類別包含在會記錄資料指標效能的追蹤當中。  
  
 當追蹤包含此事件類別時，所造成的負擔量是依據追蹤期間，對資料庫使用資料指標 (而且此類資料指標需要進行隱含轉換) 的頻率而定。 如果大量使用資料指標，追蹤可能會明顯地妨礙效能。  
  
## <a name="cursorimplicitconversion-event-class-data-columns"></a>CursorImplicitConversion 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|**BinaryData**|**image**|結果的資料指標類型。 值為：<br /><br /> 1 = 索引鍵集<br /><br /> 2 = 動態<br /><br /> 4 = 順向<br /><br /> 8 = 靜態<br /><br /> 16 = 向前快轉|2|是|  
|**ClientProcessID**|**int**|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|**DatabaseID**|**int**|由 *database* 陳述式所指定的資料庫識別碼；如果沒有針對指定執行個體發出 USE *database*陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**DatabaseName**|**nvarchar**|正在執行使用者陳述式的資料庫名稱。|35|是|  
|**EventClass**|**int**|記錄的事件類型 = 76。|27|否|  
|**EventSequence**|**int**|批次中之 **CursorClose** 事件類別的順序。|51|否|  
|**GroupID**|**int**|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|**Handle**|**int**|事件所參考之物件的控制代碼。|33|是|  
|**HostName**|**nvarchar**|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|**IntegerData**|**int**|要求的資料指標類型。 值為：<br /><br /> 1 = 索引鍵集<br /><br /> 2 = 動態<br /><br /> 4 = 順向<br /><br /> 8 = 靜態<br /><br /> 16 = 向前快轉|25|否|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|**LoginName**|**nvarchar**|使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|**LoginSid**|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 **sys.server_principals** 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|**NTDomainName**|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|**NTUserName**|**nvarchar**|Windows 使用者名稱。|6|是|  
|**RequestID**|**int**|隱含轉換的要求識別碼。|49|是|  
|**ServerName**|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|**SessionLoginName**|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 執行陳述式，則 **SessionLoginName** 將顯示 Login1 而 **LoginName** 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|**SPID**|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|**TransactionID**|**bigint**|由系統指派給交易的識別碼。|4|是|  
|**XactSequence**|**bigint**|描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
