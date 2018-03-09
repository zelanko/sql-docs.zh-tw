---
title: "建立 XML 索引 （選擇性 XML 索引） |Microsoft 文件"
ms.custom: 
ms.date: 08/10/2017
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
dev_langs:
- TSQL
ms.assetid: 1f510151-41d5-45c2-9cd0-b1ca0246fffe
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b0cd1c2dd0c77409768e8ea7838724ca4d6b827e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="create-xml-index-selective-xml-indexes"></a>CREATE XML INDEX (選擇性 XML 索引)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  在已由現有選擇性 XML 索引建立索引的單一路徑上，建立新的次要選擇性 XML 索引。 您也可以建立主要選擇性 XML 索引。 如需資訊，請參閱[Create、 Alter 和卸除選擇性 XML 索引](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE XML INDEX index_name  
    ON <table_object> ( xml_column_name )  
    USING XML INDEX sxi_index_name  
    FOR ( <xquery_or_sql_values_path> )  
    [WITH ( <index_options> )]  
  
<table_object> ::=   
{ [database_name. [schema_name ] . | schema_name. ] table_name }  
  
<xquery_or_sql_values_path>::=   
<path_name>   
  
<path_name> ::=   
character string literal  
  
<xmlnamespace_list> ::=   
<xmlnamespace_item> [, <xmlnamespace_list>]  
  
<xmlnamespace_item> ::=   
xmlnamespace_uri AS xmlnamespace_prefix  
  
<index_options> ::=   
(    
  | PAD_INDEX  = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = OFF  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
)  
```  
  
##  <a name="Arguments"></a> 引數  
 *index_name*  
 這是要建立之新索引的名稱。 索引名稱在資料表中必須是唯一的，但是在資料庫中不一定要是唯一的。 索引名稱必須遵守的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。  
  
 ON  *\<table_object >*包含索引之 XML 資料行的資料表。 您可以使用下列格式：  
  
-   `database_name.schema_name.table_name`  
  
-   `database_name..table_name`  
  
-   `schema_name.table_name`  
  
 *xml_column_name*  
 這是包含要索引之路徑的 XML 資料行名稱。  
  
 USING XML INDEX *sxi_index_name*  
 這是現有選擇性 XML 索引的名稱。  
  
 如**(** \<xquery_or_sql_values_path > **)**是用來建立次要選擇性 XML 索引的索引路徑的名稱。 索引路徑是來自 CREATE SELECTIVE XML INDEX 陳述式的指派名稱。 如需詳細資訊，請參閱 [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md)。  
  
 與\<index_options > 索引選項的相關資訊，請參閱[CREATE XML INDEX](../../t-sql/statements/create-xml-index-selective-xml-indexes.md)。  
  
## <a name="remarks"></a>備註  
 基底資料表中的每個 XML 資料行可以擁有多個次要選擇性 XML 索引。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 XML 資料行上必須先有選擇性 XML 索引，才能在該資料行上建立次要選擇性 XML 索引。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要資料表或檢視表的 ALTER 權限。 使用者必須是 **系統管理員** 固定伺服器角色的成員，或是 **db_ddladmin** 和 **db_owner** 固定資料庫角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會在 `pathabc`路徑上建立次要選擇性 XML 索引。 索引路徑是從指派的名稱[CREATE SELECTIVE XML INDEX &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md).  
  
```  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR ( pathabc );  
```  
  
## <a name="see-also"></a>另請參閱  
 [選擇性 XML 索引 &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [建立、修改和卸除次要選擇性 XML 索引](../../relational-databases/xml/create-alter-and-drop-secondary-selective-xml-indexes.md)  
  
  

