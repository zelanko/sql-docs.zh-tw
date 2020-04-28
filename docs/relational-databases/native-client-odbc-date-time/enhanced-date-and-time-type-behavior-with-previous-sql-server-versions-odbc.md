---
title: SQL 版本中的日期時間（ODBC）
ms.custom: ''
ms.date: 12/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC], enhanced behavior with earlier SQL Server versions
ms.assetid: cd4e137f-dc5e-4df7-bc95-51fe18c587e0
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8e5147a8eef08c70605bf13f6c1cb04887d0d926
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301876"
---
# <a name="enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc"></a>舊版 SQL Server 的增強型日期/時間類型行為 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主題描述使用增強型日期和時間增強功能的用戶端應用程式與早於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 版本進行通訊時，以及使用 Microsoft Data Access Components、Windows Data Access Components，或早於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Native Client 版本的應用程式將命令傳送到支援增強型日期和時間功能的伺服器時的預期行為。  
  
## <a name="down-level-client-behavior"></a>下層用戶端行為  
 使用早於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Native Client 版本編譯的用戶端應用程式會將新的日期/時間類型視為 nvarchar 資料行。 資料行內容是常值標記法，如[ODBC 日期和時間改善的資料類型支援的](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)「資料格式：字串和常值」一節中所述。 資料行大小是針對資料行指定之小數秒有效位數的最大常值長度。  
  
 資料庫目錄 API 將會傳回與傳回到用戶端之下層資料類型程式碼一致的中繼資料 (例如，nvarchar)，以及相關聯的下層表示法 (例如，適當的常值格式)。 不過，傳回的資料類型名稱將會是實際的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 類型名稱。  
  
 SQLDescribeCol、SQLDescribeParam、SQGetDescField 和 SQLColAttribute 所傳回的語句中繼資料，會傳回與下層類型一致的中繼資料，包括類型名稱。 這類下層類型的範例是**Nvarchar**。  
  
 當下層用戶端應用程式針對已建立日期[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] /時間類型的架構變更的（或更新版本）伺服器執行時，預期的行為如下所示：  
  
|SQL Server 2005 類型|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (或更新版本) 類型|ODBC 用戶端類型|結果轉換 (SQL 到 C)|參數轉換 (C 到 SQL)|  
|--------------------------|----------------------------------------------|----------------------|------------------------------------|---------------------------------------|  
|Datetime|Date|SQL_C_TYPE_DATE|[確定]|確定（1）|  
|||SQL_C_TYPE_TIMESTAMP|時間欄位會設定為零。|OK (2)<br /><br /> 如果時間欄位不為零，就會失敗。 使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。|  
||Time(0)|SQL_C_TYPE_TIME|[確定]|確定（1）|  
|||SQL_C_TYPE_TIMESTAMP|日期欄位設定為目前的日期。|OK (2)<br /><br /> 忽略日期。 如果小數秒不是零，就會失敗。 使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。|  
||Time(7)|SQL_C_TIME|失敗-不正確時間常值。|確定（1）|  
|||SQL_C_TYPE_TIMESTAMP|失敗-不正確時間常值。|確定（1）|  
||Datetime2 （3）|SQL_C_TYPE_TIMESTAMP|[確定]|確定（1）|  
||Datetime2 （7）|SQL_C_TYPE_TIMESTAMP|[確定]|用戶端轉換會將值捨入為 1/300 秒。|  
|Smalldatetime|Date|SQL_C_TYPE_DATE|[確定]|[確定]|  
|||SQL_C_TYPE_TIMESTAMP|時間欄位會設定為零。|OK (2)<br /><br /> 如果時間欄位不為零，就會失敗。 使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。|  
||Time(0)|SQL_C_TYPE_TIME|[確定]|[確定]|  
|||SQL_C_TYPE_TIMESTAMP|日期欄位設定為目前的日期。|OK (2)<br /><br /> 忽略日期。 如果小數秒不是零，就會失敗。<br /><br /> 使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。|  
||Datetime2(0)|SQL_C_TYPE_TIMESTAMP|[確定]|[確定]|  
|||||

