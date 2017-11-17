---
title: "傳送 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SEND_ON_CONVERSATION_TSQL
- ON_CONVERSATION_TSQL
- SEND
- SEND_TSQL
- SEND ON CONVERSATION
- ON CONVERSATION
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker], message sending
- SEND statement
- messages [Service Broker], sending
- sending messages
ms.assetid: b6e66aeb-1714-4c2b-b7c2-d386d77b0d46
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b149c44df4fb417ed143147cd38b4ae838318ece
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="send-transact-sql"></a>SEND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  利用一個或多個現有的交談來傳送訊息。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SEND  
   ON CONVERSATION [(]conversation_handle [,.. @conversation_handle_n][)]  
   [ MESSAGE TYPE message_type_name ]  
   [ ( message_body_expression ) ]  
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 在交談上*conversation_handle [..@conversation_handle_n]*  
 指定訊息所屬的交談。 *Conversation_handle*必須包含有效的交談識別碼。 相同的交談控制代碼不可使用超過一次。  
  
 訊息類型*message_type_name*  
 指定所傳送之訊息的訊息類型。 這個訊息類型必須包括在這些交談所用的服務合約中。 這些合約必須允許從交談的這一端傳送這個訊息類型。 例如，交談的目標服務只能傳送合約中指定為 SENT BY TARGET 或 SENT BY ANY 的訊息。 如果省略這個子句，訊息的訊息類型便是 DEFAULT。  
  
 *message_body_expression*  
 提供代表訊息主體的運算式。 *Message_body_expression*是選擇性的。 不過，如果*message_body_expression*存在於運算式必須是可以轉換成的型別**varbinary （max)**。 運算式不能是 NULL。 如果省略這個子句，訊息主體就是空白的。  
  
## <a name="remarks"></a>備註  
  
> [!IMPORTANT]  
>  如果 SEND 陳述式不是批次或預存程序中的第一個陳述式，就必須利用分號 (;) 來結束前一個陳述式。  
  
 SEND 陳述式會將一個或多個 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 交談某一端上服務的訊息傳輸到這些交談另一端上的服務。 然後會使用 RECEIVE 陳述式來從與目標服務有關的佇列中擷取傳送的訊息。  
  
 提供給 ON CONVERSATION 子句的交談控制代碼來自以下三個來源的其中一個：  
  
-   當傳送的訊息不是要回應從另一個服務所接收而來的訊息時，請使用建立此交談之 BEGIN DIALOG 陳述式傳回的交談控制代碼。  
  
-   當傳送的訊息是要回應之前從另一個服務所接收而來的訊息時，請使用之前傳回原始訊息之 RECEIVE 陳述式所傳回的交談控制代碼。  
  
 在大多數情況下，包含 SEND 陳述式的程式碼會與包含提供交談控制代碼之 BEGIN DIALOG 或 RECEIVE 陳述式的程式碼分開。 在這些情況下，交談控制代碼必須是傳遞給包含 SEND 陳述式之程式碼的狀態資訊內的其中一個資料項目。  
  
 傳送給其他 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體中之服務的訊息會儲存在目前資料庫的傳輸佇列中，直到可以將這些訊息傳輸到遠端執行個體內的服務佇列為止。 傳送至相同 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體內之服務的訊息，將會直接放入與該服務相關的佇列中。 如果某個狀況阻止將本機訊息直接放入目標服務佇列中，可以將該訊息儲存在傳輸佇列中，直到解決該狀況為止。 發生此狀況的例子包括某些錯誤類型或是目標服務佇列不在使用中。 您可以使用**sys.transmission_queue**系統檢視表來查看傳輸佇列中的訊息。  
  
 SEND 是不可部分完成的陳述式，也就是如果 SEND 陳述式無法傳送多個交談的訊息 (例如因為交談處於錯誤狀態)，則不會將訊息儲存在傳輸佇列中或放入任何目標服務佇列。  
  
 Service Broker 會最佳化相同 SEND 陳述式中多個交談上所傳送訊息的儲存和傳輸。  
  
 某個執行個體之傳輸佇列中的訊息是依照下列順序傳輸的：  
  
-   其相關之交談端點的優先權等級。  
  
-   其在優先權等級內的交談中傳送順序。  
  
 如果 HONOR_BROKER_PRIORITY 資料庫選項設定為 ON，在交談優先權中指定的優先權等級只會套用至傳輸佇列中的訊息。 如果 HONOR_BROKER_PRIORITY 設定為 OFF，則放置於該資料庫之傳輸佇列中的所有訊息都會使用預設優先權等級 5 加以指派。 優先權等級不會套用到 SEND，此狀況下的訊息會直接放入相同 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體內的服務佇列。  
  
 SEND 陳述式會分別鎖定傳送訊息的每一個交談，以確保每個交談的排序傳遞。  
  
 在使用者自訂函數中，SEND 無效。  
  
## <a name="permissions"></a>Permissions  
 若要傳送訊息，目前的使用者必須有傳送訊息之每個服務佇列的 RECEIVE 權限。  
  
## <a name="examples"></a>範例  
 下列範例會啟動一個對話，且會在對話中傳送一則 XML 訊息。 若要傳送訊息，此範例 xml 將物件轉換成**varbinary （max)**。  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER,  
        @ExpenseReport XML ;  
  
SET @ExpenseReport = < construct message as appropriate for the application > ;  
  
BEGIN DIALOG @dialog_handle  
FROM SERVICE [//Adventure-Works.com/Expenses/ExpenseClient]  
TO SERVICE '//Adventure-Works.com/Expenses'  
ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseProcessing] ;  
  
SEND ON CONVERSATION @dialog_handle  
    MESSAGE TYPE [//Adventure-Works.com/Expenses/SubmitExpense]  
    (@ExpenseReport) ;  
```  
  
 下列範例會啟動三個對話，且會在每個對話中傳送一則 XML 訊息。  
  
```  
DECLARE @dialog_handle1 UNIQUEIDENTIFIER,  
        @dialog_handle2 UNIQUEIDENTIFIER,  
        @dialog_handle3 UNIQUEIDENTIFIER,  
        @OrderMsg XML ;  
  
SET @OrderMsg = < construct message as appropriate for the application > ;  
  
BEGIN DIALOG @dialog_handle1  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB1/TargetService’  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
BEGIN DIALOG @dialog_handle2  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB2/TargetService’  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
BEGIN DIALOG @dialog_handle3  
FROM SERVICE [//InitiatorDB/InitiatorService]  
TO SERVICE '//TargetDB3/TargetService’  
ON CONTRACT [//AllDBs/OrderProcessing] ;  
  
SEND ON CONVERSATION (@dialog_handle1, @dialog_handle2, @dialog_handle3)  
    MESSAGE TYPE [//AllDBs/OrderMsg]  
    (@OrderMsg) ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [BEGIN DIALOG CONVERSATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [END CONVERSATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [接收 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/receive-transact-sql.md)   
 [sys.transmission_queue &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-transmission-queue-transact-sql.md)  
  
  

