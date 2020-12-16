---
description: Degree of Parallelism (7.0 Insert) 事件類別
title: Degree of Parallelism (7.0 Insert) 事件類別 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Degree of Parallelism event class
ms.assetid: 6753ef30-890f-47a3-b0b6-8abb184e1d83
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 451bba0eaf89722fdb29265db8880bfc369da1ce
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469759"
---
# <a name="degree-of-parallelism-70-insert-event-class"></a>Degree of Parallelism (7.0 Insert) 事件類別
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  每當 **執行 SELECT、INSERT、UPDATE 或 DELETE 陳述式時，即會發生** Degree of Parallelism (7.0 Insert) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件類別。  
  
 當追蹤包含這個事件類別時，如果這些事件經常發生，產生的負擔可能會大幅降低效能。 為了將產生的負擔降至最低，請將這個事件類別限制使用於短暫監視特定問題的追蹤。  
  
## <a name="degree-of-parallelism-70-insert-event-class-data-columns"></a>Degree of Parallelism (7.0 Insert) 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|**BinaryData**|**image**|用來完成處理序的 CPU 數量，根據的值如下：<br /><br /> 0x00000000，表示依序執行的序列計畫。<br /><br /> 0x01000000，表示依序執行的平行計畫。<br /><br /> >= 0x02000000，表示平行執行的平行計畫。|2|否|  
|**ClientProcessID**|**int**|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供處理序識別碼，這個資料行就會擴展。|9|是|  
|**DatabaseID**|**int**|由 USE database 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE database 陳述式，則是預設的資料庫。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**DatabaseName**|**nvarchar**|正在執行使用者陳述式的資料庫名稱。|35|是|  
|**Event Class**|**int**|事件類型 = 28。|27|否|  
|**EventSequence**|**int**|要求中的給定事件順序。|51|否|  
|**EventSubClass**|**int**|表示執行的陳述式，根據的值如下：<br /><br /> 1=選取<br /><br /> 2=插入<br /><br /> 3=更新<br /><br /> 4=刪除|21|否|  
|**GroupID**|**int**|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|**HostName**|**nvarchar**|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|**Integer Data**|**int**|授與查詢來執行雜湊、排序或建立索引等作業的「工作空間記憶體」數量 (以 KB 為單位)。 執行期間會視需要取得記憶體。|25|是|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|**LoginName**|**nvarchar**|使用者的登入名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\\*username* 格式的 Windows 登入認證)。|11|是|  
|**LoginSid**|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|**NTDomainName**|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|**NTUserName**|**nvarchar**|Windows 使用者名稱。|6|是|  
|**RequestID**|**int**|初始化全文檢索查詢的要求識別。|49|是|  
|**ServerName**|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|**SessionLoginName**|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 執行陳述式，則 **SessionLoginName** 將顯示 Login1 而 **LoginName** 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|**SPID**|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|**TransactionID**|**bigint**|由系統指派給交易的識別碼。|4|是|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)  
  
  
