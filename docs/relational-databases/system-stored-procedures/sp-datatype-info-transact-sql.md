---
description: sp_datatype_info (Transact-SQL)
title: sp_datatype_info (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 05/25/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_datatype_info_TSQL
- sp_datatype_info
dev_langs:
- TSQL
helpviewer_keywords:
- sp_datatype_info
ms.assetid: 045f3b5d-6bb7-4748-8b4c-8deb4bc44147
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f35043a8886165431e42b4b8641a1abbcf0fb1cf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486097"
---
# <a name="sp_datatype_info-transact-sql"></a>sp_datatype_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  傳回目前環境所支援之資料類型的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_datatype_info [ [ @data_type = ] data_type ]   
     [ , [ @ODBCVer = ] odbc_version ]   
```  
  
## <a name="arguments"></a>引數  
`[ @data_type = ] data_type` 這是指定之資料類型的代碼編號。 若要取得所有資料類型的清單，請省略這個參數。 *data_type* 是 **int**，預設值是0。  
  
`[ @ODBCVer = ] odbc_version` 這是所使用的 ODBC 版本。 *odbc_version* 是 **Tinyint**，預設值是2。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|TYPE_NAME|**sysname**|DBMS 相依資料類型。|  
|DATA_TYPE|**smallint**|這個類型的所有資料行所對應之 ODBC 類型的代碼。|  
|PRECISION|**int**|資料來源的資料類型最大有效位數。 有效位數不適用的資料類型會傳回 NULL。 PRECISION 資料行的傳回值為十進位數。|  
|LITERAL_PREFIX|**Varchar (** 32 **) **|常數前面所用的一或多個字元。 例如，單引號 (**'**) 用於字元類型，0x 用於二進位。|  
|LITERAL_SUFFIX|**Varchar (** 32 **) **|用來結束常數的一或多個字元。 例如，單引號 (**'**) 用於字元類型，而不是二進位引號。|  
|CREATE_PARAMS|**Varchar (** 32 **) **|這個資料類型之建立參數的描述。 例如， **decimal** 為 "precision，scale"， **float** 為 Null，且 **Varchar** 為 "max_length"。|  
|NULLABLE|**smallint**|指定 Null 屬性。<br /><br /> 1 = 允許 Null 值。<br /><br /> 0 = 不允許 Null 值。|  
|CASE_SENSITIVE|**smallint**|指定是否區分大小寫。<br /><br /> 1 = 這類型的所有資料行都會區分大小寫 (用於定序)。<br /><br /> 0 = 這個類型的所有資料行都不區分大小寫。|  
|可搜尋|**smallint**|指定資料行類型的搜尋功能：<br /><br /> 1 = 無法搜尋。<br /><br /> 2 = 可使用 LIKE 搜尋。<br /><br /> 3 = 可使用 WHERE 搜尋。<br /><br /> 4 = 可使用 WHERE 或 LIKE 搜尋。|  
|UNSIGNED_ATTRIBUTE|**smallint**|指定資料類型的正負號。<br /><br /> 1 = 資料類型不帶正負號。<br /><br /> 0 = 資料類型帶正負號。|  
|MONEY|**smallint**|指定 **money** 資料類型。<br /><br /> 1 = **money** 資料類型。<br /><br /> 0 = 不是 **money** 資料類型。|  
|AUTO_INCREMENT|**smallint**|指定自動累加。<br /><br /> 1 = 自動累加。<br /><br /> 0 = 不自動累加。<br /><br /> NULL = 屬性不適用。<br /><br /> 應用程式可以將值插入包含這個屬性的資料行中，但應用程式不能更新這個資料行中的值。 除了 **bit** 資料類型之外，AUTO_INCREMENT 僅適用于屬於精確數值和近似數值資料類型類別目錄的資料類型。|  
|LOCAL_TYPE_NAME|**sysname**|資料類型之資料來源相依名稱的當地語系化版本。 例如，法文的 DECIMAL 是 DECIMALE。 如果資料來源不支援當地語系化名稱，便傳回 NULL。|  
|MINIMUM_SCALE|**smallint**|資料來源的資料類型最小小數位數。 如果資料類型有固定的小數位數，MINIMUM_SCALE 和 MAXIMUM_SCALE 資料行都包含這個值。 當小數位數不適用時，會傳回 NULL。|  
|MAXIMUM_SCALE|**smallint**|資料來源的資料類型最大小數位數。 如果未在資料來源上個別定義最大小數位數，而是定義成與最大有效位數相同，這個資料行會包含與 PRECISION 資料行相同的值。|  
|SQL_DATA_TYPE|**smallint**|SQL 資料類型出現在描述子之 TYPE 欄位時的值。 除了 **datetime** 和 ANSI **interval** 資料類型以外，這個資料行與 DATA_TYPE 資料行相同。 這個欄位一律會傳回值。|  
|SQL_DATETIME_SUB|**smallint**|如果 SQL_DATA_TYPE 的值是 SQL_DATETIME 或 SQL_INTERVAL，則為**日期時間**或 ANSI**間隔**子代碼。 若為 **datetime** 和 ANSI **間隔**以外的資料類型，此欄位為 Null。|  
|NUM_PREC_RADIX|**int**|用來計算資料行所能保留的最大數字之位元或位數數目。 如果資料類型是近似數值資料類型，這個資料行會包含 2 這個值來表示多個位元。 如果是精確數值類型，這個資料行會包含 10 這個值來表示多個十進位數。 否則，這個資料行就是 NULL。 藉由組合有效位數和基數，應用程式可以計算資料行所能保留的最大數目。|  
|INTERVAL_PRECISION|**smallint**|如果 *data_type* 為 **間隔**，則為間隔前置精確度的值;否則為 Null。|  
|USERTYPE|**smallint**|從 systypes 資料表**usertype**值。|  
  
## <a name="remarks"></a>備註  
 sp_datatype_info 相當於 ODBC 中的 SQLGetTypeInfo。 傳回的結果是依 DATA_TYPE 排序，之後，再依資料類型與對應的 ODBC SQL 資料類型的對應緊密程度來排序。  
  
## <a name="permissions"></a>權限  
 需要 public 角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會藉由指定的*data_type*值，來取得**sysname**和**Nvarchar**資料類型的資訊 `-9` 。  
  
```  
USE master;  
GO  
EXEC sp_datatype_info -9;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的資料庫引擎預存程式 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
