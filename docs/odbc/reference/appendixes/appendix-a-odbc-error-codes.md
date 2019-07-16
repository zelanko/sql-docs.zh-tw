---
title: 附錄 A：ODBC 錯誤碼 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error codes [ODBC]
- SQLSTATE [ODBC]
- error codes [ODBC], SQLSTATE
ms.assetid: c06902e4-721d-42e2-b818-05f0e18e4ce0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5c16ec959f847f1b2dba5bdfbea8f886bb00545a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996242"
---
# <a name="appendix-a-odbc-error-codes"></a>附錄 A：ODBC 錯誤碼
本主題會討論 ODBC 3 SQLSTATE 值。*x*。 如需有關 ODBC 3 的詳細資訊。*x* SQLSTATE 值，請參閱[SQLSTATE 對應](../../../odbc/reference/develop-app/sqlstate-mappings.md)。  
  
 **SQLGetDiagRec**或是**SQLGetDiagField** Open Group 所定義，會傳回 SQLSTATE 值*資料管理：結構化查詢語言 (SQL)、 第 2 版*(1995 年 3 月)。 SQLSTATE 值是包含五個字元的字串。 下表列出的驅動程式可傳回的 SQLSTATE 值**SQLGetDiagRec**。  
  
 傳回為 SQLSTATE 的字元字串值是由兩個字元類別值，後面接著三個字元的子類別值所組成。 類別值為"01"表示警告，並伴隨著 SQL_SUCCESS_WITH_INFO 傳回碼。 類別"01，「 類別 」 IM，「 除了以外的值表示錯誤，並附帶 SQL_ERROR 傳回值。 類別"IM 」 是特定警告和錯誤衍生自 ODBC 本身的實作。 在任何類別中的子類別值"000 」 不表示該 SQLSTATE 任何子類別。 SQL-92 定義的類別和子類別值的指派。  
  
> [!NOTE]  
>  雖然函式成功執行通常由傳回值為 SQL_SUCCESS，SQLSTATE 00000 也會表示成功。  
  
