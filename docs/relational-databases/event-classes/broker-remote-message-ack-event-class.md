---
title: "Broker:Remote Message Ack 事件類別 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Broker:Remote Message Ack event class
ms.assetid: 3d67efe1-74b4-4633-b029-c6e05b19f4dc
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 747d421d4a9e6a86295ce843aa6c2b943bf006cf
ms.lasthandoff: 04/11/2017

---
# <a name="brokerremote-message-ack-event-class"></a>Broker:Remote Message Ack 事件類別
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當 **傳送或接收訊息收條時，會產生** Broker:Remote Message Ack [!INCLUDE[ssSB](../../includes/sssb-md.md)] 事件。  
  
## <a name="brokerremote-message-ack-event-class-data-columns"></a>Broker:Remote Message Ack 事件類別資料行  
  
|資料行|型別|說明|資料行編號|可篩選|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|**BigintData1**|**bigint**|包含收條之訊息的序號。|52|否|  
|**BigintData2**|**bigint**|確認之訊息的序號。|53|否|  
|**ClientProcessID**|**int**|主機電腦指派給用戶端應用程式執行中處理序的識別碼。 如果用戶端提供處理序識別碼，這個資料行就會擴展。|9|是|  
|**DatabaseID**|**int**|USE *database* 陳述式指定之資料庫的識別碼。 如果未針對指定的執行個體發出 USE *database* 陳述式，則為預設資料庫的識別碼。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**EventClass**|**int**|擷取的事件類別類型。 對於 **Broker:Message Ack** 一律是 **149**。|27|否|  
|**EventSequence**|**int**|此事件的序號。|51|否|  
|**EventSubClass**|**nvarchar**|事件子類別的類型，可為每個事件類別提供詳細的資訊。 此資料行可包含下列值：<br /><br /> **Message With Acknowledgement Sent**：<br />                    [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會將收條當做標準循序訊息的一部分傳送。<br /><br /> **Acknowledgement Sent**：<br />                    [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會在標準循序訊息的外面傳送收條。<br /><br /> **Message With Acknowledgement Received**：<br />                  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會將收條當做標準循序訊息的一部分接收。<br /><br /> **Acknowledgement Received**：<br />                  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會在循序訊息的外面接收收條。|21|是|  
|**GUID**|**uniqueidentifier**|對話的交談識別碼。 此識別碼是以訊息的一部份傳送，並在交談的兩端之間共用。|54|否|  
|**HonorBrokerPriority**|**Int**|資料庫 HONOR_BROKER_PRIORITY 選項目前的值為：0 = OFF，1 = ON。|32|是|  
|**HostName**|**nvarchar**|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。 若要判斷主機名稱，請使用 HOST_NAME 函數。|8|是|  
|**IntegerData**|**int**|包含收條之訊息的片段編號。|25|否|  
|**IntegerData2**|**int**|所認可之訊息的片段編號。|55|否|  
|**IsSystem**|**int**|指出事件是發生在系統處理序或使用者處理序。<br /><br /> 0 = 使用者<br /><br /> 1 = 系統|60|否|  
|**LoginSid**|**image**|已登入之使用者的安全性識別碼 (SID)。 伺服器上的每一個登入之 SID 是唯一的。|41|是|  
|**NTDomainName**|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|**NTUserName**|**nvarchar**|擁有產生此事件之連接的使用者名稱。|6|是|  
|**優先權**|**int**|交談的優先權等級。|5|是|  
|**RoleName**|**nvarchar**|認可訊息之執行個體的角色。 為 **initiator** 或 **target**其中一個角色。|38|否|  
|**ServerName**|**nvarchar**|所追蹤的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。|26|否|  
|**SPID**|**int**|由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指派給用戶端相關之處理序的伺服器處理序識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|**StarvationElevation**|**int**|傳送訊息時，使用的優先權高於原本為交談所設定的優先權：0 = false，1 = true。|33|是|  
|**TransactionID**|**bigint**|系統指派的交易識別碼。|4|否|  
  
  
