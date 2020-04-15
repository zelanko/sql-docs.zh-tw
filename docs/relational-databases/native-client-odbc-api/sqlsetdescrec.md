---
title: SQLSetDescRec |微軟文件
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
ms.openlocfilehash: a083aa6d17a84ff4c801ad5f5b270c7f0ddcb355
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301909"
---
# <a name="sqlsetdescrec"></a>SQLSetDescRec
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主題討論特定於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端的 SQLSetDescRec 功能。  
  
## <a name="sqlsetdescrec-and-table-valued-parameters"></a>SQLSetDescRec 和資料表值參數  
 SQLSetDescRec 可用於為表值參數和表值參數列設置描述符欄位。 只有當描述項標頭欄位 SQL_SOPT_SS_PARAM_FOCUS 設定為將 SQL_DESC_TYPE 設定為 SQL_SS_TABLE 之記錄的序數時，才可使用資料表值參數資料行。 有關SQL_SOPT_SS_PARAM_FOCUS的詳細資訊,請參閱[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 下表描述參數與描述項欄位之間的對應。  
  
|參數|非表值參數類型的相關屬性,包括表值參數欄位|資料表值參數的相關屬性|  
|---------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------|  
|*型別*|SQL_DESC_TYPE|SQL_SS_TABLE|  
|*亞*|忽略|如果是 SQL_DATETIME 或 SQL_INTERVAL 類型的記錄，請將這個設定為 SQL_DESC_DATETIME_INTERVAL_CODE。|  
|*長度*|SQL_DESC_OCTET_LENGTH|資料表值參數類型名稱的長度。 如果此類型名稱以 null 結尾，這項設定可以是 SQL_NTS；如果不需要資料表值參數類型名稱則為零。|  
|*精度*|SQL_DESC_PRECISION|SQL_DESC_ARRAY_SIZE|  
|*調整*|SQL_DESC_SCALE|未使用的。 這個參數應為零。|  
|*資料Ptr*|SQL_DESC_DATA_PTR in APD|SQL_CA_SS_TYPE_NAME<br /><br /> 這個參數對於預存程序呼叫而言是選擇性的，如果不需要的話可以指定 NULL。 必須針對不是程序呼叫的 SQL 陳述式指定這個參數。<br /><br /> *DataPtr*還可用作一個唯一值,當使用變數行綁定時,應用程式可以使用該值來標識此表值參數。|  
|*字串長度 Ptr*|SQL_DESC_OCTET_LENGTH_PTR|SQL_DESC_OCTET_LENGTH_PTR<br /><br /> 如果是資料表值參數，這就是要傳送的資料列數或 SQL_DATA_AT_EXEC。 這是指向一個值的指標,該值保存要使用 SQLExecDirect 傳輸的行數。|  
|*指標Ptr*|SQL_DESC_INDICATOR_PTR|SQL_DESC_INDICATOR_PTR|  
  
 有關表值參數的詳細資訊,請參閱[&#40;ODBC&#41;的表值參數](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlsetdescrec-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLSetDescRec 支援  
 日期/時間類型所允許的值如下：  
  
||*型別*|*亞*|*長度*|*精度*|*調整*|  
|-|------------|---------------|--------------|-----------------|-------------|  
|Datetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|date|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 有關詳細資訊,請參閱[&#40;ODBC&#41;的日期和時間改進](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlsetdescrec-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLSetDescRec 支援  
 **SQLSetDescRec**支援大型 CLR 用戶定義類型 (UDT)。 有關詳細資訊,請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLSetDescRec](https://go.microsoft.com/fwlink/?LinkId=80704)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
