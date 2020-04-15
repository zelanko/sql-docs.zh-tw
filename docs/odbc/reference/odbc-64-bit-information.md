---
title: ODBC 64 位元資訊 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ed9851ce-44ee-4c8e-b626-1d0b52da30fe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b9cb8e3fc42d0ad71ac83f1432c165f243f39012
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298298"
---
# <a name="odbc-64-bit-information"></a>ODBC 64 位元資訊
從 Windows Server 2003 開始,Microsoft 操作系統支援 64 位元 ODBC 庫。 最初隨 MDAC 2.7 SDK 附帶的 ODBC 標頭和庫包含更改,允許程式師輕鬆為新 64 位元平台編寫代碼。 通過確保代碼使用下面列出的 ODBC 定義類型,您可以基於 **_WIN64**或**WIN32**宏為 64 位元和 32 位元平台編譯相同的原始碼。  
  
 在 64 位元處理器程式設計時,需要記住幾個要點:  
  
-   儘管指標的大小從 4 位元組更改為 8 位元組,但整數和長數仍為 4 位元組值。 **INT64**和**UINT64**的類型已為 8 個字節整數定義。 新的 ODBC 類型**SQLLEN**和**SQLULEN**在訂 **_WIN64**時,在 ODBC 標頭檔中定義為**INT64**和**UINT64。**  
  
-   ODBC 中的多個函數聲明為採用指標參數。 在 32 位 ODBC 中,定義為指標的參數經常用於傳遞整數值或指向緩衝區的指標,具體取決於調用的上下文。 當然,這是可能的,因為指標和整數具有相同的大小。 在 64 位 Windows 中,情況並非如此。  
  
-   以前使用**SQLINTEGER**和**SQLUINTEGER**參數定義的一些 ODBC 函數已根據需要更改,以使用新的**SQLLEN**和**SQLULEN**類型defs。 這些更改列在下一節"函數聲明更改"中。  
  
-   可以通過各種**SQLSet**和**SQLGet**函數設置的一些描述符欄位已更改,以適應 64 位值,而其他欄位仍為 32 位值。 在設置和檢索這些欄位時,請確保使用適當大小的變數。 描述符欄位已更改的具體細節列在函數聲明更改下。  
  
## <a name="function-declaration-changes"></a>函式宣告變更  
 對於 64 位元設計,以下函數簽名已更改。 粗體文字中的項是不同的特定參數。  
  
