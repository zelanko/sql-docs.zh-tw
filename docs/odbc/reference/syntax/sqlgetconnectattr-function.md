---
title: "SQLGetConnectAttr 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectAttr
helpviewer_keywords:
- SQLGetConnectAttr function [ODBC]
ms.assetid: 2cb4ffa8-19d3-4664-8c2f-6682cdcc3f33
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fc8f754301b5b0c0d5259cd7613bacdf302a06e7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetconnectattr-function"></a>SQLGetConnectAttr 函數
**一致性**  
 版本引進了： ODBC 3.0 版的標準相容性： ISO 92  
  
 **摘要**  
 **SQLGetConnectAttr**傳回連接屬性的目前設定。  
  
> [!NOTE]  
>  如需有關什麼驅動程式管理員會對應到此函式時 ODBC 3*.x*應用程式使用 ODBC 2*.x*驅動程式，請參閱[向後的對應取代函式應用程式的相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLGetConnectAttr(  
     SQLHDBC        ConnectionHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>引數  
 *ConnectionHandle*  
 [輸入]連接控制代碼。  
  
 *Attribute*  
 [輸入]要擷取的屬性。  
  
 *ValuePtr*  
 [輸出]傳回所指定之屬性的目前值的記憶體指標*屬性*。 對於整數類型的屬性，有些驅動程式可能只會寫入較低的 32 位元或 16 位元的緩衝區並保留不變的更高序位位元。 因此，應用程式應該使用 SQLULEN 的緩衝區，並初始化為 0 的值之前呼叫這個函式。  
  
 如果*ValuePtr*是 NULL， *StringLengthPtr*仍會傳回的總位元組數 （不含字元資料 null 結束字元） 可用來傳回所指向之緩衝區中*ValuePtr*。  
  
 *Columnsize*  
 [輸入]如果*屬性*是 ODBC 定義的屬性和*ValuePtr*指向字元字串或二進位的緩衝區，這個引數應該是長度\* *ValuePtr*. 如果*屬性*是 ODBC 定義的屬性和\* *ValuePtr*是整數， *Columnsize*會被忽略。 如果中的值* \*ValuePtr*是 Unicode 字串 (當呼叫**SQLGetConnectAttrW**)、 *Columnsize*引數必須是偶數。  
  
 如果*屬性*是驅動程式定義的屬性，應用程式設定指出屬性給驅動程式管理員性質*Columnsize*引數。 *Columnsize*可以是下列值：  
  
-   如果* \*ValuePtr*是字元字串的指標*Columnsize*是字串的長度。  
  
-   如果* \*ValuePtr* SQL_LEN_BINARY_ATTR 的結果是二進位的緩衝區，應用程式位置的指標 (*長度*) 中的巨集*Columnsize*。 這樣做會放在負值*Columnsize*。  
  
-   如果* \*ValuePtr*是字元字串或二進位字串以外的值的指標*Columnsize*應該有 SQL_IS_POINTER 的值。  
  
-   如果* \*ValuePtr*包含固定長度資料類型， *Columnsize*是 SQL_IS_INTEGER 或 SQL_IS_UINTEGER，視需要。  
  
 *StringLengthPtr*  
 [輸出]這是要傳回的總位元組數 （不包括 null 結束字元） 的緩衝區的指標可用來傳回中\* *ValuePtr*。 如果\* *ValuePtr*為 null 指標，則會傳回任何長度。 如果屬性值是字元字串，而且可用來傳回的位元組數目大於*Columnsize*的 null 結束的字元中的資料長度減去* \*ValuePtr*會被截斷成*Columnsize* null 結束字元的長度減而且是以 null 結束的驅動程式。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetConnectAttr**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以取自診斷資料結構藉由呼叫**SQLGetDiagRec**與*HandleType*利用 SQL_HANDLE_DBC 的和*處理*的*ConnectionHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLGetConnectAttr** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 位於驅動程式管理員傳回的 Sqlstate 的說明. 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|中傳回的資料\* *ValuePtr*已截斷為*Columnsize*減去 null 結束字元的長度。 中會傳回未截斷的字串值的長度 **StringLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08003|未開啟連線。|(DM)*屬性*指定所需的開啟連接的值。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 引數所傳回的診斷資料結構的錯誤訊息*MessageText*中**SQLGetDiagField**描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY010|函數順序錯誤|(DM) **SQLBrowseConnect**針對呼叫*ConnectionHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前**SQLBrowseConnect**傳回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*ConnectionHandle*並傳回 SQL_PARAM_DATA_可以使用。 此函式呼叫之前的所有資料流處理的參數擷取資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY090|字串或緩衝區長度無效|(DM) * \*ValuePtr*是字元字串，但 Columnsize 小於零，但不是等於 SQL_NTS。|  
|HY092|屬性/選項識別碼無效|指定的引數的值*屬性*對 ODBC 驅動程式支援的版本無效。|  
|HY114|驅動程式不支援連接層級的非同步函式執行|(DM) 應用程式嘗試啟用 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 與驅動程式不支援非同步連線作業的非同步函式執行。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|指定的引數的值*屬性*的 ODBC 版本支援的驅動程式，但不支援此驅動程式是有效的 ODBC 連接屬性。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式對應至*ConnectionHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 如需連接屬性的一般資訊，請參閱[連接屬性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 如需可設定屬性的清單，請參閱[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。 請注意，如果*屬性*指定屬性會傳回字串， *ValuePtr*必須是字串緩衝區的指標。 傳回的字串，包括 null 結束的字元，最大長度將*Columnsize*位元組。  
  
 屬性，根據應用程式沒有建立連線，然後再呼叫**SQLGetConnectAttr**。 不過，如果**SQLGetConnectAttr**稱為和指定的屬性沒有預設值，而且由先前呼叫尚未設定**SQLSetConnectAttr**， **SQLGetConnectAttr**會傳回 sql_no_data 為止。  
  
 如果*屬性*SQL_ATTR_ 追蹤或 SQL_ATTR_ TRACEFILE *ConnectionHandle*沒有有效的與**SQLGetConnectAttr**不會傳回 SQL_ERROR 或 SQL_INVALID_HANDLE 如果*ConnectionHandle*無效。 這些屬性會套用到所有連線。 **SQLGetConnectAttr**將會傳回 SQL_ERROR 或 SQL_INVALID_HANDLE 如果另一個引數無效。  
  
 雖然應用程式可以透過設定陳述式屬性**SQLSetConnectAttr**，應用程式無法使用**SQLGetConnectAttr**擷取陳述式屬性值; 它必須呼叫**SQLGetStmtAttr**擷取陳述式屬性的設定。  
  
 呼叫可傳回 SQL_ATTR_AUTO_IPD 和 SQL_ATTR_CONNECTION_DEAD 連接屬性**SQLGetConnectAttr**但不能設定呼叫**SQLSetConnectAttr**。  
  
> [!NOTE]  
>  沒有任何非同步支援**SQLGetConnectAttr**。 當實作**SQLGetConnectAttr**，驅動程式可以改善效能的資訊傳送，或從伺服器要求的次數降到最低。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|傳回陳述式屬性的設定|[SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函式](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定環境屬性|[SQLSetEnvAttr 函式](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|設定陳述式屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
