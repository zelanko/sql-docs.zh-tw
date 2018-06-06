---
title: Database Mirroring State Change 事件類別 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- database mirroring [SQL Server], event notifications
- Database Mirroring State Change event class
ms.assetid: f936a99e-2a81-4768-8177-5c969bbe2e04
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e82a44cce407d627a3767ce417fa3786265d7c78
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="database-mirroring-state-change-event-class"></a>Database Mirroring State Change 事件類別
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **Database Mirroring State Change** 事件類別指出鏡像資料庫狀態的變更。 請在監視鏡像資料庫狀況的追蹤中包含此事件類別。  
  
 當追蹤中包含 **Database Mirroring State Change** 事件類別時，負擔會相對的低。 但如果鏡像資料庫的狀態數目增加，負擔將會提高。  
  
## <a name="data-database-mirroring-state-change-event-class-data-columns"></a>Database Mirroring State Change 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**DatabaseName**|**nvarchar**|鏡像資料庫名稱。|35|是|  
|**EventClass**|**int**|事件類型 = 167。|27|否|  
|**EventSequence**|**int**|批次中的事件類別順序。|51|否|  
|**IntegerData**|**int**|舊的狀態識別碼。|25|是|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|**LoginSid**|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 **sys.server_principals** 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|**RequestID**|**int**|包含陳述式之要求的識別碼。|49|是|  
|**ServerName**|**nvarchar**|正在追蹤之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|**SessionLoginName**|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 執行陳述式，則 **SessionLoginName** 將顯示 Login1 而 **LoginName** 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|**SPID**|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|**State**|**整數**|新鏡像作業的狀態識別碼：<br /><br /> 0 = Null 通知<br /><br /> 1 = 已同步處理主體伺服器，有見證伺服器監督<br /><br /> 2 = 已同步處理主體伺服器，沒有見證伺服器監督<br /><br /> 3 = 已同步處理鏡像伺服器，有見證伺服器監督<br /><br /> 4 = 已同步處理鏡像伺服器，沒有見證伺服器監督<br /><br /> 5 = 主體伺服器連接中斷<br /><br /> 6 = 鏡像伺服器連接中斷<br /><br /> 7 = 手動容錯移轉<br /><br /> 8 = 自動容錯移轉<br /><br /> 9 = 鏡像作業暫停<br /><br /> 10 = 無仲裁伺服器<br /><br /> 11 = 正在同步處理鏡像伺服器<br /><br /> 12 = 執行中的主體伺服器已公開|30|是|  
|**TextData**|**ntext**|狀態變更描述。|@shouldalert|是|  
|**TransactionID**|**bigint**|由系統指派給交易的識別碼。|4|是|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
