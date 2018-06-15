---
title: sp_help_publication_access (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_help_publication_access
- sp_help_publication_access_TSQL
helpviewer_keywords:
- sp_help_publication_access
ms.assetid: 9408fa13-54a0-4cb1-8fb0-845e5536ef50
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: f4a8503a1c93283c2af8e6b4e2494cfdaff632b2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32995605"
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
 [ **@publication=**] **'***publication***'**  
 這是要存取的發行集名稱。 *發行集*是**sysname**，沒有預設值。  
  
 [  **@return_granted=**] **'***return_granted***'**  
 這是登入識別碼。 *return_granted*是**元**，預設值是 1。 如果**0**指定和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用驗證，則會傳回出現在 「 發行者 」，但不是在散發者端的可用登入。 如果**0**指定和使用 Windows 驗證、 登入未明確拒絕存取 「 發行者 」 或 「 散發者 」 會傳回。  
  
 [  **@login=**] **'***登入***'**  
 這是標準安全性登入識別碼。 *登入*是**sysname**，預設值是**%**。  
  
 [  **@initial_list =**] *initial_list*  
 指定傳回含發行集存取權的所有成員，或只傳回在新成員加入清單之前有存取權的成員。 *initial_list* bit，預設值是**0**。  
  
 **1**傳回資訊的所有成員**sysadmin**固定的伺服器角色已存在發行集建立時，散發者端的有效登入，以及目前登入。  
  
 **0**傳回資訊的所有成員**sysadmin**時建立發行集以及為所有使用者在發行集存取清單中，存在於散發者端的有效登入並不固定的伺服器角色屬於**sysadmin**固定的伺服器角色。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**Loginname**|**nvarchar(256)**|實際的登入名稱。|  
|**Isntname**|**int**|**0** = 登入不是 Windows 使用者。<br /><br /> **1** = 登入是 Windows 使用者。|  
|**Isntgroup**|**int**|**0** = 登入不是 Windows 群組。<br /><br /> **1** = 登入是 Windows 群組。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_help_publication_access**用於所有複寫類型。  
  
 當同時**Isntname**和**Isntgroup**在結果集是**0**，則會假設登入為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_help_publication_access**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_grant_publication_access &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)   
 [sp_revoke_publication_access &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
