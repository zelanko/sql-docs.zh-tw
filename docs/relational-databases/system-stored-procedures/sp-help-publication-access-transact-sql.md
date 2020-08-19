---
description: sp_help_publication_access (Transact-SQL)
title: sp_help_publication_access (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_publication_access
- sp_help_publication_access_TSQL
helpviewer_keywords:
- sp_help_publication_access
ms.assetid: 9408fa13-54a0-4cb1-8fb0-845e5536ef50
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5a40f12ade4dcbb08609da6184fa0a96ca9926cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485981"
---
# <a name="sp_help_publication_access-transact-sql"></a>sp_help_publication_access (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  傳回發行集所有已授與之登入的清單。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_publication_access [ @publication = ] 'publication'  
    [ , [ @return_granted = ] 'return_granted' ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @initial_list = ] initial_list ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是要存取的發行集名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @return_granted = ] 'return_granted'` 這是登入識別碼。 *return_granted* 是 **bit**，預設值是1。 如果指定 **0** ，且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用驗證，則會傳回出現在發行者端但不在散發者端的可用登入。 如果指定 **0** ，且使用 Windows 驗證，則會傳回「發行者」或「散發者」端未明確拒絕存取的登入。  
  
`[ @login = ] 'login'` 這是標準安全性登入識別碼。 *login* 是 **sysname**，預設值是 **%** 。  
  
`[ @initial_list = ] initial_list` 指定是否要傳回具有發行集存取權的所有成員，或只傳回在新成員加入清單之前有存取權的成員。 *initial_list* 是 bit，預設值是 **0**。  
  
 **1** 會傳回 **系統管理員（sysadmin** ）固定伺服器角色的所有成員的資訊，在建立發行集時存在的散發者端具有有效的登入，以及目前的登入。  
  
 **0** 會傳回 **系統管理員（sysadmin** ）固定伺服器角色的所有成員的資訊，在散發者端建立發行集時，以及發行集存取清單中的所有使用者都不屬於 **系統管理員（sysadmin** ）固定伺服器角色的所有使用者，都會傳回這些成員的有效登入。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**Loginname**|**nvarchar(256)**|實際的登入名稱。|  
|**Isntname**|**int**|**0** = 登入不是 Windows 使用者。<br /><br /> **1** = 登入是 Windows 使用者。|  
|**Isntgroup**|**int**|**0** = 登入不是 Windows 群組。<br /><br /> **1** = 登入是 Windows 群組。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_help_publication_access** 用於所有類型的複寫中。  
  
 當結果集中的 **Isntname** 和 **Isntgroup** 都是 **0**時，會假設登入為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_help_publication_access**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_grant_publication_access &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)   
 [sp_revoke_publication_access &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
