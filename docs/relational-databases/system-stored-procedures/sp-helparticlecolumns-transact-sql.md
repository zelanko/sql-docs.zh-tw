---
title: sp_helparticlecolumns (TRANSACT-SQL) |Microsoft Docs
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
- sp_helparticlecolumns
- sp_helparticlecolumns_TSQL
helpviewer_keywords:
- sp_helparticlecolumns
ms.assetid: 9ea55df3-2e99-4683-88ad-bde718288bc7
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6847491bbf8cbf517478ab6cb620f158577ca3e3
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43034320"
---
# <a name="sphelparticlecolumns-transact-sql"></a>sp_helparticlecolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回基礎資料表的所有資料行。 這個預存程序執行於發行集資料庫的發行者端。 如果是 Oracle 發行者，這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helparticlecolumns [ @publication = ] 'publication'   
        , [ @article = ] 'article'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@publication =**] **'***發行集***'**  
 這是發行項所在的發行集名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [  **@article=**] **'***文章***'**  
 這是傳回具有資料行的發行項名稱。 *發行項*已**sysname**，沒有預設值。  
  
 [ **@publisher**=] **'***發行者***'**  
 指定非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *發行者*已**sysname**，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*不應指定當要求的發行項由發佈[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （未發行的資料行） 或**1** （發行的資料行）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**資料行識別碼**|**int**|資料行的識別碼。|  
|**column**|**sysname**|資料行的名稱。|  
|**發行**|**bit**|資料行是否已發行：<br /><br /> **0** = 否<br /><br /> **1** = 是|  
|**發行者類型**|**sysname**|在發行者端之資料行的資料類型。|  
|**訂閱者類型**|**sysname**|在訂閱者端之資料行的資料類型。|  
  
## <a name="remarks"></a>備註  
 **sp_helparticlecolumns**用於快照式和異動複寫。  
  
 **sp_helparticlecolumns**可用於檢查垂直資料分割。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定伺服器角色**db_owner**固定的資料庫角色或目前發行集之發行集存取清單能夠執行**sp_helparticlecolumns**.  
  
## <a name="see-also"></a>另請參閱  
 [定義及修改資料行篩選](../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)   
 [sp_addarticle &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_droppublication &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
