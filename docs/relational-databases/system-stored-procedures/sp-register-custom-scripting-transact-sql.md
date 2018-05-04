---
title: sp_register_custom_scripting (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_register_custom_scripting
- sp_register_custom_scripting_TSQL
helpviewer_keywords:
- sp_register_custom_scripting
ms.assetid: a8159282-de3b-4b9e-bdc9-3d3fce485c7f
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 37d5ec660480bad1bc93fadafaeb80e5006c4399
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spregistercustomscripting-transact-sql"></a>sp_register_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  複寫可讓使用者自訂的自訂預存程序，取代異動複寫所用的一個或多個預設程序。 當複寫資料表變更結構描述時，就會重新建立這些預存程序。 **sp_register_custom_scripting**註冊預存程序或[!INCLUDE[tsql](../../includes/tsql-md.md)]以編寫新使用者定義自訂預存程序定義的結構描述變更發生時執行的指令碼檔案。 這個新的使用者自訂之自訂預存程序，應該要反映該資料表的新結構描述。 **sp_register_custom_scripting**執行於發行集資料庫中，「 發行者 」 和註冊的指令碼檔案或預存程序執行於訂閱者端發生結構描述變更時。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_register_custom_scripting [ @type  = ] 'type'  
    [ @value = ] 'value'   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@type** =] **'***類型***'**  
 這是要登錄之自訂預存程序或指令碼的類型。 *型別*是**varchar （16)**，沒有預設值，它可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**insert**|註冊的自訂預存程序是在複寫 INSERT 陳述式時執行。|  
|**更新**|註冊的自訂預存程序是在複寫 UPDATE 陳述式時執行。|  
|**delete**|註冊的自訂預存程序是在複寫 DELETE 陳述式時執行。|  
|**custom_script**|指令碼是在資料定義語言 (DDL) 觸發程序結尾執行。|  
  
 [ **@value**=] **'***值***'**  
 預存程序的名稱，或是正在註冊之 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼檔案的名稱和完整路徑。 *值*是**nvarchar （1024)**，沒有預設值。  
  
> [!NOTE]  
>  指定 NULL*值*參數將會取消註冊先前註冊的指令碼，也就是執行相同[sp_unregister_custom_scripting](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)。  
  
 時的值*類型*是**custom_script**，完整路徑與名稱[!INCLUDE[tsql](../../includes/tsql-md.md)]指令碼檔案。 否則，*值*必須是已註冊的預存程序的名稱。  
  
 [ **@publication**=] **'***發行集***'**  
 要登錄自訂預存程序或指令碼的發行集名稱。 *發行集*是**sysname**，預設值是**NULL**。  
  
 [ **@article**=] **'***文章***'**  
 要登錄自訂預存程序或指令碼的發行項名稱。 *發行項*是**sysname**，預設值是**NULL**。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_register_custom_scripting**用於快照式和異動複寫。  
  
 在變更複寫資料表的結構描述之前，要先執行這個預存程序。 如需有關如何使用這個預存程序的詳細資訊，請參閱[重新產生自訂交易程序以反映結構描述變更](../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md)。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定伺服器角色、 **db_owner**固定資料庫角色或**db_ddladmin**固定的資料庫角色可以執行**sp_register_custom_scripting**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_unregister_custom_scripting &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)  
  
  
