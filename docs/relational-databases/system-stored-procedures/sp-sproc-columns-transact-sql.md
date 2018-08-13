---
title: sp_sproc_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_sproc_columns
- sp_sproc_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_sproc_columns
ms.assetid: 62c18c21-35c5-4772-be0d-ffdcc19c97ab
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 71a70042d76f24179040256139502daab7105bc0
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39565412"
---
# <a name="spsproccolumns-transact-sql"></a>sp_sproc_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回目前環境中單一預存程序或使用者自訂函數的資料行資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_sproc_columns [[@procedure_name = ] 'name']   
    [ , [@procedure_owner = ] 'owner']   
    [ , [@procedure_qualifier = ] 'qualifier']   
    [ , [@column_name = ] 'column_name']  
    [ , [@ODBCVer = ] 'ODBCVer']  
    [ , [@fUsePattern = ] 'fUsePattern']  
```  
  
## <a name="arguments"></a>引數  
 [ **@procedure_name =** ] **'***name***'**  
 這是用來傳回目錄資訊的程序名稱。 *名稱*已**nvarchar (** 390 **)**，預設值是 %，代表目前資料庫中的所有資料表。 支援萬用字元的模式比對。  
  
 [  **@procedure_owner =**] **'***擁有者***'**  
 這是程序擁有者的名稱。 *擁有者*已**nvarchar (** 384 **)**，預設值是 NULL。 支援萬用字元的模式比對。 如果*擁有者*未指定，會套用基礎 DBMS 的預設程序可見性規則。  
  
 如果目前使用者擁有含指定名稱的程序，就會傳回這個程序的相關資訊。 如果*擁有者*未指定且目前使用者並未擁有指定之名稱的程序**sp_sproc_columns**會尋找具有指定名稱的資料庫擁有者所擁有的程序。 如果程序存在，就會傳回它的資料行的相關資訊。  
  
 [  **@procedure_qualifier =**] **'***限定詞***'**  
 這是程序限定詞的名稱。 *限定詞*已**sysname**，預設值是 NULL。 各種 DBMS 產品都支援三部分的資料表命名 (*qualifier.owner.name*)。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這個參數代表資料庫名稱。 在某些產品中，它代表資料表之資料庫環境的伺服器名稱。  
  
 [ **@column_name =**] **'***column_name***'**  
 這是個單一資料行，當只需要一個目錄資訊的資料行時，便會使用這個單一資料行。 *column_name*已**nvarchar (** 384 **)**，預設值是 NULL。 如果*column_name*已省略，會傳回所有資料行。 支援萬用字元的模式比對。 若要有最大交互操作能力，閘道用戶端應該只採用 ISO 標準模式比對 (% 和 _ 萬用字元)。  
  
 [  **@ODBCVer =**] **'***ODBCVer***'**  
 這是所使用的 ODBC 版本。 *ODBCVer*已**int**，預設值是 2，表示 ODBC 2.0 版。 如需有關 ODBC 2.0 版和 ODBC 3.0 版之間的差異的詳細資訊，請參閱 ODBC **SQLProcedureColumns** odbc 3.0 版規格  
  
 [  **@fUsePattern =**] **'***fUsePattern***'**  
 判斷是否將底線 (_)、百分比 (%) 和方括號 ([ ]) 字元解譯成萬用字元。 有效值是 0 (關閉模式比對) 和 1 (開啟模式比對)。 *fUsePattern*已**元**，預設值是 1。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**PROCEDURE_QUALIFIER**|**sysname**|程序限定詞名稱。 這個資料行可以是 NULL。|  
|**PROCEDURE_OWNER**|**sysname**|程序擁有者名稱。 這個資料行一律會傳回值。|  
|**程序名稱**|**nvarchar (** 134 **)**|程序名稱。 這個資料行一律會傳回值。|  
|**COLUMN_NAME**|**sysname**|每個資料行的資料行名稱**TABLE_NAME**傳回。 這個資料行一律會傳回值。|  
|**COLUMN_TYPE**|**smallint**|這個欄位一律會傳回值：<br /><br /> 0 = SQL_PARAM_TYPE_UNKNOWN<br /><br /> 1 = SQL_PARAM_TYPE_INPUT<br /><br /> 2 = SQL_PARAM_TYPE_OUTPUT<br /><br /> 3 = SQL_RESULT_COL<br /><br /> 4 = SQL_PARAM_OUTPUT<br /><br /> 5 = SQL_RETURN_VALUE|  
|**DATA_TYPE**|**smallint**|ODBC 資料類型的整數碼。 如果這個資料類型無法對應至 ISO 類型，此值就是 NULL。 原生資料型別名稱都會傳入**TYPE_NAME**資料行。|  
|**TYPE_NAME**|**sysname**|資料類型的字串表示法。 這是基礎 DBMS 所提供的資料類型名稱。|  
|**PRECISION**|**int**|有效位數的數目。 傳回值**精確度**資料行是在基底為 10。|  
|**LENGTH**|**int**|資料的傳送大小。|  
|**SCALE**|**smallint**|小數點右側的位數。|  
|**RADIX**|**smallint**|這是數值類型的基底。|  
|**可為 NULL**|**smallint**|指定 Null 屬性：<br /><br /> 1 = 資料類型可以建立成允許 Null 值。<br /><br /> 0 = 不允許 Null 值。|  
|**註解**|**varchar (** 254 **)**|程序資料行的描述。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會傳回這個資料行的值。|  
|**COLUMN_DEF**|**nvarchar (** 4000 **)**|資料行的預設值。|  
|**SQL_DATA_TYPE**|**smallint**|它會出現在 SQL 資料類型的值**型別**描述項欄位。 這個資料行是相同**DATA_TYPE**資料行，除了**datetime**和 ISO**間隔**資料型別。 這個資料行一律會傳回值。|  
|**SQL_DATETIME_SUB**|**smallint**|**Datetime** ISO**間隔**子代碼，如果值**SQL_DATA_TYPE**是**SQL_DATETIME**或**SQL_INTERVAL**. 資料類型以外**datetime**和 ISO**間隔**，這個欄位是 NULL。|  
|**CHAR_OCTET_LENGTH**|**int**|以位元組為單位的最大長度**字元**或是**二進位**資料類型資料行。 所有其他資料類型的這個資料行都會傳回 NULL。|  
|**ORDINAL_POSITION**|**int**|資料行在資料表中的序數位置。 資料表中的第一個資料行是 1。 這個資料行一律會傳回值。|  
|**IS_NULLABLE**|**varchar(254)**|資料表中資料行的 Null 屬性。 遵照 ISO 規則來決定 Null 屬性。 ISO 標準 DBMS 無法傳回空字串。<br /><br /> 如果資料行可以包括 NULLS，便顯示 YES，如果資料行不能包括 NULLS，便顯示 NO。<br /><br /> 如果 Null 屬性不明，這個資料行會傳回長度為零的字串。<br /><br /> 這個資料行的傳回值不同於 NULLABLE 資料行的傳回值。|  
|**SS_DATA_TYPE**|**tinyint**|擴充預存程序所用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。 如需詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)。|  
  
## <a name="remarks"></a>備註  
 **sp_sproc_columns**相當於**SQLProcedureColumns** ODBC 中。 傳回的結果都會按照**PROCEDURE_QUALIFIER**， **PROCEDURE_OWNER**， **PROCEDURE_NAME**，以及參數出現在此程序的順序定義。  
  
## <a name="permissions"></a>Permissions  
 需要結構描述的 SELECT 權限。  
  
## <a name="see-also"></a>另請參閱  
 [目錄預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
