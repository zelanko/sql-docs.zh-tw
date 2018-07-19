---
title: sp_altermessage (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_altermessage_TSQL
- sp_altermessage
dev_langs:
- TSQL
helpviewer_keywords:
- sp_altermessage
ms.assetid: 1b28f280-8ef9-48e9-bd99-ec14d79abaca
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cce6620bbc74d5c83cef907ab87f8252f963748a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33239668"
---
# <a name="spaltermessage-transact-sql"></a>sp_altermessage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更使用者定義狀態或在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體中之系統訊息。 您可以使用檢視使用者定義訊息**sys.messages**目錄檢視。  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_altermessage [ @message_id = ] message_number   ,[ @parameter = ]'write_to_log'  
   ,[ @parameter_value = ]'value'   
```  
  
## <a name="arguments"></a>引數  
 [**@message_id =** ] *message_number*  
 是從變更之訊息的錯誤數目**sys.messages**。 *message_number*是**int** ，沒有預設值。  
  
 [ **@parameter =** ] **'***write_to_log*'  
 搭配使用**@parameter_value**來指示訊息寫入到[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 應用程式記錄檔。 *write_to_log*是**sysname** ，沒有預設值。 *write_to_log*必須設為 WITH_LOG 或 NULL。 如果*write_to_log*設為 WITH_LOG 或 NULL，且值**@parameter_value**是**true**，訊息會寫入 Windows 應用程式記錄檔。 如果*write_to_log*設為 WITH_LOG 或 NULL 值和**@parameter_value**是**false**，訊息不一定會寫入 Windows 應用程式記錄檔，但可能寫入錯誤的產生方式而定。 如果*write_to_log*指定的值**@parameter_value**也必須指定。  
  
> [!NOTE]  
>  如果訊息寫入 Windows 應用程式記錄檔中，它也會寫入 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 錯誤記錄檔中。  
  
 [ **@parameter_value =** ]**'***value*'  
 搭配使用**@parameter**來指出錯誤寫入至[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 應用程式記錄檔。 *值*是**varchar(5)**，沒有預設值。 如果**true**，錯誤一律會寫入 Windows 應用程式記錄檔。 如果**false**，錯誤不一定會寫入 Windows 應用程式記錄檔，但也可能會寫入錯誤的產生方式而定。 如果*值*指定，則*write_to_log*如**@parameter**也必須指定。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 效果**sp_altermessage** WITH_LOG 選項是類似於 RAISERROR WITH LOG 參數，不過， **sp_altermessage**變更現有訊息的記錄行為。 如果訊息已改成 WITH_LOG，它便一律會寫入 Windows 應用程式記錄檔中，不論使用者如何叫用錯誤都是如此。 即使執行 RAISERROR 時未設定 WITH_LOG 選項，仍會將錯誤寫入 Windows 應用程式記錄檔中。  
  
 可以使用來修改系統訊息**sp_altermessage**。  
  
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
  
  
