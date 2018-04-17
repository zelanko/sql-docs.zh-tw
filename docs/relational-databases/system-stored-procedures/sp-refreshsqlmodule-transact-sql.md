---
title: sp_refreshsqlmodule (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_refreshsqlmodule_TSQL
- sp_refreshsqlmodule
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server], stored procedures
- metadata [SQL Server], triggers
- metadata [SQL Server], views
- triggers [SQL Server], refreshing metadata
- views [SQL Server], refreshing metadata
- sp_refreshsqlmodule
- metadata [SQL Server], functions
- stored procedures [SQL Server], refreshing metadata
- user-defined functions [SQL Server], refreshing metadata
ms.assetid: f0022a05-50dd-4620-961d-361b1681d375
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0a5979dd6b797ced4b4785fedd068671ae9e05f9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sprefreshsqlmodule-transact-sql"></a>sp_refreshsqlmodule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對目前資料庫中指定的非結構描述繫結預存程序、使用者自訂函數、檢視、DML 觸發程序、資料庫層級 DDL 觸發程序或伺服器層級 DDL 觸發程序，更新其中繼資料。 這些物件的基礎物件變更之後，其保存中繼資料也可能會過期，例如參數的資料類型。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_refreshsqlmodule [ @name = ] 'module_name'   
    [ , [ @namespace = ] ' <class> ' ]  
  
<class> ::=  
{  
  | DATABASE_DDL_TRIGGER  
  | SERVER_DDL_TRIGGER  
}  
  
```  
  
## <a name="arguments"></a>引數  
 [  **@name=** ] **'***適於***'**  
 這是預存程序、使用者自訂函數、檢視、DML 觸發程序、資料庫層級 DDL 觸發程序或伺服器層級 DDL 觸發程序的名稱。 *適於*不能在 common language runtime (CLR) 預存程序或 CLR 函數。 *適於*無法結構描述繫結。 *適於*是**nvarchar**，沒有預設值。 *適於*可以是多重部分識別碼，但只能參考目前資料庫中的物件。  
  
 [ **，** @**命名空間**=] **'** \<類別 > **'**  
 這是指定之模組的類別。 當*適於*DDL 觸發程序，\<類別 > 為必要。 *\<類別 >*是**nvarchar**(20)。 有效輸入包括：  
  
|||  
|-|-|  
|DATABASE_DDL_TRIGGER||  
|SERVER_DDL_TRIGGER|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或非零數字 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_refreshsqlmodule**變更會影響其定義的物件基礎的模組時，應該執行。 否則，在查詢或叫用模組時，可能會產生非預期的結果。 若要重新整理檢視，您可以使用**sp_refreshsqlmodule**或**sp_refreshview**相同的結果。  
  
 **sp_refreshsqlmodule**不會影響任何權限、 擴充的屬性或設定與物件相關聯的選項。  
  
 若要重新整理伺服器層級 DDL 觸發程序，請從任何資料庫的內容執行此預存程序。  
  
> [!NOTE]  
>  當您執行時，會卸除與物件相關聯的任何簽章**sp_refreshsqlmodule**。  
  
## <a name="permissions"></a>Permissions  
 需要模組的 ALTER 權限，以及物件所參考之任何 CLR 使用者自訂型別和 XML 結構描述集合的 REFERENCES 權限。 當指定的模組是資料庫層級 DDL 觸發程序時，便需要目前資料庫的 ALTER ANY DATABASE DDL TRIGGER 權限。 當指定的模組是伺服器層級 DDL 觸發程序時，便需要 CONTROL SERVER 權限。  
  
 此外，對於使用 EXECUTE AS 子句定義的模組，也必須對指定的主體具備 IMPERSONATE 權限。 一般而言，重新整理物件不會變更其 EXECUTE AS 主體，除非模組是使用 EXECUTE AS USER 定義，而且主體的使用者名稱這時解析出來不是模組建立當時的使用者。  
  
## <a name="examples"></a>範例  
  
### <a name="a-refreshing-a-user-defined-function"></a>A. 重新整理使用者自訂函數  
 下列範例會重新整理使用者自訂函數。 這個範例會建立別名資料類型 `mytype`，以及使用 `to_upper` 的使用者自訂函數 `mytype`。 接著，`mytype` 會重新命名為 `myoldtype`，而且會建立有不同定義的新 `mytype`。 `dbo.to_upper` 函數會重新整理，以參考 `mytype` 的新實作，而非舊實作。  
  
```  
-- Create an alias type.  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT 'mytype' FROM sys.types WHERE name = 'mytype')  
DROP TYPE mytype;  
GO  
  
CREATE TYPE mytype FROM nvarchar(5);  
GO  
  
IF OBJECT_ID ('dbo.to_upper', 'FN') IS NOT NULL  
DROP FUNCTION dbo.to_upper;  
GO  
  
CREATE FUNCTION dbo.to_upper (@a mytype)  
RETURNS mytype  
WITH ENCRYPTION  
AS  
BEGIN  
RETURN upper(@a)  
END;  
GO  
  
SELECT dbo.to_upper('abcde');  
GO  
  
-- Increase the length of the alias type.  
sp_rename 'mytype', 'myoldtype', 'userdatatype';  
GO  
  
CREATE TYPE mytype FROM nvarchar(10);  
GO  
  
-- The function parameter still uses the old type.  
SELECT name, type_name(user_type_id)   
FROM sys.parameters   
WHERE object_id = OBJECT_ID('dbo.to_upper');  
GO  
  
SELECT dbo.to_upper('abcdefgh'); -- Fails because of truncation  
GO  
  
-- Refresh the function to bind to the renamed type.  
EXEC sys.sp_refreshsqlmodule 'dbo.to_upper';  
  
-- The function parameters are now bound to the correct type and the statement works correctly.  
SELECT name, type_name(user_type_id) FROM sys.parameters  
WHERE object_id = OBJECT_ID('dbo.to_upper');  
GO  
  
SELECT dbo.to_upper('abcdefgh');  
GO  
```  
  
### <a name="b-refreshing-a-database-level-ddl-trigger"></a>B. 重新整理資料庫層級 DDL 觸發程序  
 下列範例會重新整理資料庫層級 DDL 觸發程序。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_refreshsqlmodule @name = 'ddlDatabaseTriggerLog' , @namespace = 'DATABASE_DDL_TRIGGER';  
GO  
```  
  
### <a name="c-refreshing-a-server-level-ddl-trigger"></a>C. 重新整理伺服器層級 DDL 觸發程序  
 下列範例會重新整理伺服器層級 DDL 觸發程序。  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
  
```  
USE master;  
GO  
EXEC sys.sp_refreshsqlmodule @name = 'ddl_trig_database' , @namespace = 'SERVER_DDL_TRIGGER';  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_refreshview &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refreshview-transact-sql.md)   
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
