---
title: SQLGetConnectAttr 函式 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6076f14ff0c33fec38b99e9c43b8a688970a7a9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285628"
---
# <a name="sqlgetconnectattr-function"></a>SQLGetConnectAttr 函數
**標準**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **摘要**  
 **SQLGetConnectAttr**會傳回連接屬性的目前設定。  
  
> [!NOTE]
>  如需 ODBC 3.x 應用程式與 ODBC 2.x*驅動程式搭配*使用時，驅動程式管理員將此函式對應至哪個 *.x*功能的詳細資訊，請參閱對應取代函式[以取得應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
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
  
 *特性*  
 源要取出的屬性。  
  
 *ValuePtr*  
 輸出記憶體的指標，會在其中傳回*屬性*所指定之屬性的目前值。 對於整數型別屬性，某些驅動程式可能只會寫入較低的32位或16位的緩衝區，並不會變更較高的順序位。 因此，應用程式應該使用 SQLULEN 的緩衝區，並在呼叫此函式之前，將值初始化為0。  
  
 如果*valueptr 是*為 Null， *StringLengthPtr*仍會傳回*valueptr 是*所指向的緩衝區中可傳回的位元組總數（不包括字元資料的 Null 終止字元）。  
  
 *BufferLength*  
 源如果*attribute*是 ODBC 定義的屬性，而且*valueptr 是*指向字元字串或二進位緩衝區，則這個引數應該是\* *valueptr 是*的長度。 如果*attribute*是 ODBC 定義的屬性，而\* *valueptr 是*是整數，則會忽略*BufferLength* 。 如果* \*valueptr 是*中的值是 Unicode 字串（在呼叫**SQLGetConnectAttrW**時），則*BufferLength*引數必須是偶數。  
  
 如果*屬性*是驅動程式定義的屬性，則應用程式會藉由設定*BufferLength*引數，來指出該屬性對驅動程式管理員的本質。 *BufferLength*可以有下列值：  
  
-   如果* \*valueptr 是*是字元字串的指標， *BufferLength*就是字串的長度。  
  
-   如果* \*valueptr 是*是二進位緩衝區的指標，應用程式會將 SQL_LEN_BINARY_ATTR （*長度*）宏的結果放在*BufferLength*中。 這會將負數值放在*BufferLength*中。  
  
-   如果* \*valueptr 是*是字元字串或二進位字串以外的值指標， *BufferLength*應該會有值 SQL_IS_POINTER。  
  
-   如果* \*valueptr 是*包含固定長度的資料類型， *BufferLength*會適當地 SQL_IS_INTEGER 或 SQL_IS_UINTEGER。  
  
 *StringLengthPtr*  
 輸出緩衝區的指標，要在其中傳回\* *valueptr 是*中可傳回的位元組總數（不包括 null 終止字元）。 如果\* *valueptr 是*為 null 指標，則不會傳回長度。 如果屬性值是字元字串，而且可傳回的位元組數目大於*BufferLength*減去 null 終止字元的長度，則* \*valueptr 是*中的資料會截斷為*BufferLength*減去 null 終止字元的長度，並由驅動程式以 null 終止。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetConnectAttr**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以從診斷資料結構取得相關聯的 SQLSTATE 值，方法是呼叫**SQLGetDiagRec**搭配*HandleType*的 SQL_HANDLE_DBC 以及*ConnectionHandle*的*控制碼*。 下表列出通常由**SQLGetConnectAttr**所傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|\* *Valueptr 是*中傳回的資料被截斷為*BufferLength*減去 null 終止字元的長度。 Untruncated 字串值的長度會在 **StringLengthPtr*中傳回。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08003|連接未開啟|（DM）指定了需要開啟連接的*屬性*值。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagField**中的引數*MessageText*從診斷資料結構傳回的錯誤訊息描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY010|函數順序錯誤|已針對*ConnectionHandle*呼叫（DM） **SQLBrowseConnect** ，並傳回 SQL_NEED_DATA。 在**SQLBrowseConnect**傳回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS 之前，會呼叫這個函式。<br /><br /> （DM）已針對*ConnectionHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並 SQL_PARAM_DATA_AVAILABLE 傳回。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|（DM） * \*valueptr 是*是字元字串，BufferLength 小於零，但不等於 SQL_NTS。|  
|HY092|不正確屬性/選項識別碼|為引數*屬性*指定的值對驅動程式支援的 ODBC 版本無效。|  
|HY114|驅動程式不支援連接層級的非同步函式執行|（DM）應用程式嘗試為不支援非同步連接作業的驅動程式，使用 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 來啟用非同步函數執行。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|為引數*屬性*指定的值，對於驅動程式所支援的 odbc 版本而言是有效的 odbc 連接屬性，但驅動程式並不支援。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）對應至*ConnectionHandle*的驅動程式不支援函數。|  
  
## <a name="comments"></a>評價  
 如需連接屬性的一般資訊，請參閱[連接屬性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 如需可設定的屬性清單，請參閱[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。 請注意，如果*屬性*指定的屬性會傳回字串，則*valueptr 是*必須是字串緩衝區的指標。 傳回字串的最大長度，包括 null 終止字元，將會是*BufferLength*位元組。  
  
 視屬性而定，應用程式在呼叫**SQLGetConnectAttr**之前，不需要建立連接。 不過，如果呼叫**SQLGetConnectAttr** ，而且指定的屬性沒有預設值，而且尚未由先前的**SQLSetConnectAttr**呼叫所設定，則**SQLGetConnectAttr**會傳回 SQL_NO_DATA。  
  
 如果*屬性*是 SQL_ATTR_ 追蹤或 SQL_ATTR_ TRACEFILE，則*ConnectionHandle*不需要有效，而且**SQLGetConnectAttr**不會傳回 SQL_ERROR 或 SQL_INVALID_HANDLE （如果*ConnectionHandle*無效）。 這些屬性適用于所有連接。 如果另一個引數無效， **SQLGetConnectAttr**會傳回 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
 雖然應用程式可以使用**SQLSetConnectAttr**來設定語句屬性，但應用程式無法使用**SQLGetConnectAttr**來取出語句屬性值;它必須呼叫**SQLGetStmtAttr**來取得語句屬性的設定。  
  
 SQL_ATTR_AUTO_IPD 和 SQL_ATTR_CONNECTION_DEAD 連接屬性都可透過呼叫**SQLGetConnectAttr**來傳回，但不能由**SQLSetConnectAttr**的呼叫所設定。  
  
> [!NOTE]  
>  **SQLGetConnectAttr**沒有非同步支援。 在執行**SQLGetConnectAttr**時，驅動程式可以將資訊從伺服器傳送或要求的次數減至最少，藉此改善效能。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|傳回語句屬性的設定|[SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定環境屬性|[SQLSetEnvAttr 函式](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|設定語句屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