```cpp
SQLBindCol (SQLHSTMT StatementHandle, SQLUSMALLINT ColumnNumber,  
   SQLSMALLINT TargetType, SQLPOINTER TargetValuePtr, SQLLEN BufferLength,   SQLLEN * StrLen_or_Ind);  
  
SQLBindParam (SQLHSTMT StatementHandle, SQLUSMALLINT ParameterNumber,  
   SQLSMALLINT ValueType, SQLSMALLINT ParameterType,   
   SQLULEN ColumnSize, SQLSMALLINT DecimalDigits,   
   SQLPOINTER ParameterValuePtr, SQLLEN *StrLen_or_Ind);  
  
SQLBindParameter (SQLHSTMT StatementHandle, SQLUSMALLINT ParameterNumber,   
   SQLSMALLINT InputOutputType, SQLSMALLINT ValueType,   
   SQLSMALLINT ParameterType, SQLULEN ColumnSize, SQLSMALLINT DecimalDigits,   
   SQLPOINTER ParameterValuePtr, SQLLEN BufferLength, SQLLEN *StrLen_or_IndPtr);  
  
SQLColAttribute (SQLHSTMT StatementHandle, SQLUSMALLINT ColumnNumber,  
    SQLUSMALLINT FieldIdentifier, SQLPOINTER CharacterAttributePtr,   
   SQLSMALLINT BufferLength, SQLSMALLINT * StringLengthPtr,   
   SQLLEN* NumericAttributePtr)  
  
SQLColAttributes (SQLHSTMT hstmt, SQLUSMALLINT icol,   
   SQLUSMALLINT fDescType, SQLPOINTER rgbDesc,   
   SQLSMALLINT cbDescMax, SQLSMALLINT *pcbDesc, SQLLEN * pfDesc);  
  
SQLDescribeCol (SQLHSTMT StatementHandle, SQLUSMALLINT ColumnNumber,   
   SQLCHAR *ColumnName, SQLSMALLINT BufferLength,   
   SQLSMALLINT *NameLengthPtr, SQLSMALLINT *DataTypePtr, SQLULEN *ColumnSizePtr,   
   SQLSMALLINT *DecimalDigitsPtr, SQLSMALLINT *NullablePtr);  
  
SQLDescribeParam (SQLHSTMT StatementHandle, SQLUSMALLINT ParameterNumber,   
   SQLSMALLINT *DataTypePtr, SQLULEN *ParameterSizePtr, SQLSMALLINT *DecimalDigitsPtr,   
   SQLSMALLINT *NullablePtr);  
  
SQLExtendedFetch(SQLHSTMT StatementHandle, SQLUSMALLINT FetchOrientation, SQLLEN FetchOffset,   
   SQLULEN * RowCountPtr, SQLUSMALLINT * RowStatusArray);  
  
SQLFetchScroll (SQLHSTMT StatementHandle, SQLSMALLINT FetchOrientation,   
   SQLLEN FetchOffset);  
  
SQLGetData (SQLHSTMT StatementHandle, SQLUSMALLINT ColumnNumber,   
   SQLSMALLINT TargetType, SQLPOINTER TargetValuePtr, SQLLEN BufferLength,    SQLLEN *StrLen_or_Ind);  
  
SQLGetDescRec (SQLHDESC DescriptorHandle, SQLSMALLINT RecNumber,   
   SQLCHAR *Name, SQLSMALLINT BufferLength,   
   SQLSMALLINT *StringLengthPtr, SQLSMALLINT *TypePtr,   
   SQLSMALLINT *SubTypePtr, SQLLEN *LengthPtr,   
   SQLSMALLINT *PrecisionPtr, SQLSMALLINT *ScalePtr,   
   SQLSMALLINT *NullablePtr);  
  
SQLParamOptions(SQLHSTMT hstmt, SQLULEN crow, SQLULEN * pirow);  
  
SQLPutData (SQLHSTMT StatementHandle, SQLPOINTER DataPtr,   
   SQLLEN StrLen_or_Ind);  
  
SQLRowCount (SQLHSTMT StatementHandle, SQLLEN* RowCountPtr);  
  
SQLSetConnectOption(SQLHDBC ConnectHandle, SQLUSMALLINT Option,   
   SQLULEN Value);  
  
SQLSetPos (SQLHSTMT StatementHandle, SQLSETPOSIROW RowNumber, SQLUSMALLINT Operation,  
   SQLUSMALLINT LockType);  
  
SQLSetParam (SQLHSTMT StatementHandle, SQLUSMALLINT ParameterNumber,   
   SQLSMALLINT ValueType, SQLSMALLINT ParameterType,   
   SQLULEN LengthPrecision, SQLSMALLINT ParameterScale,   
   SQLPOINTER ParameterValue, SQLLEN *StrLen_or_Ind);  
  
SQLSetDescRec (SQLHDESC DescriptorHandle, SQLSMALLINT RecNumber,   
   SQLSMALLINT Type, SQLSMALLINT SubType, SQLLEN Length,   
   SQLSMALLINT Precision, SQLSMALLINT Scale, SQLPOINTER DataPtr,   
   SQLLEN *StringLengthPtr, SQLLEN *IndicatorPtr);  
  
SQLSetScrollOptions (SQLHSTMT hstmt, SQLUSMALLINT fConcurrency,   
   SQLLEN crowKeyset, SQLUSMALLINT crowRowset);  
  
SQLSetStmtOption (SQLHSTMT StatementHandle, SQLUSMALLINT Option,   
   SQLULEN Value);  
```  
  
