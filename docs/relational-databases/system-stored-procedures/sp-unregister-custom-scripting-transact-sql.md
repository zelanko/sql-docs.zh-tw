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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5c638c37da5907295cf4f8ef0dbb63d7eef17f05
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762774"
---
# <a name="sp_unregister_custom_scripting-transact-sql"></a>sp_unregister_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  這個預存程式會移除使用者定義的自訂預存 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式或腳本檔案，該檔案是藉由執行[sp_register_custom_scripting](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)來註冊。 這個預存程序執行於發行集資料庫的發行者端。  
  
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
|**update**|註冊的自訂預存程序或指令碼，是在複寫 UPDATE 陳述式時執行。|  
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
  
  
