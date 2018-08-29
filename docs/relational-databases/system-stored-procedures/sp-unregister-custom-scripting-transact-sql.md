---
title: sp_unregister_custom_scripting (TRANSACT-SQL) |Microsoft Docs
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
- sp_unregister_custom_scripting_TSQL
- sp_unregister_custom_scripting
helpviewer_keywords:
- sp_unregister_custom_scripting
ms.assetid: b6e9e0d2-9144-434d-88af-4874f2582399
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a62df4743139a976a5571b07b762127e95c6d5c3
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43037801"
---
# <a name="spunregistercustomscripting-transact-sql"></a>sp_unregister_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這個預存程序會移除使用者定義自訂預存程序或[!INCLUDE[tsql](../../includes/tsql-md.md)]所註冊的執行指令碼檔案[sp_register_custom_scripting](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_unregister_custom_scripting [ @type  = ] 'type'  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@type** =] **'***型別***'**  
 這是要移除之自訂預存程序或指令碼的類型。 *型別*已**varchar(16)**，沒有預設值，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**insert**|註冊的自訂預存程序或指令碼，是在複寫 INSERT 陳述式時執行。|  
|**更新**|註冊的自訂預存程序或指令碼，是在複寫 UPDATE 陳述式時執行。|  
|**delete**|註冊的自訂預存程序或指令碼，是在複寫 DELETE 陳述式時執行。|  
|**custom_script**|註冊的自訂預存程序或指令碼，是在資料定義語言 (DDL) 觸發程序結尾執行。|  
  
 [ **@publication** = ] **'***publication***'**  
 要移除之自訂預存程序或指令碼的發行集名稱。 *發行集*已**sysname**，預設值是 NULL。  
  
 [ **@article** =] **'***文章***'**  
 要移除之自訂預存程序或指令碼的發行項名稱。 *發行項*已**sysname**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_unregister_custom_scripting**用於快照式和異動複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定伺服器角色**db_owner**固定資料庫角色，或有**db_ddladmin**固定的資料庫角色可以執行**sp_unregister_custom_scripting**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_register_custom_scripting &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)  
  
  
