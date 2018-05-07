---
title: sp_add_category (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_category
- sp_add_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_category
ms.assetid: 6cca32cd-d941-4378-aed6-a7c90cb7520a
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d6f98fd4dbccc6b47297c8b0ebb2073dd23d35c6
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="spaddcategory-transact-sql"></a>sp_add_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將作業、警示或操作員的指定類別目錄加入伺服器中。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_add_category   
     [ [ @class = ] 'class', ]   
     [ [ @type = ] 'type', ]   
     { [ @name = ] 'name' }  
```  
  
## <a name="arguments"></a>引數  
 [  **@class =** ] **'***類別***'**  
 要加入之類別目錄的類別。 *類別*是**varchar(8)** 預設值是 JOB，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|JOB|加入作業類別目錄。|  
|ALERT|加入警示類別目錄。|  
|OPERATOR|加入操作員類別目錄。|  
  
 [ **@type =** ] **'***type***'**  
 要加入之類別目錄的類型。 *型別*是**varchar(12)**，預設值是**本機**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|LOCAL|本機作業類別目錄。|  
|多伺服器|多伺服器作業類別目錄。|  
|無|作業以外的類別分類**。**|  
  
 [ **@name =** ] **'***name***'**  
 要加入的類別目錄名稱。 在指定的類別內，這個名稱必須是唯一的。 *名稱*是**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 **sp_add_category**必須從執行**msdb**資料庫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色可以執行**sp_add_category**。  
  
## <a name="examples"></a>範例  
 下列範例會建立名稱為 `AdminJobs` 的本機作業類別目錄。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_category  
    @class=N'JOB',  
    @type=N'LOCAL',  
    @name=N'AdminJobs' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_delete_category &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [sp_help_category &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [sp_update_category &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [dbo.sysjobs & #40;TRANSACT-SQL & #41;](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)   
 [dbo.sysjobservers &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
