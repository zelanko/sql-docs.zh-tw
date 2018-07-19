---
title: SP:CacheRemove 事件類別 | Microsoft Docs
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
- SP:CacheRemove event class
ms.assetid: aaa3c5c4-2d3a-4832-a473-ce9bd4fb1c17
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7c5e1a05ce2007c4c99a1336c997e69bbdf047dc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37158419"
---
# <a name="spcacheremove-event-class"></a>SP:CacheRemove 事件類別
  SP:CacheRemove 事件類別指出已從計畫快取中移除預存程序。  
  
## <a name="spcacheremove-event-class-data-columns"></a>SP:CacheRemove 事件類別資料行  
  
|資料行名稱|`Data type`|描述|資料行識別碼|可篩選|  
|----------------------|-------------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|ClientProcessID|`int`|由主機電腦指派給處理序 (用戶端應用程式執行所在) 的識別碼。 如果用戶端提供用戶端處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|`int`|執行預存程序之資料庫的識別碼。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|`nvarchar`|執行預存程序之資料庫的名稱。|35|是|  
|EventClass|`int`|事件類型 = 36。|27|否|  
|EventSequence|`int`|要求中的給定事件順序。|51|否|  
|EventSubClass|`int`|事件子類別的類型：<br /><br /> 1 = 1=compplan 移除。 已從快取移除編譯的查詢計畫。<br /><br /> 2 = 程序快取排清。 從程序快取中移除所有的項目。|21|是|  
|GroupID|`int`|SQL 追蹤事件引發所在之工作負載群組的識別碼。|66|是|  
|HostName|`nvarchar`|執行用戶端的電腦名稱。 如果用戶端提供主機名稱，這個資料行就會擴展。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IsSystem|`int`|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|是|  
|LoginName|`nvarchar`|使用者登入的名稱 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性登入或 DOMAIN\username 格式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 登入認證)。|11|是|  
|LoginSid|`image`|已登入之使用者的安全性識別碼 (SID)。 您可以在 sys.server_principals 目錄檢視中找到這項資訊。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|NTDomainName|`nvarchar`|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|`nvarchar`|Windows 使用者名稱。|6|是|  
|ObjectID|`int`|系統指派的預存程序識別碼。|22|是|  
|ObjectType|`int`|代表參與事件之物件類型的值。 這個值會對應到 sys.objects 目錄檢視中的類型資料行。 如需各值，請參閱 [ObjectType 追蹤事件資料行](objecttype-trace-event-column.md)。|28|是|  
|RequestID|`int`|包含陳述式之要求的識別碼。|49|是|  
|ServerName|`nvarchar`|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|SessionLoginName|`nvarchar`|引發工作階段之使用者的登入名稱。 例如，如果您使用 Login1 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並以 Login2 身分執行陳述式，則 SessionLoginName 將顯示 Login1 而 LoginName 則顯示 Login2。 此資料行將同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|64|是|  
|SPID|`int`|事件發生所在之工作階段的識別碼。|12|是|  
|StartTime|`datetime`|事件啟動的時間 (如果有的話)。|14|是|  
|TextData|`ntext`|從快取中移除的 SQL 文字。|1|是|  
|TransactionID|`bigint`|由系統指派給交易的識別碼。|4|是|  
|XactSequence|`bigint`|描述目前交易的 Token。|50|是|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../extended-events/extended-events.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
