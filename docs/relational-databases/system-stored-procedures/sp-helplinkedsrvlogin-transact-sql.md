---
title: sp_helplinkedsrvlogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helplinkedsrvlogin_TSQL
- sp_helplinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplinkedsrvlogin
ms.assetid: a2b1eba0-bf71-47e7-a4c7-9f55feec82a3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 32d7d0098c5548666b1d2fc77e11f82c2c3fd5fe
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536850"
---
# <a name="sphelplinkedsrvlogin-transact-sql"></a>sp_helplinkedsrvlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供對特定連結伺服器 (用於分散式查詢與遠端預存程序) 所定義登入對應的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helplinkedsrvlogin [ [ @rmtsrvname = ] 'rmtsrvname' ]   
     [ , [ @locallogin = ] 'locallogin' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @rmtsrvname = ] 'rmtsrvname'` 是登入對應所套用的連結伺服器的名稱。 *rmtsrvname&lt*已**sysname**，預設值是 NULL。 如果是 NULL，會傳回對所有連結伺服器 (定義於執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本機電腦中) 定義的所有登入對應。  
  
`[ @locallogin = ] 'locallogin'` 已[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是對應至連結伺服器的本機伺服器登入*rmtsrvname&lt*。 *locallogin*已**sysname**，預設值是 NULL。 NULL 可讓您指定在定義的所有登入對應*rmtsrvname&lt*會傳回。 如果不是 NULL 的對應*locallogin*要*rmtsrvname&lt*必須已經存在。 *locallogin*可以是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入或 Windows 使用者。 必須以直接方式或透過其被授與存取權限之 Windows 群組的成員資格，來授與 Windows 使用者存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的權限。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**連結的伺服器**|**sysname**|連結伺服器名稱。|  
|**本機登入**|**sysname**|對應所套用的本機登入。|  
|**自我對應**|**smallint**|0 =**本機登入**對應至**遠端登入**當連接到**連結的伺服器**。<br /><br /> 1 =**本機登入**會對應至相同的登入和密碼連接到**連結的伺服器**。|  
|**遠端登入**|**sysname**|在 登入名稱**LinkedServer**對應至**LocalLogin**時**IsSelfMapping**為 0。 如果**IsSelfMapping**為 1，這**RemoteLogin**是 NULL。|  
  
## <a name="remarks"></a>備註  
 刪除登入對應之前，請使用**sp_helplinkedsrvlogin**來判斷所涉及的連結的伺服器。  
  
## <a name="permissions"></a>Permissions  
 不檢查任何權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-displaying-all-login-mappings-for-all-linked-servers"></a>A. 顯示所有連結伺服器的所有登入對應  
 下列範例會顯示定義於執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本機電腦之所有連結伺服器的所有登入對應。  
  
```  
EXEC sp_helplinkedsrvlogin;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Accounts         NULL          1               NULL  
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
Marketing        NULL          1               NULL  
  
(4 row(s) affected)  
```  
  
### <a name="b-displaying-all-login-mappings-for-a-linked-server"></a>B. 顯示某個連結伺服器的所有登入對應  
 下列範例會顯示 `Sales` 連結伺服器之所有定義於本機的登入對應。  
  
```  
EXEC sp_helplinkedsrvlogin 'Sales';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
  
(2 row(s) affected)  
```  
  
### <a name="c-displaying-all-login-mappings-for-a-local-login"></a>C. 顯示本機登入的所有登入對應  
 下列範例會顯示登入 `Mary` 之所有定義於本機的登入對應。  
  
```  
EXEC sp_helplinkedsrvlogin NULL, 'Mary';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
  
(2 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
