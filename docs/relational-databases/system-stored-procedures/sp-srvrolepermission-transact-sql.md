---
title: sp_srvrolepermission (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_srvrolepermission_TSQL
- sp_srvrolepermission
dev_langs:
- TSQL
helpviewer_keywords:
- sp_srvrolepermission
ms.assetid: 5709667f-e3e4-48a2-93ec-af5e22a2ac58
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a4ed3adb1fe62d3ad23a58bca3a1dedce86dabee
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43033116"
---
# <a name="spsrvrolepermission-transact-sql"></a>sp_srvrolepermission (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示固定伺服器角色的權限。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_srvrolepermission [ [ @srvrolename = ] 'role']  
```  
  
## <a name="arguments"></a>引數  
 [  **@srvrolename =** ] **'***角色***'**  
 這是要傳回權限的固定伺服器角色名稱。 *角色*已**sysname**，預設值是 NULL。 如果未指定角色，則會傳回所有固定伺服器角色的權限。 *角色*可以有下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**sysadmin**|系統管理員|  
|**securityadmin**|安全性管理員|  
|**serveradmin**|伺服器管理員|  
|**setupadmin**|安裝管理員|  
|**processadmin**|處理序管理員|  
|**diskadmin**|磁碟管理員|  
|**dbcreator**|資料庫建立者|  
|**bulkadmin**|可以執行 BULK INSERT 陳述式|  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**伺服器角色**|**sysname**|固定伺服器角色的名稱|  
|**權限**|**sysname**|與相關聯的權限**ServerRole**|  
  
## <a name="remarks"></a>備註  
 列出的權限包括可以執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，以及固定伺服器角色成員可以執行的其他特殊活動。 若要顯示固定的伺服器角色的清單，請執行**sp_helpsrvrole**。  
  
 **Sysadmin**固定的伺服器角色擁有的所有其他固定的伺服器角色的權限。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列查詢會傳回與 `sysadmin` 固定伺服器角色相關聯的權限。  
  
```  
EXEC sp_srvrolepermission 'sysadmin';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [sp_helpsrvrole &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
