---
title: sp_helpdbfixedrole （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpdbfixedrole
- sp_helpdbfixedrole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdbfixedrole
ms.assetid: ad87e9a0-b901-4e37-9950-aa517d680fc3
author: stevestein
ms.author: sstein
ms.openlocfilehash: dc461bcd1b5adbbc64b2eadaa4bb55af690ea88a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68123833"
---
# <a name="sp_helpdbfixedrole-transact-sql"></a>sp_helpdbfixedrole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回固定資料庫角色的清單。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpdbfixedrole [ [ @rolename = ] 'role' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @rolename = ] 'role'`這是固定資料庫角色的名稱。 *role*是**sysname**，預設值是 Null。 如果指定*role* ，則只會傳回該角色的相關資訊;否則，會傳回所有固定資料庫角色的清單和描述。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**DbFixedRole**|**sysname**|固定資料庫角色的名稱。|  
|**說明**|**Nvarchar （70）**|DbFixedRole 的描述 **。**|  
  
## <a name="remarks"></a>備註  
 固定資料庫角色 (如下表所示) 是在資料庫層級定義的，且擁有執行特定資料庫層級管理活動的權限。 您無法加入或移除固定資料庫角色， 且無法變更對固定資料庫角色授與的權限。  
  
|固定資料庫角色|描述|  
|-------------------------|-----------------|  
|**db_owner**|資料庫擁有者|  
|**db_accessadmin**|資料庫存取管理員|  
|**db_securityadmin**|資料庫安全性管理員|  
|**db_ddladmin**|資料庫 DDL 管理員|  
|**db_backupoperator**|資料庫備份操作員|  
|**db_datareader**|資料庫資料讀取器|  
|**db_datawriter**|資料庫資料寫入器|  
|**db_denydatareader**|資料庫拒絕資料讀取器|  
|**db_denydatawriter**|資料庫拒絕資料寫入器|  
  
 下表顯示用來修改資料庫角色的預存程序。  
  
|預存程序|動作|  
|----------------------|------------|  
|**sp_addrolemember**|將資料庫使用者加入至固定資料庫角色。|  
|**sp_helprole**|顯示固定資料庫角色成員的清單。|  
|**sp_droprolemember**|從固定資料庫角色中移除成員。|  
  
## <a name="permissions"></a>權限  
 需要 **public** 角色的成員資格。  
  
 傳回的資訊受限於中繼資料存取限制。 主體對其沒有權限的實體不會出現。  如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>範例  
 下列範例會顯示所有固定資料庫角色的清單。  
  
```  
EXEC sp_helpdbfixedrole;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的安全性預存程式](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_dbfixedrolepermission &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql.md)   
 [sp_droprolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helprole &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helprolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
