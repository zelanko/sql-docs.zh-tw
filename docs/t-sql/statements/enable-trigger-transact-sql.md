---
title: "啟用觸發程序 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ENABLE TRIGGER
- ENABLE_TSQL
- ENABLE_TRIGGER_TSQL
- ENABLE
dev_langs:
- TSQL
helpviewer_keywords:
- DDL triggers, enabling
- triggers [SQL Server], enabling
- DML triggers, enabling
- ENABLE TRIGGER statement
ms.assetid: 6e21f0ad-68d0-432f-9c7c-a119dd2d3fc9
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fb2fba080ea3c51e5c29456b2166eeea6274f8a3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="enable-trigger-transact-sql"></a>ENABLE TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  啟用 DML、DDL 或登入觸發程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
ENABLE TRIGGER { [ schema_name . ] trigger_name [ ,...n ] | ALL }  
ON { object_name | DATABASE | ALL SERVER } [ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *schema_name*  
 這是觸發程序所屬的結構描述名稱。 *schema_name*不能指定 DDL 或登入觸發程序。  
  
 *trigger_name*  
 這是您要啟用的觸發程序名稱。  
  
 ALL  
 指出啟用在 ON 子句範圍內定義的所有觸發程序。  
  
 *object_name*  
 這是資料表或檢視所在的 DML 觸發程序的名稱*trigger_name*已建立，以便執行。  
  
 DATABASE  
 DDL 觸發程序，它會指出*trigger_name*建立或修改以資料庫範圍來執行。  
  
 ALL SERVER  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 DDL 觸發程序，它會指出*trigger_name*建立或修改，以伺服器範圍下執行。 ALL SERVER 也適用於登入觸發程序。  
  
> [!NOTE]  
>  自主資料庫無法使用這個選項。  
  
## <a name="remarks"></a>備註  
 啟用觸發程序並不會重新建立它。 停用的觸發程序仍然是目前資料庫中的一個物件，但不會引發。 啟用觸發程序後，原先設定之任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式執行時，便造成觸發程序的引發。 觸發程序會停用使用[停用觸發程序](../../t-sql/statements/disable-trigger-transact-sql.md)。 可以是資料表上定義的 DML 觸發程序也會停用或啟用使用[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 若要啟用 DML 觸發程序，使用者至少要有建立這個觸發程序之資料表或檢視的 ALTER 權限。  
  
 若要啟用伺服器範圍 (ON ALL SERVER) 的 DDL 或登入觸發程序，使用者必須有伺服器的 CONTROL SERVER 權限。 若要啟用資料庫範圍 (ON DATABASE) 的 DDL 觸發程序，使用者至少要有目前資料庫中的 ALTER ANY DATABASE DDL TRIGGER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-enabling-a-dml-trigger-on-a-table"></a>A. 啟用資料表的 DML 觸發程序  
 下列範例會停用觸發程序`uAddress`所建立的資料表`Address`在 AdventureWorks 資料庫中，然後再啟用它。  
  
```  
DISABLE TRIGGER Person.uAddress ON Person.Address;  
GO  
ENABLE Trigger Person.uAddress ON Person.Address;  
GO  
```  
  
### <a name="b-enabling-a-ddl-trigger"></a>B. 啟用 DDL 觸發程序  
 下列範例會建立 DDL 觸發程序`safety`具有資料庫範圍內，然後停用再啟用它。  
  
```  
CREATE TRIGGER safety   
ON DATABASE   
FOR DROP_TABLE, ALTER_TABLE   
AS   
   PRINT 'You must disable Trigger "safety" to drop or alter tables!'   
   ROLLBACK;  
GO  
DISABLE TRIGGER safety ON DATABASE;  
GO  
ENABLE TRIGGER safety ON DATABASE;  
GO  
```  
  
### <a name="c-enabling-all-triggers-that-were-defined-with-the-same-scope"></a>C. 啟用以相同範圍來定義的所有觸發程序  
 下列範例會啟用在伺服器範圍建立的所有 DDL 觸發程序。  
  
**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
ENABLE Trigger ALL ON ALL SERVER;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
  

