---
title: sp_dbfixedrolepermission (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_dbfixedrolepermission
- sp_dbfixedrolepermission_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbfixedrolepermission
ms.assetid: b8c30191-f532-49cd-83f3-c271f63ce572
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 32ca47ff848d735c9310d894eff46c94b0c8da92
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33239678"
---
# <a name="spdbfixedrolepermission-transact-sql"></a>sp_dbfixedrolepermission (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示固定資料庫角色的權限。 **sp_dbfixedrolepermission**傳回正確的資訊[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]。 輸出不會反映 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中實作的權限階層變更。 如需詳細資訊，請參閱[權限&#40;Database Engine&#41;](../../relational-databases/security/permissions-database-engine.md)。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dbfixedrolepermission [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@rolename =** ] **'***角色***'**  
 這是有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定資料庫角色名稱。 *角色*是**sysname**，預設值是 NULL。 如果*角色*未指定，會顯示所有固定的資料庫角色的權限。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**DbFixedRole**|**sysname**|固定資料庫角色的名稱|  
|**權限**|**nvarchar （70)**|與相關聯的權限**DbFixedRole**|  
  
## <a name="remarks"></a>備註  
 若要顯示固定的資料庫角色的清單，請執行**sp_helpdbfixedrole**。 下表顯示固定資料庫角色。  
  
|固定資料庫角色|Description|  
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
  
 成員**db_owner**固定的資料庫角色具有所有其他固定的資料庫角色的權限。 若要顯示固定的伺服器角色的權限，請執行**sp_srvrolepermission**。  
  
 結果集包括可以執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，以及資料庫角色成員可以執行的其他特殊活動。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列查詢會傳回所有固定資料庫角色的權限，因為該查詢未指定固定資料庫角色。  
  
```  
EXEC sp_dbfixedrolepermission;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprolemember & #40;TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helpdbfixedrole &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql.md)   
 [sp_srvrolepermission &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
