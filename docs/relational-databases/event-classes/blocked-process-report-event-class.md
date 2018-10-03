---
title: Blocked Process Report 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Blocked Process Report event class
ms.assetid: e8acb408-938d-4b36-81dd-04f087410cc5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 790cbbd195e96304a150b06627a10113dfb5aba9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47688649"
---
# <a name="blocked-process-report-event-class"></a>Blocked Process Report 事件類別
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **Blocked Process Report** 事件類別指出封鎖工作的時間已超過指定的時間量。 這個事件類別不包含系統工作，或在無法偵測死結的資源上等候的工作。  
  
 若要設定產生報告的臨界值和頻率，請使用 **sp_configure** 命令來設定 [已封鎖的處理序臨界值] 選項。 預設不會針對已封鎖的處理序產生任何報告。 如需設定 [已封鎖的處理序臨界值] 選項的詳細資訊，請參閱[已封鎖的處理序臨界值伺服器組態選項](../../database-engine/configure-windows/blocked-process-threshold-server-configuration-option.md)。  
  
 如需篩選 **Blocked Process Report** 事件類別所傳回資料的詳細資訊，請參閱[篩選追蹤中的事件 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)、[設定追蹤篩選 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md) 或 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)。  
  
## <a name="blocked-process-report-event-class-data-columns"></a>Blocked Process Report 事件類別資料行  
  
|資料行名稱|資料類型|Description|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|取得鎖定之資料庫的識別碼。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**有效期間**|**bigint**|封鎖處理序的時間量 (以毫秒為單位)。|13|是|  
|**EndTime**|**datetime**|事件結束的時間。 啟動事件類別 (如 **SQL:BatchStarting** 或 **SP:Starting**) 不會擴展這個資料行。|15|是|  
|**EventClass**|**int**|事件類型 = 137。|27|否|  
|**EventSequence**|**int**|要求中之給定事件的順序。|51|否|  
|**IndexID**|**int**|事件所影響之物件的索引識別碼。 若要確定物件的索引識別碼，請使用 **sysindexes** 系統資料表的 **indid** 資料行。|24|是|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|**LoginSid**|**image**|已登入之使用者的安全性識別碼 (SID)。 此事件一律由系統執行緒報告。 IsSystem = 1；SID = sa。|41|是|  
|**模式**|**int**|事件已接收或正在要求的狀態。<br /><br /> 0=NULL<br /><br /> 1=Sch-S<br /><br /> 2=Sch-M<br /><br /> 3=S<br /><br /> 4=U<br /><br /> 5=X<br /><br /> 6=IS<br /><br /> 7=IU<br /><br /> 8=IX<br /><br /> 9=SIU<br /><br /> 10=SIX<br /><br /> 11=UIX<br /><br /> 12=BU<br /><br /> 13=RangeS-S<br /><br /> 14=RangeS-U<br /><br /> 15=RangeI-N<br /><br /> 16=RangeI-S<br /><br /> 17=RangeI-U<br /><br /> 18=RangeI-X<br /><br /> 19=RangeX-S<br /><br /> 20=RangeX-U<br /><br /> 21=RangeX-X|32|是|  
|**Exchange Spill**|**int**|取得鎖定所在之物件的系統指派識別碼，如果可用且適用的話。|22|是|  
|**ServerName**|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26||  
|**SessionLoginName**|**nvarchar**|最先建立工作階段的使用者的登入名稱。 例如，如果您使用 Login1 連接到 SQL Server，並以 Login2 執行陳述式，則 **SessionLoginName** 會顯示 Login1；而 **LoginName** 會顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|**TextData**|**ntext**|與追蹤中所擷取的事件類別有關的文字值。|1|是|  
|**TransactionID**|**bigint**|由系統指派給交易的識別碼。|4|是|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
