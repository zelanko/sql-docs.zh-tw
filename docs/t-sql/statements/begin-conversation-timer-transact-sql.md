---
title: BEGIN CONVERSATION TIMER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: bff71c5286d0bf48e43bda62cdc4b7c26a10b038
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
---
# <a name="begin-conversation-timer-transact-sql"></a>BEGIN CONVERSATION TIMER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  啟動計時器。 當逾時到期時，[!INCLUDE[ssSB](../../includes/sssb-md.md)] 將 `http://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer` 型別的訊息放在交談的本機佇列上。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
BEGIN CONVERSATION TIMER ( conversation_handle )  
   TIMEOUT = timeout   
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 BEGIN CONVERSATION TIMER **(***conversation_handle***)**  
 指定要計時的交談。 *conversation_handle* 必須是 **uniqueidentifier** 型別。  
  
 TIMEOUT   
 指定等待多久之後，便將訊息放入佇列 (以秒為單位)。  
  
## <a name="remarks"></a>Remarks  
 交談計時器提供一種方式，供應用程式在特定時間量之後，接收交談的訊息。 在計時器到期之前，在交談上呼叫 BEGIN CONVERSATION TIMER，會將逾時設為新值。 這不像交談存留期間，交談的每一端都會有獨立的交談計時器。 **DialogTimer** 訊息到達本機佇列時，不會影響交談的遠端。 因此，應用程式可以為了任何目的而使用計時器訊息。  
  
 例如，您可以利用交談計時器，使應用程式不會為了逾期回應而等待太久。 如果您預期應用程式會在 30 秒內完成對話，您可以將這項對話的交談計時器設為 60 秒 (30 秒加上 30 秒的寬限期)。 如果在 60 秒之後，對話仍在開啟狀態，應用程式會在這項對話的佇列上，收到一則逾時訊息。  
  
 另外，應用程式也可以利用交談計時器，要求在特定時間啟用。 例如，您可以建立一項服務，每隔幾分鐘報告使用中的連接數目，或建立一項服務來報告每個晚上開立的採購單數目。 服務會設定一個在所需時間到期的交談計時器；當計時器到期時，[!INCLUDE[ssSB](../../includes/sssb-md.md)] 會傳送 **DialogTimer** 訊息。 **DialogTimer** 訊息會造成 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 啟動佇列的啟用預存程序。 這個預存程序會傳送一則訊息給遠端服務，且會重新啟動交談計時器。  
  
 在使用者自訂函數中，BEGIN CONVERSATION TIMER 無效。  
  
## <a name="permissions"></a>Permissions  
 交談計時器的設定權限預設給有交談服務之 SEND 權限的使用者、系統管理員 (**sysadmin**) 固定伺服器角色的成員，以及 **db_owner** 固定資料庫角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會在 `@dialog_handle` 所識別的對話上設定兩分鐘逾時。  
  
```  
-- @dialog_handle is of type uniqueidentifier and  
-- contains a valid conversation handle.  
  
BEGIN CONVERSATION TIMER (@dialog_handle)  
TIMEOUT = 120 ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [END CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md)  
  
  