## <a name="changes-in-sql-data-types"></a>SQL 資料型態的變更  
 以下四種 SQL 類型仍僅在 32 位上受支援;但僅支援以下四種 SQL 類型。它們不是為 64 位編譯器定義的。 這些類型不再用於 MDAC 2.7 中的任何參數;使用這些類型將導致 64 位元平臺上的編譯器失敗。  
  
```cpp
#ifdef WIN32   
typedef SQLULEN SQLROWCOUNT;   
typedef SQLULEN SQLROWSETSIZE;   
typedef SQLULEN SQLTRANSID;   
typedef SQLLEN SQLROWOFFSET;   
#endif  
```  
  
 對於 32 位元和 64 位元編譯器,SQLSETPOSIROW 的定義已更改:  
  
```cpp
#ifdef _WIN64   
typedef UINT64 SQLSETPOSIROW;   
#else   
#define SQLSETPOSIROW SQLUSMALLINT   
#endif  
```  
  
 SQLLEN 與 SQLULEN 的定義已變更為 64 位元編譯器:  
  
```cpp
#ifdef _WIN64   
typedef INT64 SQLLEN;   
typedef UINT64 SQLULEN;   
#else   
#define SQLLEN SQLINTEGER   
#define SQLULEN SQLUINTEGER   
#endif  
```  
  
 儘管在 ODBC 3.0 中棄用了SQL_C_BOOKMARK,但對於 2.0 用戶端上的 64 位元編譯器,此值已更改:  
  
```cpp
#ifdef _WIN64   
#define SQL_C_BOOKMARK SQL_C_UBIGINT   
#else   
#define SQL_C_BOOKMARK SQL_C_ULONG   
#endif  
```  
  
 BOOKMARK 類型在較新的標頭中定義的方式不同:  
  
```cpp
typedef SQLULEN BOOKMARK;  
```  
  
