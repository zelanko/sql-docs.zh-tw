---
title: SQLSetDescRec |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetDescRec function
ms.assetid: 203d02a2-aa09-462b-a489-a2cdd6f6023b
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 785c5f308745f93070dae4ca5a5e7355e8359764
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86012405"
---
# <a name="sqlsetdescrec"></a>SQLSetDescRec
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  本主題討論 Native Client 特有的 SQLSetDescRec 功能 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="sqlsetdescrec-and-table-valued-parameters"></a>SQLSetDescRec 和資料表值參數  
 SQLSetDescRec 可以用來設定資料表值參數和資料表值參數資料行的描述項欄位。 只有當描述項標頭欄位 SQL_SOPT_SS_PARAM_FOCUS 設定為將 SQL_DESC_TYPE 設定為 SQL_SS_TABLE 之記錄的序數時，才可使用資料表值參數資料行。 如需 SQL_SOPT_SS_PARAM_FOCUS 的詳細資訊，請參閱[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 下表描述參數與描述項欄位之間的對應。  
  
|參數|非資料表值參數類型的相關屬性，包括資料表值參數資料行|資料表值參數的相關屬性|  
|---------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------|  
|*型別*|SQL_DESC_TYPE|SQL_SS_TABLE|  
|*類型*|忽略|如果是 SQL_DATETIME 或 SQL_INTERVAL 類型的記錄，請將這個設定為 SQL_DESC_DATETIME_INTERVAL_CODE。|  
|*長度*|SQL_DESC_OCTET_LENGTH|資料表值參數類型名稱的長度。 如果此類型名稱以 null 結尾，這項設定可以是 SQL_NTS；如果不需要資料表值參數類型名稱則為零。|  
|*有效位數*|SQL_DESC_PRECISION|SQL_DESC_ARRAY_SIZE|  
|*縮放比例*|SQL_DESC_SCALE|未使用的。 這個參數應為零。|  
|*DataPtr*|SQL_DESC_DATA_PTR in APD|SQL_CA_SS_TYPE_NAME<br /><br /> 這個參數對於預存程序呼叫而言是選擇性的，如果不需要的話可以指定 NULL。 必須針對不是程序呼叫的 SQL 陳述式指定這個參數。<br /><br /> *DataPtr*也可做為唯一的值，應用程式可以在使用變數資料列系結時，用來識別這個資料表值參數。|  
|*StringLengthPtr*|SQL_DESC_OCTET_LENGTH_PTR|SQL_DESC_OCTET_LENGTH_PTR<br /><br /> 如果是資料表值參數，這就是要傳送的資料列數或 SQL_DATA_AT_EXEC。 這是值的指標，其中包含要與 SQLExecDirect 一起傳送的資料列數目。|  
|*IndicatorPtr*|SQL_DESC_INDICATOR_PTR|SQL_DESC_INDICATOR_PTR|  
  
 如需資料表值參數的詳細資訊，請參閱[ODBC&#41;&#40;的資料表值參數](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlsetdescrec-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLSetDescRec 支援  
 日期/時間類型所允許的值如下：  
  
||*型別*|*類型*|*長度*|*有效位數*|*縮放比例*|  
|-|------------|---------------|--------------|-----------------|-------------|  
|Datetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|date|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 如需詳細資訊，請參閱[ODBC&#41;&#40;的日期和時間改善](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlsetdescrec-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLSetDescRec 支援  
 **SQLSetDescRec**支援大型 CLR 使用者定義型別（udt）。 如需詳細資訊，請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLSetDescRec](https://go.microsoft.com/fwlink/?LinkId=80704)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
