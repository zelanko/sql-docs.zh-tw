---
title: SQLSetEnvAttr 函數 |微軟文件
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetEnvAttr
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetEnvAttr
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC]
ms.assetid: 0343241c-4b15-4d4b-aa2b-2e8ab5215cd2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 640b1e6947d67b92e2b7f8e623597e1d99d4a877
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299538"
---
# <a name="sqlsetenvattr-function"></a>SQLSetEnvAttr 函數
**一致性**  
 推出版本: ODBC 3.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLSetEnvAttr**設置管理環境方面的屬性。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLSetEnvAttr(  
     SQLHENV      EnvironmentHandle,  
     SQLINTEGER   Attribute,  
     SQLPOINTER   ValuePtr,  
     SQLINTEGER   StringLength);  
```  
  
## <a name="arguments"></a>引數  
 *環境處理*  
 [輸入]環境句柄。  
  
 *屬性*  
 [輸入]要設置的屬性,列在"註釋"中。  
  
 *ValuePtr*  
 [輸入]指向要與*屬性*關聯的值的指標。 根據*屬性*的值 *,ValuePtr*將是一個 32 位元整數值或指向 null 端接的字串。  
  
 *字串長度*  
 [輸入]如果*ValuePtr*指向字串或二進位緩衝區,則此參數應為 **ValuePtr*的長度。 對於字串資料,此參數應包含字串中的位元組數。  
  
 如果*ValuePtr*是整數,則忽略*字串長度*。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetEnvAttr**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_ENV的處理*類型*和環境*句柄**句柄。* 下表列出了**SQLSetEnvAttr**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。 如果驅動程式不支援環境屬性,則只能在連接期間返回錯誤。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01S02|選項值已變更|驅動程式不支援*ValuePtr*中指定的值,並替換了類似的值。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY009|不合法的空白指標|屬性參數標識了需要字串值的環境屬性 *,ValuePtr*參數為空指標。|  
|HY010|函式序列錯誤|(DM) 已在*環境句柄*上分配了連接句柄。<br /><br /> (DM) **SQL_ATTR_ODBC_VERSION**尚未使用**SQLSetEnvAttr**設定,*屬性*不等於**SQL_ATTR_ODBC_VERSION**。 如果使用**SQLAllocHandleStd,** 則無需顯式設置**SQL_ATTR_ODBC_VERSION。**|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY024|不合法屬性值|給定指定的*屬性*值,在*ValuePtr*中指定了無效值。|  
|HY090|不合法的字串或緩衝區長度|*字串長度*參數小於 0,但沒有SQL_NTS。|  
|HY092|不合法屬性/選項識別碼|(DM) 為參數*屬性*指定的值對驅動程式支援的 ODBC 版本無效。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|為參數*屬性*指定的值是驅動程式支援的 ODBC 版本的有效 ODBC 環境屬性,但驅動程式不支援該屬性。<br /><br /> (DM)*屬性*參數*SQL_ATTR_OUTPUT_NTS,ValuePtr* SQL_FALSE。|  
  
## <a name="comments"></a>註解  
 僅當未在環境中分配連接句柄時,應用程式才能調用**SQLSetEnvAttr。** 應用程式為環境成功設置的所有環境屬性將一直持續到在環境上調用**SQLFreeHandle**為止。 可以在 ODBC *3.x*中同時分配多個環境句柄。  
  
 用*ValuePtr*設定的資訊格式來指定的*屬性*。 **SQLSetEnvAttr**將接受兩種不同格式之一的屬性資訊:空端字元字串或 32 位元整數值。 每個格式在屬性的說明中註明。  
  
 沒有特定於驅動程式的環境屬性。  
  
 連接屬性不能通過調用**SQLSetEnvAttr**來設置。 嘗試執行此操作將返回 SQLSTATE HY092(無效屬性/選項標識符)。  
  
|*屬性*|*價值 Ptr*內容|  
|-----------------|-------------------------|  
|SQL_ATTR_CONNECTION_POOLING (ODBC 3.8)|32 位元SQLUINTEGER值,可在環境等級啟用或禁用連接池。 使用以下值:<br /><br /> SQL_CP_OFF = 連接池已關閉。 這是預設值。<br /><br /> SQL_CP_ONE_PER_DRIVER = 每個驅動程式都支援單個連接池。 池中的每個連接都與一個驅動程序相關聯。<br /><br /> SQL_CP_ONE_PER_HENV = 每個環境都支援單個連接池。 池中的每個連接都與一個環境相關聯。<br /><br /> SQL_CP_DRIVER_AWARE = 如果驅動程式可用,請使用驅動程式的連接池感知功能。 如果驅動程式不支援連接池感知,則忽略SQL_CP_DRIVER_AWARE,並使用SQL_CP_ONE_PER_HENV。 有關詳細資訊,請參閱[驅動程式感知連接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。 在某些驅動程式支援並且某些驅動程式不支援連接池感知的環境中,SQL_CP_DRIVER_AWARE可以在支援驅動程式上啟用連接池感知功能,但它等效於將設置為SQL_CP_ONE_PER_HENV不支援連接池感知功能的驅動程式。<br /><br /> 通過調用**SQLSetEnvAttr**將SQL_ATTR_CONNECTION_POOLING屬性設置為SQL_CP_ONE_PER_DRIVER或SQL_CP_ONE_PER_HENV,從而啟用連接池。 在應用程式分配要為其啟用連接池的共用環境之前,必須進行此調用。 **SQLSetEnvAttr**調用中的環境句柄設置為 null,這使得SQL_ATTR_CONNECTION_POOLING進程級屬性。 啟用連接池後,應用程式將調用**SQLAllocHandle**並設置為 SQL_HANDLE_ENV的 *「輸入句柄*」參數來分配隱式共用環境。<br /><br /> 啟用連接池並為應用程式選擇共享環境後,無法為該環境重置SQL_ATTR_CONNECTION_POOLING,因為在設置此屬性時使用空環境句柄調用**SQLSetEnvAttr。** 如果在共用環境中啟用連接池時設置了此屬性,則該屬性僅影響隨後分配的共用環境。<br /><br /> 還可以在環境中啟用連接池。 請注意以下有關環境連接池:<br /><br /> - 在 NULL 句柄上啟用連接池是進程級屬性。 隨後分配的環境將是一個共用環境,並將繼承進程級連接池設置。<br />- 分配環境後,應用程式仍可以更改其連接池設置。<br />- 如果啟用了環境連接池,並且連接的驅動程式使用驅動程式池,則環境池將優先。<br /><br /> SQL_ATTR_CONNECTION_POOLING在驅動程式管理器內實現。 驅動程式不需要實現SQL_ATTR_CONNECTION_POOLING。 ODBC 2.0 和 3.0 應用程式可以設置此環境屬性。<br /><br /> 如需詳細資訊，請參閱 [ODBC 連接共用](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。|  
|SQL_ATTR_CP_MATCH (ODBC 3.0)|32 位元SQLUINTEGER值,用於確定如何從連接池中選擇連接。 當調用**SQLConnect**或**SQLDriverConnect**時,驅動程式管理器確定從池中重用哪個連接。 驅動程式管理員嘗試將調用中的連接選項以及應用程式設置的連接屬性與池中連接的關鍵字和連接屬性相匹配。 此屬性的值確定匹配條件的精度級別。<br /><br /> 以下值用於設定此屬性的值:<br /><br /> SQL_CP_STRICT_MATCH = 僅重複使用與調用中的連接選項和應用程式設置的連接屬性完全匹配的連接。 這是預設值。<br /><br /> SQL_CP_RELAXED_MATCH = 可以使用具有匹配連接字串關鍵字的連接。 關鍵字必須匹配,但不是所有連接屬性都必須匹配。<br /><br /> 有關驅動程式管理員在連接到池連接時如何執行匹配的詳細資訊,請參閱[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)。 有關連接池的詳細資訊,請參閱[ODBC 連接池](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。|  
|SQL_ATTR_ODBC_VERSION (ODBC 3.0)|32 位元整數,用於確定某些功能是否顯示 ODBC *2.x*行為還是 ODBC *3.x*行為。 以下值用於設定此屬性的值:<br /><br /> SQL_OV_ODBC3_80 = 驅動程式管理員和驅動程式表現出以下 ODBC 3.8 行為:<br /><br /> - 驅動程式傳回並期望 ODBC *3.x*日期、時間和時間戳的代碼。<br />- 當呼叫**SQLError、SQLGetDiagField**或**SQLGetDiagRec**時,驅動程式返回 ODBC *3.x* SQLSTATE 代碼。 **SQLError**<br />- 對**SQLTables**的呼叫中的*目錄名稱*參數接受搜尋模式。<br />- 驅動程式管理員支援 C 資料類型擴充性。 關於 C 資料型態擴充的詳細資訊,請參考[ODBC 中的 C 資料型態](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。<br /><br /> 有關詳細資訊,請參閱[ODBC 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。<br /><br /> SQL_OV_ODBC3 = 驅動程式管理員與驅動程式表現出以下 ODBC *3.x*行為:<br /><br /> - 驅動程式傳回並期望 ODBC *3.x*日期、時間和時間戳的代碼。<br />- 當呼叫**SQLError、SQLGetDiagField**或**SQLGetDiagRec**時,驅動程式返回 ODBC *3.x* SQLSTATE 代碼。 **SQLError**<br />- 對**SQLTables**的呼叫中的*目錄名稱*參數接受搜尋模式。<br />- 驅動程式管理員不支援 C 資料類型擴充性。<br /><br /> SQL_OV_ODBC2 = 驅動程式管理器和驅動程式表現出以下 ODBC *2.x*行為。 這對於使用 ODBC *3.x*驅動程式的 ODBC *2.x*應用程式特別有用。<br /><br /> - 驅動程式傳回並期望 ODBC *2.x*日期、時間和時間戳的代碼。<br />- 當呼叫**SQLError、SQLGetDiagField**或**SQLGetDiagRec**時,驅動程式返回 ODBC *2.x* SQLSTATE 代碼。 **SQLError**<br />- 呼叫**SQLTables**中的*目錄名稱*參數不接受搜尋模式。<br />- 驅動程式管理員不支援 C 資料類型擴充性。<br /><br /> 應用程式在調用具有 SQLHENV 參數的任何函數之前必須設置此環境屬性,否則調用將返回 SQLSTATE HY010(函數序列錯誤)。 這些環境標誌是否存在其他行為是特定於驅動程式的。<br /><br /> - 關於詳細資訊,請參考[「 宣告應用程式」的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)[與行為變更](../../../odbc/reference/develop-app/behavioral-changes.md)。|  
|SQL_ATTR_OUTPUT_NTS (ODBC 3.0)|一個 32 位整數,用於確定驅動程式返回字串數據的方式。 如果SQL_TRUE,驅動程式返回字串數據為 null 終止。 如果SQL_FALSE,驅動程式不會返回字串數據為 null 終止。<br /><br /> 此屬性預設為SQL_TRUE。 調用**SQLSetEnv Attr**將其設置為SQL_TRUE返回SQL_SUCCESS。 呼叫**SQLSetEnvAttr**將其設定為SQL_FALSE返回SQL_ERROR和 SQLSTATE HYC00(未實現可選功能)。|  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|配置控點|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|傳回環境屬性的設定|[SQLGetEnvAttr 函式](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標題檔案](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 3.8 的新功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
