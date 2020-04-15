---
title: SQLGetDescRec |微軟文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLGetDescRec function
ms.assetid: f3389ff2-f3be-4035-9fb5-c9ebc2f15025
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 42c8a45bb50e5fda8946cc3819aa4702f5c2fb3f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299558"
---
# <a name="sqlgetdescrec"></a>SQLGetDescRec
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主題討論特定於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端的 SQLGetDescRec 功能。  
  
## <a name="sqlgetdescrec-and-table-valued-parameters"></a>SQLGetDescRec 和資料表值參數  
 SQLGetDescRec 可用於獲取表值參數和表值參數列的屬性的值。 SQLGetDescRec 的*RecNumber*參數對應於 SQLBind 參數的*參數編號*參數。  
  
 只有當描述項標頭欄位 SQL_SOPT_SS_PARAM_FOCUS 設定為將 SQL_DESC_TYPE 設定為 SQL_SS_TABLE 之記錄的序數時，才可使用資料表值參數資料行。 有關有關SQL_SOPT_SS_PARAM_FOCUS的詳細資訊,請參閱[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 SQLGetDescRec 傳回以下資料:  
  
|參數|資料表值參數|資料表值參數資料行和其他參數|  
|---------------|-----------------------------|----------------------------------------------------------|  
|*名稱*|預存程序呼叫的型式參數名稱，否則為 0 長度字串。|資料表值參數資料行名稱。|  
|*類型 Ptr*|SQL_DESC_TYPE。 如果是資料表值參數，這就是 SQL_SS_TABLE。|SQL_DESC_TYPE|  
|*子型別的 Ptr*|未定義|SQL_DESC_DATETIME_INTERVAL_CODE (如果是 SQL_DATETIME 或 SQL_INTERVAL 類型的記錄)。|  
|*長度Ptr*|0|SQL_DESC_OCTET_LENGTH|  
|*精密Ptr*|0|SQL_DESC_PRECISION|  
|*縮放器*|0|SQL_DESC_SCALE|  
|*空可點*|1|SQL_DESC_NULLABLE|  
  
 有關表值參數的詳細資訊,請參閱[&#40;ODBC&#41;的表值參數](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlgetdescrec-support-for-enhanced-date-and-time-features"></a>SQLGetDescRec 對於增強型日期和時間功能的支援  
 針對日期/時間類型所傳回的值如下：  
  
||*類型 Ptr*|*子型別的 Ptr*|*長度Ptr*|*精密Ptr*|*縮放器*|  
|-|---------------|------------------|-----------------|--------------------|----------------|  
|Datetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|date|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 有關詳細資訊,請參閱[&#40;ODBC&#41;的日期和時間改進](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlgetdescrec-support-for-large-clr-udts"></a>SQLGetDescRec 對於大型 CLR UDT 的支援  
 **SQLGetDescRec**支援大型 CLR 用戶定義類型 (UDT)。 有關詳細資訊,請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLGetDescRec](https://go.microsoft.com/fwlink/?LinkId=80707)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
