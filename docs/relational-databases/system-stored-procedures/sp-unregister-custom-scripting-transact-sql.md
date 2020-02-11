---
title: sp_unregister_custom_scripting （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: fe6bfe4c93ccabfaaec27739f7a1fd0e09348526
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68017906"
---
# <a name="sp_unregister_custom_scripting-transact-sql"></a>sp_unregister_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  這個預存程式會移除使用者定義的自訂預[!INCLUDE[tsql](../../includes/tsql-md.md)]存程式或腳本檔案，該檔案是藉由執行[sp_register_custom_scripting](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)來註冊。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_unregister_custom_scripting [ @type  = ] 'type'  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @type = ] 'type'`這是要移除之自訂預存程式或腳本的類型。 *類型*為**Varchar （16）**，沒有預設值，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**插入**|註冊的自訂預存程序或指令碼，是在複寫 INSERT 陳述式時執行。|  
|**更新**|註冊的自訂預存程序或指令碼，是在複寫 UPDATE 陳述式時執行。|  
|**delete**|註冊的自訂預存程序或指令碼，是在複寫 DELETE 陳述式時執行。|  
|**custom_script**|註冊的自訂預存程序或指令碼，是在資料定義語言 (DDL) 觸發程序結尾執行。|  
  
`[ @publication = ] 'publication'`要移除其自訂預存程式或腳本的發行集名稱。 *發行*集是**sysname**，預設值是 Null。  
  
`[ @article = ] 'article'`要移除之自訂預存程式或腳本的發行項名稱。 發行*項是* **sysname**，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_unregister_custom_scripting**用於快照式和異動複寫中。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色、 **db_owner**固定資料庫角色或**db_ddladmin**固定資料庫角色的成員，才能夠執行**sp_unregister_custom_scripting**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_register_custom_scripting &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)  
  
  
