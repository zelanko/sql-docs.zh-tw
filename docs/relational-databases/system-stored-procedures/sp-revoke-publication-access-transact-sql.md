---
title: "sp_revoke_publication_access (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_revoke_publication_access_TSQL
- sp_revoke_publication_access
helpviewer_keywords:
- sp_revoke_publication_access
ms.assetid: 84ed9e77-991f-4fa5-a21f-7c6bfec1b3e3
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b5f65077097b5ad19e1cec0e3a7380731ab1eb70
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sprevokepublicationaccess-transact-sql"></a>sp_revoke_publication_access (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從發行集存取清單中移除登入。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_revoke_publication_access [ @publication = ] 'publication' , [ @login = ] 'login'  
```  
  
## <a name="arguments"></a>引數  
 [  **@publication=**] **'***發行集***'**  
 這是要存取的發行集名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@login=**] **'***登入***'**  
 這是登入識別碼。 *登入*是**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_revoke_publication_access**用於快照式、 交易式和合併式複寫。  
  
 **sp_revoke_publication_access**可以重複呼叫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_revoke_publication_access**。  
  
## <a name="see-also"></a>請參閱＜  
 [sp_grant_publication_access &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)   
 [sp_help_publication_access &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-publication-access-transact-sql.md)   
 [保護發行者](../../relational-databases/replication/security/secure-the-publisher.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
