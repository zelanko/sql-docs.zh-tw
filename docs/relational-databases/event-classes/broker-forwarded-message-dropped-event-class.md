---
title: Broker:Forwarded Message Dropped 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Broker:Forwarded Message Dropped event class
ms.assetid: ec242d0b-77b0-45f5-8b12-186a14b173a8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c2fb2e65589e8cec209eb1d7336ec83da3b14737
ms.sourcegitcommit: 02df4e7965b2a858030bb508eaf8daa9bc10b00b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/28/2019
ms.locfileid: "66265520"
---
# <a name="brokerforwarded-message-dropped-event-class"></a>Broker:Forwarded Message Dropped 事件類別

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當 Service Broker 卸除計畫轉寄的訊息時，會產生 Broker:Forwarded Message Dropped 事件。  
  
## <a name="brokerforwarded-message-dropped-event-class-data-columns"></a>Broker:Forwarded Message Dropped 事件類別資料行  
  
|資料行|類型|Description|資料行編號|可篩選|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|BigintData1|**bigint**|訊息序號。|52|否|  
|ClientProcessID|**int**|主機電腦指派給用戶端應用程式執行中處理序的識別碼。 如果用戶端提供處理序識別碼，這個資料行就會擴展。|9|是|  
|DatabaseID|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database*陳述式，則是預設資料庫的識別碼。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 就會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|DatabaseName|**nvarchar**|正在其中執行使用者陳述式的資料庫名稱。|35|是|  
|DBUserName|**nvarchar**|此訊息的來源 Broker 執行個體識別碼。|40|否|  
|錯誤|**int**|sys.messages 中的訊息識別碼，代表事件內的文字。|31|否|  
|EventClass|**int**|擷取的事件類別類型。 Broker:Forwarded Message Dropped 永遠都是 191。|27|否|  
|EventSequence|**int**|此事件的序號。|51|否|  
|FileName|**nvarchar**|送出訊息的服務名稱。|36|否|  
|GUID|**uniqueidentifier**|對話的交談識別碼。 此識別碼是以訊息的一部份傳送，並在交談的兩端之間共用。|54|否|  
|HostName|**nvarchar**|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|IndexID|**int**|轉寄訊息的躍點剩餘數目。|24|否|  
|IntegerData|**int**|轉寄訊息的片段號碼。|25|否|  
|LoginSid|**image**|已登入之使用者的安全性識別碼 (SID)。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|NTDomainName|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|NTUserName|**nvarchar**|擁有產生此事件之連接的使用者名稱。|6|是|  
|ObjectId|**int**|轉寄訊息的存留時間值。|22|否|  
|ObjectName|**nvarchar**|轉寄訊息的訊息識別碼。|34|否|  
|OwnerName|**nvarchar**|訊息目的地之 Broker 執行個體識別碼。|37|否|  
|RoleName|**nvarchar**|交談控制代碼的角色。 它是下列項目之一：<br /><br /> -Initiator. 此 Broker 起始了交談。<br /><br /> -Target. 此 Broker 是交談的目標。|38|否|  
|ServerName|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|Severity|**int**|事件中文字的嚴重性編號。|29|否|  
|SPID|**int**|由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指派給用戶端關聯之處理序的伺服器處理序識別碼。|12|是|  
|StartTime|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|State|**int**|指出產生事件的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原始程式碼內的位置。 每個可能產生此事件的位置都有不同的狀態碼。 Microsoft 支援工程師可以使用此狀態碼來尋找產生事件的位置。|30|否|  
|成功|**int**|訊息已經存留的時間量。 當此值大於或等於存留時間時，就會卸除訊息。|23|否|  
|TargetLoginName|**nvarchar**|將轉寄訊息的目的網路位址。|42|否|  
|TargetUserName|**nvarchar**|訊息的起始端服務名稱。|39|否|  
|TextData|**ntext**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 卸除訊息的原因描述。|1|是|  
|Transaction ID|**bigint**|系統指派的交易識別碼。|4|否|  
  
 此事件的 TextData 資料行包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 卸除訊息的原因描述。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
