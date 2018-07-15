---
title: QN:Subscription 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- event classes [SQL Server], QN:Subscription
ms.assetid: 4916167e-8541-43b4-900e-ec8e6adcbc34
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 79e75ea52d0e1ed2d80dd4e2ef9dcc2d2092e6c3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37188475"
---
# <a name="qnsubscription-event-class"></a>QN:Subscription 事件類別
  QN:Subscription 事件會報告通知訂閱的資訊。  
  
## <a name="qnsubscription-event-class-data-columns"></a>QN:Subscription 事件類別資料行  
  
|資料行|類型|描述|資料行編號|可篩選|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|`nvarchar`|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|ClientProcessID|`int`|主機電腦指派給用戶端應用程式執行中處理序的識別碼。 如果用戶端提供處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|`int`|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database*陳述式，則是預設資料庫的識別碼。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 就會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|`nvarchar`|正在其中執行使用者陳述式的資料庫名稱。|35|是|  
|EventClass|`int`|事件類別 = 199。|27|否|  
|EventSequence|`int`|此事件的序號。|51|否|  
|EventSubClass|`nvarchar`|事件子類別的類型，針對每個事件類別提供更詳細的相關資訊。 這個資料行可包含下列值：<br /><br /> 註冊訂用帳戶： 表示資料庫中已成功註冊查詢通知訂閱。<br /><br /> 倒轉的訂用帳戶： 指示何時[!INCLUDE[ssDE](../../includes/ssde-md.md)]收到完全符合現有的訂用帳戶的訂用帳戶要求。 在此情況下， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會將現有訂閱的逾時值設成新訂閱要求中所指定的逾時。<br /><br /> 引發的訂用帳戶： 表示通知訂閱產生通知訊息。<br /><br /> 引發失敗，訊息代理程式錯誤： 這個值表示通知訊息時失敗原因為[!INCLUDE[ssSB](../../includes/sssb-md.md)]時發生錯誤。<br /><br /> 引發失敗不會發生 broker 錯誤： 表示通知訊息失敗，但不是因為[!INCLUDE[ssSB](../../includes/sssb-md.md)]時發生錯誤。<br /><br /> Broker 攔截的錯誤： 指出[!INCLUDE[ssSB](../../includes/sssb-md.md)]查詢通知使用的交談中傳遞錯誤。<br /><br /> 訂用帳戶刪除嘗試： 指出[!INCLUDE[ssDE](../../includes/ssde-md.md)]嘗試刪除過期的訂閱，以便釋出資源。<br /><br /> 訂用帳戶刪除失敗： 表示嘗試刪除過期的訂用帳戶已失敗。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 將自動重新排程訂閱的刪除作業，以便釋出資源。<br /><br /> 終結的訂用帳戶： 指出[!INCLUDE[ssDE](../../includes/ssde-md.md)]已成功刪除過期的訂用帳戶|21|是|  
|GroupID|`int`|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|HostName|`nvarchar`|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IsSystem|`int`|指出事件是發生在系統處理序或使用者處理序。<br /><br /> 0 = 使用者<br /><br /> 1 = 系統|60|否|  
|LoginName|`nvarchar`|使用者的登入名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\Username 格式的 Windows 登入認證)。|11|否|  
|LoginSID|`image`|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|NTDomainName|`nvarchar`|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|`nvarchar`|擁有產生此事件之連接的使用者名稱。|6|是|  
|RequestID|`int`|包含陳述式之要求的識別碼。|49|是|  
|ssSqlProfiler|`nvarchar`|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|SessionLoginName|`nvarchar`|引發工作階段之使用者的登入名稱。 例如，如果應用程式使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 會顯示 "Login1"，而 LoginName 則會顯示 "Login2"。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|`int`|事件發生所在之工作階段的識別碼。|12|是|  
|StartTime|`datetime`|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|`ntext`|傳回包含這個事件相關資訊的 XML 文件。 這份文件符合 [SQL Server 查詢通知 Profiler 事件結構描述](http://go.microsoft.com/fwlink/?LinkId=63331) 網頁上所提供的 XML 結構描述。|1|是|  
  
  
