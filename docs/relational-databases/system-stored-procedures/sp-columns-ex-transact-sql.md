---
title: sp_columns_ex (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_columns_ex
- sp_columns_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_columns_ex
ms.assetid: c12ef6df-58c6-4391-bbbf-683ea874bd81
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7224a4e301565dc1bc6f6968da3477792b8cfc22
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781487"
---
# <a name="spcolumnsex-transact-sql"></a>sp_columns_ex (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回指定之連結伺服器資料表的資料行資訊，每個資料行一個資料列。 **sp_columns_ex**傳回的特定資料行的資料行資訊，如果*資料行*指定。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_columns_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @column_name = ] 'column' ]   
     [ , [ @ODBCVer = ] 'ODBCVer' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@table_server =** ] **'***table_server&lt***'**  
 這是傳回資料行資訊所屬的連結伺服器名稱。 *table_server&lt*已**sysname**，沒有預設值。  
  
 [  **@table_name =** ] **'***table_name***'**  
 這是傳回資料行資訊所屬的資料表名稱。 *table_name*已**sysname**，預設值是 NULL。  
  
 [  **@table_schema =** ] **'***table_schema***'**  
 這是傳回資料行資訊所屬之資料表的結構描述名稱。 *table_schema*已**sysname**，預設值是 NULL。  
  
 [  **@table_catalog =** ] **'***table_catalog 排列***'**  
 這是傳回的資料行資訊所屬之資料表的目錄名稱。 *table_catalog 排列*已**sysname**，預設值是 NULL。  
  
 [  **@column_name =** ] **'***資料行***'**  
 這是提供的權限資訊所屬的資料庫資料行名稱。 *資料行*已**sysname**，預設值是 NULL。  
  
 [  **@ODBCVer =** ] **'***ODBCVer***'**  
 這是要使用之 ODBC 的版本。 *ODBCVer*已**int**，預設值是 2。 這表示 ODBC 2。 有效值是 2 或 3。 如需有關 2 和 3 版之間行為差異的詳細資訊，請參閱 ODBC SQLColumns 規格。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|資料表或檢視表限定詞名稱。 各種 DBMS 產品都支援三部分的資料表命名 (*限定詞 ***。*** 擁有者 ***。*** 名稱*)。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個資料行代表資料庫名稱。 在某些產品中，它代表資料表之資料庫環境的伺服器名稱。 這個欄位可以是 NULL。|  
|**再依據 TABLE_SCHEM 排列**|**sysname**|資料表或檢視表擁有者名稱。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個資料行代表建立資料表的資料庫使用者名稱。 這個欄位一律會傳回值。|  
|**TABLE_NAME**|**sysname**|資料表或檢視表名稱。 這個欄位一律會傳回值。|  
|**COLUMN_NAME**|**sysname**|資料行名稱，每個資料行**TABLE_NAME**傳回。 這個欄位一律會傳回值。|  
|**DATA_TYPE**|**smallint**|對應於 ODBC 類型指標的整數值。 如果這是無法對應於 ODBC 類型的資料類型，這個值就是 NULL。 原生資料型別名稱都會傳入**TYPE_NAME**資料行。|  
|**TYPE_NAME**|**varchar (** 13 **)**|代表資料類型的字串。 基礎 DBMS 提供這個資料類型名稱。|  
|**COLUMN_SIZE**|**int**|有效位數的數目。 傳回值**精確度**資料行是在基底為 10。|  
|**BUFFER_LENGTH**|**int**|資料的傳送大小。1|  
|**DECIMAL_DIGITS**|**smallint**|小數點右側的位數。|  
|**NUM_PREC_RADIX**|**smallint**|這是數值資料類型的基礎。|  
|**可為 NULL**|**smallint**|指定 Null 屬性。<br /><br /> 1 = 可能是 NULL。<br /><br /> 0 = 非 NULL。|  
|**註解**|**varchar (** 254 **)**|這個欄位一律會傳回 NULL。|  
|**COLUMN_DEF**|**varchar (** 254 **)**|資料行的預設值。|  
|**SQL_DATA_TYPE**|**smallint**|SQL 資料類型出現在描述子之 TYPE 欄位時的值。 這個資料行是相同**DATA_TYPE**資料行，除了**datetime**和 SQL-92**間隔**資料型別。 這個資料行一律會傳回值。|  
|**SQL_DATETIME_SUB**|**smallint**|子類型代碼**datetime**和 SQL-92**間隔**資料型別。 其他資料類型的這個資料行都會傳回 NULL。|  
|**CHAR_OCTET_LENGTH**|**int**|字元或整數資料類型資料行的最大長度 (以位元組為單位)。 其他所有資料類型的這個資料行都會傳回 NULL。|  
|**ORDINAL_POSITION**|**int**|資料行在資料表中的序數位置。 資料表中的第一個資料行是 1。 這個資料行一律會傳回值。|  
|**IS_NULLABLE**|**varchar (** 254 **)**|資料表中資料行的 Null 屬性。 遵照 ISO 規則來決定 Null 屬性。 ISO SQL 標準 DBMS 無法傳回空字串。<br /><br /> YES = 資料行可以包括 NULLS。<br /><br /> NO = 資料行不能包括 NULLS。<br /><br /> 如果 Null 屬性不明，這個資料行會傳回長度為零的字串。<br /><br /> 傳回的值，這個資料行是針對傳回的值不同**NULLABLE**資料行。|  
|**SS_DATA_TYPE**|**tinyint**|擴充預存程序所用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。|  
  
 如需詳細資訊，請參閱 Microsoft ODBC 文件集。  
  
## <a name="remarks"></a>備註  
 **sp_columns_ex**執行查詢的資料行資料列集**IDBSchemaRowset**對應至 OLE DB 提供者介面*table_server&lt*。 *Table_name*， *table_schema*， *table_catalog 排列*，以及*資料行*參數傳遞給這個介面來限制的資料列傳回此項目。  
  
 **sp_columns_ex**會傳回空的結果集，如果指定連結伺服器的 OLE DB 提供者不支援的資料行資料列集**IDBSchemaRowset**介面。  
  
## <a name="permissions"></a>Permissions  
 需要結構描述的 SELECT 權限。  
  
## <a name="remarks"></a>備註  
 **sp_columns_ex**遵循分隔識別碼的需求。 如需詳細資訊，請參閱＜ [Database Identifiers](../../relational-databases/databases/database-identifiers.md)＞。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 `JobTitle` 連結伺服器 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中之 `HumanResources.Employee` 資料表 `Seattle1` 資料行的資料類型。  
  
```  
EXEC sp_columns_ex 'Seattle1',   
   'Employee',   
   'HumanResources',   
   'AdventureWorks2012',   
   'JobTitle';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_catalogs &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_foreignkeys &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [< sp_indexes &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [idbschemarowset &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [idbschemarowset &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
