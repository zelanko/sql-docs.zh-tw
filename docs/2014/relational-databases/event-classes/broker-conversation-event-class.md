---
title: Broker:Conversation 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Conversation event class
ms.assetid: 784707b5-cc67-46a3-8ae6-8f8ecf4b27c0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2d6f29eba93e7841d2d64db57266d8f2ad859377
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62664364"
---
# <a name="brokerconversation-event-class"></a>Broker:Conversation 事件類別
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生 **Broker:Conversation** 事件以報告 Service Broker 交談的進度。  
  
## <a name="brokerconversation-event-class-data-columns"></a>Broker:Conversation 事件類別資料行  
  
|資料行|類型|描述|資料行編號|可篩選|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|`nvarchar`|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|**ClientProcessID**|`int`|主機電腦指派給用戶端應用程式執行中處理序的識別碼。 如果用戶端提供處理序識別碼，這個資料行就會擴展。|9|是|  
|**DatabaseID**|`int`|USE *database* 陳述式指定之資料庫的識別碼。 如果未發出 USE *database*陳述式，則為預設資料庫的識別碼。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 **DB_ID** 函數判斷資料庫的值。|3|是|  
|**EventClass**|`int`|擷取的事件類別類型。 **Broker:Conversation** 永遠為 **124**。|27|否|  
|**EventSequence**|`int`|此事件的序號。|51|否|  
|**EventSubClass**|`nvarchar`|事件子類別的類型。 這會提供有關每一個事件類別的詳細資訊。|21|是|  
|**GUID**|`uniqueidentifier`|對話的交談識別碼。 此識別碼是以訊息的一部份傳送，並在交談的兩端之間共用。|54|否|  
|**HostName**|`nvarchar`|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。 若要判斷主機名稱，請使用 **HOST_NAME** 函數。|8|是|  
|**IsSystem**|`int`|指出事件是發生在系統處理序或使用者處理序。<br /><br /> 0 = 使用者<br /><br /> 1 = 系統|60|否|  
|**LoginSid**|`image`|已登入之使用者的安全性識別碼 (SID)。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|**MethodName**|`nvarchar`|交談所屬的交談群組。|47|否|  
|**NTDomainName**|`nvarchar`|使用者所隸屬的 Windows 網域。|7|是|  
|**NTUserName**|`nvarchar`|擁有產生此事件之連接的使用者名稱。|6|是|  
|**ObjectName**|`nvarchar`|對話的交談控制代碼。|34|否|  
|**優先權**|`int`|交談的優先權等級。|5|是|  
|**RoleName**|`nvarchar`|交談控制代碼的角色。 為 **initiator** 或 **target**其中一個角色。|38|否|  
|**ServerName**|`nvarchar`|所追蹤的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。|26|否|  
|**Severity**|`int`|如果此事件報告錯誤，即為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤嚴重性。|29|否|  
|**SPID**|`int`|由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指派給用戶端相關之處理序的伺服器處理序識別碼。|12|是|  
|**StartTime**|`datetime`|事件啟動的時間 (如果有的話)。|14|是|  
|**TextData**|`ntext`|交談的目前狀態。 它有下列幾種：<br /><br /> **SO**。 已開始傳出。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已處理此交談的 BEGIN CONVERSATION，但尚未傳送任何訊息。<br /><br /> **SI**。 已起始傳入。 另一個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體啟動了與目前執行個體的新交談，但是目前的執行個體尚未完成第一個訊息的接收動作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果第一個訊息被分割或者 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 收到訊息的順序不正確，就可能會建立處於此狀態的交談。 然而，如果收到交談的第一次傳輸包含完整的第一則訊息，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會建立 CO 狀態的交談。<br /><br /> **CO**。 正在交談。 已建立交談，且交談兩端可以傳送訊息。 一般服務的大部分通訊都發生在這個狀態的交談中。<br /><br /> **DI**。 已中斷傳入。 交談的遠端發出了 END CONVERSATION。 交談會保留在這個狀態中，直到交談的本機端發出 END CONVERSATION 為止。 應用程式仍可接收交談的訊息。 由於交談的遠端已經結束交談，所以應用程式無法在此交談中傳送訊息。 當應用程式發出 END CONVERSATION 時，交談會移到已關閉 (CD) 狀態。<br /><br /> **DO**。 已中斷傳出。 交談的本機端發出了 END CONVERSATION。 交談會保留在這個狀態中，直到交談的遠端收到 END CONVERSATION 為止。 應用程式無法傳送或接收交談的訊息。 當交談的遠端收到 END CONVERSATION 時，交談會移到已關閉 (CD) 狀態。<br /><br /> **ER**。 錯誤。 這個端點發生錯誤。 錯誤、嚴重性和狀態資料行包含有關發生之特定錯誤的資訊。<br /><br /> **CD**。 已關閉。 交談端點已不在使用中。|1|是|  
|**Transaction ID**|`bigint`|系統指派的交易識別碼。|4|否|  
  
 下表列出此事件類別的子類別值。  
  
