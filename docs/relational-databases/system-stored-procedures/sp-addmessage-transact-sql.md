---
title: sp_addmessage (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addmessage
- sp_addmessage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addmessage
ms.assetid: 54746d30-f944-40e5-a707-f2d9be0fb9eb
author: stevestein
ms.author: sstein
ms.openlocfilehash: 52d3db15c46af273e2f151e769a6b04be322ce5b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061842"
---
# <a name="spaddmessage-transact-sql"></a>sp_addmessage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將新的使用者自訂錯誤訊息儲存在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體中。 使用儲存的訊息**sp_addmessage**可以使用檢視**sys.messages**目錄檢視。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addmessage [ @msgnum= ] msg_id , [ @severity= ] severity , [ @msgtext= ] 'msg'   
     [ , [ @lang= ] 'language' ]   
     [ , [ @with_log= ] { 'TRUE' | 'FALSE' } ]   
     [ , [ @replace= ] 'replace' ]   
```  
  
## <a name="arguments"></a>引數  
`[ \@msgnum = ] msg_id` 是訊息的識別碼。 *msg_id*已**int**預設值是 NULL。 *msg_id*使用者定義錯誤訊息可以是 50,001 和 2,147,483,647 之間的整數。 組合*msg_id*並*語言*必須是唯一的; 如果指定的語言的識別碼已經存在，會傳回錯誤。  
  
`[ \@severity = ]severity` 是錯誤的嚴重性層級。 *嚴重性*已**smallint**預設值是 NULL。 有效的層級範圍是 1 到 25。 如需有關嚴重性的詳細資訊，請參閱 [Database Engine 錯誤嚴重性](../../relational-databases/errors-events/database-engine-error-severities.md)。  
  
`[ \@msgtext = ] 'msg'` 這是錯誤訊息的文字。 *msg*已**nvarchar(255)** 預設值是 NULL。  
  
`[ \@lang = ] 'language'` 為此訊息的語言。 *語言*已**sysname**預設值是 NULL。 因為可以在相同的伺服器上安裝多種語言*語言*指定撰寫每個訊息的語言。 當*語言*已省略，語言是預設語言工作階段。  
  
`[ \@with_log = ] { 'TRUE' | 'FALSE' }` 將訊息寫入 Windows 應用程式記錄檔，當它發生時。 **\@with_log**已**varchar(5)** 預設值是 FALSE。 如果是 TRUE，錯誤一律會寫入 Windows 應用程式記錄檔中。 如果是 FALSE，錯誤就不一定會寫入 Windows 應用程式記錄檔中，但隨著錯誤的產生方式而不同，也可能會寫入。 只有成員**sysadmin**伺服器角色可以使用此選項。  
  
> [!NOTE]  
>  如果訊息寫入 Windows 應用程式記錄檔中，它也會寫入 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 錯誤記錄檔中。  
  
`[ \@replace = ] 'replace'` 如果指定為字串*取代*，新訊息文字和嚴重性層級覆寫現有的錯誤訊息。 *取代*已**varchar(7)** 預設值是 NULL。 必須指定此選項，如果*msg_id*已經存在。 如果您取代 U.S.English 訊息，嚴重性層級會取代所有具有相同的其他語言中的所有訊息*msg_id*。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 對於非英文版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，美國訊息可以使用另一種語言加入之前，必須已經存在之訊息的英文版。 兩個版本的訊息，嚴重性必須相符。  
  
 當您將包含參數的訊息當地語系化時，請使用對應於原始訊息中之參數的參數號碼。 請在每個參數號碼之後，插入驚歎號 (!)。  
  
|原始訊息|當地語系化的訊息|  
|----------------------|-----------------------|  
|'Original message param 1: %s,<br /><br /> param 2: %d'|'Localized message param 1: %1!,<br /><br /> param 2: %2!'|  
  
 由於語言語法差異，當地語系化訊息中的參數號碼可能與原始訊息中的順序不符。  
  
## <a name="permissions"></a>Permissions  
需要的成員資格**sysadmin**或是**serveradmin**固定伺服器角色。  
  
## <a name="examples"></a>範例  
  
### <a name="a-defining-a-custom-message"></a>A. 定義自訂訊息  
 下列範例會將自訂訊息**sys.messages**。  
  
```  
USE master;  
GO  
EXEC sp_addmessage 50001, 16,   
   N'Percentage expects a value between 20 and 100.   
   Please reexecute with a more appropriate value.';  
GO  
```  
  
### <a name="b-adding-a-message-in-two-languages"></a>B. 加入兩種語言的訊息  
 下列範例首先會將訊息加入美國再加入法文的相同的訊息`.`  
  
```  
USE master;  
GO  
EXEC sp_addmessage @msgnum = 60000, @severity = 16,   
   @msgtext = N'The item named %s already exists in %s.',   
   @lang = 'us_english';  
  
EXEC sp_addmessage @msgnum = 60000, @severity = 16,   
   @msgtext = N'L''élément nommé %1! existe déjà dans %2!',   
   @lang = 'French';  
GO  
```  
  
### <a name="c-changing-the-order-of-parameters"></a>C. 變更參數的順序  
 下列範例首先會將訊息加入美國英文、，然後將加入當地語系化的訊息中的參數順序會變更。  
  
```  
USE master;  
GO  
  
EXEC sp_addmessage   
    @msgnum = 60000,   
    @severity = 16,  
    @msgtext =   
        N'This is a test message with one numeric  
        parameter (%d), one string parameter (%s),   
        and another string parameter (%s).',  
    @lang = 'us_english';  
  
EXEC sp_addmessage   
    @msgnum = 60000,   
    @severity = 16,  
    @msgtext =   
        -- In the localized version of the message,  
        -- the parameter order has changed. The   
        -- string parameters are first and second  
        -- place in the message, and the numeric   
        -- parameter is third place.  
        N'Dies ist eine Testmeldung mit einem   
        Zeichenfolgenparameter (%3!),  
        einem weiteren Zeichenfolgenparameter (%2!),   
        und einem numerischen Parameter (%1!).',  
    @lang = 'German';  
GO    
  
-- Changing the session language to use the U.S. English  
-- version of the error message.  
SET LANGUAGE us_english;  
GO  
  
RAISERROR(60000,1,1,15,'param1','param2') -- error, severity, state,  
GO                                       -- parameters.  
  
-- Changing the session language to use the German  
-- version of the error message.  
SET LANGUAGE German;  
GO  
  
RAISERROR(60000,1,1,15,'param1','param2'); -- error, severity, state,   
GO                                       -- parameters.  
```  
  
## <a name="see-also"></a>另請參閱  
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [sp_altermessage &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
