---
title: SQLGetDescRec |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLGetDescRec function
ms.assetid: f3389ff2-f3be-4035-9fb5-c9ebc2f15025
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41bd489752dc1b4084d9c012cad97413c6ff98b5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62657711"
---
# <a name="sqlgetdescrec"></a>SQLGetDescRec
  本主題討論[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 特有的 SQLGetDescRec 功能。  
  
## <a name="sqlgetdescrec-and-table-valued-parameters"></a>SQLGetDescRec 和資料表值參數  
 SQLGetDescRec 可以用來取得資料表值參數和資料表值參數資料行的屬性值。 SQLGetDescRec 的*RecNumber*參數對應至 SQLBindParameter 的*ParameterNumber*參數。  
  
 只有當描述項標頭欄位 SQL_SOPT_SS_PARAM_FOCUS 設定為將 SQL_DESC_TYPE 設定為 SQL_SS_TABLE 之記錄的序數時，才可使用資料表值參數資料行。 如需有關 SQL_SOPT_SS_PARAM_FOCUS 的詳細資訊，請參閱[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
 SQLGetDescRec 會傳回下列資料：  
  
|參數|資料表值參數|資料表值參數資料行和其他參數|  
|---------------|-----------------------------|----------------------------------------------------------|  
|*名稱*|預存程序呼叫的型式參數名稱，否則為 0 長度字串。|資料表值參數資料行名稱。|  
|*TypePtr*|SQL_DESC_TYPE。 如果是資料表值參數，這就是 SQL_SS_TABLE。|SQL_DESC_TYPE|  
|*SubTypePtr*|未定義|SQL_DESC_DATETIME_INTERVAL_CODE (如果是 SQL_DATETIME 或 SQL_INTERVAL 類型的記錄)。|  
|*LengthPtr*|0|SQL_DESC_OCTET_LENGTH|  
|*PrecisionPtr*|0|SQL_DESC_PRECISION|  
|*ScalePtr*|0|SQL_DESC_SCALE|  
|*NullablePtr*|1|SQL_DESC_NULLABLE|  
  
 如需資料表值參數的詳細資訊，請參閱[ODBC&#41;&#40;的資料表值參數](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="sqlgetdescrec-support-for-enhanced-date-and-time-features"></a>SQLGetDescRec 對於增強型日期和時間功能的支援  
 針對日期/時間類型所傳回的值如下：  
  
||*TypePtr*|*SubTypePtr*|*LengthPtr*|*PrecisionPtr*|*ScalePtr*|  
|-|---------------|------------------|-----------------|--------------------|----------------|  
|Datetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|4|3|3|  
|smalldatetime|SQL_DATETIME|SQL_CODE_TIMESTAMP|8|0|0|  
|date|SQL_DATETIME|SQL_CODE_DATE|6|0|0|  
|time|SQL_SS_TIME2|0|10|0..7|0..7|  
|datetime2|SQL_DATETIME|SQL_CODE_TIMESTAMP|16|0..7|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|0|20|0..7|0..7|  
  
 如需詳細資訊，請參閱[ODBC&#41;&#40;的日期和時間改善](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlgetdescrec-support-for-large-clr-udts"></a>SQLGetDescRec 對於大型 CLR UDT 的支援  
 
  `SQLGetDescRec` 支援大型 CLR 使用者定義型別 (UDT)。 如需詳細資訊，請參閱[&#40;ODBC&#41;的大型 CLR 使用者定義類型](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLGetDescRec](https://go.microsoft.com/fwlink/?LinkId=80707)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