|ID|子類別|描述|  
|--------|--------------|-----------------|  
|1|SEND Message|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當 **執行 SEND 陳述式時，會產生** SEND Message [!INCLUDE[ssDE](../../includes/ssde-md.md)] 事件。|  
|2|END CONVERSATION|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當 **執行未包括 WITH ERROR 子句的 END CONVERSATION 陳述式時，會產生** END CONVERSATION [!INCLUDE[ssDE](../../includes/ssde-md.md)] 事件。|  
|3|END CONVERSATION WITH ERROR|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當 **執行包括 WITH ERROR 子句的 END CONVERSATION 陳述式時，會產生** END CONVERSATION WITH ERROR [!INCLUDE[ssDE](../../includes/ssde-md.md)] 事件。|  
|4|Broker Initiated Error|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 每當 **建立錯誤訊息時，會產生** Broker Initiated Error [!INCLUDE[ssSB](../../includes/sssb-md.md)] 事件。 例如，當 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 未能成功地路由傳送對話的訊息時，Broker 會針對該對話建立一個錯誤訊息，並產生此事件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果應用程式結束交談時發生錯誤，不會產生此事件。|  
|5|Terminate Dialog|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 會結束此對話。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 對於無法繼續使用對話的情況 (但並不是錯誤或正常結束交談的情況)，會終止對話來加以回應。 例如，卸除服務會導致 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 終止該項服務的所有對話。|  
|6|Received Sequenced Message|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當 **收到包含訊息序號的訊息時，會產生** Received Sequenced Message [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件類別。 所有使用者定義的訊息類型都是循序訊息。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會在兩個情況下產生非循序訊息：<br /><br /> 由 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 產生的錯誤訊息即非循序。<br /><br /> 訊息收條可能為非循序。 為了提高效率， [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會將任何可用的收條當做循序訊息的一部分併入訊息中。 但是，如果應用程式未能在某一段時間內，將循序訊息傳送到遠端端點， [!INCLUDE[ssSB](../../includes/sssb-md.md)] 就會為訊息收條建立非循序訊息。|  
|7|Received END CONVERSATION|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 收到交談另一端的「結束對話」訊息時，會產生 Received END CONVERSATION 事件。|  
|8|Received END CONVERSATION WITH ERROR|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當 **收到來自交談另一端的使用者定義錯誤時，會產生** Received END CONVERSATION WITH ERROR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 收到 Broker 定義的錯誤時，不會產生此事件。|  
|9|Received Broker Error Message|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當 **收到來自交談另一端的 Broker 定義錯誤訊息時，會產生** Received Broker Error Message [!INCLUDE[ssSB](../../includes/sssb-md.md)] 事件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 收到由應用程式產生的錯誤訊息時，不會產生此事件。<br /><br /> 例如，如果目前的資料庫包含轉寄資料庫的預設路由， [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會以未知的服務名稱將訊息路由傳送到轉寄資料庫。 如果那個資料庫無法路由訊息，則資料庫中的 Broker 就會建立錯誤訊息，然後將該錯誤訊息傳回目前的資料庫。 當目前的資料庫從轉寄資料庫收到 Broker 產生的錯誤，目前的資料庫就會產生 **Received Broker Error Message** 事件。|  
|10|Received END CONVERSATION Ack|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當交談另一端認可由交談這一端傳送的「結束對話」或「錯誤」訊息時，會產生 **Received END CONVERSATION Ack** 事件類別。|  
|11|BEGIN DIALOG|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當 Database Engine 執行 BEGIN DIALOG 命令時，會產生 **BEGIN DIALOG** 事件。|  
|12|Dialog Created|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當 **為對話建立端點時，會產生** Dialog Created [!INCLUDE[ssSB](../../includes/sssb-md.md)] 事件。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 每當建立新的對話時，就會建立一個端點，不論目前的資料庫是否為該對話的起始端或目標。|  
|13|END CONVERSATION WITH CLEANUP|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行包括 WITH CLEANUP 子句的 END CONVERSATION 陳述式時，會產生 END CONVERSATION WITH CLEANUP 事件。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
