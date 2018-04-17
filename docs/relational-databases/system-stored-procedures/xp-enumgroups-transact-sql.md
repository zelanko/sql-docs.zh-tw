---
title: xp_enumgroups (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xp_enumgroups_TSQL
- xp_enumgroups
dev_langs:
- TSQL
helpviewer_keywords:
- xp_enumgroups
ms.assetid: 0bd3ed36-e260-469c-a5ff-b033fb9ea59d
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8c36dc60e01a42d94b279193216b2d861c9dda95
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="xpenumgroups-transact-sql"></a>xp_enumgroups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供本機 Microsoft Windows 群組的清單或在特定 Windows 網域中定義的全域群組清單。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_enumgroups [ 'domain_name' ]  
```  
  
## <a name="arguments"></a>引數  
 **'** *domain_name* **'**  
 這是要列舉全域群組清單的 Windows 網域名稱。 *domain_name*是**sysname**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**群組**|**sysname**|Windows 群組的名稱|  
|**註解**|**sysname**|Windows 提供的 Windows 群組描述|  
  
## <a name="remarks"></a>備註  
 如果*domain_name*是與 Windows 型電腦的名稱，執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是指定執行，或沒有網域名稱，則**xp_enumgroups**列舉從電腦的本機群組執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 **xp_enumgroups**的執行個體時，無法使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Windows 98 上執行。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**db_owner**固定的資料庫角色中**主要**資料庫或中的成員資格**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 下列範例會列出 `sales` 網域中的群組。  
  
```  
EXEC xp_enumgroups 'sales';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [一般擴充預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_loginconfig &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