|SQLSTATE|錯誤|可以從傳回|  
|--------------|-----------|--------------------------|  
|01000|一般警告|以外的所有 ODBC 函數：<br /><br /> **SQLError**<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|01001|資料指標作業衝突|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|01002|中斷連線時發生錯誤|**SQLDisconnect**|  
|01003|Set 函式刪除了 NULL 值|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|01004|字串資料，右邊已截斷|**SQLBrowseConnect**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLDataSources**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLDrivers**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLGetEnvAttr**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLNative**<br /><br /> **Sql SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetCursorName**|  
|01006|未撤銷權限|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|01007|未授與的權限|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|01S00|連接字串屬性無效|**SQLBrowseConnect**<br /><br /> **SQLDriverConnec**|  
|01S01|資料列中的錯誤|**SQLBulkOperations**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLSetPos**|  
|01S02|選項值已變更|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**|  
|01S06|嘗試擷取結果集傳回第一個資料列集之前|**SQLExtendedFetch**<br /><br /> **SQLFetchScroll**|  
|01S07|小數位數截斷|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|01S08|儲存檔案 DSN 時發生錯誤|**SQLDriverConnect**|  
|01S09|無效的關鍵字|**SQLDriverConnect**|  
|07001|參數數目不正確|**SQLExecDirect**<br /><br /> **SQLExecute**|  
|07002|COUNT 欄位不正確|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**|  
|07005|無法準備陳述式*資料指標規格*|**SQLColAttribute**<br /><br /> **SQLDescribeCol**|  
|07006|受限制的資料類型屬性違規|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|07009|描述項索引無效|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLParamData**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRecSQLSetPos**|  
|07S01|預設參數用法無效|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**|  
|08001|無法建立連線的用戶端|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|08002|使用中的連接名稱|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLSetConnectAttr**|  
|08003|未開啟連接|**SQLAllocHandle**<br /><br /> **SQLDisconnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetInfo**<br /><br /> **SQLNativeSql**<br /><br /> **SQLSetConnectAttr**|  
|08004|伺服器拒絕連線|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|08007|在交易期間的連線失敗|**SQLEndTran**|  
|08S01|通訊連結失敗|**SQLBrowseConnect**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLCopyDesc**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLGetFunctions**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLNativeSql**<br /><br /> **SQLNumParams**<br /><br /> **SQLNumResultCols**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|21S01|插入的值清單不符合資料行清單|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|21S02|衍生資料表的程度與資料行清單不符|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetPos**|  
|22001|字串資料，右邊已截斷|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetPos**|  
|22002|指標變數但未提供|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**|  
|22003|數值超出範圍|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLGetInfo**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22007|無效的日期時間格式|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22008|日期時間欄位溢位|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **QLParamData**<br /><br /> **SQLPutData**|  
|22012|除數為零|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLPutData**|  
|22015|間隔欄位溢位|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22018|轉換規格的字元值無效|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**<br /><br /> **SQLParamData**<br /><br /> **SQLPutData**<br /><br /> **SQLSetPos**|  
|22019|無效的逸出字元|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|22025|無效的逸出序列|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|22026|字串資料，長度不符|**SQLParamData**|  
|23000|完整性條件約束違規|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|24000|指標狀態無效|**SQLBulkOperations**<br /><br /> **SQLCloseCursor**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetData**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLNativeSql**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|25000|交易狀態無效|**SQLDisconnect**|  
|25S01|交易狀態|**SQLEndTran**|  
|25S02|交易仍為使用|**SQLEndTran**|  
|25S03|回復交易|**SQLEndTran**|  
|28000|無效的授權規格|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|34000|指標名稱無效|**SQLExecDirect**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetCursorName**|  
|3C000|重複的資料指標名稱|**SQLSetCursorName**|  
|3D000|無效的目錄名稱|**SQLExecDirect**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetConnectAttr**|  
|3F000|無效的結構描述名稱|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|40001|序列化失敗|**SQLBulkOperations**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLParamData**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|40002|完整性條件約束違規|**SQLEndTran**|  
|40003|未知的陳述式完成|**SQLBulkOperations**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|42000|語法錯誤或存取違規|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLSetPos**|  
|42S01|基底資料表或檢視已經存在|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S02|基底資料表或檢視找不到|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S11|索引已經存在|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S12|找不到索引|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S21|資料行已經存在|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|42S22|找不到的資料行|**SQLExecDirect**<br /><br /> **SQLPrepare**|  
|44000|WITH CHECK OPTION 違規|**SQLBulkOperations**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|HY000|一般錯誤|以外的所有 ODBC 函數：<br /><br /> **SQLError**<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|HY001|記憶體配置錯誤|以外的所有 ODBC 函數：<br /><br /> **SQLError**<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|HY003|無效的應用程式緩衝區類型|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLGetData**|  
|HY004|無效的 SQL 資料類型|**SQLBindParameter**<br /><br /> **SQLGetTypeInfo**|  
|HY007|尚未備妥相關聯的陳述式|**SQLCopyDesc**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**|  
|HY008|已取消作業|可以以非同步方式處理所有 ODBC 函數：<br /><br /> **SQLBrowseConnect**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **SQLDisconnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetData**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLNumParams**<br /><br /> **SQLNumResultCols**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HY009|使用無效的 null 指標|**SQLAllocHandle**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLExecDirect**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetFunctions**<br /><br /> **SQLNativeSql**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HY010|函數順序錯誤|**SQLAllocHandle**<br /><br /> **SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLCloseCursor**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLCopyDesc**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDescribeParam**<br /><br /> **SQLDisconnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetDescRec**<br /><br /> **SQLGetFunctions**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLMoreResults**<br /><br /> **SQLNumParams**<br /><br /> **SQLNumResultCols**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLRowCount**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetDescRec**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HY011|現在無法設定屬性|**SQLBulkOperations**<br /><br /> **SQLParamData**<br /><br /> **QLSetPos**<br /><br /> **SQLSetStmtAttr**|  
|HY012|無效的交易作業碼|**SQLEndTran**|  
|HY013|記憶體管理錯誤|以外的所有 ODBC 函數：<br /><br /> **SQLGetDiagField**<br /><br /> **SQLGetDiagRec**|  
|HY014|超出處理數目限制|**SQLAllocHandle**|  
|HY015|沒有可用的資料指標名稱|**SQLGetCursorName**|  
|HY016|無法修改實作資料列描述項|**SQLCopyDesc**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**|  
|HY017|使用自動配置描述項控制代碼無效|**SQLFreeHandle**<br /><br /> **SQLSetStmtAttr**|  
|HY018|伺服器拒絕取消要求|**SQLCancel**|  
|HY019|整塊傳送非字元及非二進位的資料|**SQLPutData**|  
|HY020|嘗試串連 null 值|**SQLPutData**|  
|HY021|不一致的描述元資訊|**SQLBindParameter**<br /><br /> **SQLCopyDesc**<br /><br /> **SQLGetDescField**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**|  
|HY024|屬性值無效|**SQLSetConnectAttr**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**|  
|HY090|字串或緩衝區長度無效|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBrowseConnect**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLDataSources**<br /><br /> **SQLDescribeCol**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLDrivers**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetCursorName**<br /><br /> **SQLGetData**<br /><br /> **SQLGetDescField**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLNativeSql**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLPutData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetCursorName**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetDescRec**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HY091|無效的描述項欄位識別碼|**SQLColAttribute**<br /><br /> **SQLGetDescField**<br /><br /> **SQLSetDescField**|  
|HY092|屬性/選項識別碼無效|**SQLAllocHandle**<br /><br /> **QLBulkOperations**<br /><br /> **SQLCopyDesc**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetEnvAttr**<br /><br /> **QLParamData**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetDescField**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**|  
|HY095|函數類型超出範圍|**SQLGetFunctions**|  
|HY096|無效的資訊類型|**SQLGetInfo**|  
|HY097|資料行類型超出範圍|**SQLSpecialColumns**|  
|HY098|範圍類型超出範圍|**SQLSpecialColumns**|  
|HY099|可為 null 類型超出範圍|**SQLSpecialColumns**|  
|HY100|唯一性選項類型超出範圍|**SQLStatistics**|  
|HY101|精確度選項類型超出範圍|**SQLStatistics**|  
|HY103|無效的擷取程式碼|**SQLDataSources**<br /><br /> **SQLDrivers**|  
|HY104|無效的有效位數或小數位數的值|**SQLBindParameter**|  
|HY105|無效的參數類型|**SQLBindParameter**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLParamData**<br /><br /> **SQLSetDescField**|  
|HY106|擷取類型超出範圍|**SQLExtendedFetch**<br /><br /> **SQLFetchScroll**|  
|HY107|資料列值超出範圍|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLSetPos**|  
|HY109|無效的資料指標位置|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLGetData**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLNativeSql**<br /><br /> **SQLParamData**<br /><br /> **SQLSetPos**|  
|HY110|無效的驅動程式完成|**SQLDriverConnect**|  
|HY111|無效的書籤值|**SQLExtendedFetch**<br /><br /> **SQLFetchScroll**|  
|HYC00|未實作選擇性功能|**SQLBindCol**<br /><br /> **SQLBindParameter**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColAttribute**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLEndTran**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetConnectAttr**<br /><br /> **SQLGetData**<br /><br /> **SQLGetEnvAttr**<br /><br /> **SQLGetInfo**<br /><br /> **SQLGetStmtAttr**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetConnectAttr**<br /><br /> **SQLSetEnvAttr**<br /><br /> **SQLSetPos**<br /><br /> **SQLSetStmtAttr**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HYT00|已超過逾時的設定|**SQLBrowseConnect**<br /><br /> **SQLBulkOperations**<br /><br /> **SQLColumnPrivileges**<br /><br /> **SQLColumns**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLExtendedFetch**<br /><br /> **SQLForeignKeys**<br /><br /> **SQLGetTypeInfo**<br /><br /> **SQLParamData**<br /><br /> **SQLPrepare**<br /><br /> **SQLPrimaryKeys**<br /><br /> **SQLProcedureColumns**<br /><br /> **SQLProcedures**<br /><br /> **SQLSetPos**<br /><br /> **SQLSpecialColumns**<br /><br /> **SQLStatistics**<br /><br /> **SQLTablePrivileges**<br /><br /> **SQLTables**|  
|HYT01|連接逾時過期|以外的所有 ODBC 函數：<br /><br /> **SQLDrivers**<br /><br /> **SQLDataSources**<br /><br /> **SQLGetEnvAttr**<br /><br /> **SQLSetEnvAttr**|  
|IM001|驅動程式不支援此函式|以外的所有 ODBC 函數：<br /><br /> **SQLAllocHandle**<br /><br /> **SQLDataSources**<br /><br /> **SQLDrivers**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLGetFunctions**|  
|IM002|找不到的資料來源名稱和指定的任何預設驅動程式|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM003|無法載入指定的驅動程式|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM004|駕**SQLAllocHandle**上 SQL_HANDLE_ENV 失敗|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM005|駕**SQLAllocHandle**上利用 SQL_HANDLE_DBC 失敗|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM006|駕**SQLSetConnectAttr**失敗|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM007|任何資料來源或驅動程式指定;禁止使用的對話方塊|**SQLDriverConnect**|  
|IM008|對話方塊失敗|**SQLDriverConnect**|  
|IM009|無法載入轉譯 DLL|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**<br /><br /> **SQLSetConnectAttr**|  
|IM010|資料來源名稱太長|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|IM011|驅動程式名稱太長|**SQLBrowseConnect**<br /><br /> **SQLDriverConnect**|  
|IM012|驅動程式關鍵字的語法錯誤|**SQLBrowseConnect**<br /><br /> **SQLDriverConnect**|  
|IM013|追蹤檔案時發生錯誤|所有的 ODBC 函式。|  
|IM014|無效的檔案 DSN 的名稱|**SQLDriverConnect**|  
|IM015|損毀的檔案資料來源|**SQLDriverConnect**|
