---
title: sp_columns (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1d61c0d2a7c7b15db9e96a354d5b7f062d10ca8f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52514082"
---
# <a name="spcolumns-transact-sql"></a>sp_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

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
 [ **@table_name=**] *object*  
 這是用來傳回目錄資訊之物件的名稱。 *物件*可以是資料表、 檢視或其他物件，例如資料表值函式的資料行。 *物件*已**nvarchar(384)**，沒有預設值。 支援萬用字元的模式比對。  
  
 [ **@table_owner****=**] *owner*  
 這是用來傳回目錄資訊之物件的物件擁有者。 *擁有者*已**nvarchar(384)**，預設值是 NULL。 支援萬用字元的模式比對。 如果*擁有者*未指定，套用基礎 dbms 的預設物件可見性規則。  
  
 如果目前使用者擁有一個含有指定名稱的物件，就會傳回該物件的資料行。 如果*擁有者*未指定且目前使用者並未擁有具有指定的物件*物件*， **sp_columns**尋找具有指定之物件*物件*資料庫擁有者所擁有。 如果存在，就會傳回該物件的資料行。  
  
 [ **@table_qualifier****=**] *qualifier*  
 這是物件限定詞的名稱。 *限定詞*已**sysname**，預設值是 NULL。 各種 DBMS 產品都支援三部分命名物件 (_限定詞_**。**_擁有者_**。**_名稱_)。 在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，這個資料行代表資料庫名稱。 在某些產品中，它代表物件之資料庫環境的伺服器名稱。  
  
 [  **@column_name=**]*資料行*  
 這是個單一資料行，當只需要一個目錄資訊的資料行時，就會使用這個單一資料行。 *資料行*已**nvarchar(384)**，預設值是 NULL。 如果*資料行*是未指定，會傳回所有資料行。 在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，*資料行*代表的資料行名稱，如下所示**syscolumns**資料表。 支援萬用字元的模式比對。 若要有最大交互操作能力，閘道用戶端應該只採用 SQL-92 標準模式比對 (% 和 _ 萬用字元)。  
  
 [ **@ODBCVer=**] *ODBCVer*  
 這是要使用之 ODBC 的版本。 *ODBCVer*已**int**，預設值是 2。 這表示 ODBC 2。 有效值是 2 或 3。 如需 2 和 3 版之間行為差異，請參閱 ODBC **SQLColumns**規格。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="result-sets"></a>結果集  
 **Sp_columns**目錄預存程序相當於**SQLColumns** ODBC 中。 傳回的結果都會按照**TABLE_QUALIFIER**， **TABLE_OWNER**，並**TABLE_NAME**。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|物件限定詞名稱。 這個欄位可以是 NULL。|  
|**TABLE_OWNER**|**sysname**|物件擁有者名稱。 這個欄位一律會傳回值。|  
|**TABLE_NAME**|**sysname**|物件名稱。 這個欄位一律會傳回值。|  
|**COLUMN_NAME**|**sysname**|資料行名稱，每個資料行**TABLE_NAME**傳回。 這個欄位一律會傳回值。|  
|**DATA_TYPE**|**smallint**|ODBC 資料類型的整數碼。 如果這是無法對應於 ODBC 類型的資料類型，它就是 NULL。 原生資料型別名稱都會傳入**TYPE_NAME**資料行。|  
|**TYPE_NAME**|**sysname**|代表資料類型的字串。 基礎 DBMS 提供這個資料類型名稱。|  
|**PRECISION**|**int**|有效位數的數目。 傳回值**精確度**資料行是在基底為 10。|  
|**LENGTH**|**int**|傳送資料的大小。<sup>1</sup>|  
|**SCALE**|**smallint**|小數點右側的位數。|  
|**RADIX**|**smallint**|數值資料類型的基底。|  
|**可為 NULL**|**smallint**|指定 Null 屬性。<br /><br /> 1 = 可能是 NULL。<br /><br /> 0 = 非 NULL。|  
|**註解**|**varchar(254)**|這個欄位一律會傳回 NULL。|  
|**COLUMN_DEF**|**nvarchar(4000)**|資料行的預設值。|  
|**SQL_DATA_TYPE**|**smallint**|SQL 資料類型出現在描述子之 TYPE 欄位時的值。 這個資料行是相同**DATA_TYPE**資料行，除了**datetime**和 SQL-92**間隔**資料型別。 這個資料行一律會傳回值。|  
|**SQL_DATETIME_SUB**|**smallint**|子類型代碼**datetime**和 SQL-92**間隔**資料型別。 其他資料類型的這個資料行都會傳回 NULL。|  
|**CHAR_OCTET_LENGTH**|**int**|字元或整數資料類型資料行的最大長度 (以位元組為單位)。 其他所有資料類型的這個資料行都會傳回 NULL。|  
|**ORDINAL_POSITION**|**int**|資料行在物件中的序數位置。 物件中的第一個資料行是 1。 這個資料行一律會傳回值。|  
|**IS_NULLABLE**|**varchar(254)**|物件中資料行的 Null 屬性。 遵照 ISO 規則來決定 Null 屬性。 ISO SQL 標準 DBMS 無法傳回空字串。<br /><br /> YES = 資料行可以包括 NULLS。<br /><br /> NO = 資料行不能包括 NULLS。<br /><br /> 如果 Null 屬性不明，這個資料行會傳回長度為零的字串。<br /><br /> 傳回的值，這個資料行是針對傳回的值不同**NULLABLE**資料行。|  
|**SS_DATA_TYPE**|**tinyint**|擴充預存程序所用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。 如需詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)。|  
  
 <sup>1</sup>如需詳細資訊，請參閱 Microsoft ODBC 文件。  
  
## <a name="permissions"></a>Permissions  
 需要結構描述的 SELECT 和 VIEW DEFINITION 權限。  
  
## <a name="remarks"></a>備註  
 **sp_columns**遵循分隔識別碼的需求。 如需詳細資訊，請參閱＜ [Database Identifiers](../../relational-databases/databases/database-identifiers.md)＞。  
  
## <a name="examples"></a>範例  
 下列範例會傳回指定之資料表的資料行資訊。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_columns @table_name = N'Department',  
   @table_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會傳回指定之資料表的資料行資訊。  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_columns @table_name = N'DimEmployee',  
   @table_owner = N'dbo';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_tables &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-tables-transact-sql.md)   
 [目錄預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  


