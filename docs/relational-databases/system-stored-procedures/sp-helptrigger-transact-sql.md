---
title: sp_helptrigger (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dfb494c7b25d3a580059e4d1ad3250abbe91ee54
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828976"
---
# <a name="sphelptrigger-transact-sql"></a>sp_helptrigger (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回在目前資料庫之指定資料表定義的 DML 觸發程序類型。 sp_helptrigger 無法搭配 DDL 觸發程序。 查詢[系統預存程序](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)目錄檢視。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helptrigger [ @tabname = ] 'table'   
     [ , [ @triggertype = ] 'type' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@tabname=** ] **'***表格***'**  
 這是目前資料庫中傳回觸發程序資訊的資料表名稱。 *表格*已**nvarchar(776)**，沒有預設值。  
  
 [ **@triggertype=** ] **'***type***'**  
 這是傳回相關資訊的 DML 觸發程序類型。 *型別*已**char(6)**，預設值是 NULL，而且可以是下列值之一。  
  
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
|**了 trigger_schema，做**|**sysname**|觸發程序所屬的結構描述名稱。|  
  
## <a name="permissions"></a>Permissions  
 需要[中繼資料可見性組態](../../relational-databases/security/metadata-visibility-configuration.md)資料表的權限。  
  
## <a name="examples"></a>範例  
 下列範例會執行 `sp_helptrigger` 以產生 `Person.Person` 資料表上的觸發程序資訊。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helptrigger 'Person.Person';  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
