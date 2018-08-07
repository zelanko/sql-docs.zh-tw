---
title: Audit Broker Conversation 事件類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Audit Broker Conversation event class
ms.assetid: d58e3577-e297-42e5-b8fe-206665a75d13
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: a47a6adddf212c2da97813143b8ca6bf96f520e0
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39563492"
---
# <a name="audit-broker-conversation-event-class"></a>Audit Broker 交談事件類別
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會建立 **Audit Broker Conversation** 事件，以報告與 Service Broker 對話安全性相關的稽核訊息。  
  
## <a name="audit-broker-conversation-event-class-data-columns"></a>Audit Broker 交談事件類別的資料行  
  
|資料行|類型|Description|資料行編號|可篩選|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|10|是|  
|**BigintData1**|**bigint**|訊息的訊息序號。|52|否|  
|**ClientProcessID**|**int**|主機電腦指派給用戶端應用程式執行中處理序的識別碼。 如果用戶端提供處理序識別碼，這個資料行就會擴展。|9|是|  
|**DatabaseID**|**int**|由 USE *database* 陳述式所指定的資料庫識別碼，或者如果沒有針對指定執行個體發出 USE *database* 陳述式，則是預設資料庫的識別碼。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 資料行，則 **ServerName** 會顯示資料庫的名稱。 請使用 DB_ID 函數判斷資料庫的值。|3|是|  
|**錯誤**|**int**|如果此事件報告錯誤，即為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤號碼。|31|否|  
|**EventClass**|**int**|擷取的事件類別類型。 **Audit Broker Conversation** 永遠都是 **158**。|27|否|  
|**EventSubClass**|**int**|事件子類別的類型，針對每個事件類別提供更詳細的相關資訊。 下表列出此事件的事件子類別值。|21|是|  
|**FileName**|**nvarchar**|登入失敗的原因。 如果登入成功，此資料行則為空白。|36|否|  
|**GUID**|**uniqueidentifier**|對話的交談識別碼。 此識別碼是以訊息的一部份傳送，並在交談的兩端之間共用。|54|否|  
|**HostName**|**nvarchar**|執行用戶端的電腦名稱。 這個資料行會在用戶端提供主機名稱時填入。 若要判斷主機名稱，請使用 **HOST_NAME** 函數。|8|是|  
|**IntegerData**|**int**|訊息的片段號碼。|25|否|  
|**NTDomainName**|**nvarchar**|使用者所隸屬的 Windows 網域。|7|是|  
|**NTUserName**|**nvarchar**|擁有產生此事件之連接的使用者名稱。|6|是|  
|**ObjectId**|**int**|目標服務的使用者識別碼。|22|否|  
|**RoleName**|**nvarchar**|交談控制代碼的角色。 為 **initiator** 或 **target**其中一個角色。|38|否|  
|**ServerName**|**nvarchar**|正在追蹤之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的名稱。|26|否|  
|**Severity**|**int**|如果此事件報告錯誤，即為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤嚴重性。|29|否|  
|**SPID**|**int**|由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指派給用戶端關聯之處理序的伺服器處理序識別碼。|12|是|  
|**StartTime**|**datetime**|事件啟動的時間 (如果有的話)。|14|是|  
|**State**|**int**|指出產生事件的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原始程式碼內的位置。 每個可能產生此事件的位置都有不同的狀態碼。 Microsoft 支援工程師可以使用此狀態碼來尋找產生事件的位置。|30|否|  
|**TextData**|**ntext**|對於錯誤，包含描述失敗原因的訊息。 為下列其中一個值：<br /><br /> <br /><br /> **找不到憑證**。 為對話方塊通訊協定安全性所指定的使用者沒有憑證。<br /><br /> **不在有效的時間週期內**。 為對話通訊協定安全性所指定的使用者擁有憑證，但是憑證已過期。<br /><br /> **憑證太大無法進行記憶體配置**。 為對話通訊協定安全性所指定的使用者擁有憑證，但是憑證太大。 Service Broker 支援的憑證大小上限為 32,768 位元組。<br /><br /> **找不到私密金鑰**。 為對話通訊協定安全性所指定的使用者擁有憑證，但是沒有與該憑證關聯的私密金鑰。<br /><br /> **憑證的私密金鑰大小與密碼編譯提供者不相容**。 憑證的私密金鑰大小太大而無法成功處理。 私密金鑰大小必須是 64 位元組的倍數。<br /><br /> **憑證的公開金鑰大小與密碼編譯提供者不相容**。 憑證的公開金鑰大小太大而無法成功處理。 公開金鑰大小必須是 64 位元組的倍數。<br /><br /> **憑證的私密金鑰大小與加密金鑰交換金鑰不相容**。 在金鑰交換金鑰中所指定的金鑰大小與憑證的私密金鑰大小不相符。 這通常表示在遠端電腦上的憑證與資料庫中的憑證不相符。<br /><br /> **憑證的公開金鑰大小與安全性標頭的簽章不相容**。 安全性標頭包含無法使用憑證的公開金鑰進行驗證的簽章。 這通常表示在遠端電腦上的憑證與資料庫中的憑證不相符。|@shouldalert|是|  
  
 下表列出此事件類別的子類別值。  
  
|ID|子類別|Description|  
|--------|--------------|-----------------|  
|@shouldalert|沒有安全性標頭|在安全交談期間，Service Broker 收到不包含工作階段金鑰的訊息。 一旦建立安全交談，對話通訊協定需要交談中的所有訊息都包含工作階段金鑰。|  
|2|沒有憑證|Service Broker 在交談中找不到其中一個參與者的可用憑證。 為了保護交談的安全，資料庫必須包含同時針對交談的寄件者與收件者的憑證。|  
|3|無效的簽章|Broker 無法使用寄件者憑證中的公開金鑰來驗證寄件者所提供的訊息簽章。 這可能表示訊息已經損毀、訊息已經遭到竄改、遠端服務與本機服務並未以相同的使用者憑證設定，或是憑證已過期。|  
|4|以目標失敗執行|目的地使用者沒有目的地佇列的接收權限。 為了防止未經授權的使用者接收訊息，不論起始使用者是否擁有將訊息加入佇列的權限，Service Broker 並未將含有無法接收佇列的目的地使用者之訊息加入佇列。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
