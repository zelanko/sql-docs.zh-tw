---
title: Background Job Error 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Background Job Error event class
ms.assetid: 9e6d2a0e-919d-4fe2-a306-b20b8d41c197
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5689c86e530fd7bf7f78cb58f3e1e53f9b731bc3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62686824"
---
# <a name="background-job-error-event-class"></a>Background Job Error 事件類別
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  當背景作業異常中止時，就會發生 **Background Job Error** 事件類別。 這種狀況可能需要系統管理員注意。  
  
## <a name="background-job-error-event-class-data-columns"></a>Background Job Error 事件類別資料行  
  
|資料行名稱|資料類型|Description|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|作業所指定的資料庫識別碼。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**DatabaseName**|**nvarchar**|正在執行使用者陳述式的資料庫名稱。|35|是|  
|**錯誤**|**int**|上次嘗試的錯誤號碼 (只限**EventSubClass** 1)。|31|是|  
|**EventClass**|**int**|事件類型 = 193。|27|否|  
|**EventSequence**|**int**|要求中之給定事件的順序。|51|否|  
|**EventSubClass**|**int**|事件子類別的類型。<br /><br /> 1 = 失敗後放棄背景作業。<br /><br /> 2 = 卸除背景作業 - 佇列已滿。<br /><br /> 3 = 背景作業傳回錯誤。|21|是|  
|**IndexID**|**int**|事件所影響之物件的索引識別碼。 若要確定物件的索引識別碼，請使用 **sysindexes** 系統資料表的 **indid** 資料行。|24|是|  
|**IntegerData**|**int**|作業所嘗試的次數 (只限**EventSubClass** 1)。|25|是|  
|**IntegerData2**|**int**|作業序號。|55|是|  
|**Exchange Spill**|**int**|系統指派給物件的識別碼。|22|是|  
|**SessionLoginName**|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 執行陳述式，則 **SessionLoginName** 將顯示 Login1 而 **LoginName** 則顯示 Login2。 這個資料行會同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入。|64|是|  
|**Severity**|**int**|上次嘗試時所發生錯誤的嚴重性層級 (只限**EventSubClass** 1)。|20|是|  
|**StartTime**|**datetime**|建立作業的時間。|14|是|  
|**State**|**int**|上次嘗試時的錯誤狀態 (只限**EventSubClass** 1)。|30|是|  
|**TextData**|**ntext**|事件子類別值的文字描述。|1|是|  
|**型別**|**int**|作業類型。|57|是|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Auto Stats 事件類別](../../relational-databases/event-classes/auto-stats-event-class.md)  
  
  
