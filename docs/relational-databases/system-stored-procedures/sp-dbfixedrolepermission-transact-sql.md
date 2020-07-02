---
title: sp_dbfixedrolepermission （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbfixedrolepermission
- sp_dbfixedrolepermission_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbfixedrolepermission
ms.assetid: b8c30191-f532-49cd-83f3-c271f63ce572
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 52aeca25fd6fcf112adcb2410269fdcb1c049a52
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771144"
---
# <a name="sp_dbfixedrolepermission-transact-sql"></a>sp_dbfixedrolepermission (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  顯示固定資料庫角色的權限。 **sp_dbfixedrolepermission**會在中傳回正確的資訊 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 。 輸出不會反映 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中實作的權限階層變更。 如需詳細資訊，請參閱[資料庫層級角色](../../relational-databases/security/authentication-access/database-level-roles.md#fixed-database-roles)，這會顯示固定資料庫角色的清單及其對應的許可權。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dbfixedrolepermission [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @rolename = ] 'role'`這是有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定資料庫角色的名稱。 *role*是**sysname**，預設值是 Null。 如果未指定*role* ，則會顯示所有固定資料庫角色的許可權。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**DbFixedRole**|**sysname**|固定資料庫角色的名稱|  
|**權限**|**Nvarchar （70）**|與**DbFixedRole**相關聯的許可權|  
  
## <a name="remarks"></a>備註  
 若要顯示固定資料庫角色的清單，請執行**sp_helpdbfixedrole**。 下表顯示固定資料庫角色。  
  
|固定資料庫角色|描述|  
|-------------------------|-----------------|  
|**db_owner**|資料庫擁有者|  
|**db_accessadmin**|資料庫存取管理員|  
|**db_securityadmin**|資料庫安全性管理員|  
|**db_ddladmin**|資料庫資料定義語言 (DDL) 管理員|  
|**db_backupoperator**|資料庫備份操作員|  
|**db_datareader**|資料庫資料讀取器|  
|**db_datawriter**|資料庫資料寫入器|  
|**db_denydatareader**|資料庫拒絕資料讀取器|  
|**db_denydatawriter**|資料庫拒絕資料寫入器|  
  
 **Db_owner**固定資料庫角色的成員具有所有其他固定資料庫角色的許可權。 若要顯示固定伺服器角色的許可權，請執行**sp_srvrolepermission**。  
  
 結果集包括可以執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，以及資料庫角色成員可以執行的其他特殊活動。  
  
## <a name="permissions"></a>權限  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列查詢會傳回所有固定資料庫角色的權限，因為該查詢未指定固定資料庫角色。  
  
```  
EXEC sp_dbfixedrolepermission;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的安全性預存程式](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helpdbfixedrole &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql.md)   
 [sp_srvrolepermission &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
