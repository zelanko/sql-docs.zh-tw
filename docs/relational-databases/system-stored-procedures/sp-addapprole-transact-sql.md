---
title: "sp_addapprole (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_addapprole_TSQL
- sp_addapprole
dev_langs: TSQL
helpviewer_keywords: sp_addapprole
ms.assetid: 24200295-9a54-4cab-9922-fb2e88632721
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7556f2f78890a0e52efde7758077fbf124ed3bac
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="spaddapprole-transact-sql"></a>sp_addapprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將應用程式角色加入至目前資料庫中。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用[CREATE APPLICATION ROLE](../../t-sql/statements/create-application-role-transact-sql.md)改為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addapprole [ @rolename = ] 'role' , [ @password = ] 'password'  
```  
  
## <a name="arguments"></a>引數  
 [  **@rolename =** ] **'***角色***'**  
 這是新應用程式角色的名稱。 *角色*是**sysname**，沒有預設值。 *角色*必須是有效的識別項，而且不能存在於目前資料庫。  
  
 應用程式角色名稱可包含 1 到 128 個字元，其中包括字母、符號和數字。 角色名稱不能包含反斜線 (\\) 也不能是 NULL 或空字串 （"）。  
  
 [  **@password =** ] **'***密碼***'**  
 啟動應用程式角色所需的密碼。 *密碼*是**sysname**，沒有預設值。 *密碼*不能是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 在舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，使用者 (和角色) 並未與結構描述完全區分。 從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，結構描述就與角色完全分開。 這個新架構會反映在 CREATE APPLICATION ROLE 的行為上。 此陳述式會取代**sp_addapprole**。  
  
 若要維護與舊版的回溯相容性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]， **sp_addapprole**會執行下列動作：  
  
-   如果尚未有與應用程式角色同名的結構描述，就會建立這類結構描述。 新的結構描述是由應用程式角色所擁有，它會是應用程式角色的預設結構描述。  
  
-   如果已經有與應用程式角色同名的結構描述，該程序就會失敗。  
  
-   不會檢查密碼複雜性**sp_addapprole**。 但是，CREATE APPLICATION ROLE 會檢查密碼複雜性。  
  
 參數*密碼*儲存為單向雜湊。  
  
 **Sp_addapprole**預存程序無法從使用者定義交易內執行。  
  
> [!IMPORTANT]  
>  Microsoft ODBC**加密**選項不支援**SqlClient**。 可以的話，請提示使用者在執行階段輸入應用程式角色認證。 請避免將認證儲存在檔案中。 如果您必須保存認證，請利用 CryptoAPI 函數來加密認證。  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 ALTER ANY APPLICATION ROLE 權限。 如果尚未有與新角色同名以及同一個擁有者的結構描述，也會需要資料庫的 CREATE SCHEMA 權限。  
  
## <a name="examples"></a>範例  
 下列範例會將新的應用程式角色`SalesApp`密碼`x97898jLJfcooFUYLKm387gf3`到目前的資料庫。  
  
```  
EXEC sp_addapprole 'SalesApp', 'x97898jLJfcooFUYLKm387gf3' ;  
GO  
```  
  
## <a name="see-also"></a>請參閱  
 [建立應用程式角色 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)  
  
  
