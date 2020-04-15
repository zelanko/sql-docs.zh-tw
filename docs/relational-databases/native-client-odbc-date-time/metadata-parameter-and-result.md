---
title: 參數和結果中繼資料 :微軟文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- metadata [ODBC]
ms.assetid: 1518e6e5-a6a8-4489-b779-064c5624df53
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8ba66c950f25663dabc3c0c46f83a7589df300ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304089"
---
# <a name="metadata---parameter-and-result"></a>中繼資料 - 參數和結果
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主題將描述在日期和時間資料類型之實作參數描述項 (IPD) 與實作資料列描述項 (IRD) 欄位中傳回的資訊。  
  
## <a name="information-returned-in-ipd-fields"></a>在 IPD 欄位中傳回的資訊  
 下列資訊會在 IPD 欄位中傳回：  
  
|參數類型|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|--------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQL_CODE_DATE|0|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|10|8,10..16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|10|8,10..16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_OCTET_LENGTH|6|12|4|8|16|20|  
|SQL_DESC_PRECISION|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_SCALE|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_TYPE|SQL_TYPE_DATE|SQL_SS_TYPE_TIME2|SQL_DATETIME|SQL_DATETIME|SQL_DATETIME|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_TYPE_NAME|**日期**|**time**|IRD 中的**小日期時間**,IPD 中的**日期時間2**|**IRD**中的日期時間 **,IPD 中的日期時間2**|**datetime2**|datetimeoffset|  
|SQL_CA_SS_VARIANT_TYPE|SQL_C_TYPE_DATE|SQL_C_TYPE_BINARY|SQL_C_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|SQL_C_TYPE_BINARY|  
|SQL_CA_SS_VARIANT_SQL_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|SQL_CA_SS_SERVER_TYPE|N/A|N/A|SQL_SS_TYPE_SMALLDATETIME|SQL_SS_TYPE_DATETIME|SQL_SS_TYPE_DEFAULT|N/A|  
  
 有時候，數值範圍會存在不連續的情況。 例如，8,10..16 中便遺漏了 9。 這是當小數有效位數大於零時增加的小數點所導致。  
  
 **datetime2**將作為**小日期**時間和**日期時間的**類型名稱返回,因為驅動程式將此作為將所有**SQL_TYPE_TIMESTAMP**值傳輸到伺服器的通用類型。  
  
 SQL_CA_SS_VARIANT_SQL_TYPE 是新的描述項欄位。 此欄位已加入 IRD 與 IPD 中,讓應用程式能夠指定與**sqlvariant** (SQL_SSVARIANT) 欄與參數關聯的值類型  
  
 SQL_CA_SS_SERVER_TYPE 是新的僅限 IPD 欄位，可讓應用程式控制繫結成 SQL_TYPE_TYPETIMESTAMP (或繫結成具有 SQL_C_TYPE_TIMESTAMP 之 C 類型的 SQL_SS_VARIANT) 的參數值如何傳送至伺服器。 如果在呼叫 SQLExecute 或 SQLExecDirect 時SQL_TYPE_TIMESTAMPSQL_DESC_CONCISE_TYPE(或SQL_SS_VARIANT c 類型,並且 C 類型SQL_C_TYPE_TIMESTAMP),則SQL_CA_SS_SERVER_TYPE的值確定參數值的表格資料流 (TDS) 類型,如下所示:  
  
|SQL_CA_SS_SERVER_TYPE 的值|SQL_DESC_PRECISION 的有效值|SQL_DESC_LENGTH 的有效值|TDS 類型|  
|----------------------------------------|-------------------------------------------|----------------------------------------|--------------|  
|SQL_SS_TYPE_DEFAULT|0..7|19, 21..27|**datetime2**|  
|SQL_SS_TYPE_SMALLDATETIME|0|19|**smalldatetime**|  
|SQL_SS_TYPE_DATETIME|3|23|**datetime**|  
  
 SQL_CA_SS_SERVER_TYPE 的預設設定為 SQL_SS_TYPE_DEFAULT。 SQL_DESC_PRECISION 和 SQL_DESC_LENGTH 的設定會使用 SQL_CA_SS_SERVER_TYPE 的設定進行驗證，如上表所述。 如果這項驗證失敗，系統就會傳回 SQL_ERROR 並且使用 SQLState 07006 和訊息「限制的資料類型屬性違規」來記錄診斷記錄。 如果 SQL_CA_SS_SERVER_TYPE 設定為 SQL_SS_TYPE DEFAULT 以外的值，而且 DESC_CONCISE_TYPE 不是 SQL_TYPE_TIMESTAMP，系統也會傳回這個錯誤。 這些驗證會在發生描述項一致性違規時執行，例如：  
  
