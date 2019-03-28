---
title: sp_help_publication_access (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fb281923e5b6d48a23cb6aa3f60bf36bbe9764da
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531870"
---
# <a name="sphelppublicationaccess-transact-sql"></a>sp_help_publication_access (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
`[ @publication = ] 'publication'` 是要存取的發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
`[ @return_granted = ] 'return_granted'` 這是登入識別碼。 *return_granted*已**元**，預設值是 1。 如果**0**指定和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用驗證時，會傳回出現在 「 發行者 」，而不是在散發者端的可用登入。 如果**0**指定和使用 Windows 驗證、 登入未明確拒絕存取在 「 發行者 」 或 「 散發者 」 會傳回。  
  
`[ @login = ] 'login'` 這是標準安全性登入識別碼。 *登入*已**sysname**，預設值是**%**。  
  
`[ @initial_list = ] initial_list` 指定是否傳回含發行集存取權，或只是新成員加入至清單之前有存取權的所有成員。 *initial_list* bit，預設值是**0**。  
  
 **1**傳回的所有成員的資訊**sysadmin**固定的伺服器角色已存在時建立發行集，散發者端的有效登入，以及目前登入。  
  
 **0**傳回的所有成員的資訊**sysadmin**存在於發行集建立時以及所有使用者在發行集存取清單中的散發者端的有效登入沒有與固定的伺服器角色屬於**sysadmin**固定的伺服器角色。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**Loginname**|**nvarchar(256)**|實際的登入名稱。|  
|**isntname**|**int**|**0** = 登入不是 Windows 使用者。<br /><br /> **1** = 登入是 Windows 使用者。|  
|**Isntgroup**|**int**|**0** = 登入不是 Windows 群組。<br /><br /> **1** = 登入是 Windows 群組。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_help_publication_access**用於所有類型的複寫。  
  
 時兩者**Isntname**並**Isntgroup**在結果集都是**0**，則會假設登入為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_help_publication_access**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_grant_publication_access &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)   
 [sp_revoke_publication_access &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
