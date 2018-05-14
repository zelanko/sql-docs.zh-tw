---
title: 進度報表：Online Index Operation 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: event-classes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 'Progress Report: Online Index Operation event class [SQL Server]'
ms.assetid: 491616c1-f666-4b16-a5ea-1192bf156692
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8f9d7aec25ce6ac24cf47d0c34f856e586fdce28
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="progress-report-online-index-operation-event-class"></a>進度報表：線上索引作業事件類別
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Progress Report: Online Index Operation 事件類別指出在執行建立程序時，線上索引建立作業的進度。  
  
## <a name="progress-report-online-index-operation-event-class-data-columns"></a>Progress Report: Online Index Operation 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|BigintData1|**bigint**|插入的資料列數目。|52|是|  
|BigintData2|**bigint**|0 = 序列計畫，否則為平行執行期間的執行緒識別碼。|53|是|  
|ClientProcessID|**int**|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 如果在追蹤中擷取 ServerName 資料行，則會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|**nvarchar**|正在執行使用者陳述式的資料庫名稱。|35|是|  
|Duration|**bigint**|事件所花費的時間量 (以百萬分之一秒為單位)。|13|是|  
|EndTime|**datetime**|線上索引作業完成的時間。|15|是|  
|EventClass|**int**|事件類別 = 190。|27|否|  
|EventSequence|**int**|要求中的給定事件順序。|51|否|  
|EventSubClass|**int**|事件子類別的類型。<br /><br /> 1=開始<br /><br /> 2=階段 1 執行開始<br /><br /> 3=階段 1 執行結束<br /><br /> 4=階段 2 執行開始<br /><br /> 5=階段 2 執行結束<br /><br /> 6=插入的資料列計數<br /><br /> 7=完成<br /><br /> 階段 1 指的是基底物件 (叢集索引或堆積)，或者索引作業是否只包含一個非叢集索引。 當索引建立作業牽涉到原始重建加上額外的非叢集索引時，便會使用階段 2。  例如，若物件擁有一個叢集索引和數個非叢集索引，'rebuild all' 會重建所有索引。 基底物件 (叢集索引) 會在階段 1 重建，然後所有非叢集索引會在階段 2 重建。|21|是|  
|GroupID|**int**|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|HostName|**nvarchar**|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IndexID|**int**|事件所影響之物件的索引識別碼。|24|是|  
|IsSystem|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|LoginName|**nvarchar**|使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|LoginSid|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|NTDomainName|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|**nvarchar**|Windows 使用者名稱。|6|是|  
|ObjectID|**int**|系統指派給物件的識別碼。|22|是|  
|ObjectName|**nvarchar**|正在參考之物件的名稱。|34|是|  
|PartitionId|**bigint**|正在建立之分割區區的識別碼。|65|是|  
|PartitionNumber|**int**|正在建立之分割區區的一般號碼。|25|是|  
|ServerName|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|SessionLoginName|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|StartTime|**datetime**|事件開始的時間。|14|是|  
|TransactionID|**bigint**|由系統指派給交易的識別碼。|4|是|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
