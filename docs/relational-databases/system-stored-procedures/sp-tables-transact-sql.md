---
title: sp_tables (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_tables
- sp_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tables
ms.assetid: 787a2fa5-87a1-49bd-938b-6043c245f46b
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a11d686bef327e4e3daba1ed5365289f78169853
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2020
ms.locfileid: "88173088"
---
# <a name="sp_tables-transact-sql"></a>sp_tables (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  傳回目前環境中所能查詢的物件清單。 這表示任何資料表或檢視表，但同義字物件除外。  
  
> [!NOTE]  
>  若要判斷同義字的基底物件名稱，請查詢[sys.databases](../../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md)目錄檢視。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_tables [ [ @table_name = ] 'name' ]   
     [ , [ @table_owner = ] 'owner' ]   
     [ , [ @table_qualifier = ] 'qualifier' ]   
     [ , [ @table_type = ] "type" ]   
     [ , [@fUsePattern = ] 'fUsePattern'];  
```  
  
## <a name="arguments"></a>引數  
`[ @table_name = ] 'name'`這是用來傳回目錄資訊的資料表。 *name*是**Nvarchar (384) **，預設值是 Null。 支援萬用字元的模式比對。  
  
`[ @table_owner = ] 'owner'`這是用來傳回目錄資訊之資料表的資料表擁有者。 *owner*是**Nvarchar (384) **，預設值是 Null。 支援萬用字元的模式比對。 如果未指定擁有者，就會套用基礎 DBMS 的預設資料表可見性規則。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，如果目前使用者擁有一份含指定之名稱的資料表，就會傳回該資料表的資料行。 如果未指定擁有者，且目前使用者並未擁有指定之名稱的資料表，這個程序就會尋找資料庫擁有者所擁有之指定名稱的資料表。 如果資料表存在，就會傳回這份資料表的資料行。  
  
`[ @table_qualifier = ] 'qualifier'`這是資料表限定詞的名稱。 *限定詞*是**sysname**，預設值是 Null。 各種 DBMS 產品都支援三部分的資料表命名 (辨識_符號_**。**_擁有_者 **。**_名稱_) 。 在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，這個資料行代表資料庫名稱。 在某些產品中，它代表資料表之資料庫環境的伺服器名稱。  
  
``[ , [ @table_type = ] "'type', 'type'" ]``這是以逗號分隔的值清單，提供指定之資料表類型的所有資料表的相關資訊。 其中包括**TABLE**、 **SYSTEMTABLE**和**VIEW**。 *類型*是**Varchar (100) **，預設值是 Null。  
  
> [!NOTE]  
>  每個資料表類型都必須用單引號括住，整個參數必須用雙引號括住。 資料表類型必須是大寫。 如果 SET QUOTED_IDENTIFIER 是 ON，每個單引號都必須變成兩個，整個參數必須用單引號括住。  
  
`[ @fUsePattern = ] 'fUsePattern'`判斷底線 ( _ ) 、百分比 (% ) 和方括弧 ( [或] ) 字元是否會被視為萬用字元。 有效值是 0 (關閉模式比對) 和 1 (開啟模式比對)。 *fUsePattern*是**bit**，預設值是1。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|資料表限定詞名稱。 在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，這個資料行代表資料庫名稱。 這個欄位可以是 NULL。|  
|**TABLE_OWNER**|**sysname**|資料表擁有者名稱。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個資料行代表建立資料表的資料庫使用者名稱。 這個欄位一律會傳回值。|  
|**TABLE_NAME**|**sysname**|資料表名稱。 這個欄位一律會傳回值。|  
|**TABLE_TYPE**|**varchar(32)**|資料表、系統資料表或檢視表。|  
|**備註**|**Varchar (254) **|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會傳回這個資料行的值。|  
  
## <a name="remarks"></a>備註  
 為取得最大交互操作能力，閘道用戶端應該只採用 SQL-92 標準 SQL 模式比對 (% 和 _ 萬用字元)。  
  
 不一定會檢查目前使用者對特定資料表之讀取或寫入權限的權限相關資訊。 因此，存取權並無保證。 這個結果集不只包括資料表和檢視表，它也包括支援這些類型之 DBMS 產品閘道的同義字和別名。 如果在**sp_server_info**的結果集中，伺服器屬性**ACCESSIBLE_TABLES**是 Y，則只會傳回目前使用者可存取的資料表。  
  
 **sp_tables**相當於 ODBC 中的**SQLTables** 。 傳回的結果會依**TABLE_TYPE**、 **TABLE_QUALIFIER**、 **TABLE_OWNER**和**TABLE_NAME**排序。  
  
## <a name="permissions"></a>權限  
 需要結構描述的 SELECT 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-a-list-of-objects-that-can-be-queried-in-the-current-environment"></a>A. 傳回目前環境中所能查詢之物件的清單  
 下列範例會傳回目前環境中所能查詢之物件的清單。  
  
```sql  
EXEC sp_tables ;  
```  
  
### <a name="b-returning-information-about-the-tables-in-a-specified-schema"></a>B. 傳回指定結構描述中之資料表的相關資訊  
 下列範例會傳回屬於 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中的`Person` 結構描述之資料表的相關資訊。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_tables   
   @table_name = '%',  
   @table_owner = 'Person',  
   @table_qualifier = 'AdventureWorks2012';  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-returning-a-list-of-objects-that-can-be-queried-in-the-current-environment"></a>C. 傳回目前環境中所能查詢之物件的清單  
 下列範例會傳回目前環境中所能查詢之物件的清單。  
  
```sql  
EXEC sp_tables ;  
```  
  
### <a name="d-returning-information-about-the-tables-in-a-specified-schema"></a>D. 傳回指定結構描述中之資料表的相關資訊  
 下列範例會傳回資料庫中維度資料表的相關資訊 `AdventureWorksPDW201` 。  
  
```sql  
-- Uses AdventureWorks  
  
EXEC sp_tables   
   @table_name = 'Dim%',  
   @table_owner = 'dbo',  
   @table_qualifier = 'AdventureWorksPDW2012';  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的同義字](../../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

