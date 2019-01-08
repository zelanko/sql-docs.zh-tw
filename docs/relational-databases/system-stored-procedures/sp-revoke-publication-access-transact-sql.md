---
title: sp_revoke_publication_access (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_revoke_publication_access_TSQL
- sp_revoke_publication_access
helpviewer_keywords:
- sp_revoke_publication_access
ms.assetid: 84ed9e77-991f-4fa5-a21f-7c6bfec1b3e3
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 3e2a52ca65288fa6dc00160ab36be5faf1f4aed6
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52808400"
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
 [ **@publication=**] **'***publication***'**  
 這是要存取的發行集名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [  **@login=**] **'***登入***'**  
 這是登入識別碼。 *登入*已**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_revoke_publication_access**用於快照式、 交易式和合併式複寫。  
  
 **sp_revoke_publication_access**可以重複呼叫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_revoke_publication_access**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_grant_publication_access &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)   
 [sp_help_publication_access &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-help-publication-access-transact-sql.md)   
 [保護發行者](../../relational-databases/replication/security/secure-the-publisher.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
