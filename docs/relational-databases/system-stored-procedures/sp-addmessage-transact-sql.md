---
title: sp_addmessage （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: adf32fad3c233023529d362cd7382ca6376b3cee
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85877386"
---
# <a name="sp_addmessage-transact-sql"></a>sp_addmessage (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將新的使用者自訂錯誤訊息儲存在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體中。 使用 [ **sp_addmessage** ] 儲存的訊息，可以使用 [ **sys.databases** ] 目錄檢視來查看。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addmessage [ @msgnum= ] msg_id , [ @severity= ] severity , [ @msgtext= ] 'msg'   
     [ , [ @lang= ] 'language' ]   
     [ , [ @with_log= ] { 'TRUE' | 'FALSE' } ]   
     [ , [ @replace= ] 'replace' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @msgnum = ] msg_id`這是訊息的識別碼。 *msg_id*是**int** ，預設值是 Null。 使用者自訂錯誤訊息的*msg_id*可以是介於50001和2147483647之間的整數。 *Msg_id*和*語言*的組合必須是唯一的;如果已有指定語言的識別碼，則會傳回錯誤。  
  
`[ @severity = ]severity`這是錯誤的嚴重性層級。 *嚴重性*是**Smallint** ，預設值是 Null。 有效的層級範圍是 1 到 25。 如需有關嚴重性的詳細資訊，請參閱 [Database Engine 錯誤嚴重性](../../relational-databases/errors-events/database-engine-error-severities.md)。  
  
`[ @msgtext = ] 'msg'`這是錯誤訊息的文字。 *msg*是**Nvarchar （255）** ，預設值是 Null。  
  
`[ @lang = ] 'language'`這是此訊息的語言。 *language*是**sysname** ，預設值是 Null。 因為多個語言可以安裝在同一部伺服器上，所以*language*會指定要在其中寫入每個訊息的語言。 省略*language*時，語言是會話的預設語言。  
  
`[ @with_log = ] { 'TRUE' | 'FALSE' }`這是指訊息發生時是否要寫入 Windows 應用程式記錄檔。 ** \@ with_log**是**Varchar （5）** ，預設值是 FALSE。 如果是 TRUE，錯誤一律會寫入 Windows 應用程式記錄檔中。 如果是 FALSE，錯誤就不一定會寫入 Windows 應用程式記錄檔中，但隨著錯誤的產生方式而不同，也可能會寫入。 只有**系統管理員（sysadmin** ）伺服器角色的成員可以使用此選項。  
  
> [!NOTE]  
>  如果訊息寫入 Windows 應用程式記錄檔中，它也會寫入 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 錯誤記錄檔中。  
  
`[ @replace = ] 'replace'`如果指定為字串*replace*，則會以新的郵件內文和嚴重性層級來覆寫現有的錯誤訊息。 *replace*是**Varchar （7）** ，預設值是 Null。 如果*msg_id*已經存在，就必須指定此選項。 如果您取代美式英文訊息，則會取代所有其他語言中具有相同*msg_id*的所有訊息的嚴重性層級。  
  
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
需要**系統管理員（sysadmin** ）或**serveradmin**固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-defining-a-custom-message"></a>A. 定義自訂訊息  
 下列範例會將自訂訊息新增至**sys.databases**。  
  
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
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [sp_altermessage &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
