---
title: sp_helpmergearticleconflicts (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- sp_helpmergearticleconflicts
- sp_helpmergearticleconflicts_TSQL
helpviewer_keywords:
- sp_helpmergearticleconflicts
ms.assetid: 4678a2b9-9a5f-4193-a20d-2e11fc896c3a
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9fb4fe8ff1dadebe5f2bb2a7af5209c2e761e0af
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43037301"
---
# <a name="sphelpmergearticleconflicts-transact-sql"></a>sp_helpmergearticleconflicts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回發行集中發生衝突的發行項。 這個預存程序執行於發行集資料庫的發行者端，或合併訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpmergearticleconflicts [ [ @publication = ] 'publication' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publsher_db' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@publication=**] **'***publication***'**  
 為合併式發行集的名稱。*出版物*是**sysname**，預設值是**%**，它會傳回所有發行項有衝突的資料庫中。  
  
 [ **@publisher=**] **'***publisher***'**  
 是 「 發行者 」 的名稱。*發行者*是**sysname**，預設值是 NULL。  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 是發行者資料庫的名稱。*publisher_db*是**sysname**，預設值是 NULL。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**article**|**sysname**|發行項的名稱。|  
|**source_owner**|**sysname**|來源物件的擁有者。|  
|**source_object**|**nvarchar(386)**|來源物件的名稱。|  
|**conflict_table**|**nvarchar(258)**|儲存插入或更新衝突的資料表名稱。|  
|**guidcolname**|**sysname**|來源物件的 RowGuidCol 名稱。|  
|**centralized_conflicts**|**int**|是否將衝突記錄儲存在給定的發行者。|  
  
 如果發行項只有刪除衝突，且沒有**conflict_table**資料列的名稱**conflict_table**結果集為 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpmergearticleconflicts**用於合併式複寫中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色並**db_owner**固定的資料庫角色可以執行**sp_helpmergearticleconflicts**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