## <a name="values-returned-from-odbc-api-calls-through-pointers"></a>從 ODBC API 呼叫傳回的值  
 以下 ODBC 函數調用將指向從驅動程式返回數據的緩衝區的指標作為輸入參數。 返回數據的上下文和含義由函數的其他輸入參數確定。 在某些情況下,這些方法現在可能返回 64 位(8 位元組整數)值,而不是典型的 32 位(4 位元組)整數值。 這些情況如下:  
  
 **SQLColAttribute**  
  
 當*FieldIdentifier 參數*有以下值之一時,在 #*數字屬性*中傳回 64 位元 :  
  
 SQL_DESC_AUTO_UNIQUE_VALUE  
  
 SQL_DESC_CASE_SENSITIVE  
  
 SQL_DESC_CONCISE_TYPE  
  
 SQL_DESC_COUNT  
  
 SQL_DESC_DISPLAY_SIZE  
  
 SQL_DESC_FIXED_PREC_SCALE  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_NULLABLE  
  
 SQL_DESC_NUM_PREC_RADIX  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_PRECISION  
  
 SQL_DESC_SCALE  
  
 SQL_DESC_SEARCHABLE  
  
 SQL_DESC_TYPE  
  
 SQL_DESC_UNNAMED  
  
 SQL_DESC_UNSIGNED  
  
 SQL_DESC_UPDATABLE  
  
 **SQLColattributes**  
  
 當*fDescType*參數具有以下值之一時,在 =*pfDesc*中傳回 64 位元值 :  
  
 SQL_COLUMN_COUNT  
  
 SQL_COLUMN_DISPLAY_SIZE  
  
 SQL_COLUMN_LENGTH  
  
 SQL_DESC_AUTO_UNIQUE_VALUE  
  
 SQL_DESC_CASE_SENSITIVE  
  
 SQL_DESC_CONCISE_TYPE  
  
 SQL_DESC_FIXED_PREC_SCALE  
  
 SQL_DESC_SEARCHABLE  
  
 SQL_DESC_UNSIGNED  
  
 SQL_DESC_UPDATABLE  
  
 **SQLGetConnectAttr**  
  
 當*屬性*參數有以下值之一時,值中傳回 64 位*元 :*  
  
 SQL_ATTR_ASYNC_ENABLE  
  
 SQL_ATTR_ENLIST_IN_DTC  
  
 SQL_ATTR_ODBC_CURSORS  
  
 SQL_ATTR_QUIET_MODE  
  
 **SQLGetConnectOption**  
  
 當*屬性*參數有以下值之一時,值中傳回 64 位*元 :*  
  
 SQL_ATTR_QUIET_MODE  
  
 **SQLGetDescField**  
  
 當*FieldIdentifier 參數*有以下值之一時,在 #*ValuePtr*中傳回 64 位元值 :  
  
 SQL_DESC_ARRAY_SIZE  
  
 SQL_DESC_ARRAY_STATUS_PTR  
  
 SQL_DESC_BIND_OFFSET_PTR  
  
 SQL_DESC_DATA_PTR  
  
 SQL_DESC_DISPLAY_SIZE  
  
 SQL_DESC_INDICATOR_PTR  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_OCTET_LENGTH_PTR  
  
 SQL_DESC_ROWS_PROCESSED_PTR  
  
 **SQLGetDiagField**  
  
 當*DiagIdentifier 參數*具有以下值之一時,在 #*DiagInfoPtr*中傳回 64 位元值 :  
  
 SQL_DIAG_CURSOR_ROW_COUNT  
  
 SQL_DIAG_ROW_COUNT  
  
 SQL_DIAG_ROW_NUMBER  
  
 **SQLGetInfo**  
  
 當*InfoType*參數有以下值之一時,在 [*InfoValuePtr*: 中傳回 64 位元值》 :  
  
 SQL_DRIVER_HDBC  
  
 SQL_DRIVER_HENV  
  
 SQL_DRIVER_HLIB  
  
 當*InfoType*具有以下 2 個值之一時 -*InfoValuePtr*在輸入和輸出上均為 64 位:  
  
 SQL_DRIVER_HDESC  
  
 SQL_DRIVER_HSTMT  
  
 **SQLGetStmtAttr**  
  
 當*屬性*參數具有以下值之一時,在 #*ValuePtr*中傳回 64 位元值 :  
  
 SQL_ATTR_APP_PARAM_DESC  
  
 SQL_ATTR_APP_ROW_DESC  
  
 SQL_ATTR_ASYNC_ENABLE  
  
 SQL_ATTR_CONCURRENCY  
  
 SQL_ATTR_CURSOR_SCROLLABLE  
  
 SQL_ATTR_CURSOR_SENSITIVITY  
  
 SQL_ATTR_CURSOR_TYPE  
  
 SQL_ATTR_ENABLE_AUTO_IPD  
  
 SQL_ATTR_FETCH_BOOKMARK_PTR  
  
 SQL_ATTR_ROWS_FETCHED_PTR  
  
 SQL_ATTR_IMP_PARAM_DESC  
  
 SQL_ATTR_IMP_ROW_DESC  
  
 SQL_ATTR_KEYSET_SIZE  
  
 SQL_ATTR_MAX_LENGTH  
  
 SQL_ATTR_MAX_ROWS  
  
 SQL_ATTR_METADATA_ID  
  
 SQL_ATTR_NOSCAN  
  
 SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
 SQL_ATTR_PARAM_BIND_TYPE  
  
 SQL_ATTR_PARAM_OPERATION_PTR  
  
 SQL_ATTR_PARAM_STATUS_PTR  
  
 SQL_ATTR_PARAMS_PROCESSED_PTR  
  
 SQL_ATTR_PARAMSET_SIZE  
  
 SQL_ATTR_QUERY_TIMEOUT  
  
 SQL_ATTR_RETRIEVE_DATA  
  
 SQL_ATTR_ROW_ARRAY_SIZE  
  
 SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
 SQL_ATTR_ROW_NUMBER  
  
 SQL_ATTR_ROW_OPERATION_PTR  
  
 SQL_ATTR_ROW_STATUS_PTR  
  
 SQL_ATTR_SIMULATE_CURSOR  
  
 SQL_ATTR_USE_BOOKMARKS  
  
 **SQLGetStmtOption**  
  
 當*Option*參數具有以下值之一時,在 = 值中傳回 64 位*元*值 :  
  
 SQL_KEYSET_SIZE  
  
 SQL_MAX_LENGTH  
  
 SQL_MAX_ROWS  
  
 SQL_ROWSET_SIZE  
  
 **SQLSetConnectAttr**  
  
 當*屬性*參數具有以下值之一時,值中傳遞 64 位*元值*:  
  
 SQL_ATTR_ASYNC_ENABLE  
  
 SQL_ATTR_ENLIST_IN_DTC  
  
 SQL_ATTR_ODBC_CURSORS  
  
 SQL_ATTR_QUIET_MODE  
  
 **SQLSet 連線選項**  
  
 當*屬性*參數具有以下值之一時,值中傳遞 64 位*元值*:  
  
 SQL_ATTR_QUIET_MODE  
  
 **SQLSetDescField**  
  
 當*Field 識別子參數*具有以下值之一時,值*Ptr*中傳遞 64 位元值:  
  
 SQL_DESC_ARRAY_SIZE  
  
 SQL_DESC_ARRAY_STATUS_PTR  
  
 SQL_DESC_BIND_OFFSET_PTR  
  
 SQL_DESC_DATA_PTR  
  
 SQL_DESC_DISPLAY_SIZE  
  
 SQL_DESC_INDICATOR_PTR  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_OCTET_LENGTH_PTR  
  
 SQL_DESC_ROWS_PROCESSED_PTR  
  
 **SQLSetStmtAttr**  
  
 當*屬性*參數具有以下值之一時,值*Ptr*中傳遞 64 位元值:  
  
 SQL_ATTR_APP_PARAM_DESC  
  
 SQL_ATTR_APP_ROW_DESC  
  
 SQL_ATTR_ASYNC_ENABLE  
  
 SQL_ATTR_CONCURRENCY  
  
 SQL_ATTR_CURSOR_SCROLLABLE  
  
 SQL_ATTR_CURSOR_SENSITIVITY  
  
 SQL_ATTR_CURSOR_TYPE  
  
 SQL_ATTR_ENABLE_AUTO_IPD  
  
 SQL_ATTR_FETCH_BOOKMARK_PTR  
  
 SQL_ATTR_IMP_PARAM_DESC  
  
 SQL_ATTR_IMP_ROW_DESC  
  
 SQL_ATTR_KEYSET_SIZE  
  
 SQL_ATTR_MAX_LENGTH  
  
 SQL_ATTR_MAX_ROWS  
  
 SQL_ATTR_METADATA_ID  
  
 SQL_ATTR_NOSCAN  
  
 SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
 SQL_ATTR_PARAM_BIND_TYPE  
  
 SQL_ATTR_PARAM_OPERATION_PTR  
  
 SQL_ATTR_PARAM_STATUS_PTR  
  
 SQL_ATTR_PARAMS_PROCESSED_PTR  
  
 SQL_ATTR_PARAMSET_SIZE  
  
 SQL_ATTR_QUERY_TIMEOUT  
  
 SQL_ATTR_RETRIEVE_DATA  
  
 SQL_ATTR_ROW_ARRAY_SIZE  
  
 SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
 SQL_ATTR_ROW_NUMBER  
  
 SQL_ATTR_ROW_OPERATION_PTR  
  
 SQL_ATTR_ROW_STATUS_PTR  
  
 SQL_ATTR_ROWS_FETCHED_PTR  
  
 SQL_ATTR_SIMULATE_CURSOR  
  
 SQL_ATTR_USE_BOOKMARKS  
  
 **SQLSetStmtOption**  
  
 當*Option*參數中, 以以下值之一時, 值中傳遞 64 位*元*:  
  
 SQL_KEYSET_SIZE  
  
 SQL_MAX_LENGTH  
  
 SQL_MAX_ROWS  
  
 SQL_ROWSET_SIZE  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 簡介](../../odbc/reference/introduction-to-odbc.md)
