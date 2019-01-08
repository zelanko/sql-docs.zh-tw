---
title: sp_add_category (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_category
- sp_add_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_category
ms.assetid: 6cca32cd-d941-4378-aed6-a7c90cb7520a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 295f29b86e53a8d58622e4c79c1b36734acdbe3e
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591012"
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
 [  **@class =** ] **'**_類別_**'**  
 要加入之類別目錄的類別。 *類別*已**varchar(8)** 預設值是 JOB，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|JOB|加入作業類別目錄。|  
|ALERT|加入警示類別目錄。|  
|OPERATOR|加入操作員類別目錄。|  
  
 [  **@type =** ] **'**_型別_**'**  
 要加入之類別目錄的類型。 *型別*已**varchar(12)**，預設值是**本機**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|LOCAL|本機作業類別目錄。|  
|多伺服器|多伺服器作業類別目錄。|  
|無|工作以外的類別分類 **。**|  
  
 [  **@name =** ] **'**_名稱_**'**  
 要加入的類別目錄名稱。 在指定的類別內，這個名稱必須是唯一的。 *名稱*已**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
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
 [sp_delete_category &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [sp_help_category &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-help-category-transact-sql.md)   
 [sp_update_category &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [dbo.sysjobs &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)   
 [dbo.sysjobservers &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysjobservers-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
