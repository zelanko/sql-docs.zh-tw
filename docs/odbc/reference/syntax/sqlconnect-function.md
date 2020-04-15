---
title: SQLConnect 功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConnect
helpviewer_keywords:
- SQLConnect function [ODBC]
ms.assetid: 59075e46-a0ca-47bf-972a-367b08bb518d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ab0a31845efeb484c554a9c9cf1afeaeab1a8bea
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301214"
---
# <a name="sqlconnect-function"></a>SQLConnect 函數
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLConnect**建立與驅動程式和數據源的連接。 連接句柄引用有關數據源連接的所有資訊的存儲,包括狀態、事務狀態和錯誤資訊。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLConnect(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      ServerName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      UserName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      Authentication,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>引數  
 *連接句柄*  
 [輸入] 連線控制代碼。  
  
 *ServerName*  
 [輸入]數據源名稱。 數據可能位於與程式相同的電腦上,或者位於網路上的另一台電腦上。 關於應用程式如何選擇資料來源的資訊,請參考[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 *NameLength1*  
 [輸入]長度 = 以字元表示*伺服器名稱*。  
  
 *使用者*  
 [輸入]用戶識別碼。  
  
 *名稱長度2*  
 [輸入]長度 =*字元中的使用者名稱*。  
  
 *驗證*  
 [輸入]身份驗證字串(通常是密碼)。  
  
 *名稱長度3*  
 [輸入]長度 =*字元認證*。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE 或SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLConnect**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_DBC的*句柄類型*和*連線句柄*的*句柄*。 下表列出了**SQLConnect**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01S02|選項值已變更|驅動程式不支援**SQLSetConnectAttr**中*ValuePtr*參數的指定值,並替換了類似的值。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08001|用戶端無法建立連線|驅動程式無法與數據源建立連接。|  
|08002|使用的連線名稱|(DM) 指定的*ConnectHandle*已用於與資料源建立連接,並且連接仍處於打開狀態或使用者正在瀏覽連接。|  
|08004|伺服器拒絕連接|數據源出於實現定義的原因拒絕建立連接。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程序嘗試連接到的數據源之間的通信鏈路失敗。|  
|28000|不合法的授權規範|為參數*UserName*指定的值或為參數指定的值*身份驗證*違反了數據來源定義的限制。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|(DM) 驅動程式管理員無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|為*連接句柄*啟用了非同步處理。 SQLConnect 函數被調用,在完成執行之前,在 ConnectHandle 上調用[了 SQLCancelHandle 函數](../../../odbc/reference/syntax/sqlcancelhandle-function.md),然後在**SQLConnect** *ConnectHandle*上再次調用**SQLConnect**函數。 *ConnectionHandle*<br /><br /> 或者 **,SQLConnect**函數被調用,在完成執行之前 **,SQLCancelHandle**是從多線程應用程式中的不同線程調用的*ConnectHandle。*|  
|HY010|函式序列錯誤|(DM) 為*ConnectHandle*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) 為參數*NameLength1、NameLength2*或*NameLength3*指定的值小於 0,*NameLength2*但不等於SQL_NTS。<br /><br /> (DM) 為參數*NameLength1*指定的值超過了資料源名稱的最大長度。|  
|HYT00|已超過逾時的設定|查詢超時期限在連接到數據源之前過期。 超時期間通過**SQLSetConnectAttr**SQL_ATTR_LOGIN_TIMEOUT設置。|  
|HY114|驅動程式不支援連接層級功能執行|(DM) 在進行連接之前,應用程式在連接句柄上啟用了非同步操作。 但是,驅動程式不支援對連接句柄的非同步操作。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 資料來源名稱指定的驅動程式不支援該函數。|  
|IM002|找不到資料來源,未指定預設驅動程式|(DM) 參數*ServerName*中指定的資料來源名稱未在系統資訊中找到,也沒有預設驅動程式規範。|  
|IM003|指定的驅動程式無法連線到|(DM) 由於其他原因,找不到或無法連接到系統資訊中的數據源規範中列出的驅動程式。|  
|IM004|驅動程式的 SQLAllocHandle 上SQL_HANDLE_ENV失敗|(DM) 在**SQLConnect**期間,驅動程式管理器呼叫驅動程式的**SQLAllocHandle**函數,該函數具有SQL_HANDLE_ENV的*句柄類型*,驅動程式傳回了錯誤。|  
|IM005|驅動程式的 SQLAllocHandle 上SQL_HANDLE_DBC失敗|(DM) 在**SQLConnect**期間,驅動程式管理器呼叫驅動程式的**SQLAllocHandle**函數,該*函數具有SQL_HANDLE_DBC的句柄類型*,驅動程式傳回了錯誤。|  
|IM006|驅動程式的 SQLSetConnectAttr 失敗|在**SQLConnect**期間,驅動程式管理器呼叫驅動程式的**SQLSetConnectAttr**函數,驅動程式傳回了錯誤。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|IM009|無法連線到翻譯 DLL|驅動程式無法連接到為資料來源指定的轉換 DLL。|  
|IM010|資料來源名稱太長|(DM)*\*伺服器名稱*長於SQL_MAX_DSN_LENGTH個字元。|  
|IM014|指定的 DSN 包含驅動程式與應用程式之間的架構結構不符合|(DM) 32 位元應用程式使用 DSN 連接到 64 位元驅動程式;反之亦然。|  
|IM015|驅動程式的 SQLConnect SQL_HANDLE_DBC_INFO_HANDLE發生故障|如果驅動程式返回SQL_ERROR,驅動程式管理員將返回SQL_ERROR到應用程式,連接將失敗。<br /><br /> 有關SQL_HANDLE_DBC_INFO_TOKEN的詳細資訊,請參閱在[ODBC 驅動程式中開發連接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
|S1118|驅動程式不支援非同步通知|當驅動程式不支援非同步通知時,無法設置SQL_ATTR_ASYNC_DBC_EVENT或SQL_ATTR_ASYNC_DBC_RETCODE_PTR。|  
  
## <a name="comments"></a>註解  
 有關應用程式使用**SQLConnect**的原因的資訊,請參閱[與 SQLConnect 連線](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)。  
  
 驅動程式管理員不會連接到驅動程式,直到應用程式呼叫函數 **(SQLConnect,** **SQLDriverConnect,** 或**SQLBrowseConnect**) 連接到驅動程式. 在此之前,驅動程式管理器使用其自己的句柄並管理連接資訊。 當應用程式呼叫連線函數時,驅動程式管理員檢查驅動程式目前是否連接到指定的*ConnectHandle*:  
  
-   如果驅動程式未連接到,驅動程式管理器連接到驅動程式,並且調用**SQLAllocHandle**與 SQL_HANDLE_ENV 的*句柄類型*、具有*SQL_HANDLE_DBC句柄類型的*SQLAllocHandle、SQLSetConnectAttr(如果應用程式指定任何連接屬性)**SQLAllocHandle****SQLSetConnectAttr**和驅動程式中的連接功能。 如果驅動程式返回**SQLSetConnectAttr**的錯誤,驅動程式管理器將返回 SQLSTATE IM006(驅動程式的**SQLSetConnectOption**失敗)和連接函數SQL_SUCCESS_WITH_INFO。 關於詳細資訊,請參考[連接到資料來源或驅動程式](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)。  
  
-   如果指定的驅動程式已連接到*ConnectHandle*上,則驅動程式管理器僅調用驅動程式中的連接功能。 在這種情況下,驅動程式必須確保*ConnectHandle*的所有連接屬性都保持其當前設置。  
  
-   如果連接到其他驅動程式,驅動程式管理器將**SQLFreeHandle**調用具有 SQL_HANDLE_DBC 的*句柄類型*,然後,如果該環境中沒有其他驅動程式連接到**SQLFreeHandle,則調用 SQLFreeHandle,** 在連接的驅動程式中使用 SQL_HANDLE_ENV的*句柄類型*,然後斷開該驅動程式。 然後,它執行與驅動程式未連接到時相同的操作。  
  
 然後,驅動程式分配句柄並初始化自身。  
  
 當應用程式呼叫**SQLDISCONNECT**時,驅動程式管理器在驅動程式中調用**SQLDISCONNECT。** 但是,它不會斷開驅動程式。 這樣,對於反覆連接到數據源並斷開與數據源的連接的應用程序,驅動程式將保留在記憶體中。 當應用程式使用*SQL_HANDLE_DBC的句柄類型*呼叫**SQLFreeHandle**時,驅動程式管理器使用SQL_HANDLE_DBC*的句柄類型*調用**SQLFreeHandle,** 然後在驅動程式中使用 SQL_HANDLE_ENV的*句柄類型*調用**SQLFreeHandle,** 然後斷開驅動程式的連接。  
  
 ODBC 應用程式可以建立多個連接。  
  
## <a name="driver-manager-guidelines"></a>駕駛員經理指南  
 **ServerName*的內容會影響驅動程式管理員和驅動程式協同工作以建立與資料源的連接的方式。  
  
-   如果\* *ServerName*包含合法資料來源名稱,驅動程式管理員將尋找系統資訊中的相應資料來源規範並連接到關聯的驅動程式。 驅動程式管理員將每個**SQLConnect**參數傳遞給驅動程式。  
  
-   如果找不到資料來源名稱或*ServerName*是空指標,驅動程式管理員將尋找預設資料來源規範並連接到關聯的驅動程式。 驅動程式管理員將*未修改的使用者名稱*和*身份驗證*參數傳遞給驅動程式,將*伺服器名稱*參數的"DEFAULT"傳遞給驅動程式。  
  
-   如果*伺服器名稱*參數為"DEFAULT",驅動程式管理員將查找預設數據源規範並連接到關聯的驅動程式。 驅動程式管理員將每個**SQLConnect**參數傳遞給驅動程式。  
  
-   如果找不到資料源名稱或*ServerName*是空指標,並且預設資料來源規範不存在,則驅動程式管理器將返回 SQL_ERROR SQLSTATE IM002(找不到資料源名稱,未指定預設驅動程式)。  
  
 驅動程式管理員連接到它後,驅動程式可以在系統資訊中尋找其相應的資料來源規範,並使用規範中的特定於驅動程式的資訊來完成其所需的連接資訊集。  
  
 如果在數據源的系統資訊中指定了默認翻譯庫,則驅動程式將連接到該庫。 使用SQL_ATTR_TRANSLATE_LIB屬性調用**SQLSetConnectAttr,** 可以連接到不同的翻譯庫。 可以通過使用SQL_ATTR_TRANSLATE_OPTION屬性調用**SQLSetConnectAttr**來指定轉換選項。  
  
 如果驅動程式支援**SQLConnect,** 則驅動程式的系統資訊的驅動程式關鍵字部分必須包含**ConnectFunctions**關鍵字,第一個字元設置為「Y」。。  
  
### <a name="connection-pooling"></a>連接共用  
 連接池允許應用程式重用已創建的連接。 啟用連接池並調用**SQLConnect**時,驅動程式管理器嘗試使用已指定用於連接池的環境中的連接池的一部分進行連接。 此環境是一個共享環境,由使用池中連接的所有應用程式使用。  
  
 在分配環境之前,通過調用**SQLSetEnvAttr**將SQL_ATTR_CONNECTION_POOLING設置為SQL_CP_ONE_PER_DRIVER(每個驅動程式最多指定一個池)或SQL_CP_ONE_PER_HENV(每個環境最多指定一個池)。在分配環境之前啟用連接池。 在這種情況下 **,SQLSetEnvAttr**調用*環境處理設置為*null,這使得屬性成為進程級屬性。 如果SQL_ATTR_CONNECTION_POOLING設置為SQL_CP_OFF,則禁用連接池。  
  
 啟用連接池后,將調用具有*句柄類型*SQL_HANDLE_ENV **SQLAllocHandle**來分配環境。 此調用分配的環境是共用環境,因為連接池已啟用。 但是,在調用具有SQL_HANDLE_DBC的**SQLAllocHandle**之前,不會確定*HandleType*將使用的環境。  
  
 調用具有*處理類型*SQL_HANDLE_DBC的**SQLAllocHandle**來分配連接。 驅動程式管理員嘗試尋找與應用程式設定的環境屬性匹配的現有共享環境。 如果不存在此類環境,則建立一個環境作為隱式*共用環境*。 如果找到匹配的共用環境,環境句柄將返回到應用程式,其引用計數將遞增。  
  
 但是,在調用**SQLConnect**之前,不會確定將使用的連接。 此時,驅動程式管理器嘗試在連接池中找到與應用程式請求的條件匹配的現有連接。 這些標準包括在調用**SQLConnect**時請求的連線選項(*伺服器名稱*、*使用者名稱*和*身份驗證*關鍵字的值)以及自呼叫具有*SQL_HANDLE_DBC的***SQLAllocHandle**以來設定的任何連接屬性。 驅動程式管理員根據池中連接中的相應連接關鍵字和屬性檢查這些標準。 如果找到匹配項,則使用池中的連接。 如果未找到匹配項,則創建新連接。  
  
 如果SQL_ATTR_CP_MATCH環境屬性設置為SQL_CP_STRICT_MATCH,則使用池中的連接必須精確匹配。 如果將SQL_ATTR_CP_MATCH環境屬性設置為SQL_CP_RELAXED_MATCH,則調用**SQLConnect**中的連接選項必須匹配,但不是所有連接屬性必須匹配。  
  
 當呼叫**SQLConnect**之前由應用程式設定的連線屬性與池中連接的連線屬性不匹配時,將應用以下規則:  
  
-   如果在建立連線之前必須設定連線屬性:  
  
     如果SQL_CP_STRICT_MATCHSQL_ATTR_CP_MATCH,則池連接中的SQL_ATTR_PACKET_SIZE必須與應用程式設置的屬性相同。 如果SQL_CP_RELAXED_MATCH,則SQL_ATTR_PACKET_SIZE的值可能不同。  
  
     SQL_ATTR_LOGIN_VALUE的值不會影響匹配。  
  
-   如果在建立連線之前或之後可以設定連接屬性:  
  
     如果連接屬性尚未由應用程式設置,但已在池中的連接上設置,並且存在預設值,則池連接中的連接屬性將設置回預設值並聲明匹配。 如果沒有預設值,則池連接不被視為匹配。  
  
     如果連接屬性已由應用程式設置,但尚未在池中的連接上設置,則池上的連接屬性將由應用程式更改為該集,並聲明匹配項。  
  
     如果連接屬性已由應用程式設置,並且也已在池中的連接上設置,但值不同,則使用應用程式的連接屬性的值並聲明匹配項。  
  
-   如果特定於驅動程式的連接屬性的值不相同,並且SQL_ATTR_CP_MATCH設置為SQL_CP_STRICT_MATCH,則不使用池中的連接。  
  
 當應用程式調用**SQLDisconnect**斷開連接時,連接將返回到連接池,可供重用。  
  
### <a name="optimizing-connection-pooling-performance"></a>優化連線池效能  
 當涉及分散式事務時,可以使用**SQL_DTC_TRANSITION_COST**來優化連接池性能,這是SQLUINTEGER位掩碼。 引用的過渡是連接屬性SQL_ATTR_ENLIST_IN_DTC從值 0 到非零的過渡,反之亦然。 這是一個連接,從未在分散式事務中登記到在分散式事務中登記,反之亦然。 根據驅動程式如何實現登記(設置連接屬性SQL_ATTR_ENLIST_IN_DTC),這些轉換可能非常昂貴,因此應避免進行,以獲得最佳性能。  
  
 驅動程式傳回的值包含以下位的任意組合:  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**,設置時,意味著零到非零轉換比從非零轉換到另一個非零值(在其下一個事務中登記以前登記的連接)要昂貴得多。  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**設置時,意味著非零到零轉換比使用SQL_ATTR_ENLIST_IN_DTC屬性已設置為零的連接要昂貴得多。  
  
 性能與連接使用權衡。 如果驅動程式指示其中一個或多個轉換成本高昂,則驅動程式管理器的連接池管理器通過在池中保留更多連接來回應此。 池中的某些連接是非事務用途的首選,有些連接是事務用途的首選。 但是,如果驅動程式指示這些轉換不昂貴,則可以使用較少的連接,也許在非事務性和事務性使用之間交替使用。  
  
 不支援SQL_ATTR_ENLIST_IN_DTC的驅動程式不需要支援SQL_DTC_TRANSITION_COST。 對於支援SQL_ATTR_ENLIST_IN_DTC但不SQL_DTC_TRANSITION_COST的驅動程式,假定轉換並不昂貴,就像驅動程式為此值返回 0(未設置位)。  
  
 雖然在 ODBC 3.5 中引入了SQL_DTC_TRANSITION_COST,但 ODBC 2。*x*驅動程式也可以支援它,因為驅動程式管理員將查詢此資訊,而不考慮驅動程式版本。  
  
### <a name="code-example"></a>程式碼範例  
 在下面的示例中,應用程式分配環境和連接句柄。 然後,它使用使用者 ID JohnS 和密碼芝麻連接到 SalesOrders 數據源並處理數據。 處理完數據后,它將斷開數據源的連接並釋放句柄。  
  
```cpp  
// SQLConnect_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR * OutConnStr = (SQLCHAR * )malloc(255);  
   SQLSMALLINT * OutConnStrLen = (SQLSMALLINT *)malloc(255);  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLCHAR*) "NorthWind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
### <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|配置控點|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|找到與枚舉連線到資料來源所需的值|[SQLBrowseConnect 函式](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|與資料源斷線連線|[SQLDisconnect 函式](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|使用連接字串或對話框連接到資料來源|[SQLDriverConnect 函數](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|傳回連線屬性的設定|[SQLGetConnectAttr 函數](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|設定連線屬性|[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
