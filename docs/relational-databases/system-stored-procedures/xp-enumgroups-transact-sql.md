---
title: xp_enumgroups （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_enumgroups_TSQL
- xp_enumgroups
dev_langs:
- TSQL
helpviewer_keywords:
- xp_enumgroups
ms.assetid: 0bd3ed36-e260-469c-a5ff-b033fb9ea59d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 885e29f8abbeb185017bc2472566e41596a56900
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68116774"
---
# <a name="xp_enumgroups-transact-sql"></a>xp_enumgroups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供本機 Microsoft Windows 群組的清單或在特定 Windows 網域中定義的全域群組清單。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_enumgroups [ 'domain_name' ]  
```  
  
## <a name="arguments"></a>引數  
 **'** *domain_name* **'**  
 這是要列舉全域群組清單的 Windows 網域名稱。 *domain_name*是**sysname**，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**群組**|**sysname**|Windows 群組的名稱|  
|**加以**|**sysname**|Windows 提供的 Windows 群組描述|  
  
## <a name="remarks"></a>備註  
 如果*domain_name*是實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行所在之 Windows 電腦的名稱，或未指定功能變數名稱， **xp_enumgroups**會從執行的電腦列舉本機群組[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 **xp_enumgroups**當的實例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在 Windows 98 上執行時，無法使用 xp_enumgroups。  
  
## <a name="permissions"></a>權限  
 需要**master**資料庫中**db_owner**固定資料庫角色的成員資格，或**系統管理員（sysadmin** ）固定伺服器角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會列出 `sales` 網域中的群組。  
  
```  
EXEC xp_enumgroups 'sales';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_grantlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql 的一般擴充預存程式&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_loginconfig &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
