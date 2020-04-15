---
title: SQLGetConnectAttr 函數 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285628"
---
# <a name="sqlgetconnectattr-function"></a>SQLGetConnectAttr 函數
**一致性**  
 推出版本: ODBC 3.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLGetConnectAttr**傳回連接屬性的當前設置。  
  
> [!NOTE]
>  有關驅動程式管理員將此功能映射到 ODBC 3 *.x*應用程式使用 ODBC 2 *.x*驅動程式時的詳細資訊,請參閱[映射應用程式向後相容性的替代函數](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
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
 *連接句柄*  
 [輸入] 連線控制代碼。  
  
 *屬性*  
 [輸入]要檢索的屬性。  
  
 *ValuePtr*  
 【輸出]指向記憶體的指標,用於返回*屬性*指定的屬性的當前值。 對於整數類型屬性,某些驅動程式可能只寫入緩衝區的較低 32 位元或 16 位元,並且保持高階位不變。 因此,應用程式應在調用此函數之前使用 SQLULEN 的緩衝區並將該值初始化為 0。  
  
 如果*ValuePtr*為 NULL,*則 StringLengthPtr*仍將返回可用返回*ValuePtr*指向的緩衝區中的位元組總數(不包括字元資料的空終止字元)。  
  
 *緩衝區長度*  
 [輸入]如果*屬性*是 ODBC 定義的屬性 *,ValuePtr*指向字串或二進位緩衝區,\*則此參數應為*ValuePtr*的長度。 如果*屬性*是 ODBC\*定義的屬性 *,ValuePtr*是整數,則忽略*緩衝區長度*。 如果*\*ValuePtr*中的值是 Unicode 字串(在呼叫**SQLGetConnectAttrW**時),*緩衝區長度*參數必須是偶數。  
  
 如果*屬性*是驅動程式定義的屬性,則應用程式通過設置*BufferLength*參數指示該屬性對驅動程式管理員的性質。 *緩衝區長度*可以具有以下值:  
  
-   如果*\*ValuePtr*是指向字串的指標,*則緩衝區長度*是字串的長度。  
  
-   如果*\*ValuePtr*是指向二進位緩衝區的指標,則應用程式將SQL_LEN_BINARY_ATTR(*長度*)宏的結果放在*緩衝區長度*中。 這將在*緩衝區長度*中放置負值。  
  
-   如果*\*ValuePtr*是指向字串或二進位元字串以外的值的指標,*則 BufferLength*應具有該值SQL_IS_POINTER。  
  
-   如果*\*ValuePtr*包含固定長度的數據類型,則*緩衝區長度*SQL_IS_INTEGER或SQL_IS_UINTEGER(視適用)。  
  
 *字串長度 Ptr*  
 【輸出]指向緩衝區的指標,用於返回可在\**ValuePtr*中返回的位元組總數(不包括空終止字元)。 如果\* *ValuePtr*是空指標,則不返回任何長度。 如果屬性值是字串,並且可供返回的位元組數大於*BufferLength*減去空終止字元的長度,則*\*ValuePtr*中的數據將截斷為*BufferLength*減去空終止字元的長度,並且驅動程式為 null 終止。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetConnect Attr**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec,** 使用SQL_HANDLE_DBC的*句柄和**連接句柄*從診斷*Handle*資料結構獲取關聯的 SQLSTATE 值。 下表列出了**SQLGetConnectAttr**通常返回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|\* *ValuePtr*中返回的數據被截斷為*緩衝區長度*減去空終止字元的長度。 未壓縮字串值的長度在 #*StringLengthPtr*中返回。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08003|連線未開啟|(DM) 指定了需要打開連接*的屬性*值。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagField**中的參數*MessageText*從診斷資料結構傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY010|函式序列錯誤|(DM) **SQLBrowseConnect**被調用用於*連接句柄*並返回SQL_NEED_DATA。 在**SQLBrowseConnect**返回SQL_SUCCESS_WITH_INFO或SQL_SUCCESS之前調用此功能。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用用於**SQLExecDirect***連接處理*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) * \*ValuePtr*是一個字串,緩衝區長度小於零但不等於SQL_NTS。|  
|HY092|不合法屬性/選項識別碼|為參數*屬性*指定的值對於驅動程式支援的 ODBC 版本無效。|  
|HY114|驅動程式不支援連接層數執行|(DM) 應用程式嘗試為不支援非同步連接操作的驅動程式啟用具有SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE非同步函數執行。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|為參數*屬性*指定的值是驅動程式支援的 ODBC 版本的有效 ODBC 連接屬性,但驅動程式不支援該屬性。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 對應於*連接句柄*的驅動程式不支援該功能。|  
  
## <a name="comments"></a>註解  
 有關連線屬性的一般資訊,請參閱[連接屬性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 有關可以設定的屬性清單,請參閱[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。 請注意,如果*屬性*指定返回字串的屬性 *,ValuePtr*必須是指向字串緩衝區的指標。 返回的字串(包括空終止字元)的最大長度將為*BufferLength*位元組。  
  
 根據屬性,應用程式在調用**SQLGetConnectAttr**之前不必建立連接。 但是,如果調用**SQLGetConnectAttr**並且指定的屬性沒有預設值,並且未通過事先調用**SQLSetConnectAttr**設置,**則 SQLGetConnect Attr**將返回SQL_NO_DATA。  
  
 如果*屬性*SQL_ATTR_ TRACE 或 SQL_ATTR_ TRACEFILE,*則連接句柄*不必有效,如果*連接句柄*無效 **,SQLGetConnectAttr**將不會返回SQL_ERROR或SQL_INVALID_HANDLE。 這些屬性適用於所有連接。 如果另一個參數無效 **,SQLGetConnectAttr**將返回SQL_ERROR或SQL_INVALID_HANDLE。  
  
 儘管應用程式可以使用**SQLSetConnectAttr**設定語句屬性,但應用程式不能使用**SQLGetConnectAttr**來檢索語句屬性值;因此,應用程式無法使用 SQLGetConnectAttr 來檢索語句屬性值。它必須調用**SQLGetStmtAttr**來檢索語句屬性的設置。  
  
 SQL_ATTR_AUTO_IPD和SQL_ATTR_CONNECTION_DEAD連接屬性都可以通過調用**SQLGetConnectAttr**返回,但不能通過調用**SQLSetConnectAttr**來設置。  
  
> [!NOTE]  
>  **SQLGetConnectAttr**沒有非同步支援。 實現**SQLGetConnect Attr**時,驅動程式可以通過最大限度地減少從伺服器發送或請求資訊的次數來提高性能。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|傳回敘述屬性的設定|[SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|設定連線屬性|[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定環境屬性|[SQLSetEnvAttr 函式](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|設定敘述屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
