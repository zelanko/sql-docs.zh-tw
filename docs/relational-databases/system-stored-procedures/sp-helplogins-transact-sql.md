---
title: "sp_helplogins (TRANSACT-SQL) |Microsoft 文件"
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
- sp_helplogins_TSQL
- sp_helplogins
dev_langs: TSQL
helpviewer_keywords: sp_helplogins
ms.assetid: f9ad3767-5b9f-420d-8922-b637811404f7
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 75e0521889f38db02bfdc9eabd3332d3fa76afb9
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
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
 [  **@LoginNamePattern =** ] **'***登入***'**  
 這是登入名稱。 *登入*是**sysname**，預設值是 NULL。 *登入*指定必須存在。 如果*登入*是未指定，會傳回有關所有登入資訊。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 第一份報表包含有關指定之每一項登入的資訊，如下表所示。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|登入名稱。|  
|**SID**|**varbinary(85)**|登入安全性識別碼 (SID)。|  
|**DefDBName**|**sysname**|預設資料庫**LoginName**連接到的執行個體時，會使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**DefLangName**|**sysname**|所使用的預設語言**LoginName**。|  
|**Auser**|**char(5)**|Yes = **LoginName**資料庫中具有相關聯的使用者名稱。<br /><br /> 否 = **LoginName**沒有相關聯的使用者名稱。|  
|**Xxxxx**|**char(7)**|Yes = **LoginName**具有相關聯的遠端登入。<br /><br /> 否 = **LoginName**沒有相關聯的登入。|  
  
 第二份報表包含有關對應到每一項登入的使用者以及登入的角色成員資格等資訊，如下表所示。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|登入名稱。|  
|**DBName**|**sysname**|預設資料庫**LoginName**連接到的執行個體時，會使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**UserName**|**sysname**|使用者帳戶**LoginName**對應到在**DBName**，和角色， **LoginName**是在屬於**DBName**。|  
|**UserOrAlias**|**char （8)**|MemberOf = **UserName**是角色。<br /><br /> 使用者 = **UserName**是使用者帳戶。|  
  
## <a name="remarks"></a>備註  
 之前先移除登入，使用**sp_helplogins**識別對應至登入的使用者帳戶。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**securityadmin**固定的伺服器角色。  
  
 若要找出所有的使用者帳戶對應到給定的登入， **sp_helplogins**必須檢查伺服器內的所有資料庫。 因此，對於伺服器上的每一個資料庫，至少下列其中一個條件必須為真：  
  
-   使用者執行**sp_helplogins**有權存取資料庫。  
  
-   **客體**資料庫中啟用使用者帳戶。  
  
 如果**sp_helplogins**無法存取資料庫， **sp_helplogins**會傳回資訊及顯示錯誤訊息 15622。  
  
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
  
## <a name="see-also"></a>請參閱  
 [安全性預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_helpdb &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sp_helpuser &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
