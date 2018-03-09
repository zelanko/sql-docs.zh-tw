---
title: "sp_restoremergeidentityrange (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
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
- sp_restoremergeidentityrange_TSQL
- sp_restoremergeidentityrange
helpviewer_keywords:
- sp_restoremergeidentityrange
ms.assetid: 7923e422-2748-40c0-b5a8-6410c48d5b70
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a42807009ffd42b16fe08fde76b7f91e34d62742
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sprestoremergeidentityrange-transact-sql"></a>sp_restoremergeidentityrange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這個預存程序用來更新識別範圍的指派。 它會確定自動識別範圍管理在發行者從備份還原之後，有正常運作。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_restoremergeidentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@publication**  =] **'***發行集***'**  
 這是發行集的名稱。 *發行集*是**sysname**，預設值是**所有**。 當指定時，只有該發行集的識別範圍才會還原。  
  
 [  **@article**  =] **'***文章***'**  
 這是發行項的名稱。 *發行項*是**sysname**，預設值是**所有**。 當指定時，只有該發行項的識別範圍才會還原。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_restoremergeidentityrange**用於合併式複寫。  
  
 **sp_restoremergeidentityrange**從散發者取得最大的識別範圍配置資訊，並更新中的值**max_used**資料行[MSmerge_identity_range_allocations & #40。TRANSACT-SQL &#41;](../../relational-databases/system-tables/msmerge-identity-range-allocations-transact-sql.md)之發行項使用自動識別範圍管理。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_restoremergeidentityrange**。  
  
## <a name="see-also"></a>請參閱＜  
 [sp_addmergearticle &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [複寫識別欄位](../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  
