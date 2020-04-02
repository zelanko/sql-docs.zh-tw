---
title: sp_addmessage(轉算-SQL) |微軟文件
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
ms.openlocfilehash: d040fa0ccfe9b962f8847db0a841b95a534326fa
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/01/2020
ms.locfileid: "80531038"
---
# <a name="sp_addmessage-transact-sql"></a>sp_addmessage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將新的使用者自訂錯誤訊息儲存在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體中。 可以使用**sp_addmessage**存儲的消息可以使用**sys.訊息**目錄視圖進行查看。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addmessage [ @msgnum= ] msg_id , [ @severity= ] severity , [ @msgtext= ] 'msg'   
     [ , [ @lang= ] 'language' ]   
     [ , [ @with_log= ] { 'TRUE' | 'FALSE' } ]   
     [ , [ @replace= ] 'replace' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @msgnum = ] msg_id`是消息的 ID。 *msg_id***為 int,** 預設值為 NULL。 使用者定義的錯誤消息*msg_id*可以是 50,001 和 2,147,483,647 之間的整數。 *msg_id*和*語言*的結合必須是唯一的;如果指定語言的 ID 已存在,則傳回錯誤。  
  
`[ @severity = ]severity`是錯誤的嚴重性級別。 *嚴重性*較小 **,** 預設值為 NULL。 有效的層級範圍是 1 到 25。 如需有關嚴重性的詳細資訊，請參閱 [Database Engine 錯誤嚴重性](../../relational-databases/errors-events/database-engine-error-severities.md)。  
  
`[ @msgtext = ] 'msg'`是錯誤消息的文本。 *msg*是**nvarchar (255),** 預設值為 NULL。  
  
`[ @lang = ] 'language'`是此消息的語言。 *語言*是預設為 NULL 的**sysname。** 由於可以在同一台伺服器上安裝多種語言,*因此語言*指定每條消息的編寫語言。 省略*語言*時,該語言是會話的默認語言。  
  
`[ @with_log = ] { 'TRUE' | 'FALSE' }`是消息在發生時是否寫入 Windows 應用程式日誌。 with_log是**varchar(5),** 預設值為 FALSE。 ** \@ ** 如果是 TRUE，錯誤一律會寫入 Windows 應用程式記錄檔中。 如果是 FALSE，錯誤就不一定會寫入 Windows 應用程式記錄檔中，但隨著錯誤的產生方式而不同，也可能會寫入。 只有**系統管理員**伺服器角色的成員才能使用此選項。  
  
> [!NOTE]  
>  如果訊息寫入 Windows 應用程式記錄檔中，它也會寫入 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 錯誤記錄檔中。  
  
`[ @replace = ] 'replace'`如果指定為字串*替換*,則現有錯誤消息將被新的消息文本和嚴重性級別覆蓋。 *替換*的預設值為 NULL 的**varchar(7)。** 如果msg_id已存在 *,* 則必須指定此選項。 如果替換美國英語消息,則將替換具有相同*msg_id*的所有其他語言的所有郵件的嚴重性級別。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 如果是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的非英文版本，訊息的 U.S. English 版本必須已存在，之後才能利用其他語言來加入訊息。 兩個版本的訊息，嚴重性必須相符。  
  
 當您將包含參數的訊息當地語系化時，請使用對應於原始訊息中之參數的參數號碼。 請在每個參數號碼之後，插入驚歎號 (!)。  
  
|原始訊息|當地語系化的訊息|  
|----------------------|-----------------------|  
|'Original message param 1: %s,<br /><br /> param 2: %d'|'Localized message param 1: %1!,<br /><br /> param 2: %2!'|  
  
 由於語言語法差異，當地語系化訊息中的參數號碼可能與原始訊息中的順序不符。  
  
## <a name="permissions"></a>權限  
需要**系統管理員**或**伺服器管理員**固定伺服器角色的成員身份。  
  
## <a name="examples"></a>範例  
  
### <a name="a-defining-a-custom-message"></a>A. 定義自訂訊息  
 下面的範例向**sys.消息**添加自訂訊息。  
  
```  
USE master;  
GO  
EXEC sp_addmessage 50001, 16,   
   N'Percentage expects a value between 20 and 100.   
   Please reexecute with a more appropriate value.';  
GO  
```  
  
### <a name="b-adding-a-message-in-two-languages"></a>B. 加入兩種語言的訊息  
 下列範例會先加入 U.S. English 的訊息，再加入法文的相同訊息。`.`  
  
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
 下列範例會先加入 U.S. English 的訊息，再加入變更了參數順序的當地語系化訊息。  
  
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
 [&#40;转瞬即发-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [sp_altermessage&#40;交易-SQL&#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
