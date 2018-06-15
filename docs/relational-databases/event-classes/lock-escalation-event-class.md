---
title: Lock:Escalation 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Escalation event class
- lock escalation [SQL Server], event class
ms.assetid: d253b44c-7600-4afa-a3a7-03cc937c6a4b
caps.latest.revision: 47
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b3a98c74f69ea96f37812c441ef391a8c6670bbf
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
ms.locfileid: "34330929"
---
# <a name="lockescalation-event-class"></a>Lock:Escalation 事件類別
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **Lock:Escalation** 事件類別指出細粒鎖定已經轉換成粗粒鎖定；例如，轉換成物件鎖定的資料列鎖定。 擴大事件類別是事件識別碼 60。  
  
## <a name="lockescalation-event-class-data-columns"></a>Lock:Escalation 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|**ClientProcessID**|**int**|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|**DatabaseID**|**int**|取得鎖定之資料庫的識別碼。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**DatabaseName**|**nvarchar**|發生擴大的資料庫名稱。|35|是|  
|**EventClass**|**int**|事件類型 = 60。|27|否|  
|**EventSubClass**|**int**|鎖定擴大的原因：<br /><br /> **0 - LOCK_THRESHOLD** 指出陳述式超過鎖定臨界值。<br /><br /> **1 - MEMORY_THRESHOLD** 指出陳述式超過記憶體臨界值。|21|是|  
|**EventSequence**|**int**|要求中的給定事件順序。|51|否|  
|**GroupID**|**int**|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|**HostName**|**nvarchar**|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|**IntegerData**|**int**|HoBT 鎖定計數。 鎖定擴大時，HoBT 的鎖定數目。|25|是|  
|**IntegerData2**|**int**|擴大的鎖定計數。 已轉換的鎖定總數。 這些鎖定結構會被取消配置，因為它們已經由擴大的鎖定涵蓋了。|55|是|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|**LineNumber**|**int**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的行號。|5|是|  
|**LoginName**|**nvarchar**|使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|**LoginSid**|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 **sys.server_principals** 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|**模式**|**int**|擴大之後產生的鎖定模式：<br /><br /> 0=NULL - 與其他所有鎖定模式相容 (LCK_M_NL)<br /><br /> 1=結構描述穩定性鎖定 (LCK_M_SCH_S)<br /><br /> 2=結構描述修改鎖定 (LCK_M_SCH_M)<br /><br /> 3=共用鎖定 (LCK_M_S)<br /><br /> 4=更新鎖定 (LCK_M_U)<br /><br /> 5=獨佔鎖定 (LCK_M_X)<br /><br /> 6=意圖共用鎖定 (LCK_M_IS)<br /><br /> 7=意圖更新鎖定 (LCK_M_IU)<br /><br /> 8=意圖獨佔鎖定 (LCK_M_IX)<br /><br /> 9=與意圖更新共用 (LCK_M_SIU)<br /><br /> 10=與意圖獨佔共用 (LCK_M_SIX)<br /><br /> 11=以意圖獨佔更新 (LCK_M_UIX)<br /><br /> 12=大量更新鎖定 (LCK_M_BU)<br /><br /> 13=關鍵範圍共用/共用 (LCK_M_RS_S)<br /><br /> 14=關鍵範圍共用/更新 (LCK_M_RS_U)<br /><br /> 15=關鍵範圍插入 NULL (LCK_M_RI_NL)<br /><br /> 16=關鍵範圍插入共用 (LCK_M_RI_S)<br /><br /> 17=關鍵範圍插入更新 (LCK_M_RI_U)<br /><br /> 18=關鍵範圍插入獨佔 (LCK_M_RI_X)<br /><br /> 19=關鍵範圍獨佔共用 (LCK_M_RX_S)<br /><br /> 20=關鍵範圍獨佔更新 (LCK_M_RX_U)<br /><br /> 21=關鍵範圍獨佔獨佔 (LCK_M_RX_X)|32|是|  
|**NTDomainName**|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|**NTUserName**|**nvarchar**|Windows 使用者名稱。|6|是|  
|**Exchange Spill**|**int**|已觸發鎖定擴大之資料表的系統指派識別碼。|22|是|  
|**ObjectID2**|**bigint**|相關物件或實體的識別碼。 (已觸發鎖定擴大的 HoBT 識別碼)。|56|是|  
|**Offset**|**int**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的起始位移。|61|是|  
|**OwnerID**|**int**|1=TRANSACTION<br /><br /> 2=CURSOR<br /><br /> 3=SESSION<br /><br /> 4=SHARED_TRANSACTION_WORKSPACE<br /><br /> 5=EXCLUSIVE_TRANSACTION_WORKSPACE<br /><br /> 6=WAITFOR_QUERY|58|是|  
|**RequestID**|**int**|包含陳述式之要求的識別碼。|49|是|  
|**ServerName**|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|**SessionLoginName**|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 執行陳述式，則 **SessionLoginName** 將顯示 Login1 而 **LoginName** 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|**SPID**|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|**TextData**|**ntext**|導致鎖定擴大之 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的文字。|@shouldalert|是|  
|**TransactionID**|**bigint**|由系統指派給交易的識別碼。|4|是|  
|**型別**|**int**|鎖定擴大資料粒度：<br /><br /> 1=NULL_RESOURCE<br /><br /> 2=DATABASE<br /><br /> 3=FILE<br /><br /> 5=OBJECT (資料表層級)<br /><br /> 6=PAGE<br /><br /> 7=KEY<br /><br /> 8=EXTENT<br /><br /> 9=RID<br /><br /> 10=APPLICATION<br /><br /> 11=METADATA<br /><br /> 12=HOBT<br /><br /> 13=ALLOCATION_UNIT|57|是|  
  
