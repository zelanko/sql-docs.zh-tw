---
description: sp_register_custom_scripting (Transact-SQL)
title: sp_register_custom_scripting (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4f73353cc5d2e0e9be02be5a0e6dc59eaf2f909f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547490"
---
# <a name="sp_register_custom_scripting-transact-sql"></a>sp_register_custom_scripting (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  複寫可讓使用者自訂的自訂預存程序，取代異動複寫所用的一個或多個預設程序。 當複寫資料表變更結構描述時，就會重新建立這些預存程序。 **sp_register_custom_scripting** 註冊在架構變更時所執行的預存程式或腳本檔案， [!INCLUDE[tsql](../../includes/tsql-md.md)] 以編寫新使用者定義之自訂預存程式的定義腳本。 這個新的使用者自訂之自訂預存程序，應該要反映該資料表的新結構描述。 **sp_register_custom_scripting** 是在發行集資料庫的「發行者」端執行，而註冊的腳本檔案或預存程式則是在架構變更發生時于「訂閱者」端執行。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_register_custom_scripting [ @type  = ] 'type'  
    [ @value = ] 'value'   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @type = ] 'type'` 這是要註冊之自訂預存程式或腳本的類型。 *type* 是 **Varchar (16) **，沒有預設值，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**insert**|註冊的自訂預存程序是在複寫 INSERT 陳述式時執行。|  
|**update**|註冊的自訂預存程序是在複寫 UPDATE 陳述式時執行。|  
|**delete**|註冊的自訂預存程序是在複寫 DELETE 陳述式時執行。|  
|**custom_script**|指令碼是在資料定義語言 (DDL) 觸發程序結尾執行。|  
  
`[ @value = ] 'value'` 預存程式的名稱，或是正在註冊之腳本檔案的名稱和完整路徑 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 *值* 為 **Nvarchar (1024) **，沒有預設值。  
  
> [!NOTE]  
>  針對 *value*參數指定 Null 將會取消登錄先前註冊的腳本，這與執行 [sp_unregister_custom_scripting](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)的相同。  
  
 當 *type* 的值是 **custom_script**時，腳本檔案的名稱和完整路徑就是預期的名稱和完整路徑 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 否則， *值* 必須是已註冊預存程式的名稱。  
  
`[ @publication = ] 'publication'` 要註冊之自訂預存程式或腳本的發行集名稱。 *發行* 集是 **sysname**，預設值是 **Null**。  
  
`[ @article = ] 'article'` 要註冊之自訂預存程式或腳本的發行項名稱。 *文章* 是 **sysname**，預設值是 **Null**。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_register_custom_scripting** 用於快照式和異動複寫中。  
  
 在變更複寫資料表的結構描述之前，要先執行這個預存程序。 如需使用這個預存程式的詳細資訊，請參閱 [重新產生自訂交易程式以反映架構變更](../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md)。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色、 **db_owner** 固定資料庫角色或 **db_ddladmin** 固定資料庫角色的成員，才能夠執行 **sp_register_custom_scripting**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_unregister_custom_scripting &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)  
  
  
