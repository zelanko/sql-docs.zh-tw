---
title: Broker:Message Classify 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: event-classes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Broker:Message Classify event class
ms.assetid: e51f3351-1239-4c41-b87c-1dd86968e027
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5da895fcfba7a0e5ad8179ddfce4b41df70c91ba
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="brokermessage-classify-event-class"></a>Broker:Message Classify 事件類別
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當 Service Broker 為訊息決定路由時，產生 **Broker:Message Classify** 事件。  
  
## <a name="brokermessage-classify-event-class-data-columns"></a>Broker:Message Classify 事件類別資料行  
  
|資料行|資料類型|描述|資料行編號|可篩選|  
|-----------------|---------------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|**ClientProcessID**|**int**|主機電腦指派給用戶端應用程式執行中處理序的識別碼。 如果用戶端提供處理序識別碼，這個資料行就會擴展。|9|是|  
|**DatabaseID**|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設資料庫的識別碼。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**EventClass**|**int**|擷取的事件類別類型。 **Broker:Message Classify** 永遠都是 **141**。|27|否|  
|**EventSequence**|**int**|此事件的序號。|51|否|  
|**EventSubClass**|**nvarchar**|事件子類別的類型，針對每個事件類別提供更詳細的相關資訊。 此資料行可包含下列值。<br /><br /> **本機**：選擇的路由已處理 LOCAL。<br /><br /> **遠端**：選擇的路由有 LOCAL 以外的位址。<br /><br /> **延遲**：訊息已延遲，原因是因為停用轉寄或沒有符合的路由存在。|21|是|  
|**FileName**|**nvarchar**|訊息已導向至服務名稱。|36|否|  
|**GUID**|**uniqueidentifier**|對話的交談識別碼。 此識別碼是以訊息的一部份傳送，並在交談的兩端之間共用。|54|否|  
|**HostName**|**nvarchar**|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。 1 = 系統，0 = 使用者。|60|否|  
|**LoginSid**|**image**|已登入之使用者的安全性識別碼 (SID)。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|**NTDomainName**|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|**NTUserName**|**nvarchar**|擁有產生此事件之連接的使用者名稱。|6|是|  
|**OwnerName**|**nvarchar**|將訊息導向的 Broker 識別碼。|37|否|  
|**RoleName**|**nvarchar**|指出是否可從網路接收訊息，或起源於此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。|38|否|  
|**ServerName**|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|**SPID**|**int**|由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指派給用戶端關聯之處理序的伺服器處理序識別碼。|12|是|  
|**Start Time**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|**TargetUserName**|**nvarchar**|下一個躍點 Broker 的網址。|39|否|  
|**TransactionID**|**bigint**|系統指派的交易識別碼。|4|否|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
