---
title: QN:Dynamics 事件類別 | Microsoft Docs
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
- event classes [SQL Server], QN:Dynamics
ms.assetid: 3c1ffa0c-c9e5-40a6-a26b-28339f60ebc3
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d32bc6928ecb62c9047e0ff4f6dbcf795ca43c46
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="qndynamics-event-class"></a>QN:Dynamics 事件類別
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  QN:Dynamics 事件類別會報告 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 為了支援查詢通知所執行之背景活動的相關資訊 在 [!INCLUDE[ssDE](../../includes/ssde-md.md)]內，背景執行緒會監視訂閱逾時、暫止要引發的訂閱以及參數資料表解構。  
  
## <a name="qndynamics-event-class-data-columns"></a>QN:Dynamics 事件類別資料行  
  
|資料行|類型|描述|資料行編號|可篩選|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|ClientProcessID|**int**|主機電腦指派給用戶端應用程式執行中處理序的識別碼。 如果用戶端提供處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database*陳述式，則是預設資料庫的識別碼。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 就會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|**nvarchar**|正在其中執行使用者陳述式的資料庫名稱。|35|是|  
|EventClass|**int**|事件類型 = 202|27|否|  
|EventSequence|**int**|此事件的序號。|51|否|  
|EventSubClass|**nvarchar**|事件子類別的類型，針對每個事件類別提供更詳細的相關資訊。 這個資料行可包含下列值：<br /><br /> **Clock run started**：表示 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中排程要清除過期參數資料表的背景執行緒已啟動。<br /><br /> **Clock run finished**：表示 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中排程要清除過期參數資料表的背景執行緒已完成。<br /><br /> **Master cleanup task started**：表示移除過期查詢通知訂閱資料的清除作業 (記憶體回收) 已啟動。<br /><br /> **Master cleanup task finished**：表示移除過期查詢通知訂閱資料的清除作業 (記憶體回收) 已完成。<br /><br /> **Master cleanup task skipped**：表示 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 並未執行清除作業 (記憶體回收) 來移除過期查詢通知訂閱資料。|21|是|  
|GroupID|**int**|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|HostName|**nvarchar**|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IsSystem|**int**|指出事件是發生在系統處理序或使用者處理序。<br /><br /> 0 = 使用者<br /><br /> 1 = 系統|60|否|  
|LoginName|**nvarchar**|使用者的登入名稱 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或「網域\使用者名稱」格式的 Windows 登入認證)。|11|否|  
|LoginSID|**image**|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|NTDomainName|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|**nvarchar**|擁有產生此事件之連接的使用者名稱。|6|是|  
|RequestID|**int**|包含陳述式之要求的識別碼。|49|是|  
|ServerName|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|SessionLoginName|**nvarchar**|引發工作階段之使用者的登入名稱。 例如，如果應用程式使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 會顯示 "Login1"，而 LoginName 則會顯示 "Login2"。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|**int**|事件發生所在之工作階段的識別碼。|12|是|  
|StartTime|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|**ntext**|傳回包含這個事件相關資訊的 XML 文件。 這份文件符合 [SQL Server 查詢通知 Profiler 事件結構描述](http://go.microsoft.com/fwlink/?LinkId=63331) 網頁上所提供的 XML 結構描述。|@shouldalert|是|  
  
  
