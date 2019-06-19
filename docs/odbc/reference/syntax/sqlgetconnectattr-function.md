---
title: SQLGetConnectAttr Function | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7051c94e4883c57daab4d5706feb073323e1c371
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65538025"
---
# <a name="sqlgetconnectattr-function"></a>SQLGetConnectAttr 函數
**合規性**  
 導入的版本：ODBC 3.0 版的標準合規性：ISO 92  
  
 **摘要**  
 **SQLGetConnectAttr**傳回連接屬性的目前設定。  
  
> [!NOTE]
>  如需有關什麼驅動程式管理員會對應到此函式時 ODBC 3 *.x*應用程式正在使用的 ODBC 2 *.x*驅動程式，請參閱[對應為向後取代函式應用程式的相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLGetConnectAttr(  
     SQLHDBC        ConnectionHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>引數  
 *ConnectionHandle*  
 [輸入] 連線控制代碼。  
  
 *Attribute*  
 [輸入]要擷取的屬性。  
  
 *ValuePtr*  
 [輸出]要在其中傳回所指定之屬性的目前值的記憶體指標*屬性*。 對於整數類型屬性，有些驅動程式可能只會寫入較低的 32 位元或 16 位元的緩衝區並保留不變的較高順序位元。 因此，應用程式應該使用 SQLULEN 的緩衝區，並呼叫此函式之前初始化為 0 的值。  
  
 如果*ValuePtr*為 NULL，就*StringLengthPtr*仍會傳回的總位元組數 （不含字元資料之 null 結束字元） 可用來傳回中指向緩衝區*ValuePtr*。  
  
 *BufferLength*  
 [輸入]如果*屬性*ODBC 定義的屬性和*ValuePtr*指向字元字串或二進位的緩衝區，這個引數應該是長度\* *ValuePtr*. 如果*屬性*ODBC 定義的屬性和\* *ValuePtr*是一個整數， *Columnsize*會被忽略。 如果中的值 *\*ValuePtr*是 Unicode 字串 (呼叫時**SQLGetConnectAttrW**)，則*Columnsize*引數必須是偶數。  
  
 如果*屬性*是驅動程式定義的屬性，應用程式設定指出屬性給驅動程式管理員性質*Columnsize*引數。 *BufferLength*可以有下列值：  
  
-   如果 *\*ValuePtr*是字元字串的指標*Columnsize*是字串的長度。  
  
-   如果 *\*ValuePtr* SQL_LEN_BINARY_ATTR 的結果是二進位緩衝區中，應用程式位置的指標 (*長度*) 中的巨集*Columnsize*。 這會放在負值*Columnsize*。  
  
-   如果 *\*ValuePtr*是字元字串或二進位字串，以外的值的指標*Columnsize*應有 SQL_IS_POINTER 的值。  
  
-   如果 *\*ValuePtr*包含固定長度的資料型別*Columnsize*是 SQL_IS_INTEGER 或 SQL_IS_UINTEGER，視需要。  
  
 *StringLengthPtr*  
 [輸出]在其中傳回的總位元組數 （不包括 null 結束字元） 緩衝區的指標來傳回在可用\* *ValuePtr*。 如果\* *ValuePtr*為 null 指標，會傳回任何長度。 如果屬性值是字元字串，而且可用來傳回的位元組數目大於*Columnsize*減去的 null 終止的字元中的資料長度 *\*ValuePtr*會被截斷成*BufferLength*減去之 null 結束字元的長度，是以 null 終止的驅動程式。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetConnectAttr**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得診斷資料結構**SQLGetDiagRec** 與*HandleType*利用 SQL_HANDLE_DBC 的並*處理*的*ConnectionHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLGetConnectAttr** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前的驅動程式管理員所傳回的 Sqlstate 的描述. 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|中傳回的資料\* *ValuePtr*被截斷成會*Columnsize*減去 null 結束字元的長度。 中會傳回未截斷的字串值的長度 **StringLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08003|未開啟連接|(DM)*屬性*指定所需的開啟連接的值。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 引數所傳回的診斷資料結構的錯誤訊息*MessageText*中**SQLGetDiagField**描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY010|函數順序錯誤|(DM) **SQLBrowseConnect**針對呼叫*ConnectionHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前**SQLBrowseConnect**傳回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*ConnectionHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|(DM)  *\*ValuePtr*為字元字串，而且 Columnsize 小於零，但不是等於 SQL_NTS。|  
|HY092|屬性/選項識別碼無效|指定的引數的值*屬性*ODBC 驅動程式支援的版本無效。|  
|HY114|驅動程式不支援連接層級非同步函式執行|(DM) 應用程式嘗試啟用 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 與驅動程式不支援非同步連接作業的非同步函式執行。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|指定的引數的值*屬性*的 ODBC 版本支援的驅動程式，但不支援此驅動程式是有效的 ODBC 連接屬性。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 至對應的磁碟機*ConnectionHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 如需連接屬性的一般資訊，請參閱[連接屬性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 如需可設定屬性的清單，請參閱 < [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。 請注意，如果*屬性*指定的屬性會傳回字串， *ValuePtr*必須是字串緩衝區的指標。 會傳回的字串，包括 null 終止字元的最大長度*Columnsize*位元組。  
  
 屬性，根據應用程式不需要建立的連線，然後再呼叫**SQLGetConnectAttr**。 不過，如果**SQLGetConnectAttr**稱為和指定的屬性並沒有預設值，而且尚未設定先前呼叫所**SQLSetConnectAttr**， **SQLGetConnectAttr**會傳回 sql_no_data 為止。  
  
 如果*屬性*SQL_ATTR_ 追蹤或 SQL_ATTR_ TRACEFILE *ConnectionHandle*沒有有效的並**SQLGetConnectAttr**不會傳回 SQL_ERROR 或 SQL_INVALID_HANDLE 如果*ConnectionHandle*無效。 這些屬性套用至所有連線。 **SQLGetConnectAttr**會傳回 SQL_ERROR 或 SQL_INVALID_HANDLE 如果另一個引數無效。  
  
 雖然應用程式可以透過設定陳述式屬性**SQLSetConnectAttr**，不能使用應用程式**SQLGetConnectAttr**擷取陳述式屬性值; 它必須呼叫**SQLGetStmtAttr**擷取陳述式屬性的設定。  
  
 呼叫可傳回 SQL_ATTR_AUTO_IPD 和 SQL_ATTR_CONNECTION_DEAD 連接屬性**SQLGetConnectAttr**但不能設定的呼叫所**SQLSetConnectAttr**。  
  
> [!NOTE]  
>  沒有任何非同步支援**SQLGetConnectAttr**。 實作時**SQLGetConnectAttr**，驅動程式可以改善效能的資訊會傳送，或從伺服器要求的次數降至最低。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|傳回陳述式屬性的設定|[SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函式](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定環境屬性|[SQLSetEnvAttr 函式](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|設定陳述式屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
