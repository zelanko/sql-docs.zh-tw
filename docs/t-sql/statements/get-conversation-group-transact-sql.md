---
title: "取得交談群組 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GET
- CONVERSATION_GROUP_TSQL
- GET_TSQL
- GET_CONVERSATION_GROUP_TSQL
- GET CONVERSATION GROUP
- CONVERSATION GROUP
- GET CONVERSATION
- GET_CONVERSATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GET CONVERSATION GROUP statement
- conversations [Service Broker], groups
ms.assetid: 4da8a855-33c0-43b2-a49d-527487cb3b5c
caps.latest.revision: 39
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5cf1bd19e9ccc290c2c822ab59f00be75d447ba1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="get-conversation-group-transact-sql"></a>GET CONVERSATION GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對下一則要接收的訊息，傳回交談群組識別碼，並且針對含有該訊息的交談，鎖定交談群組。 您可以利用交談群組識別碼，先擷取交談狀態資訊，再擷取訊息本身。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
[ WAITFOR ( ]  
   GET CONVERSATION GROUP @conversation_group_id  
      FROM <queue>  
[ ) ] [ , TIMEOUT timeout ]  
[ ; ]  
  
<queue> ::=  
{  
    [ database_name . [ schema_name ] . | schema_name . ] queue_name  
}  
```  
  
## <a name="arguments"></a>引數  
 WAITFOR  
 指定如果目前沒有訊息，GET CONVERSATION GROUP 陳述式便會等待訊息到達佇列。  
  
 *@conversation_group_id*  
 這是一個變數，用來儲存 GET CONVERSATION GROUP 陳述式所傳回的交談群組識別碼。 變數必須屬於型別**uniqueidentifier**。 如果沒有可用的交談群組，變數就設為 NULL。  
  
 FROM  
 指定佇列，從中取得交談群組。  
  
 *database_name*  
 這是包含要取得交談群組所在之佇列的資料庫名稱。 若未*database_name*提供，則預設為目前的資料庫。  
  
 *schema_name*  
 這是擁有要取得交談群組所在佇列的結構描述名稱。 若未*schema_name*提供，則預設為目前使用者的預設結構描述。  
  
 *queue_name*  
 這是取得交談群組所在的佇列名稱。  
  
 逾時*逾時*  
 指定 Service Broker 等待訊息到達佇列的時間長度 (以毫秒為單位)。 這個子句只適用於 WAITFOR 子句。 如果使用 WAITFOR 的陳述式不包含這個子句或*逾時*為-1，等候時間是無限制。 在逾時到期，GET CONVERSATION GROUP 會將 *@conversation_group_id* 變數設為 NULL。  
  
## <a name="remarks"></a>備註  
  
> [!IMPORTANT]  
>  如果 GET CONVERSATION GROUP 陳述式不是在批次或預存程序的第一個陳述式，必須以分號結束之前的陳述式 (**;**)、[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式結束字元。  
  
 如果 GET CONVERSATION GROUP 陳述式中指定的佇列無法使用，陳述式便會發生 [!INCLUDE[tsql](../../includes/tsql-md.md)] 錯誤而失敗。  
  
 此陳述式會傳回以下所有條件都成立的下一個交談群組：  
  
-   交談群組可以成功鎖定。  
  
-   交談群組在佇列中有可用的訊息。  
  
-   在符合之前列出之準則的所有交談群組中，此交談群組具有最高的優先權等級。 交談群組的優先權等級為指派給任何交談的最高優先權等級 (此交談必須為此群組的成員，而且在佇列中有訊息)。  
  
 如果接著再呼叫同一交易中的 GET CONVERSATION GROUP，可能會鎖定不只一個交談群組。 如果沒有可用的交談群組，陳述式便會傳回 NULL 當作交談群組的識別碼。  
  
 在指定 WAITFOR 子句時，陳述式會等候指定的逾期時間到達，或者等到出現可用的交談群組為止。 如果佇列在陳述式等候時被卸除，陳述式會立即傳回錯誤。  
  
 在使用者自訂函數中，GET CONVERSATION GROUP 無效。  
  
## <a name="permissions"></a>Permissions  
 若要從佇列取得交談群組識別碼，目前使用者必須有佇列的 RECEIVE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-getting-a-conversation-group-waiting-indefinitely"></a>A. 取得交談群組，無限期等候  
 下列範例會將 `@conversation_group_id` 設定為 `ExpenseQueue` 中下一個可用訊息的交談群組識別碼。 命令會等到訊息成為可用訊息為止。  
  
```  
DECLARE @conversation_group_id UNIQUEIDENTIFIER ;  
  
WAITFOR (  
 GET CONVERSATION GROUP @conversation_group_id  
     FROM ExpenseQueue  
) ;  
```  
  
### <a name="b-getting-a-conversation-group-waiting-one-minute"></a>B. 取得交談群組，等候一分鐘  
 下列範例會將 `@conversation_group_id` 設定為 `ExpenseQueue` 中下一個可用訊息的交談群組識別碼。 如果一分鐘內還沒有出現可用訊息，GET CONVERSATION GROUP 便會傳回，而不改變 `@conversation_group_id` 的值。  
  
```  
DECLARE @conversation_group_id UNIQUEIDENTIFIER  
  
WAITFOR (  
    GET CONVERSATION GROUP @conversation_group_id   
    FROM ExpenseQueue ),  
TIMEOUT 60000 ;  
```  
  
### <a name="c-getting-a-conversation-group-returning-immediately"></a>C. 取得交談群組，立即傳回  
 下列範例會將 `@conversation_group_id` 設定為 `ExpenseQueue` 中下一個可用訊息的交談群組識別碼。 如果沒有可用訊息，`GET CONVERSATION GROUP` 便會立即傳回，而不變更 `@conversation_group_id`。  
  
```  
DECLARE @conversation_group_id UNIQUEIDENTIFIER ;  
  
GET CONVERSATION GROUP @conversation_group_id  
FROM AdventureWorks.dbo.ExpenseQueue ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [BEGIN DIALOG CONVERSATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [移動交談 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/move-conversation-transact-sql.md)  
  
  

