---
title: "ALTER SCHEMA (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER SCHEMA
- ALTER_SCHEMA_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], transferring
- transferring objects between schemas
- ALTER SCHEMA statement
- schemas [SQL Server], modifying
- modifying schemas
ms.assetid: 0a760138-460e-410a-a3c1-d60af03bf2ed
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ad157c7d4d7b92bc199c4a490d4387acc0af0908
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="alter-schema-transact-sql"></a>ALTER SCHEMA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在結構描述之間傳送安全性實體。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
ALTER SCHEMA schema_name   
   TRANSFER [ <entity_type> :: ] securable_name   
[;]  
  
<entity_type> ::=  
    {  
    Object | Type | XML Schema Collection  
    }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER SCHEMA schema_name   
   TRANSFER [ OBJECT :: ] securable_name   
[;]  
```  
  
## <a name="arguments"></a>引數  
 *schema_name*  
 這是安全性實體要移至的目前資料庫中的結構描述名稱。 不可以是 SYS 或 INFORMATION_SCHEMA。  
  
 \<entity_type >  
 這是變更擁有者的實體類別。 物件是預設值。  
  
 *securable_name*  
 這是要移至結構描述的結構描述內含安全性實體之一部分或兩部分名稱。  
  
## <a name="remarks"></a>備註  
 使用者和結構描述完全分隔。  
  
 ALTER SCHEMA 只能用來移動相同資料庫中結構描述之間的安全性實體。 若要變更或卸除結構描述內的安全性實體，請使用該安全性實體特定的 ALTER 或 DROP 陳述式。  
  
 如果一段式名稱會用於*securable_name*，名稱解析規則目前實際上會用來尋找該安全性實體。  
  
 當安全性實體移至新結構描述時，將卸除與這個安全性實體相關聯的所有權限。 如果已明確設定安全性實體的擁有者，該擁有者將保持不變。 如果安全性實體的擁有者已設為 SCHEMA OWNER，該擁有者將維持為 SCHEMA OWNER；不過，在移動之後，SCHEMA OWNER 將解析為新結構描述的擁有者。 新擁有者的 principal_id 會是 NULL。  
  
 若要變更資料表或檢視表的結構描述使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，在 [物件總管] 中，以滑鼠右鍵按一下資料表或檢視表，然後按一下**設計**。 按**F4**以開啟 [屬性] 視窗。 在**結構描述**方塊中，選取新的結構描述。  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permissions  
 若要從另一個結構描述傳送安全性實體，目前使用者必須對安全性實體 (而非結構描述) 具有 CONTROL 權限，並對目標結構描述具有 ALTER 權限。  
  
 如果安全性實體上有 EXECUTE AS OWNER 規格，且擁有者設為 SCHEMA OWNER，則該使用者也必須對目標結構描述的擁有者具有 IMPERSONATION 權限。  
  
 移動要傳送的安全性實體時，將會卸除與該安全性實體相關聯的所有權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-transferring-ownership-of-a-table"></a>A. 傳送資料表的擁有權  
 下列範例會將 `HumanResources` 結構描述中的 `Address` 資料表傳送到 `Person` 結構描述中，以修改這個結構描述。  
  
```  
USE AdventureWorks2012;  
GO  
ALTER SCHEMA HumanResources TRANSFER Person.Address;  
GO  
```  
  
### <a name="b-transferring-ownership-of-a-type"></a>B. 傳送某個類型的擁有權  
 下列範例會在 `Production` 結構描述中建立某個類型，然後將此類型傳送至 `Person` 結構描述。  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TYPE Production.TestType FROM [varchar](10) NOT NULL ;  
GO  
  
-- Check the type owner.  
SELECT sys.types.name, sys.types.schema_id, sys.schemas.name  
    FROM sys.types JOIN sys.schemas   
        ON sys.types.schema_id = sys.schemas.schema_id   
    WHERE sys.types.name = 'TestType' ;  
GO  
  
-- Change the type to the Person schema.  
ALTER SCHEMA Person TRANSFER type::Production.TestType ;  
GO  
  
-- Check the type owner.  
SELECT sys.types.name, sys.types.schema_id, sys.schemas.name  
    FROM sys.types JOIN sys.schemas   
        ON sys.types.schema_id = sys.schemas.schema_id   
    WHERE sys.types.name = 'TestType' ;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-transferring-ownership-of-a-table"></a>C. 傳送資料表的擁有權  
 下列範例會建立資料表`Region`中`dbo`結構描述中，建立`Sales`結構描述，然後再移動`Region`資料表中`dbo`結構描述以`Sales`結構描述。  
  
```  
CREATE TABLE dbo.Region   
    (Region_id int NOT NULL,  
    Region_Name char(5) NOT NULL)  
WITH (DISTRIBUTION = REPLICATE);  
GO  
  
CREATE SCHEMA Sales;  
GO  
  
ALTER SCHEMA Sales TRANSFER OBJECT::dbo.Region;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立結構描述 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-schema-transact-sql.md)   
 [卸除結構描述 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-schema-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  


