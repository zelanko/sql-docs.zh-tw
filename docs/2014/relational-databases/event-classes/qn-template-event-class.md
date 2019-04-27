---
title: QN:Template 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- event classes [SQL Server], QN:Template
ms.assetid: 9f752040-5901-42e1-8fdc-105528d9960a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3ca0ef50d40b1c4d4f481bef4de89b43ff4a275c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62650411"
---
# <a name="qntemplate-event-class"></a>QN:Template 事件類別
  QN:Template 事件會報告查詢範本的內部使用資訊。 查詢範本是 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 用以共用通知查詢定義的機制。 這些範本是與參數資料表一起建立的。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 在建立、使用或終結查詢範本時，會建立此類型的事件。  
  
## <a name="qntemplate-event-class-data-columns"></a>QN:Template 事件類別資料行  
  
|資料行|類型|描述|資料行編號|可篩選|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|`nvarchar`|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|ClientProcessID|`int`|主機電腦指派給用戶端應用程式執行中處理序的識別碼。 如果用戶端提供處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|`int`|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database*陳述式，則是預設資料庫的識別碼。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 就會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|`nvarchar`|正在其中執行使用者陳述式的資料庫名稱。|35|是|  
|EventClass|`int`|事件類型 = 201。|27|否|  
|EventSequence|`int`|此事件的序號。|51|否|  
|EventSubClass|`nvarchar`|事件子類別的類型，針對每個事件類別提供更詳細的相關資訊。 這個資料行可包含下列值：<br /><br /> 建立的範本：表示查詢通知範本已經建立的資料庫中。<br /><br /> 比對的範本：指出當查詢通知範本中重複使用。<br /><br /> 卸除的範本：表示從資料庫移除查詢通知範本時。|21|是|  
|GroupID|`int`|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|HostName|`nvarchar`|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IsSystem|`int`|指出事件是發生在系統處理序或使用者處理序。<br /><br /> 0 = 使用者<br /><br /> 1 = 系統|60|否|  
|LoginName|`nvarchar`|使用者的登入名稱 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或「網域\使用者名稱」格式的 Windows 登入認證)。|11|否|  
|LoginSID|`image`|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|NTDomainName|`nvarchar`|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|`nvarchar`|擁有產生此事件之連接的使用者名稱。|6|是|  
|RequestID|`int`|包含陳述式之要求的識別碼。|49|是|  
|ssSqlProfiler|`nvarchar`|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|SessionLoginName|`nvarchar`|引發工作階段之使用者的登入名稱。 例如，如果應用程式使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 會顯示 "Login1"，而 LoginName 則會顯示 "Login2"。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|`int`|事件發生所在之工作階段的識別碼。|12|是|  
|StartTime|`datetime`|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|`ntext`|傳回包含這個事件相關資訊的 XML 文件。 這份文件符合 [SQL Server Query Notification Profiler Event Schema](https://go.microsoft.com/fwlink/?LinkId=63331) (SQL Server 查詢通知 Profiler 事件結構描述) 頁面上所提供的 XML 結構描述。|1|是|  
  
  
