---
description: sp_addapprole (Transact-SQL)
title: sp_addapprole (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addapprole_TSQL
- sp_addapprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addapprole
ms.assetid: 24200295-9a54-4cab-9922-fb2e88632721
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: fa68e8b0d965fae3a1c27f5ca2705bc003d7b616
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481542"
---
# <a name="sp_addapprole-transact-sql"></a>sp_addapprole (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將應用程式角色加入至目前資料庫中。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用 [CREATE APPLICATION ROLE](../../t-sql/statements/create-application-role-transact-sql.md) 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addapprole [ @rolename = ] 'role' , [ @password = ] 'password'  
```  
  
## <a name="arguments"></a>引數  
`[ @rolename = ] 'role'` 這是新應用程式角色的名稱。 *role* 是 **sysname**，沒有預設值。 *角色* 必須是有效的識別碼，且不能存在於目前的資料庫中。  
  
 應用程式角色名稱可包含 1 到 128 個字元，其中包括字母、符號和數字。 角色名稱不能包含反斜線 (\\) 不能是 Null，也不能 ( ' ' ) 的空字串。  
  
`[ @password = ] 'password'` 這是啟用應用程式角色所需的密碼。 *password* 是 **sysname**，沒有預設值。 *密碼* 不可為 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 在舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，使用者 (和角色) 並未與結構描述完全區分。 從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，結構描述就與角色完全分開。 這個新架構會反映在 CREATE APPLICATION ROLE 的行為上。 這個語句會取代 **sp_addapprole**。  
  
 為了維持與舊版的回溯相容性 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ， **sp_addapprole** 將會執行下列作業：  
  
-   如果尚未有與應用程式角色同名的結構描述，就會建立這類結構描述。 新的結構描述是由應用程式角色所擁有，它會是應用程式角色的預設結構描述。  
  
-   如果已經有與應用程式角色同名的結構描述，該程序就會失敗。  
  
-   **Sp_addapprole**不會檢查密碼複雜性。 但是，CREATE APPLICATION ROLE 會檢查密碼複雜性。  
  
 參數 *密碼* 會儲存為單向雜湊。  
  
 **Sp_addapprole**預存程式無法在使用者自訂交易內執行。  
  
> [!IMPORTANT]  
>  **SqlClient**不支援 Microsoft ODBC **encrypt**選項。 可以的話，請提示使用者在執行階段輸入應用程式角色認證。 請避免將認證儲存在檔案中。 如果您必須保存認證，請利用 CryptoAPI 函數來加密認證。  
  
## <a name="permissions"></a>權限  
 需要資料庫的 ALTER ANY APPLICATION ROLE 權限。 如果尚未有與新角色同名以及同一個擁有者的結構描述，也會需要資料庫的 CREATE SCHEMA 權限。  
  
## <a name="examples"></a>範例  
 下列範例會將具有密碼的新應用程式角色加入 `SalesApp` `x97898jLJfcooFUYLKm387gf3` 至目前的資料庫。  
  
```  
EXEC sp_addapprole 'SalesApp', 'x97898jLJfcooFUYLKm387gf3' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)  
  
  
