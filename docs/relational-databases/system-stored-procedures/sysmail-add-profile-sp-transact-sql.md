---
description: sysmail_add_profile_sp (Transact-SQL)
title: sysmail_add_profile_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_profile_sp_TSQL
- sysmail_add_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profile_sp
ms.assetid: a828e55c-633a-41cf-9769-a0698b446e6c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f78f4ea075f04c4deb447ad9b68e3707b4e19ffb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480859"
---
# <a name="sysmail_add_profile_sp-transact-sql"></a>sysmail_add_profile_sp (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  建立新的 Database Mail 設定檔。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_add_profile_sp [ @profile_name = ] 'profile_name'  
    [ , [ @description = ] 'description' ]  
    [ , [ @profile_id = ] new_profile_id OUTPUT ]  
```  
  
## <a name="arguments"></a>引數  
`[ @profile_name = ] 'profile\_name'` 新設定檔的名稱。 *profile_name* 是 **sysname**，沒有預設值。  
 
   > [!NOTE]
   > 您必須呼叫使用 Azure SQL 受控執行個體 SQL Agent 的設定檔名稱 **AzureManagedInstance_dbmail_profile**
  
`[ @description = ] 'description'` 新設定檔的選擇性描述。 *描述* 是 **Nvarchar (256) **，沒有預設值。  
  
`[ @profile_id = ] _new\_profile\_id OUTPUT` 傳回新設定檔的識別碼。 *new_profile_id* 是 **int**，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 Database Mail 設定檔會保存任意數目的 Database Mail 帳戶。 Database Mail 預存程序可以利用這個程序所產生的設定檔名稱或設定檔識別碼來參考設定檔。 如需將帳戶新增至設定檔的詳細資訊，請參閱 [sysmail_add_profileaccount_sp &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql.md)。  
  
 您可以使用預存程式 **sysmail_update_profile_sp**來變更設定檔名稱和描述，而設定檔識別碼在設定檔的存留期間仍維持不變。  
  
 Microsoft [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的設定檔名稱必須是唯一的，否則，預存程序會傳回一則錯誤。  
  
 預存程式 **sysmail_add_profile_sp** 位於 **msdb** 資料庫中，而且是由 **dbo** 架構所擁有。 如果目前的資料庫不是 **msdb**，就必須以三部分名稱執行程式。  
  
## <a name="permissions"></a>權限  
 此程式的執行許可權預設為 **系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 **A. 建立新的設定檔**  
  
 下列範例會建立名稱為 `AdventureWorks Administrator` 的新 Database Mail 設定檔。  
  
```  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.' ;  
```  
  
 **B. 建立新的設定檔，將設定檔識別碼儲存在變數中**  
  
 下列範例會建立名稱為 `AdventureWorks Administrator` 的新 Database Mail 設定檔。 這個範例會將設定檔識別碼儲存在 `@profileId` 變數中，且會傳回包含新設定檔之設定檔識別碼的結果集。  
  
```  
DECLARE @profileId INT ;  
  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.',  
       @profile_id = @profileId OUTPUT ;  
  
SELECT @profileId ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [建立 Database Mail 帳戶](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail 設定物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [&#40;Transact-sql&#41;的 Database Mail 預存程式 ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
