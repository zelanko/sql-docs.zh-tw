---
title: sp_helplogins (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b043b71ca3f0349ce8ed7ac7accf136f4b7eff60
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47595226"
---
# <a name="sphelplogins-transact-sql"></a>sp_helplogins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供有關每一個資料庫中的登入及其相關聯使用者的資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helplogins [ [ @LoginNamePattern = ] 'login' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@LoginNamePattern =** ] **'***login***'**  
 這是登入名稱。 *login* 是預設值為 NULL 的 **sysname**。 *登入*指定必須存在。 如果*登入*是未指定，會傳回有關所有登入資訊。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 第一份報表包含有關指定之每一項登入的資訊，如下表所示。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|登入名稱。|  
|**SID**|**varbinary(85)**|登入安全性識別碼 (SID)。|  
|**DefDBName**|**sysname**|預設資料庫**LoginName**執行個體的連接時所用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**DefLangName**|**sysname**|預設所使用的語言**LoginName**。|  
|**Auser**|**char(5)**|Yes = **LoginName**資料庫中具有相關聯的使用者名稱。<br /><br /> 否 = **LoginName**沒有相關聯的使用者名稱。|  
|**Xxxxx**|**char(7)**|Yes = **LoginName**具有相關聯的遠端登入。<br /><br /> 否 = **LoginName**沒有相關聯的登入。|  
  
 第二份報表包含有關對應到每一項登入的使用者以及登入的角色成員資格等資訊，如下表所示。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|登入名稱。|  
|**資料庫名稱**|**sysname**|預設資料庫**LoginName**執行個體的連接時所用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**UserName**|**sysname**|使用者帳戶**LoginName**會對應到在**DBName**，以及角色的**LoginName**中的成員**DBName**。|  
|**UserOrAlias**|**char(8)**|MemberOf = **UserName**是一種角色。<br /><br /> 使用者 = **UserName**是使用者帳戶。|  
  
## <a name="remarks"></a>備註  
 在之前移除登入，使用**sp_helplogins**識別對應至登入的使用者帳戶。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**securityadmin**固定的伺服器角色。  
  
 若要找出所有與指定的登入，對應的使用者帳戶**sp_helplogins**必須檢查伺服器內的所有資料庫。 因此，對於伺服器上的每一個資料庫，至少下列其中一個條件必須為真：  
  
-   正在執行的使用者**sp_helplogins**有權存取資料庫。  
  
-   **客體**使用者帳戶已啟用資料庫中。  
  
 如果**sp_helplogins**無法存取資料庫時， **sp_helplogins**會傳回一樣多的資訊，以及它可以顯示錯誤訊息 15622。  
  
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
 [sp_helpdb &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sp_helpuser &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