-   當 SQL_DESC_DATA_PTR 已變更時。  
  
-   在準備或執行階段 (呼叫 SQLExecute、SQLExecDirect、SQLSetPos 或 SQLBulkOperations 時) 中。  
  
-   當應用程式通過禁用延遲準備調用 SQLPrepare 來強制非延遲準備,或者為已準備但未執行的語句調用 SQLNumResultCols、SQLDescribeCol 或 SQLDescribeParam 來強制準備。  
  
 當SQL_CA_SS_SERVER_TYPE由對 SQLSetDescField 的調用設置時,其值必須SQL_SS_TYPE_DEFAULT、SQL_SS_TYPE_SMALLDATETIME或SQL_SS_TYPE_DATETIME。 否則，系統就會傳回 SQL_ERROR 並且使用 SQLState HY092 和訊息「屬性/選項識別碼無效」來記錄診斷記錄。  
  
 SQL_CA_SS_SERVER_TYPE屬性可以由依賴於**日期時間和****小日期時間**支援的功能的應用程式使用,但不能由**日期時間2**來使用。 例如 **,datetime2**需要使用**日期add**和**dateiif**函數,而**日期時間和****小日期時間**也允許算術運算符。 大部分應用程式都不需要使用這個屬性，而且應該避免使用這個屬性。  
  
## <a name="information-returned-in-ird-fields"></a>在 IRD 欄位中傳回的資訊  
 下列資訊會在 IRD 欄位中傳回：  
  
|資料行類型|date|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|-----------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_CONCISE_TYPE|SQL_TYPE_DATE|SQL_SS_TIME2|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_TYPE_TIMESTAMP|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQL_CODE_DATE|0|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|SQL_CODE_TIMESTAMP|0|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|10|8,10..16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_DISPLAY_SIZE|10|8,10..16|16|23|19, 21..27|26, 28..34|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|SQL_FALSE|  
|SQL_DESC_LENGTH|10|8,10..16|16|2|19, 21..27|26, 28..34|  
|SQL_DESC_LITERAL_PREFIX|'|'|'|'|'|'|  
|SQL_DESC_LITERAL_SUFFIX|'|'|'|'|'|'|  
|SQL_DESC_LOCAL_TYPE_NAME|**日期**|**time**|**smalldatetime**|**datetime**|**datetime2**|datetimeoffset|  
|SQL_DESC_OCTET_LENGTH|6|12|4|8|16|20|  
|SQL_DESC_PRECISION|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_SCALE|0|0..7|0|3|0..7|0..7|  
|SQL_DESC_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|SQL_PRED_SEARCHABLE|  
|SQL_DESC_TYPE|SQL_DATETIME|SQL_SS_TIME2|SQL_DATETIME|SQL_DATETIME|SQL_DATETIME|SQL_SS_TIMESTAMPOFFSET|  
|SQL_DESC_TYPE_NAME|**日期**|**time**|**smalldatetime**|**datetime**|**datetime2**|datetimeoffset|  
|SQL_DESC_UNSIGNED|SQL_TRUE|SQL_TRUE|SQL_TRUE|SQL_TRUE|SQL_TRUE|SQL_TRUE|  
  
## <a name="see-also"></a>另請參閱  
 [中繼資料&#40;ODBC&#41;](https://msdn.microsoft.com/library/99133efc-b1f2-46e9-8203-d90c324a8e4c)  
  
  
