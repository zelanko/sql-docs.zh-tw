---
title: "FORMATMESSAGE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FORMATMESSAGE
- FORMATMESSAGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmessages system table
- sys.messages catalog view
- FORMATMESSAGE function
- messages [SQL Server], formats
- errors [SQL Server], formats
ms.assetid: 83f18102-2035-4a87-acd0-8d96d03efad5
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 071f6def07baf0b74919fd5ce93e65494877dda0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="formatmessage-transact-sql"></a>FORMATMESSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  建構訊息在 sys.messages 中現有的訊息，或從提供的字串。 FORMATMESSAGE 的功能類似於 RAISERROR 陳述式的功能。 不過，RAISERROR 會立即列印訊息，FORMATMESSAGE 則會傳回格式化的訊息，以便進一步處理。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
FORMATMESSAGE ( { msg_number  | ' msg_string ' } , [ param_value [ ,...n ] ] )  
```  
  
## <a name="arguments"></a>引數  
 *msg_number*  
 是儲存在 sys.messages 中之訊息的識別碼。 如果*msg_number*是 < = 13000，或如果訊息在 sys.messages 中不存在，則傳回 NULL。  
  
 *msg_string*  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。  
  
 是括在單引號和包含參數值的預留位置的字串。 這個錯誤訊息最多可有 2,047 個字元。 如果訊息包含 2,048 個或更多字元，則只會顯示前 2,044 個字元，並且會加上省略符號以表示該訊息已被截斷。 請注意，由於內部儲存行為的緣故，替代參數比輸出顯示耗用更多字元。  如需訊息字串的結構以及將字串中的參數資訊，請參閱的描述*msg_str*引數中的[RAISERROR &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
 *param_value*  
 這是訊息中所用的參數值。 它可以是多個參數值。 您必須依照預留位置變數在訊息中的出現順序來指定這些值。 最多可有 20 個值。  
  
## <a name="return-types"></a>傳回類型  
 **nvarchar**  
  
## <a name="remarks"></a>備註  
 如同 RAISERROR 陳述式，FORMATMESSAGE 會用所提供的參數值來替代訊息中的預留位置變數，以編輯訊息。 如需在錯誤訊息和編輯程序中允許之預留位置的詳細資訊，請參閱[RAISERROR &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
 FORMATMESSAGE 會用使用者目前的語言來查閱訊息。 如果沒有當地語系化版本的訊息，就會使用 U.S. English 版本。  
  
 如果是當地語系化的訊息，提供的參數值必須對應於 U.S. English 版本中的參數預留位置。 也就是說，當地語系化版本中的參數 1 必須對應於 U.S. English 版本中的參數 1，參數 2 必須對應於參數 2，依此類推。  
  
## <a name="examples"></a>範例  
  
### <a name="a-example-with-a-message-number"></a>A. 範例訊息編號  
 下列範例會使用的複寫訊息`20009`儲存為 sys.messages 中，「 發行項 '%s' 無法加入發行集 '%s'。 」FORMATMESSAGE 會將 `First Variable` 和 `Second Variable` 這兩個值代入參數預留位置中。 產生的字串"發行項 'First Variable' 無法加入發行集 'Second Variable'。 」，儲存在本機變數`@var1`。  
  
```  
SELECT text FROM sys.messages WHERE message_id = 20009 AND language_id = 1033;  
DECLARE @var1 VARCHAR(200);   
SELECT @var1 = FORMATMESSAGE(20009, 'First Variable', 'Second Variable');   
SELECT @var1;  
```  
  
### <a name="b-example-with-a-message-string"></a>B. 使用訊息字串的範例  
  
**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。  
  
 下列範例會採用字串做為輸入。  
  
```  
SELECT FORMATMESSAGE('This is the %s and this is the %s.', 'first variable', 'second variable') AS Result;  
```  
  
 傳回：`This is the first variable and this is the second variable.`  
  
### <a name="c-additional-message-string-formatting-examples"></a>C. 額外的訊息字串格式化的範例  
 下列範例顯示各種不同的格式化選項。  
  
```  
SELECT FORMATMESSAGE('Signed int %i, %d %i, %d, %+i, %+d, %+i, %+d', 5, -5, 50, -50, -11, -11, 11, 11);  
SELECT FORMATMESSAGE('Signed int with leading zero %020i', 5);  
SELECT FORMATMESSAGE('Signed int with leading zero 0 %020i', -55);  
SELECT FORMATMESSAGE('Unsigned int %u, %u', 50, -50);  
SELECT FORMATMESSAGE('Unsigned octal %o, %o', 50, -50);  
SELECT FORMATMESSAGE('Unsigned hexadecimal %x, %X, %X, %X, %x', 11, 11, -11, 50, -50);  
SELECT FORMATMESSAGE('Unsigned octal with prefix: %#o, %#o', 50, -50);  
SELECT FORMATMESSAGE('Unsigned hexadecimal with prefix: %#x, %#X, %#X, %X, %x', 11, 11, -11, 50, -50);  
SELECT FORMATMESSAGE('Hello %s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %20s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %-20s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %20s!', 'TEST');  
```  
  
## <a name="see-also"></a>另請參閱  
 [THROW &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [sp_addmessage &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [RAISERROR &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  

