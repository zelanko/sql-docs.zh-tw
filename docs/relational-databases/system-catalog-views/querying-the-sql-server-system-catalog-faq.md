---
title: 查詢 SQL Server 系統目錄常見問題集 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- catalog views [SQL Server], examples
- metadata [SQL Server], frequently asked questions
- metadata [SQL Server], example queries
- system catalogs [SQL Server], example queries
- catalog views [SQL Server], frequently asked questions
ms.assetid: ca202580-c37e-4ccd-9275-77ce79481f64
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8cdff2d0646dcce13257bb10f7f447169fd8c8b8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47749702"
---
# <a name="querying-the-sql-server-system-catalog-faq"></a>查詢 SQL Server 系統目錄 FAQ
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本主題包含常見問題集的清單。 這些問題的答案就是根據目錄檢視而來的查詢。  
  
##  <a name="_TOP"></a> 常見問題集  
 下列各節將依類別列出常見問題集。  
  
### <a name="data-types"></a>資料型別  
  
-   [如何找到指定資料表的資料行的資料類型？](#_FAQ7)  
  
-   [如何找到指定資料表的 LOB 資料類型？](#_FAQ14)  
  
-   [如何找到相依於指定的資料類型的資料行？](#_FAQ22)  
  
-   [如何找到相依於指定的 CLR 使用者定義型別或別名資料類型的計算資料行？](#_FAQ23)  
  
-   [如何找到相依於指定的 CLR 使用者定義型別或別名類型的參數？](#_FAQ24)  
  
-   [如何找到相依於指定 CLR 使用者定義類型的檢查條件約束？](#_FAQ25)  
  
-   [如何找到檢視、 TRANSACT-SQL 函數和 TRANSACT-SQL 預存程序相依於指定的 CLR 使用者定義型別或別名類型？](#_FAQ26)  
  
### <a name="tables-indexes-views-and-constraints"></a>資料表、索引、檢視表及條件約束  
  
-   [如何找到指定的資料庫中的所有使用者定義的資料表？](#_FAQ31)  
  
-   [如何找到指定的資料庫中沒有叢集的索引的所有資料表？](#_FAQ1)  
  
-   [如何找到所有沒有索引的資料表？](#_FAQ4)  
  
-   [如何找到所有沒有主索引鍵的資料表？](#_FAQ3)  
  
-   [如何找到所有具有識別欄位的資料表？](#_FAQ5)  
  
-   [如何找到所有資料表和索引來進行資料分割？](#_FAQ32)  
  
-   [如何找到資料庫中的所有檢視？](#_FAQ13)  
  
-   [如何找到檢視的定義？](#_FAQ35)  
  
-   [如何找到過去 N 天內修改過的所有實體？](#_FAQ6)  
  
-   [如何找到指定資料表的主索引鍵資料行？](#_FAQ16)  
  
-   [如何找到指定資料表的外部索引鍵資料行？](#_FAQ17)  
  
-   [如何判斷資料行用於計算資料行運算式？](#_FAQ20)  
  
-   [我要如何找到所使用的所有資料行的計算資料行運算式中？](#_FAQ21)  
  
-   [如何找到指定資料表的所有條件約束？](#_FAQ27)  
  
-   [如何找到指定的資料表所有索引？](#_FAQ28)  
  
-   [如何尋找具有指定的資料行名稱的所有資料表？](#_FAQ30)  
  
-   [如何找到指定的物件上的所有統計資料？](#_FAQ33)  
  
-   [如何在指定的物件上找到所有的統計資料和統計資料資料行？](#_FAQ34)  
  
### <a name="modules-stored-procedures-user-defined-functions-and-triggers"></a>模組 (預存程序、使用者自訂函數及觸發程序)  
  
-   [如何找到資料庫中的所有預存程序？](#_FAQ9)  
  
-   [如何找到資料庫中的所有使用者定義函式？](#_FAQ12)  
  
-   [如何找到指定的預存程序或函式的參數？](#_FAQ10)  
  
-   [如何找到指定的函式上的相依性？](#_FAQ8)  
  
-   [如何檢視模組的定義？](#_FAQ15)  
  
-   [如何檢視伺服器層級觸發程序的定義？](#_FAQ19)  
  
### <a name="schemas-users-roles-and-permissions"></a>結構描述、使用者、角色及權限  
  
-   [如何找到指定的結構描述中包含實體的所有擁有者？](#_FAQ2)  
  
-   [如何找到授與或拒絕指定主體的權限？](#_FAQ18)  
  
## <a name="answers"></a>答案  
  
###  <a name="_FAQ1"></a> 如何找到指定的資料庫中沒有叢集的索引的所有資料表？  
 在您執行下列查詢之前，請使用有效的資料庫名稱取代 `<database_name>`。  
  
```  
SELECT SCHEMA_NAME(t.schema_id) AS schema_name, t.name AS table_name  
FROM sys.tables AS t  
WHERE NOT EXISTS   
   (  
     SELECT * FROM sys.indexes AS i  
     WHERE i.object_id = t.object_id  
     AND i.type = 1  -- or type_desc = 'CLUSTERED'  
   )  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 或者，您可以使用下列範例所顯示的 `OBJECTPROPERTY` 函數。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name, name AS table_name  
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasClustIndex') = 0  
ORDER BY schema_id, name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ2"></a> 如何找到指定的結構描述中包含實體的所有擁有者？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>` 及 `<schema_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT 'OBJECT' AS entity_type  
    ,USER_NAME(OBJECTPROPERTY(object_id, 'OwnerId')) AS owner_name  
    ,name   
FROM sys.objects WHERE SCHEMA_NAME(schema_id) = '<schema_name>'  
UNION   
SELECT 'TYPE' AS entity_type  
    ,USER_NAME(TYPEPROPERTY(SCHEMA_NAME(schema_id) + '.' + name, 'OwnerId')) AS owner_name  
    ,name   
FROM sys.types WHERE SCHEMA_NAME(schema_id) = '<schema_name>'   
UNION  
SELECT 'XML SCHEMA COLLECTION' AS entity_type   
    ,COALESCE(USER_NAME(xsc.principal_id),USER_NAME(s.principal_id)) AS owner_name  
    ,xsc.name   
FROM sys.xml_schema_collections AS xsc JOIN sys.schemas AS s  
    ON s.schema_id = xsc.schema_id  
WHERE s.name = '<schema_name>';  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ3"></a> 如何找到所有沒有主索引鍵的資料表？  
 在您執行下列查詢之前，請使用有效的資料庫名稱取代 `<database_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(t.schema_id) AS schema_name  
    ,t.name AS table_name  
FROM sys.tables t   
WHERE object_id NOT IN   
   (  
    SELECT parent_object_id   
    FROM sys.key_constraints   
    WHERE type_desc = 'PRIMARY_KEY_CONSTRAINT' -- or type = 'PK'  
    );  
GO  
  
```  
  
 或者，您可以執行下列查詢。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name   
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasPrimaryKey') = 0  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ4"></a> 如何找到所有沒有索引的資料表？  
 在您執行下列查詢之前，請使用有效的資料庫名稱取代 `<database_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name  
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'IsIndexed') = 0  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ5"></a> 如何找到所有具有識別欄位的資料表？  
 在您執行下列查詢之前，請使用有效的資料庫名稱取代 `<database_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    , t.name AS table_name  
    , c.name AS column_name  
FROM sys.tables AS t  
JOIN sys.identity_columns c ON t.object_id = c.object_id  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 或者，您可以執行下列查詢。  
  
> [!NOTE]  
>  這項查詢不會傳回資料行的名稱。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name   
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasIdentity') = 1  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ7"></a> 如何找到指定資料表的資料行的資料類型？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>` 及 `<schema_name.table_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT c.name AS column_name  
    ,c.column_id  
    ,SCHEMA_NAME(t.schema_id) AS type_schema  
    ,t.name AS type_name  
    ,t.is_user_defined  
    ,t.is_assembly_type  
    ,c.max_length  
    ,c.precision  
    ,c.scale  
FROM sys.columns AS c   
JOIN sys.types AS t ON c.user_type_id=t.user_type_id  
WHERE c.object_id = OBJECT_ID('<schema_name.table_name>')  
ORDER BY c.column_id;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ8"></a> 如何找到指定的函式上的相依性？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>` 及 `<schema_name.function_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS referencing_object_name  
    ,COALESCE(COL_NAME(object_id, column_id), '(n/a)') AS referencing_column_name  
    ,*  
FROM sys.sql_dependencies  
WHERE referenced_major_id = OBJECT_ID('<schema_name.function_name>')  
ORDER BY OBJECT_NAME(object_id), COL_NAME(object_id, column_id);  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ9"></a> 如何找到資料庫中的所有預存程序？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>`。  
  
```  
  
USE <database_name>;  
GO  
SELECT name AS procedure_name   
    ,SCHEMA_NAME(schema_id) AS schema_name  
    ,type_desc  
    ,create_date  
    ,modify_date  
FROM sys.procedures;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ10"></a> 如何找到指定的預存程序或函式的參數？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>` 及 `<schema_name.object_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,o.name AS object_name  
    ,o.type_desc  
    ,p.parameter_id  
    ,p.name AS parameter_name  
    ,TYPE_NAME(p.user_type_id) AS parameter_type  
    ,p.max_length  
    ,p.precision  
    ,p.scale  
    ,p.is_output  
FROM sys.objects AS o  
INNER JOIN sys.parameters AS p ON o.object_id = p.object_id  
WHERE o.object_id = OBJECT_ID('<schema_name.object_name>')  
ORDER BY schema_name, object_name, p.parameter_id;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ12"></a> 如何找到資料庫中的所有使用者定義函式？  
 在您執行下列查詢之前，請使用有效的資料庫名稱取代 `<database_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT name AS function_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,type_desc  
  ,create_date  
  ,modify_date  
FROM sys.objects  
WHERE type_desc LIKE '%FUNCTION%';  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ13"></a> 如何找到資料庫中的所有檢視？  
 在您執行下列查詢之前，請使用有效的資料庫名稱取代 `<database_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT name AS view_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,OBJECTPROPERTYEX(object_id,'IsIndexed') AS IsIndexed  
  ,OBJECTPROPERTYEX(object_id,'IsIndexable') AS IsIndexable  
  ,create_date  
  ,modify_date  
FROM sys.views;  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ6"></a> 如何找到過去 N 天內修改過的所有實體？  
 在您執行下列查詢之前，請使用有效的值取代 `<database_name>` 及 `<n_days>`。  
  
```  
USE <database_name>;  
GO  
SELECT name AS object_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,type_desc  
  ,create_date  
  ,modify_date  
FROM sys.objects  
WHERE modify_date > GETDATE() - <n_days>  
ORDER BY modify_date;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ14"></a> 如何找到指定資料表的 LOB 資料類型？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>` 及 `<schema_name.table_name>`。  
  
```  
  
USE <database_name>;  
GO  
SELECT name AS column_name   
    ,column_id   
    ,TYPE_NAME(user_type_id) AS type_name  
    ,max_length  
    ,CASE   
       WHEN max_length = -1 AND TYPE_NAME(user_type_id) <> 'xml'  
            THEN 1  
            ELSE 0  
     END AS [(max)]  
FROM sys.columns  
WHERE object_id=OBJECT_ID('<schema_name.table_name>')   
    AND ( TYPE_NAME(user_type_id) IN ('xml','text', 'ntext','image')  
         OR (TYPE_NAME(user_type_id) IN ('varchar','nvarchar','varbinary')  
         AND max_length = -1)  
        );  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ15"></a> 如何檢視模組的定義？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>` 及 `<schema_name.object_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT definition  
FROM sys.sql_modules  
WHERE object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 或者，您可以使用下列範例所顯示的 `OBJECT_DEFINITION` 函數。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID('<schema_name.object_name>')) AS ObjectDefinition;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ19"></a> 如何檢視伺服器層級觸發程序的定義？  
  
```  
SELECT definition  
FROM sys.server_sql_modules;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ16"></a> 如何找到指定資料表的主索引鍵資料行？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>` 及 `<schema_name.table_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT i.name AS index_name  
    ,ic.index_column_id  
    ,key_ordinal  
    ,c.name AS column_name  
    ,TYPE_NAME(c.user_type_id)AS column_type   
    ,is_identity  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic   
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
INNER JOIN sys.columns AS c   
    ON ic.object_id = c.object_id AND c.column_id = ic.column_id  
WHERE i.is_primary_key = 1   
    AND i.object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 或者，您可以使用下列範例所顯示的 `COL_NAME` 函數。  
  
```  
USE <database_name>;  
GO  
SELECT i.name AS index_name  
    ,COL_NAME(ic.object_id,ic.column_id) AS column_name  
    ,ic.index_column_id  
    ,key_ordinal  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic   
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
WHERE i.is_primary_key = 1   
    AND i.object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ17"></a> 如何找到指定資料表的外部索引鍵資料行？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>` 及 `<schema_name.table_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT   
    f.name AS foreign_key_name  
   ,OBJECT_NAME(f.parent_object_id) AS table_name  
   ,COL_NAME(fc.parent_object_id, fc.parent_column_id) AS constraint_column_name  
   ,OBJECT_NAME (f.referenced_object_id) AS referenced_object  
   ,COL_NAME(fc.referenced_object_id, fc.referenced_column_id) AS referenced_column_name  
   ,is_disabled  
   ,delete_referential_action_desc  
   ,update_referential_action_desc  
FROM sys.foreign_keys AS f  
INNER JOIN sys.foreign_key_columns AS fc   
   ON f.object_id = fc.constraint_object_id   
WHERE f.parent_object_id = OBJECT_ID('<schema_name.table_name>');  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ18"></a> 如何找到授與或拒絕指定主體的權限？  
 下列範例會建立一個函數，可傳回在其上檢查權限之實體的名稱。 此函數會在後面的查詢中叫用。 您必須在想要檢查權限的每個資料庫中建立此函數。  
  
```  
-- Create a function to return the name of the entity on which the permissions are checked.  
IF OBJECT_ID (N'dbo.entity_instance_name', N'FN') IS NOT NULL  
    DROP FUNCTION dbo.entity_instance_name;  
GO  
CREATE FUNCTION dbo.entity_instance_name(@class_desc nvarchar(60), @major_id int)   
RETURNS sysname AS  
BEGIN  
    DECLARE @the_entity_name sysname  
    SELECT @the_entity_name = CASE  
        WHEN @class_desc = 'DATABASE' THEN DB_NAME()  
        WHEN @class_desc = 'SCHEMA' THEN SCHEMA_NAME(@major_id)  
        WHEN @class_desc = 'OBJECT_OR_COLUMN' THEN OBJECT_NAME(@major_id)  
        WHEN @class_desc = 'DATABASE_PRINCIPAL' THEN USER_NAME(@major_id)  
        WHEN @class_desc = 'ASSEMBLY' THEN   
            (SELECT name FROM sys.assemblies WHERE assembly_id=@major_id)  
        WHEN @class_desc = 'TYPE' THEN TYPE_NAME(@major_id)  
        WHEN @class_desc = 'XML_SCHEMA_COLLECTION' THEN   
            (SELECT name FROM sys.xml_schema_collections  
              WHERE xml_collection_id=@major_id)  
        WHEN @class_desc = 'MESSAGE_TYPE' THEN   
            (SELECT name FROM sys.service_message_types WHERE message_type_id=@major_id)  
        WHEN @class_desc = 'SERVICE_CONTRACT' THEN   
           (SELECT name FROM sys.service_contracts  
              WHERE service_contract_id=@major_id)  
        WHEN @class_desc = 'SERVICE' THEN  
          (SELECT name FROM sys.services WHERE service_id=@major_id)  
        WHEN @class_desc = 'REMOTE_SERVICE_BINDING' THEN  
          (SELECT name FROM sys.remote_service_bindings  
             WHERE remote_service_binding_id=@major_id)  
        WHEN @class_desc = 'ROUTE' THEN  
          (SELECT name FROM sys.routes WHERE route_id=@major_id)  
        WHEN @class_desc = 'FULLTEXT_CATALOG' THEN  
          (SELECT name FROM sys.fulltext_catalogs WHERE fulltext_catalog_id=@major_id)  
        WHEN @class_desc = 'SYMMETRIC_KEY' THEN  
          (SELECT name FROM sys.symmetric_keys WHERE symmetric_key_id=@major_id)  
        WHEN @class_desc = 'CERTIFICATE' THEN  
          (SELECT name FROM sys.certificates WHERE certificate_id=@major_id)  
        WHEN @class_desc = 'ASYMMETRIC_KEY' THEN  
          (SELECT name FROM sys.asymmetric_keys WHERE asymmetric_key_id=@major_id)  
        WHEN @class_desc = 'SERVER' THEN   
             (SELECT name FROM sys.servers WHERE server_id=@major_id)  
        WHEN @class_desc = 'SERVER_PRINCIPAL' THEN SUSER_NAME(@major_id)  
        WHEN @class_desc = 'ENDPOINT' THEN   
             (SELECT name FROM sys.endpoints WHERE endpoint_id=@major_id)        
        ELSE '?'  
    END  
    RETURN @the_entity_name  
END;  
GO  
-- Return server-level permissions for the user.  
SELECT class  
    ,class_desc  
    ,dbo.entity_instance_name(class_desc, major_id) AS entity_name   
    ,minor_id  
    ,SUSER_NAME(grantee_principal_id) AS grantee  
    ,SUSER_NAME(grantor_principal_id) AS grantor  
    ,type  
    ,permission_name  
    ,state_desc   
FROM sys.server_permissions   
WHERE grantee_principal_id = SUSER_ID('public');  
GO  
-- Return database-level permissions for the user.  
SELECT class  
    ,class_desc  
    ,dbo.entity_instance_name(class_desc , major_id) AS entity_name   
    ,minor_id  
    ,USER_NAME(grantee_principal_id) AS grantee  
    ,USER_NAME(grantor_principal_id) AS grantor  
    ,type  
    ,permission_name  
    ,state_desc     
FROM  sys.database_permissions   
WHERE grantee_principal_id = DATABASE_PRINCIPAL_ID('public');  
GO  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ20"></a> 如何判斷資料行用於計算資料行運算式？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>`、`<schema_name.table_name>` 及 `<column_name`>。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,COL_NAME(object_id, column_id) AS computed_column   
    ,class_desc  
    ,is_selected  
    ,is_updated  
    ,is_select_all  
FROM sys.sql_dependencies  
WHERE referenced_major_id = OBJECT_ID('<schema_name.table_name>')  
    AND referenced_minor_id = COLUMNPROPERTY(referenced_major_id, '<column_name>', 'ColumnId')  
    AND class = 1;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ21"></a> 我要如何找到所使用的所有資料行的計算資料行運算式中？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(d.referenced_major_id) AS object_name  
    ,COL_NAME(d.referenced_major_id, d.referenced_minor_id) AS column_name  
    ,OBJECT_NAME(referenced_major_id) AS dependent_object_name   
    ,COL_NAME(d.object_id, d.column_id) AS dependent_computed_column  
    ,cc.definition AS computed_column_definition  
FROM sys.sql_dependencies AS d  
JOIN sys.computed_columns AS cc   
    ON cc.object_id = d.object_id AND cc.column_id = d.column_id AND d.object_id=d.referenced_major_id       
WHERE d.class = 1  
ORDER BY object_name, column_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ22"></a> 如何找到相依於指定的 CLR 使用者定義型別或別名類型的資料行？  
 執行下列查詢之前，請取代`<database_name>`具備有效的名稱和`<schema_name.data_type_name>`有效且符合結構描述的 CLR 使用者定義型別或符合結構描述的別名類型名稱。 下列查詢需要的成員資格**db_owner**角色或權限，以查看所有的相依資料行和計算資料行在資料庫中的中繼資料。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name   
    ,c.name AS column_name   
    ,SCHEMA_NAME(t.schema_id) AS schema_name  
    ,TYPE_NAME(c.user_type_id) AS user_type_name  
    ,c.max_length  
    ,c.precision  
    ,c.scale  
    ,c.is_nullable  
    ,c.is_computed  
FROM sys.columns AS c  
INNER JOIN sys.types AS t ON c.user_type_id = t.user_type_id  
WHERE c.user_type_id = TYPE_ID('<schema_name.data_type_name>');   
GO  
  
```  
  
 下列查詢會傳回資料行的受限的窄小檢視相依於 CLR 使用者定義型別或別名，但結果集都可以看到**公開**角色。 如果您已將使用者定義型別的 REFERENCE 權限授與他人，卻沒有權限檢視使用該類型之人所建立物件的中繼資料，則可以使用這個查詢。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name   
    ,COL_NAME(object_id, column_id) AS column_name  
    ,TYPE_NAME(user_type_id) AS user_type  
FROM sys.column_type_usages  
WHERE user_type_id = TYPE_ID('<schema_name.data_type_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ23"></a> 如何找到相依於指定的 CLR 使用者定義型別或別名類型的計算資料行？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>`，並使用符合結構描述的有效 CLR 使用者定義型別、別名類型名稱來取代 `<schema_name.data_type_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,COL_NAME(object_id, column_id) AS column_name  
FROM sys.sql_dependencies  
WHERE referenced_major_id = TYPE_ID('<schema_name.data_type_name>')  
    AND class = 2 -- schema-bound references to type  
    AND OBJECTPROPERTY(object_id, 'IsTable') = 1;   -- exclude non-table dependencies  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ24"></a> 如何找到相依於指定的 CLR 使用者定義型別或別名類型的參數？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>`，並使用符合結構描述的有效 CLR 使用者定義型別、別名類型名稱來取代 `<schema_name.data_type_name>`。 下列查詢需要的成員資格**db_owner**角色或權限，以查看所有的相依資料行和計算資料行在資料庫中的中繼資料。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,NULL AS procedure_number  
    ,name AS param_name  
    ,parameter_id AS param_num  
    ,TYPE_NAME(p.user_TYPE_ID) AS type_name  
FROM sys.parameters AS p  
WHERE p.user_TYPE_ID = TYPE_ID('<schema_name.data_type_name>')  
UNION   
SELECT OBJECT_NAME(object_id) AS object_name  
    ,procedure_number  
    ,name AS param_name  
    ,parameter_id AS param_num  
    ,TYPE_NAME(p.user_TYPE_ID) AS type_name  
FROM sys.numbered_procedure_parameters AS p  
WHERE p.user_TYPE_ID = TYPE_ID('<schema_name.data_type_name>')  
ORDER BY object_name, procedure_number, param_num;  
GO  
  
```  
  
 下列查詢會傳回相依於 CLR 使用者定義型別或別名的參數的受限的窄小檢視，但結果集都可以看到**公開**角色。 如果您已將使用者定義型別的 REFERENCE 權限授與他人，卻沒有權限檢視使用該類型之人所建立物件的中繼資料，則可以使用這個查詢。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,parameter_id  
    ,TYPE_NAME(user_type_id) AS type_name  
FROM sys.parameter_type_usages   
WHERE user_type_id = TYPE_ID('<schema_name.data_type_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ25"></a> 如何找到相依於指定 CLR 使用者定義類型的檢查條件約束？  
 執行下列查詢之前，請取代`<database_name>`具備有效的名稱和`<schema_name.data_type_name>`有效且符合結構描述的 CLR 使用者定義型別名稱。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS schema_name  
    ,OBJECT_NAME(o.parent_object_id) AS table_name  
    ,OBJECT_NAME(o.object_id) AS constraint_name  
FROM sys.sql_dependencies AS d  
JOIN sys.objects AS o ON o.object_id = d.object_id  
WHERE referenced_major_id = TYPE_ID('<schema_name.data_type_name>')  
    AND class = 2 -- schema-bound references to type  
    AND OBJECTPROPERTY(o.object_id, 'IsCheckCnst') = 1; -- exclude non-CHECK dependencies  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ26"></a> 如何找到檢視、 TRANSACT-SQL 函數和 TRANSACT-SQL 預存程序相依於指定的 CLR 使用者定義型別或別名類型？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>`，並使用符合結構描述的有效 CLR 使用者定義型別、別名類型名稱來取代 `<schema_name.data_type_name>`。  
  
 在函數或程序中定義的參數隱含結構描述繫結。 因此，可以檢視相依於 CLR 使用者定義型別或別名類型的參數使用[sys.sql_dependencies](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)目錄檢視。 程序和觸發程序不是結構描述繫結。 這表示任何定義於程序或觸發程序主體的運算式，與 CLR 使用者定義型別或別名資料型別之間的相依性不會保留。 結構描述繫結檢視和結構描述繫結使用者定義的函式之運算式的相依於 CLR 使用者定義型別或別名類型會保留在**sys.sql_dependencies**目錄檢視。 類型與 CLR 函數及 CLR 程序之間的相依性不會保留。  
  
 下列查詢會針對指定的 CLR 使用者定義型別或別名資料型別，傳回其檢視、[!INCLUDE[tsql](../../includes/tsql-md.md)] 函數及 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序中的所有結構描述繫結相依性。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS dependent_object_schema  
  ,OBJECT_NAME(o.object_id) AS dependent_object_name  
  ,o.type_desc AS dependent_object_type  
  ,d.class_desc AS kind_of_dependency  
  ,TYPE_NAME (d.referenced_major_id) AS type_name  
FROM sys.sql_dependencies AS d   
JOIN sys.objects AS o  
  ON d.object_id = o.object_id  
  AND o.type IN ('FN','IF','TF', 'V', 'P')  
WHERE d.class = 2 -- dependencies on types  
  AND d.referenced_major_id = TYPE_ID('<schema_name.data_type_name>')  
ORDER BY dependent_object_schema, dependent_object_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ27"></a> 如何找到指定資料表的所有條件約束？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>` 及 `<schema_name.table_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) as constraint_name  
    ,SCHEMA_NAME(schema_id) AS schema_name  
    ,OBJECT_NAME(parent_object_id) AS table_name  
    ,type_desc  
    ,create_date  
    ,modify_date  
    ,is_ms_shipped  
    ,is_published  
    ,is_schema_published  
FROM sys.objects  
WHERE type_desc LIKE '%CONSTRAINT'   
    AND parent_object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ28"></a> 如何找到指定的資料表所有索引？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>` 及 `<schema_name.table_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT i.name AS index_name  
    ,i.type_desc  
    ,is_unique  
    ,ds.type_desc AS filegroup_or_partition_scheme  
    ,ds.name AS filegroup_or_partition_scheme_name  
    ,ignore_dup_key  
    ,is_primary_key  
    ,is_unique_constraint  
    ,fill_factor  
    ,is_padded  
    ,is_disabled  
    ,allow_row_locks  
    ,allow_page_locks  
FROM sys.indexes AS i  
INNER JOIN sys.data_spaces AS ds ON i.data_space_id = ds.data_space_id  
WHERE is_hypothetical = 0 AND i.index_id <> 0   
AND i.object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ30"></a> 如何尋找具有指定的資料行名稱的所有物件？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>` 及 `<column_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id)  
FROM sys.columns  
WHERE name = '<column_name>';  
GO  
  
```  
  
 或  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS schema_name   
    ,o.name AS object_name  
    ,type_desc  
FROM sys.objects AS o  
INNER JOIN sys.columns AS c ON o.object_id = c.object_id  
WHERE c.name = '<column_name>';  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ31"></a> 如何找到指定的資料庫中的所有使用者定義的資料表？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT *   
FROM sys.tables;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ32"></a> 如何找到所有資料表和索引來進行資料分割？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS schema_name  
    ,OBJECT_NAME(p.object_id) AS table_name  
    ,i.name AS index_name  
    ,p.partition_number  
    ,rows   
FROM sys.partitions AS p  
INNER JOIN sys.indexes AS i ON p.object_id = i.object_id AND p.index_id = i.index_id  
INNER JOIN sys.partition_schemes ps ON i.data_space_id=ps.data_space_id  
INNER JOIN sys.objects AS o ON o.object_id = i.object_id  
ORDER BY index_name, partition_number;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ33"></a> 如何找到指定的物件上的所有統計資料？  
 在您執行以下查詢之前，請使用有效的名稱取代 `<database_name>`，並使用有效的資料表、索引檢視或資料表值函數名稱來取代 `<schema_name.object_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT name AS statistics_name  
    ,stats_id  
    ,auto_created  
    ,user_created  
    ,no_recompute  
FROM sys.stats  
WHERE object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ34"></a> 如何在指定的物件上找到所有的統計資料和統計資料資料行？  
 在您執行以下查詢之前，請使用有效的名稱取代 `<database_name>`，並使用有效的資料表、索引檢視或資料表值函數名稱來取代 `<schema_name.object_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT s.name AS statistics_name  
    ,c.name AS column_name  
    ,sc.stats_column_id  
FROM sys.stats AS s  
INNER JOIN sys.stats_columns AS sc   
    ON s.object_id = sc.object_id AND s.stats_id = sc.stats_id  
INNER JOIN sys.columns AS c   
    ON sc.object_id = c.object_id AND c.column_id = sc.column_id  
WHERE s.object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="_FAQ35"></a> 如何找到檢視的定義？  
 在您執行下列查詢之前，請使用有效的名稱取代 `<database_name>` 及 `<schema_name.object_name>`。  
  
```  
USE <database_name>;  
GO  
SELECT definition  
FROM sys.sql_modules  
WHERE object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 或者，您可以使用下列範例所顯示的 `OBJECT_DEFINITION` 函數。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID('<schema_name.object_name>')) AS ObjectDefinition;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
## <a name="see-also"></a>另請參閱  
 [將系統資料表對應至系統檢視表&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
