---
description: sp_sproc_columns (Transact-SQL)
title: sp_sproc_columns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_sproc_columns
- sp_sproc_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_sproc_columns
ms.assetid: 62c18c21-35c5-4772-be0d-ffdcc19c97ab
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 180d57f7daacb1f7aeb6b638dba03f893340c1d2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97404166"
---
# <a name="sp_sproc_columns-transact-sql"></a>sp_sproc_columns (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  傳回目前環境中單一預存程序或使用者自訂函數的資料行資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure Synapse Analytics, Parallel Data Warehouse  
  
sp_sproc_columns [[@procedure_name = ] 'name']   
    [ , [@procedure_owner = ] 'owner']   
    [ , [@procedure_qualifier = ] 'qualifier']   
    [ , [@column_name = ] 'column_name']  
    [ , [@ODBCVer = ] 'ODBCVer']  
    [ , [@fUsePattern = ] 'fUsePattern']  
```  
  
## <a name="arguments"></a>引數  
`[ @procedure_name = ] 'name'` 這是用來傳回目錄資訊的程式名稱。 *名稱* 是 **Nvarchar (** 390 **)**，預設值是%，代表目前資料庫中的所有資料表。 支援萬用字元的模式比對。  
  
`[ @procedure_owner = ] 'owner'` 這是程式的擁有者名稱。 *擁有* 者是 **Nvarchar (** 384 **)**，預設值是 Null。 支援萬用字元的模式比對。 如果未指定 *owner* ，則適用基礎 DBMS 的預設程式可見度規則。  
  
 如果目前使用者擁有含指定名稱的程序，就會傳回這個程序的相關資訊。 如果未指定 *擁有* 者，且目前的使用者未擁有具有指定名稱的程式， **sp_sproc_columns** 會尋找具有指定名稱的程式，而該程式具有資料庫擁有者所擁有的名稱。 如果程序存在，就會傳回它的資料行的相關資訊。  
  
`[ @procedure_qualifier = ] 'qualifier'` 這是程式限定詞的名稱。 *限定詞* 是 **sysname**，預設值是 Null。 各種 DBMS 產品都支援三部分的 (*qualifier.owner.name*) 資料表的命名。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個參數代表資料庫名稱。 在某些產品中，它代表資料表之資料庫環境的伺服器名稱。  
  
`[ @column_name = ] 'column_name'` 是單一資料行，當只需要一個目錄資訊的資料行時，就會使用此資料行。 *column_name* 是 **Nvarchar (** 384 **)**，預設值是 Null。 如果省略 *column_name* ，則會傳回所有資料行。 支援萬用字元的模式比對。 若要有最大交互操作能力，閘道用戶端應該只採用 ISO 標準模式比對 (% 和 _ 萬用字元)。  
  
`[ @ODBCVer = ] 'ODBCVer'` 這是所使用的 ODBC 版本。 *ODBCVer* 是 **int**，預設值是2，表示 ODBC 2.0 版。 如需 ODBC 2.0 與 ODBC 3.0 版之間差異的詳細資訊，請參閱 odbc **SQLProcedureColumns** 規格 for odbc 3.0 版。  
  
`[ @fUsePattern = ] 'fUsePattern'` 決定是否將底線 (_) 、百分比 (% ) 和方括弧 ( [] ) 字元視為萬用字元。 有效值是 0 (關閉模式比對) 和 1 (開啟模式比對)。 *fUsePattern* 是 **bit**，預設值是1。  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**PROCEDURE_QUALIFIER**|**sysname**|程序限定詞名稱。 這個資料行可以是 NULL。|  
|**PROCEDURE_OWNER**|**sysname**|程序擁有者名稱。 這個資料行一律會傳回值。|  
|**PROCEDURE_NAME**|**Nvarchar (** 134 **)**|程序名稱。 這個資料行一律會傳回值。|  
|**COLUMN_NAME**|**sysname**|傳回之 **TABLE_NAME** 的每個資料行的資料行名稱。 這個資料行一律會傳回值。|  
|**COLUMN_TYPE**|**smallint**|這個欄位一律會傳回值：<br /><br /> 0 = SQL_PARAM_TYPE_UNKNOWN<br /><br /> 1 = SQL_PARAM_TYPE_INPUT<br /><br /> 2 = SQL_PARAM_TYPE_OUTPUT<br /><br /> 3 = SQL_RESULT_COL<br /><br /> 4 = SQL_PARAM_OUTPUT<br /><br /> 5 = SQL_RETURN_VALUE|  
|**DATA_TYPE**|**smallint**|ODBC 資料類型的整數碼。 如果這個資料類型無法對應至 ISO 類型，此值就是 NULL。 在 **TYPE_NAME** 資料行中會傳回原生資料類型名稱。|  
|**TYPE_NAME**|**sysname**|資料類型的字串表示法。 這是基礎 DBMS 所提供的資料類型名稱。|  
|**PRECISION**|**int**|有效位數的數目。 **PRECISION** 資料行的傳回值是以10為底數。|  
|**LENGTH**|**int**|資料的傳送大小。|  
|**規模**|**smallint**|小數點右側的位數。|  
|**RADIX**|**smallint**|這是數值類型的基底。|  
|**空**|**smallint**|指定 Null 屬性：<br /><br /> 1 = 資料類型可以建立成允許 Null 值。<br /><br /> 0 = 不允許 Null 值。|  
|**備註**|**Varchar (** 254 **)**|程序資料行的描述。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會傳回這個資料行的值。|  
|**COLUMN_DEF**|**Nvarchar (** 4000 **)**|資料行的預設值。|  
|**SQL_DATA_TYPE**|**smallint**|出現在描述項的 **類型** 欄位中的 SQL 資料類型值。 除了 **datetime** 和 **ISO interval** 資料類型，這個資料行與 **DATA_TYPE** 資料行相同。 這個資料行一律會傳回值。|  
|**SQL_DATETIME_SUB**|**smallint**|**datetime** ISO **interval** 子代碼 (如果 **SQL_DATA_TYPE** 的值是 **SQL_DATETIME** 或 **SQL_INTERVAL**)。 若為 **datetime** 和 ISO **interval** 以外的資料類型，此欄位為 Null。|  
|**CHAR_OCTET_LENGTH**|**int**|**字元** 或 **二進位** 資料類型資料行的最大長度（以位元組為單位）。 所有其他資料類型的這個資料行都會傳回 NULL。|  
|**ORDINAL_POSITION**|**int**|資料行在資料表中的序數位置。 資料表中的第一個資料行是 1。 這個資料行一律會傳回值。|  
|**IS_NULLABLE**|**Varchar (254)**|資料表中資料行的 Null 屬性。 遵照 ISO 規則來決定 Null 屬性。 ISO 標準 DBMS 無法傳回空字串。<br /><br /> 如果資料行可以包括 NULLS，便顯示 YES，如果資料行不能包括 NULLS，便顯示 NO。<br /><br /> 如果 Null 屬性不明，這個資料行會傳回長度為零的字串。<br /><br /> 這個資料行的傳回值不同於 NULLABLE 資料行的傳回值。|  
|**SS_DATA_TYPE**|**tinyint**|擴充預存程序所用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。 如需詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)。|  
  
## <a name="remarks"></a>備註  
 **sp_sproc_columns** 相當於 ODBC 中的 **SQLProcedureColumns** 。 傳回的結果會依 **PROCEDURE_QUALIFIER**、 **PROCEDURE_OWNER**、 **PROCEDURE_NAME**，以及參數出現在程序定義中的順序排序。  
  
## <a name="permissions"></a>權限  
 需要結構描述的 SELECT 權限。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的目錄預存程式 ](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
