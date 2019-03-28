---
title: sp_register_custom_scripting & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_register_custom_scripting
- sp_register_custom_scripting_TSQL
helpviewer_keywords:
- sp_register_custom_scripting
ms.assetid: a8159282-de3b-4b9e-bdc9-3d3fce485c7f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 85f9104d9a9bb634dd10dfb588cf07e01d1c1fb1
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535914"
---
# <a name="spregistercustomscripting-transact-sql"></a>sp_register_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  複寫可讓使用者自訂的自訂預存程序，取代異動複寫所用的一個或多個預設程序。 當複寫資料表變更結構描述時，就會重新建立這些預存程序。 **sp_register_custom_scripting**註冊預存程序或[!INCLUDE[tsql](../../includes/tsql-md.md)]發生新使用者定義自訂預存程序的定義編寫指令碼的結構描述變更時執行的指令碼檔案。 這個新的使用者自訂之自訂預存程序，應該要反映該資料表的新結構描述。 **sp_register_custom_scripting**執行於發行集資料庫的發行者端和已註冊的指令碼檔案或預存程序執行於訂閱者端發生結構描述變更時。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_register_custom_scripting [ @type  = ] 'type'  
    [ @value = ] 'value'   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @type = ] 'type'` 要登錄自訂預存程序或指令碼的型別。 *型別*已**varchar(16)**，沒有預設值，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**insert**|註冊的自訂預存程序是在複寫 INSERT 陳述式時執行。|  
|**update**|註冊的自訂預存程序是在複寫 UPDATE 陳述式時執行。|  
|**delete**|註冊的自訂預存程序是在複寫 DELETE 陳述式時執行。|  
|**custom_script**|指令碼是在資料定義語言 (DDL) 觸發程序結尾執行。|  
  
`[ @value = ] 'value'` 預存程序或名稱和完整路徑名稱[!INCLUDE[tsql](../../includes/tsql-md.md)]所註冊的指令碼檔案。 *值*已**nvarchar(1024)**，沒有預設值。  
  
> [!NOTE]  
>  指定針對 NULL*值*參數將會取消註冊先前註冊的指令碼，也就是執行相同[sp_unregister_custom_scripting](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)。  
  
 時的值*型別*是**custom_script**，完整路徑與名稱[!INCLUDE[tsql](../../includes/tsql-md.md)]指令碼檔案。 否則，請*值*必須是已註冊的預存程序的名稱。  
  
`[ @publication = ] 'publication'` 要登錄的自訂預存程序或指令碼的發行集名稱。 *發行集*已**sysname**，預設值是**NULL**。  
  
`[ @article = ] 'article'` 要登錄的自訂預存程序或指令碼的發行項名稱。 *發行項*已**sysname**，預設值是**NULL**。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_register_custom_scripting**用於快照式和異動複寫。  
  
 在變更複寫資料表的結構描述之前，要先執行這個預存程序。 如需使用此預存程序的詳細資訊，請參閱 <<c0> [ 重新產生自訂交易程序以反映結構描述變更](../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md)。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定伺服器角色**db_owner**固定資料庫角色，或有**db_ddladmin**固定的資料庫角色可以執行**sp_register_custom_scripting**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_unregister_custom_scripting &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)  
  
  
