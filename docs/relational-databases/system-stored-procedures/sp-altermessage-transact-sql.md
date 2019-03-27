---
title: sp_altermessage (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_altermessage_TSQL
- sp_altermessage
dev_langs:
- TSQL
helpviewer_keywords:
- sp_altermessage
ms.assetid: 1b28f280-8ef9-48e9-bd99-ec14d79abaca
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: df2bab593e0e945e854e310a394abbc93f75efa4
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493120"
---
# <a name="spaltermessage-transact-sql"></a>sp_altermessage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更使用者定義狀態或在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體中之系統訊息。 可以使用來檢視使用者自訂訊息**sys.messages**目錄檢視。  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_altermessage [ @message_id = ] message_number   ,[ @parameter = ]'write_to_log'  
   ,[ @parameter_value = ]'value'   
```  
  
## <a name="arguments"></a>引數  
 [**@message_id =** ] *message_number*  
 要從訊息錯誤號碼**sys.messages**。 *message_number*已**int** ，沒有預設值。  
  
`[ @parameter = ] 'write\_to\_log_'` 可搭配**@parameter_value**表示訊息會寫入至[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 應用程式記錄檔。 *write_to_log*已**sysname** ，沒有預設值。 *write_to_log*必須設為 WITH_LOG 或 NULL。 如果*write_to_log*設為 WITH_LOG 或 NULL，且值**@parameter_value**是**true**，訊息會寫入 Windows 應用程式記錄檔。 如果*write_to_log*設為 WITH_LOG 或 NULL，且值**@parameter_value**是**false**，訊息不一定會寫入 Windows 應用程式記錄檔，但可能寫入錯誤的產生方式而定。 如果*write_to_log*指定的值**@parameter_value**也必須指定。  
  
> [!NOTE]  
>  如果訊息寫入 Windows 應用程式記錄檔中，它也會寫入 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 錯誤記錄檔中。  
  
`[ @parameter_value = ]'value_'` 可搭配**@parameter**表示錯誤會寫入至[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 應用程式記錄檔。 *值*已**varchar(5)**，沒有預設值。 如果 **，則為 true**，錯誤一律會寫入 Windows 應用程式記錄檔。 如果**false**，錯誤不一定會寫入 Windows 應用程式記錄檔，但也可能會寫入錯誤的產生方式而定。 如果*值*指定，則*write_to_log* for **@parameter**也必須指定。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 效果**sp_altermessage**了 with_log 選項是類似於 RAISERROR WITH LOG 參數，不同之處在於**sp_altermessage**變更現有訊息的記錄行為。 如果訊息已改成 WITH_LOG，它便一律會寫入 Windows 應用程式記錄檔中，不論使用者如何叫用錯誤都是如此。 即使執行 RAISERROR 時未設定 WITH_LOG 選項，仍會將錯誤寫入 Windows 應用程式記錄檔中。  
  
 系統訊息可以藉由修改**sp_altermessage**。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**serveradmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 下列範例會使現有的訊息 `55001` 記錄到 Windows 應用程式記錄檔中。  
  
```  
EXECUTE sp_altermessage 55001, 'WITH_LOG', 'true';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
