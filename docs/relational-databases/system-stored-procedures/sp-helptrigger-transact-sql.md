---
title: sp_helptrigger （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helptrigger
- sp_helptrigger_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helptrigger
ms.assetid: e486d39b-771d-488d-a786-7136433a2203
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1e6244443fc1f6ba7d83376226fedd56563e0d39
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68048225"
---
# <a name="sp_helptrigger-transact-sql"></a>sp_helptrigger (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回在目前資料庫之指定資料表定義的 DML 觸發程序類型。 sp_helptrigger 不能與 DDL 觸發程式搭配使用。 請改為查詢[系統預存程式](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)目錄檢視。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helptrigger [ @tabname = ] 'table'   
     [ , [ @triggertype = ] 'type' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @tabname = ] 'table'`這是目前資料庫中傳回觸發程式資訊的資料表名稱。 *table*是**Nvarchar （776）**，沒有預設值。  
  
`[ @triggertype = ] 'type'`這是要傳回相關資訊的 DML 觸發程式類型。 *類型*是**char （6）**，預設值是 Null，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**DELETE**|傳回 DELETE 觸發程序資訊。|  
|**INSERT**|傳回 INSERT 觸發程序資訊。|  
|**UPDATE**|傳回 UPDATE 觸發程序資訊。|  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 下表將顯示結果集所包含的資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**trigger_name**|**sysname**|觸發程序的名稱。|  
|**trigger_owner**|**sysname**|定義觸發程序的資料表擁有者名稱。|  
|**isupdate**|**int**|1=UPDATE 觸發程序<br /><br /> 0=不是 UPDATE 觸發程序|  
|**isdelete**|**int**|1=DELETE 觸發程序<br /><br /> 0=不是 DELETE 觸發程序|  
|**isinsert**|**int**|1=INSERT 觸發程序<br /><br /> 0=不是 INSERT 觸發程序|  
|**isafter**|**int**|1=AFTER 觸發程序<br /><br /> 0=不是 AFTER 觸發程序|  
|**isinsteadof**|**int**|1=INSTEAD OF 觸發程序<br /><br /> 0=不是 INSTEAD OF 觸發程序|  
|**trigger_schema**|**sysname**|觸發程序所屬的結構描述名稱。|  
  
## <a name="permissions"></a>權限  
 需要資料表的[中繼資料可見度](../../relational-databases/security/metadata-visibility-configuration.md)設定許可權。  
  
## <a name="examples"></a>範例  
 下列範例會執行 `sp_helptrigger` 以產生 `Person.Person` 資料表上的觸發程序資訊。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helptrigger 'Person.Person';  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
