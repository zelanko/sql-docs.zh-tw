---
title: "開始交談計時器 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CONVERSATION
- BEGIN_CONVERSATION_TSQL
- TIMER_TSQL
- TIMER
- CONVERSATION TIMER
- CONVERSATION_TIMER_TSQL
- BEGIN CONVERSATION TIMER
- BEGIN_CONVERSATION_TIMER_TSQL
- CONVERSATION_TSQL
- BEGIN CONVERSATION
dev_langs:
- TSQL
helpviewer_keywords:
- BEGIN CONVERSATION TIMER statement
- DialogTimer message
- dialogs [Service Broker], beginning
- timeouts [Service Broker]
- timer messages [Service Broker]
- conversations [Service Broker], timers
- starting timers [Service Broker]
- http://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer message
ms.assetid: 98e49b3f-a38f-4180-8171-fa9cb30db4cb
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b70228860699b3fefe9a1b5adcfc0250ce5d34e1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="begin-conversation-timer-transact-sql"></a>BEGIN CONVERSATION TIMER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  啟動計時器。 當逾時到期時，[!INCLUDE[ssSB](../../includes/sssb-md.md)]類型的訊息放`http://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer`交談的本機佇列上。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
BEGIN CONVERSATION TIMER ( conversation_handle )  
   TIMEOUT = timeout   
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 BEGIN CONVERSATION TIMER **(***conversation_handle***)**  
 指定要計時的交談。 *Conversation_handle*必須是型別**uniqueidentifier**。  
  
 TIMEOUT   
 指定等待多久之後，便將訊息放入佇列 (以秒為單位)。  
  
## <a name="remarks"></a>備註  
 交談計時器提供一種方式，供應用程式在特定時間量之後，接收交談的訊息。 在計時器到期之前，在交談上呼叫 BEGIN CONVERSATION TIMER，會將逾時設為新值。 這不像交談存留期間，交談的每一端都會有獨立的交談計時器。 **DialogTimer**訊息到達本機佇列上，而不會影響交談的另一端。 因此，應用程式可以為了任何目的而使用計時器訊息。  
  
 例如，您可以利用交談計時器，使應用程式不會為了逾期回應而等待太久。 如果您預期應用程式會在 30 秒內完成對話，您可以將這項對話的交談計時器設為 60 秒 (30 秒加上 30 秒的寬限期)。 如果在 60 秒之後，對話仍在開啟狀態，應用程式會在這項對話的佇列上，收到一則逾時訊息。  
  
 另外，應用程式也可以利用交談計時器，要求在特定時間啟用。 例如，您可以建立一項服務，每隔幾分鐘報告使用中的連接數目，或建立一項服務來報告每個晚上開立的採購單數目。 服務會將交談計時器到期日設定在所需的時間。當計時器過期時，[!INCLUDE[ssSB](../../includes/sssb-md.md)]傳送**DialogTimer**訊息。 **DialogTimer**訊息會使[!INCLUDE[ssSB](../../includes/sssb-md.md)]開始啟用預存程序的佇列。 這個預存程序會傳送一則訊息給遠端服務，且會重新啟動交談計時器。  
  
 在使用者自訂函數中，BEGIN CONVERSATION TIMER 無效。  
  
## <a name="permissions"></a>Permissions  
 將交談計時器的預設值設定為具有 SEND 權限的成員，交談在服務的使用者權限**sysadmin**固定伺服器角色和成員**db_owner**固定的資料庫角色。  
  
## <a name="examples"></a>範例  
 下列範例會在 `@dialog_handle` 所識別的對話上設定兩分鐘逾時。  
  
```  
-- @dialog_handle is of type uniqueidentifier and  
-- contains a valid conversation handle.  
  
BEGIN CONVERSATION TIMER (@dialog_handle)  
TIMEOUT = 120 ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [BEGIN DIALOG CONVERSATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [END CONVERSATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [接收 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/receive-transact-sql.md)  
  
  