## <a name="key-to-symbols"></a>符號的索引鍵  
  
|符號|意義|  
|------------|-------------|  
|1|如果它使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，則應繼續使用更新版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|2|使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 的應用程式可能會因為更新版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 而失敗。|  
|||

 請注意，只有最常見的結構描述變更已經列入考慮。 以下是最常見的變更：  
  
-   在符合邏輯之處使用新的類型時，應用程式僅需要一個日期或時間值。 不過，系統會強迫應用程式使用 datetime 或 smalldatetime，因為沒有個別的日期和時間類型。  
  
-   使用新類型會得到額外的小數秒精確度或正確度。  
  
-   切換到 datetime2，因為這是慣用的日期和時間資料類型。  
  
### <a name="column-metadata-returned-by-sqlcolumns-sqlprocedurecolumns-and-sqlspecialcolumns"></a>SQLColumns、SQLProcedureColumns 和 SQLSpecialColumns 傳回的資料行中繼資料  
 系統會傳回日期/時間類型的下列資料行值：  
  
|資料行類型|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|-----------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_WVARCHAR|SQL_WVARCHAR|  
|TYPE_NAME|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|COLUMN_SIZE|10|8、10、16|16|23|19, 21..27|26, 28..34|  
|BUFFER_LENGTH|20|16、20. 32|16|16|38，42. 54|52、56. 68|  
|DECIMAL_DIGITS|NULL|NULL|0|3|NULL|NULL|  
|SQL_DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_DATETIME|SQL_DATETIME|SQL_WVARCHAR|SQL_WVARCHAR|  
|SQL_DATETIME_SUB|NULL|NULL|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|NULL|NULL|  
|CHAR_OCTET_LENGTH|NULL|NULL|NULL|NULL|NULL|NULL|  
|SS_DATA_TYPE|0|0|111|111|0|0|  
||||||||

 SQLSpecialColumns 不會傳回 SQL_DATA_TYPE、SQL_DATETIME_SUB、CHAR_OCTET_LENGTH 或 SS_DATA_TYPE。  
  
### <a name="data-type-metadata-returned-by-sqlgettypeinfo"></a>SQLGetTypeInfo 傳回的資料類型中繼資料  
 系統會傳回日期/時間類型的下列資料行值：  
  
|資料行類型|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|-----------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_WVARCHAR|SQL_WVARCHAR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|'|'|'|'|'|'|  
|LITERAL_SUFFIX|'|'|'|'|'|'|  
|CREATE_PARAMS|NULL|NULL|NULL|NULL|NULL|NULL|  
|NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|SQL_NULLABLE|  
|CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|AUTO_UNIQUE_VALUE|NULL|NULL|NULL|NULL|NULL|NULL|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|NULL|0|3|NULL|NULL|  
|MAXIMUM_SCALE|NULL|NULL|0|3|NULL|NULL|  
|SQL_DATA_TYPE|SQL_WVARCHAR|SQL_WVARCHAR|SQL_DATETIME|SQL_DATETIME|SQL_WVARCHAR|SQL_WVARCHAR|  
|SQL_DATETIME_SUB|NULL|NULL|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|NULL|NULL|  
|NUM_PREC_RADIX|NULL|NULL|NULL|NULL|NULL|NULL|  
|INTERVAL_PRECISION|NULL|NULL|NULL|NULL|NULL|NULL|  
|USERTYPE|0|0|12|22|0|0|  
||||||||

## <a name="down-level-server-behavior"></a>下層伺服器行為  
 連接到舊版 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 的伺服器執行個體時，嘗試使用新的伺服器類型或相關聯的中繼資料程式碼和描述元欄位都會傳回 SQL_ERROR。 系統將會產生包含 SQLSTATE HY004 和訊息「連接時，伺服器版本的 SQL 資料類型無效」的診斷記錄，或包含 07006 和訊息「限制的資料類型屬性違規」的診斷記錄。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC&#41;&#40;的日期和時間改善](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
