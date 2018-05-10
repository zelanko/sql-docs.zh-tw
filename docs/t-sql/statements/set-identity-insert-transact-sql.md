---
title: SET IDENTITY_INSERT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SET IDENTITY_INSERT
- SET_IDENTITY_INSERT_TSQL
- IDENTITY_INSERT_TSQL
- IDENTITY_INSERT
dev_langs:
- TSQL
helpviewer_keywords:
- IDENTITY_INSERT option
- SET IDENTITY_INSERT statement
- identity values [SQL Server], explicit values
- identity columns [SQL Server], explicit values
ms.assetid: a5dd49f2-45c7-44a8-b182-e0a5e5c373ee
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 13235669b5124c0c3f088d7550b1bdfdace30c72
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="set-identityinsert-transact-sql"></a>SET IDENTITY_INSERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  允許將明確的值插入資料表的識別欄位中。  

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SET IDENTITY_INSERT [ [ database_name . ] schema_name . ] table { ON | OFF }  
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 這是指定的資料表所在的資料庫名稱。  
  
 *schema_name*  
 這是資料表所屬的結構描述名稱。  
  
 *table*  
 這是含識別欄位之資料表的名稱。  
  
## <a name="remarks"></a>Remarks  
 不論何時，工作階段中只能有一份資料表將 IDENTITY_INSERT 屬性設為 ON。 如果已有資料表的這個屬性設為 ON，又針對另一份資料表發出 SET IDENTITY_INSERT ON 陳述式，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回一則錯誤訊息，指出 SET IDENTITY_INSERT 已設為 ON，且會報告設為 ON 所針對的資料表。  
  
 如果輸入的值大於資料表目前的識別值，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會自動利用新插入的值來作為目前的識別值。  
  
 SET IDENTITY_INSERT 的設定是在執行階段進行設定，而不是在剖析階段進行設定。  
  
## <a name="permissions"></a>Permissions  
 使用者必須擁有資料表，或對資料表擁有 ALTER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會建立含識別欄位的資料表，且會顯示如何利用 `SET IDENTITY_INSERT` 設定來填滿 `DELETE` 陳述式所造成的識別值的間距。  
  
```  
USE AdventureWorks2012;  
GO  
-- Create tool table.  
CREATE TABLE dbo.Tool(  
   ID INT IDENTITY NOT NULL PRIMARY KEY,   
   Name VARCHAR(40) NOT NULL  
);  
GO  
-- Inserting values into products table.  
INSERT INTO dbo.Tool(Name)   
VALUES ('Screwdriver')  
        , ('Hammer')  
        , ('Saw')  
        , ('Shovel');  
GO  
  
-- Create a gap in the identity values.  
DELETE dbo.Tool  
WHERE Name = 'Saw';  
GO  
  
SELECT *   
FROM dbo.Tool;  
GO  
  
-- Try to insert an explicit ID value of 3;  
-- should return a warning.  
INSERT INTO dbo.Tool (ID, Name) VALUES (3, 'Garden shovel');  
GO  
-- SET IDENTITY_INSERT to ON.  
SET IDENTITY_INSERT dbo.Tool ON;  
GO  
  
-- Try to insert an explicit ID value of 3.  
INSERT INTO dbo.Tool (ID, Name) VALUES (3, 'Garden shovel');  
GO  
  
SELECT *   
FROM dbo.Tool;  
GO  
-- Drop products table.  
DROP TABLE dbo.Tool;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [IDENTITY &#40;屬性&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
