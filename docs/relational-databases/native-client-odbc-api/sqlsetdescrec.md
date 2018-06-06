---
title: SQLSetDescRec | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLSetDescRec function
ms.assetid: 203d02a2-aa09-462b-a489-a2cdd6f6023b
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 257d60cfd6c25fa0234355214ac7db227f54743e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetdescrec"></a>SQLSetDescRec
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  本主題討論特有的 SQLSetDescRec 功能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端。  
  
## <a name="sqlsetdescrec-and-table-valued-parameters"></a>SQLSetDescRec 和資料表值參數  
 SQLSetDescRec 可以用來設定資料表值參數和資料表值參數資料行的描述項欄位。 只有當描述項標頭欄位 SQL_SOPT_SS_PARAM_FOCUS 設定為將 SQL_DESC_TYPE 設定為 SQL_SS_TABLE 之記錄的序數時，才可使用資料表值參數資料行。 如需有關 SQL_SOPT_SS_PARAM_FOCUS 的詳細資訊，請參閱[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 下表描述參數與描述項欄位之間的對應。  
  
|매개 변수|非資料表值參數類型的相關屬性，包括資料表值參數資料行。|資料表值參數的相關屬性|  
|---------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------|  
|*型別*|SQL_DESC_TYPE|SQL_SS_TABLE|  
|*子類型*|忽略|如果是 SQL_DATETIME 或 SQL_INTERVAL 類型的記錄，請將這個設定為 SQL_DESC_DATETIME_INTERVAL_CODE。|  
|*長度*|SQL_DESC_OCTET_LENGTH|資料表值參數類型名稱的長度。 如果此類型名稱以 null 結尾，這項設定可以是 SQL_NTS；如果不需要資料表值參數類型名稱則為零。|  
|*有效位數*|SQL_DESC_PRECISION|SQL_DESC_ARRAY_SIZE|  
|*小數位數*|SQL_DESC_SCALE|未使用的。 這個參數應為零。|  
|*DataPtr*|SQL_DESC_DATA_PTR in APD|SQL_CA_SS_TYPE_NAME<br /><br /> 這個參數對於預存程序呼叫而言是選擇性的，如果不需要的話可以指定 NULL。 必須針對不是程序呼叫的 SQL 陳述式指定這個參數。<br /><br /> *DataPtr*也可做為應用程式可用來識別這個資料表值參數，變數的資料列繫結時使用的唯一值。|  
|*StringLengthPtr*|SQL_DESC_OCTET_LENGTH_PTR|SQL_DESC_OCTET_LENGTH_PTR<br /><br /> 如果是資料表值參數，這就是要傳送的資料列數或 SQL_DATA_AT_EXEC。 這是保留與 SQLExecDirect 傳輸的資料列數目值的指標。|  
|*IndicatorPtr*|SQL_DESC_INDICATOR_PTR|SQL_DESC_INDICATOR_PTR|  
  
 如需有關資料表值參數的詳細資訊，請參閱[資料表值參數 & #40; ODBC & #41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlsetdescrec-support-for-enhanced-date-and-time-features"></a>增強型日期和時間功能的 SQLSetDescRec 支援  
 日期/時間類型所允許的值如下：  
  
||*型別*|*子類型*|*長度*|*有效位數*|*小數位數*|  
|-|------------|---------------|--------------|-----------------|-------------|  
|datetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|date|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 如需詳細資訊，請參閱[日期和時間增強功能 & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlsetdescrec-support-for-large-clr-udts"></a>大型 CLR UDT 的 SQLSetDescRec 支援  
 **SQLSetDescRec**支援大型 CLR 使用者定義型別 (Udt)。 如需詳細資訊，請參閱[Large CLR User-Defined 類型 & #40; ODBC & #41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLSetDescRec](http://go.microsoft.com/fwlink/?LinkId=80704)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
