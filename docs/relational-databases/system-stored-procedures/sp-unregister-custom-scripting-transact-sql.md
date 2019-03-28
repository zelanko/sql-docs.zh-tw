---
title: sp_unregister_custom_scripting (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_unregister_custom_scripting_TSQL
- sp_unregister_custom_scripting
helpviewer_keywords:
- sp_unregister_custom_scripting
ms.assetid: b6e9e0d2-9144-434d-88af-4874f2582399
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e3d9af0e5eff8aff2715ff2be6caa1757702fb8b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529560"
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
`[ @type = ] 'type'` 正在移除自訂預存程序或指令碼的型別。 *型別*已**varchar(16)**，沒有預設值，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**insert**|註冊的自訂預存程序或指令碼，是在複寫 INSERT 陳述式時執行。|  
|**update**|註冊的自訂預存程序或指令碼，是在複寫 UPDATE 陳述式時執行。|  
|**delete**|註冊的自訂預存程序或指令碼，是在複寫 DELETE 陳述式時執行。|  
|**custom_script**|註冊的自訂預存程序或指令碼，是在資料定義語言 (DDL) 觸發程序結尾執行。|  
  
`[ @publication = ] 'publication'` 要移除的自訂預存程序或指令碼的發行集的名稱。 *發行集*已**sysname**，預設值是 NULL。  
  
`[ @article = ] 'article'` 正在移除的自訂預存程序或指令碼的發行項名稱。 *發行項*已**sysname**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_unregister_custom_scripting**用於快照式和異動複寫。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定伺服器角色**db_owner**固定資料庫角色，或有**db_ddladmin**固定的資料庫角色可以執行**sp_unregister_custom_scripting**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_register_custom_scripting &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)  
  
  
