---
title: "停用觸發程序 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 05/10/2017
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
- DISABLE_TSQL
- DISABLE
- DISABLE TRIGGER
- DISABLE_TRIGGER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DML triggers, disabling
- DDL triggers, disabling
- DISABLE TRIGGER statement
- triggers [SQL Server], disabling
- disabling triggers
ms.assetid: e6529f06-e442-437e-a7bf-41790bc092c5
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 02888ae3de27c6859cd37bec9119761f4777b2bd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="disable-trigger-transact-sql"></a>DISABLE TRIGGER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  停用觸發程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
DISABLE TRIGGER { [ schema_name . ] trigger_name [ ,...n ] | ALL }  
ON { object_name | DATABASE | ALL SERVER } [ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *schema_name*  
 這是觸發程序所屬的結構描述名稱。 *schema_name*不能指定 DDL 或登入觸發程序。  
  
 *trigger_name*  
 這是要停用的觸發程序名稱。  
  
 ALL  
 指出只要是在 ON 子句範圍定義的觸發程序一律停用。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在發行用來進行合併式複寫的資料庫中建立觸發程序。 在已發行的資料庫中指定 ALL，會停用這些觸發程序，這會中斷複寫。 指定 ALL 之前，請先確認未針對合併式複寫發行目前的資料庫。  
  
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
 根據預設，在建立觸發程序時會一併將它啟用。 即使停用觸發程序，也不會卸除它。 該觸發程序仍然會以物件形式存在於目前的資料庫中。 不過，只要編寫它的任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式在執行時，觸發程序就不會引發。 使用可重新啟用觸發程序[ENABLE TRIGGER](../../t-sql/statements/enable-trigger-transact-sql.md)。 可以是資料表上定義的 DML 觸發程序也會停用或啟用使用[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)。  
  
 變更觸發程序使用**ALTER TRIGGER**陳述式可讓觸發程序。  
  
## <a name="permissions"></a>Permissions  
 若要停用 DML 觸發程序，使用者至少要對建立該觸發程序的資料表或檢視，具備 ALTER 權限。  
  
 若要停用伺服器範圍 (ON ALL SERVER) 的 DDL 觸發程序或登入觸發程序，使用者必須有伺服器的 CONTROL SERVER 權限。 若要停用以資料庫範圍 (ON DATABASE) 定義的 DDL 觸發程序，使用者至少要在目前資料庫中具備 ALTER ANY DATABASE DDL TRIGGER 權限。  
  
## <a name="examples"></a>範例  
下列範例所述 AdventureWorks2012 資料庫。
  
### <a name="a-disabling-a-dml-trigger-on-a-table"></a>A. 停用資料表的 DML 觸發程序  
 下列範例會停用在 `uAddress` 資料表中建立的觸發程序 `Address`。  
  
```  
DISABLE TRIGGER Person.uAddress ON Person.Address;  
GO  
```  
  
### <a name="b-disabling-a-ddl-trigger"></a>B. 停用 DDL 觸發程序  
 下列範例會以資料庫範圍建立 DDL 觸發程序 `safety`，然後再停用它。  
  
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
```  
  
### <a name="c-disabling-all-triggers-that-were-defined-with-the-same-scope"></a>C. 停用所有以相同範圍定義的觸發程序  
 下列範例會停用在伺服器範圍建立的所有 DDL 觸發程序。  
  
```  
DISABLE Trigger ALL ON ALL SERVER;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [sys.triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md)  
  
  

