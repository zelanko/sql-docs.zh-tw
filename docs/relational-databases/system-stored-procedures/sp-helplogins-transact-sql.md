---
description: sp_helplogins (Transact-SQL)
title: sp_helplogins (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helplogins_TSQL
- sp_helplogins
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplogins
ms.assetid: f9ad3767-5b9f-420d-8922-b637811404f7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9802a6087bd3747c8fe715d56482b54149ee55d8
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549622"
---
# <a name="sp_helplogins-transact-sql"></a>sp_helplogins (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  提供有關每一個資料庫中的登入及其相關聯使用者的資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helplogins [ [ @LoginNamePattern = ] 'login' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @LoginNamePattern = ] 'login'` 這是登入名稱。 *login* 是預設值為 NULL 的 **sysname**。 如果有指定，*登*入必須存在。 如果未指定 login，則會傳回所有 *登* 入的相關資訊。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 第一份報表包含有關指定之每一項登入的資訊，如下表所示。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|登入名稱。|  
|**SID**|**varbinary(85)**|登入安全性識別碼 (SID)。|  
|**DefDBName**|**sysname**|**LoginName**連接到的實例時，所使用的預設資料庫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**DefLangName**|**sysname**|**LoginName**所使用的預設語言。|  
|**Auser**|**char (5) **|Yes = **LoginName** 在資料庫中有相關聯的使用者名稱。<br /><br /> No = **LoginName** 沒有相關聯的使用者名稱。|  
|**ARemote**|**char (7) **|Yes = **LoginName** 具有相關聯的遠端登入。<br /><br /> No = **LoginName** 沒有相關聯的登入。|  
  
 第二份報表包含有關對應到每一項登入的使用者以及登入的角色成員資格等資訊，如下表所示。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|登入名稱。|  
|**DBName**|**sysname**|**LoginName**連接到的實例時，所使用的預設資料庫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**UserName**|**sysname**|**LoginName**對應至**dbname**的使用者帳戶，以及**LoginName**是**dbname**成員的角色。|  
|**UserOrAlias**|**char (8) **|MemberOf = 使用者 **名稱** 是角色。<br /><br /> User = **UserName** 是使用者帳戶。|  
  
## <a name="remarks"></a>備註  
 移除登入之前，請使用 **sp_helplogins** 來識別對應至登入的使用者帳戶。  
  
## <a name="permissions"></a>權限  
 需要 **securityadmin** 固定伺服器角色中的成員資格。  
  
 若要識別對應至指定登入的所有使用者帳戶， **sp_helplogins** 必須檢查伺服器內的所有資料庫。 因此，對於伺服器上的每一個資料庫，至少下列其中一個條件必須為真：  
  
-   執行 **sp_helplogins** 的使用者有權存取資料庫。  
  
-   已在資料庫中啟用 **guest** 使用者帳戶。  
  
 如果 **sp_helplogins** 無法存取資料庫， **sp_helplogins** 會傳回最多的資訊，而且會顯示錯誤訊息15622。  
  
## <a name="examples"></a>範例  
 下列範例會報告有關登入者 `John` 的資訊。  
  
```  
EXEC sp_helplogins 'John';  
GO  
  
LoginName SID                        DefDBName DefLangName AUser ARemote   
--------- -------------------------- --------- ----------- ----- -------   
John      0x23B348613497D11190C100C  master    us_english  yes   no  
  
(1 row(s) affected)  
  
LoginName   DBName   UserName   UserOrAlias   
---------   ------   --------   -----------   
John        pubs     John       User          
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_helpdb &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sp_helpuser &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