## <a name="examples"></a>範例  
 下列範例會使用 `sp_trace_create` 程序來建立追蹤、使用 `sp_trace_setevent` 將鎖定擴大資料行加入至追蹤，然後使用 `sp_trace_setstatus` 來啟動追蹤。 在 `EXEC sp_trace_setevent @TraceID, 60, 22, 1`等陳述式中，數字 `60` 表示擴大事件類別、 `22` 表示 **ObjectID** 資料行，而 `1` 會將追蹤事件設定為 ON。  
  
```  
DECLARE @RC int, @TraceID int;  
EXEC @rc = sp_trace_create @TraceID output, 0, N'C:\TraceResults';  
-- Set the events and data columns you need to capture.  
EXEC sp_trace_setevent @TraceID, 60,  1, 1; --  1 = TextData  
EXEC sp_trace_setevent @TraceID, 60, 12, 1; -- 12 = SPID  
EXEC sp_trace_setevent @TraceID, 60, 21, 1; -- 21 = EventSubClass  
EXEC sp_trace_setevent @TraceID, 60, 22, 1; -- 22 = ObjectID  
EXEC sp_trace_setevent @TraceID, 60, 25, 1; -- 25 = IntegerData  
EXEC sp_trace_setevent @TraceID, 60, 55, 1; -- 25 = IntegerData2  
EXEC sp_trace_setevent @TraceID, 60, 57, 1; -- 57 = Type  
-- Set any filter  byusing sp_trace_setfilter.  
-- Start the trace.  
EXEC sp_trace_setstatus @TraceID, 1;  
GO  
```  
  
 既然追蹤正在執行，請執行您想要追蹤的陳述式。 追蹤完成時，請執行下列程式碼來停止追蹤，然後關閉追蹤。 這個範例會使用 `fn_trace_getinfo` 函數來取得用於 `traceid` 陳述式中的 `sp_trace_setstatus` 。  
  
```  
-- After the trace is complete.  
DECLARE @TraceID int;  
-- Find the traceid of the current trace.  
SELECT @TraceID = traceid   
FROM ::fn_trace_getinfo(default)   
WHERE value = N'C:\TraceResults.trc';  
  
-- First stop the trace.   
EXEC sp_trace_setstatus @TraceID, 0;  
  
-- Close and then delete its definition from SQL Server.   
EXEC sp_trace_setstatus @TraceID, 2;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)  
  
  
