---
title: sp_datatype_info_90 （SQL 資料倉儲） |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 1d043964-dc6e-4c3e-ab61-bc444d5e25ae
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 69d37727f321e4fd2f38ca30184baba6ab432fe9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62507319"
---
# <a name="spdatatypeinfo90-sql-data-warehouse"></a>sp_datatype_info_90 （SQL 資料倉儲）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  傳回目前環境所支援之資料類型的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_datatype_info_90 [ [ @data_type = ] data_type ]   
     [ , [ @ODBCVer = ] odbc_version ]   
```  
  
## <a name="arguments"></a>引數  
`[ @data_type = ] data_type` 為指定的資料類型的代碼。 若要取得所有資料類型的清單，請省略這個參數。 *data_type*已**int**，預設值是 0。  
  
`[ @ODBCVer = ] odbc_version` 是用的 ODBC 版本。 *odbc_version&lt*已**tinyint**，預設值是 2。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|TYPE_NAME|**sysname**|DBMS 相依資料類型。|  
|DATA_TYPE|**smallint**|這個類型的所有資料行所對應之 ODBC 類型的代碼。|  
|PRECISION|**int**|資料來源的資料類型最大有效位數。 有效位數不適用的資料類型會傳回 NULL。 PRECISION 資料行的傳回值為十進位數。|  
|LITERAL_PREFIX|**varchar(** 32 **)**|常數前面所用的一或多個字元。 例如，單引號 (**'**) 用於字元類型，0x 用於二進位。|  
|LITERAL_SUFFIX|**varchar(** 32 **)**|用來結束常數的一或多個字元。 例如，單引號 (**'**) 用於字元類型，而二進位不用引號。|  
|CREATE_PARAMS|**varchar(** 32 **)**|這個資料類型之建立參數的描述。 例如，**十進位**是"precision，scale"， **float**是 NULL，並**varchar**是"max_length"。|  
|NULLABLE|**smallint**|指定 Null 屬性。<br /><br /> 1 = 允許 Null 值。<br /><br /> 0 = 不允許 Null 值。|  
|CASE_SENSITIVE|**smallint**|指定是否區分大小寫。<br /><br /> 1 = 這類型的所有資料行都會區分大小寫 (用於定序)。<br /><br /> 0 = 這個類型的所有資料行都不區分大小寫。|  
|SEARCHABLE|**smallint**|指定資料行類型的搜尋功能：<br /><br /> 1 = 無法搜尋。<br /><br /> 2 = 可使用 LIKE 搜尋。<br /><br /> 3 = 可使用 WHERE 搜尋。<br /><br /> 4 = 可使用 WHERE 或 LIKE 搜尋。|  
|UNSIGNED_ATTRIBUTE|**smallint**|指定資料類型的正負號。<br /><br /> 1 = 資料類型不帶正負號。<br /><br /> 0 = 資料類型帶正負號。|  
|MONEY|**smallint**|指定**金錢**資料型別。<br /><br /> 1 =**金錢**資料型別。<br /><br /> 0 = 未**金錢**資料型別。|  
|AUTO_INCREMENT|**smallint**|指定自動累加。<br /><br /> 1 = 自動累加。<br /><br /> 0 = 不自動累加。<br /><br /> NULL = 屬性不適用。<br /><br /> 應用程式可以將值插入包含這個屬性的資料行中，但應用程式不能更新這個資料行中的值。 除了**元**資料類型只適用於屬於精確數值 」 和近似數值資料類型類別目錄的資料類型是 AUTO_INCREMENT&AMP;LT。|  
|LOCAL_TYPE_NAME|**sysname**|資料類型之資料來源相依名稱的當地語系化版本。 例如，法文的 DECIMAL 是 DECIMALE。 如果資料來源不支援當地語系化名稱，便傳回 NULL。|  
|MINIMUM_SCALE|**smallint**|資料來源的資料類型最小小數位數。 如果資料類型有固定的小數位數，MINIMUM_SCALE 和 MAXIMUM_SCALE 資料行都包含這個值。 當小數位數不適用時，會傳回 NULL。|  
|MAXIMUM_SCALE|**smallint**|資料來源的資料類型最大小數位數。 如果未在資料來源上個別定義最大小數位數，而是定義成與最大有效位數相同，這個資料行會包含與 PRECISION 資料行相同的值。|  
|SQL_DATA_TYPE|**smallint**|SQL 資料類型出現在描述子之 TYPE 欄位時的值。 此資料行等同於 DATA_TYPE 資料行，除了**datetime**和 ANSI**間隔**資料型別。 這個欄位一律會傳回值。|  
|SQL_DATETIME_SUB|**smallint**|**日期時間**或 ANSI**間隔**如果 SQL_DATA_TYPE 的值是 SQL_DATETIME 或 SQL_INTERVAL 子代碼。 資料類型以外**datetime**和 ANSI**間隔**，這個欄位是 NULL。|  
|NUM_PREC_RADIX|**int**|用來計算資料行所能保留的最大數字之位元或位數數目。 如果資料類型是近似數值資料類型，這個資料行會包含 2 這個值來表示多個位元。 如果是精確數值類型，這個資料行會包含 10 這個值來表示多個十進位數。 否則，這個資料行就是 NULL。 藉由組合有效位數和基數，應用程式可以計算資料行所能保留的最大數目。|  
|INTERVAL_PRECISION|**smallint**|值的間隔開頭有效位數，如果*data_type*是**間隔**，否則為 NULL。|  
|USERTYPE|**smallint**|**usertype** systypes 資料表的值。|  
  
## <a name="remarks"></a>備註  
 sp_datatype_info 相當於 ODBC 中的 SQLGetTypeInfo。 傳回的結果是依 DATA_TYPE 排序，之後，再依資料類型與對應的 ODBC SQL 資料類型的對應緊密程度來排序。  
  
## <a name="permissions"></a>Permissions  
 需要 public 角色中的成員資格。  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會擷取資訊**sysname**並**nvarchar**藉由指定的資料型別*data_type*的值`-9`。  
  
```  
USE master;  
GO  
EXEC sp_datatype_info_90 -9;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲預存程序](../../relational-databases/system-stored-procedures/sql-data-warehouse-stored-procedures.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  

