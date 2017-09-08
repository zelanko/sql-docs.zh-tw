---
title: "ORIGINAL_LOGIN (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ORIGINAL_LOGIN_TSQL
- ORIGINAL_LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], context switches
- context switching [SQL Server], login names
- original login names [SQL Server]
- ORIGINAL_LOGIN function
- names [SQL Server], logins
ms.assetid: ddfb0991-cde3-4b97-a5b7-ee450133f160
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b1f97da47505e5c812e43f4481d9f36027bf14c9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="originallogin-transact-sql"></a>ORIGINAL_LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的登入名稱。 您可以利用這個函數來傳回有許多明確或隱含內容切換的工作階段中原始登入的識別。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ORIGINAL_LOGIN( )  
```  
  
## <a name="return-types"></a>傳回類型  
 **sysname**  
  
## <a name="remarks"></a>備註  
 這個函數在稽核原始連接內容的識別時很有用。 而這類函數[SESSION_USER](../../t-sql/functions/session-user-transact-sql.md)和[CURRENT_USER](../../t-sql/functions/current-user-transact-sql.md)傳回目前的執行內容，ORIGINAL_LOGIN 會傳回第一次連接到的執行個體的登入身分識別[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]於該工作階段。  
  
 會傳回 NULL 上[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
## <a name="examples"></a>範例  
 下列範例會將目前工作階段的執行內容從陳述式的呼叫端切換到 `login1`。 `SUSER_SNAME` 和 `ORIGINAL_LOGIN` 函數用來傳回目前工作階段使用者 (內容切換後的使用者)，以及原始登入帳戶。  
  
```  
USE AdventureWorks2012;  
GO  
--Create a temporary login and user.  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE USER user1 FOR LOGIN login1;  
GO  
--Execute a context switch to the temporary login account.  
DECLARE @original_login sysname;  
DECLARE @current_context sysname;  
EXECUTE AS LOGIN = 'login1';  
SET @original_login = ORIGINAL_LOGIN();  
SET @current_context = SUSER_SNAME();  
SELECT 'The current executing context is: '+ @current_context;  
SELECT 'The original login in this session was: '+ @original_login  
GO  
-- Return to the original execution context  
-- and remove the temporary principal.  
REVERT;  
GO  
DROP LOGIN login1;  
DROP USER user1;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [執行 AS &#40;TRANSACT-SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [還原 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/revert-transact-sql.md)  
  
  
