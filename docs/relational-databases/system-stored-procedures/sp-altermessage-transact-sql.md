---
description: sp_altermessage (Transact-SQL)
title: sp_altermessage (Transact-sql) |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a4af3e9a072e7ff2dca9ece41dd2e0e40a03ef76
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464571"
---
# <a name="sp_altermessage-transact-sql"></a>sp_altermessage (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  變更使用者定義狀態或在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體中之系統訊息。 您可以使用 **sys. messages** 目錄檢視來查看使用者定義的訊息。  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_altermessage [ @message_id = ] message_number   ,[ @parameter = ]'write_to_log'  
   ,[ @parameter_value = ]'value'   
```  
  
## <a name="arguments"></a>引數  
 [** @message_id =** ] *message_number*  
 這是要從 **sys.** message 變更之訊息的錯誤號碼。 *message_number* 是 **int** ，沒有預設值。  
  
`[ @parameter = ] 'write\_to\_log_'`會搭配** \@ parameter_value**使用，以表示訊息會寫入 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 應用程式記錄檔。 *write_to_log* 是 **sysname** ，沒有預設值。 *write_to_log* 必須設定為 WITH_LOG 或 Null。 如果*write_to_log*設定為 WITH_LOG 或 Null，且** \@ parameter_value**的值為**true**，則會將訊息寫入 Windows 應用程式記錄檔。 如果*write_to_log*設定為 WITH_LOG 或 Null，且** \@ parameter_value**的值為**false**，則不一定會將訊息寫入 Windows 應用程式記錄檔中，但可能會根據錯誤引發的方式寫入。 如果指定*write_to_log* ，也必須指定** \@ parameter_value**的值。  
  
> [!NOTE]  
>  如果訊息寫入 Windows 應用程式記錄檔中，它也會寫入 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 錯誤記錄檔中。  
  
`[ @parameter_value = ]'value_'`是搭配** \@ 參數**使用，以表示要將錯誤寫入 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 應用程式記錄檔。 *值* 是 **Varchar (5) **，沒有預設值。 若 **為 true**，則錯誤一律會寫入 Windows 應用程式記錄檔中。 若 **為 false**，則不一定會將錯誤寫入 Windows 應用程式記錄檔中，但可能會根據錯誤引發的方式寫入。 如果指定了*值*，則也必須指定** \@ 參數**的*write_to_log* 。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 使用 WITH_LOG 選項 **sp_altermessage** 的效果與 RAISERROR with LOG 參數的效果類似，不同之處在于 **sp_altermessage** 會變更現有訊息的記錄行為。 如果訊息已改成 WITH_LOG，它便一律會寫入 Windows 應用程式記錄檔中，不論使用者如何叫用錯誤都是如此。 即使執行 RAISERROR 時未設定 WITH_LOG 選項，仍會將錯誤寫入 Windows 應用程式記錄檔中。  
  
 您可以使用 **sp_altermessage**來修改系統訊息。  
  
## <a name="permissions"></a>權限  
 需要 **serveradmin** 固定伺服器角色中的成員資格。  
  
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
  
  
