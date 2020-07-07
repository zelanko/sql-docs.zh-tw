---
title: sp_columns （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 10/17/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_columns_TSQL
- sp_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sp_columns
ms.assetid: 2dec79cf-2baf-4c0f-8cbb-afb1a8654e1e
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 83f46ddd70061ef0f0647c902221b7f906917048
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "85999902"
---
# <a name="sp_columns-transact-sql"></a>sp_columns (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  傳回目前環境中所能查詢之指定物件的資料行資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_columns [ @table_name = ] object  
     [ , [ @table_owner = ] owner ]   
     [ , [ @table_qualifier = ] qualifier ]   
     [ , [ @column_name = ] column ]   
     [ , [ @ODBCVer = ] ODBCVer ]  
```  
  
## <a name="arguments"></a>引數  
`[ \@table_name = ] object`這是用來傳回目錄資訊之物件的名稱。 *物件*可以是資料表、view 或其他具有資料行的物件，例如資料表值函式。 *物件*是**Nvarchar （384）**，沒有預設值。 支援萬用字元的模式比對。  
  
`[ \@table_owner = ] owner`這是用來傳回目錄資訊之物件的物件擁有者。 *owner*是**Nvarchar （384）**，預設值是 Null。 支援萬用字元的模式比對。 如果未指定*owner* ，則會套用基礎 DBMS 的預設物件可見度規則。  
  
 如果目前使用者擁有一個含有指定名稱的物件，就會傳回該物件的資料行。 如果未指定*owner* ，且目前使用者並未擁有具有指定之*物件*的物件， **sp_columns**會尋找具有資料庫擁有者所擁有之指定*物件*的物件。 如果存在，就會傳回該物件的資料行。  
  
`[ \@table_qualifier = ] qualifier`這是物件辨識符號的名稱。 *限定詞*是**sysname**，預設值是 Null。 各種 DBMS 產品都支援三部分的物件命名（辨識_符號_**。**_擁有_者 **。**_名稱_）。 在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，這個資料行代表資料庫名稱。 在某些產品中，它代表物件之資料庫環境的伺服器名稱。  
  
`[ \@column_name = ] column`是單一資料行，而且只有在目錄資訊的一個資料行需要時才會使用。 資料*行*是**Nvarchar （384）**，預設值是 Null。 如果未指定資料*行*，則會傳回所有資料行。 在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，資料*行*代表**syscolumns**資料表中所列出的資料行名稱。 支援萬用字元的模式比對。 若要有最大交互操作能力，閘道用戶端應該只採用 SQL-92 標準模式比對 (% 和 _ 萬用字元)。  
  
`[ \@ODBCVer = ] ODBCVer`這是正在使用的 ODBC 版本。 *ODBCVer*是**int**，預設值是2。 這表示 ODBC 2。 有效值是 2 或 3。 如需版本2和3之間的行為差異，請參閱 ODBC **SQLColumns**規格。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="result-sets"></a>結果集  
 **Sp_columns**目錄預存程式相當於 ODBC 中的**SQLColumns** 。 傳回的結果會依**TABLE_QUALIFIER**、 **TABLE_OWNER**和**TABLE_NAME**排序。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|物件限定詞名稱。 這個欄位可以是 NULL。|  
|**TABLE_OWNER**|**sysname**|物件擁有者名稱。 這個欄位一律會傳回值。|  
|**TABLE_NAME**|**sysname**|物件名稱。 這個欄位一律會傳回值。|  
|**COLUMN_NAME**|**sysname**|資料行名稱，針對每個傳回的**TABLE_NAME**資料行。 這個欄位一律會傳回值。|  
|**DATA_TYPE**|**smallint**|ODBC 資料類型的整數碼。 如果這是無法對應於 ODBC 類型的資料類型，它就是 NULL。 原生資料類型名稱會在**TYPE_NAME**資料行中傳回。|  
|**TYPE_NAME**|**sysname**|代表資料類型的字串。 基礎 DBMS 提供這個資料類型名稱。|  
|**精密**|**int**|有效位數的數目。 **PRECISION**資料行的傳回值以基底10為底數。|  
|**LENGTH**|**int**|資料的傳輸大小。<sup>1</sup>|  
|**尺度**|**smallint**|小數點右側的位數。|  
|**基**|**smallint**|數值資料類型的基底。|  
|**Null**|**smallint**|指定 Null 屬性。<br /><br /> 1 = 可能是 NULL。<br /><br /> 0 = 非 NULL。|  
|**備註**|**Varchar （254）**|這個欄位一律會傳回 NULL。|  
|**COLUMN_DEF**|**nvarchar(4000)**|資料行的預設值。|  
|**SQL_DATA_TYPE**|**smallint**|SQL 資料類型出現在描述子之 TYPE 欄位時的值。 除了**datetime**和 SQL-92 **interval**資料類型之外，此資料行與**DATA_TYPE**資料行相同。 這個資料行一律會傳回值。|  
|**SQL_DATETIME_SUB**|**smallint**|**Datetime**和 SQL-92 **interval**資料類型的子類型代碼。 其他資料類型的這個資料行都會傳回 NULL。|  
|**CHAR_OCTET_LENGTH**|**int**|字元或整數資料類型資料行的最大長度 (以位元組為單位)。 其他所有資料類型的這個資料行都會傳回 NULL。|  
|**ORDINAL_POSITION**|**int**|資料行在物件中的序數位置。 物件中的第一個資料行是 1。 這個資料行一律會傳回值。|  
|**IS_NULLABLE**|**Varchar （254）**|物件中資料行的 Null 屬性。 遵照 ISO 規則來決定 Null 屬性。 ISO SQL 標準 DBMS 無法傳回空字串。<br /><br /> YES = 資料行可以包括 NULLS。<br /><br /> NO = 資料行不能包括 NULLS。<br /><br /> 如果 Null 屬性不明，這個資料行會傳回長度為零的字串。<br /><br /> 為此資料行傳回的值與**可為 null**資料行傳回的值不同。|  
|**SS_DATA_TYPE**|**tinyint**|擴充預存程序所用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。 如需詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)。|  
  
 <sup>1</sup>如需詳細資訊，請參閱 Microsoft ODBC 檔集。  
  
## <a name="permissions"></a>權限  
 需要架構的 SELECT 和 VIEW DEFINITION 許可權。  
  
## <a name="remarks"></a>備註  
 **sp_columns**會遵循分隔識別碼的需求。 如需詳細資訊，請參閱＜ [Database Identifiers](../../relational-databases/databases/database-identifiers.md)＞。  
  
## <a name="examples"></a>範例  
 下列範例會傳回指定之資料表的資料行資訊。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_columns @table_name = N'Department',  
   @table_owner = N'HumanResources';  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會傳回指定之資料表的資料行資訊。  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_columns @table_name = N'DimEmployee',  
   @table_owner = N'dbo';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_tables &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-tables-transact-sql.md)   
 [&#40;Transact-sql&#41;的目錄預存程式](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  


