---
title: SQLConnect 函式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a04daf57a348f20c8a5febe8d56f8ed9358b9053
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47631986"
---
# <a name="sqlconnect-function"></a>SQLConnect 函數
**合規性**  
 版本導入： ODBC 1.0 標準相容性： ISO 92  
  
 **摘要**  
 **SQLConnect**建立驅動程式和資料來源的連接。 連接控制代碼所參考 連線到資料來源，包括狀態、 交易狀態和錯誤資訊的所有資訊的儲存的體。  
  
## <a name="syntax"></a>語法  
  
```  
  
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
 *ConnectionHandle*  
 [輸入]連接控制代碼。  
  
 *ServerName*  
 [輸入]資料來源名稱。 資料可能位於程式，在同一部電腦或網路上的某個位置的另一部電腦上。 如需應用程式如何選擇資料來源資訊，請參閱[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 *NameLength1*  
 [輸入]長度 **ServerName*以字元為單位。  
  
 *UserName*  
 [輸入]使用者識別碼。  
  
 *NameLength2*  
 [輸入]長度 **UserName*以字元為單位。  
  
 *驗證*  
 [輸入]驗證字串 （通常是密碼）。  
  
 *NameLength3*  
 [輸入]長度 **驗證*以字元為單位。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLConnect**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_DBC 並*處理*的*ConnectionHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLConnect** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S02|選項值已變更|驅動程式不支援指定的值*ValuePtr*中的引數**SQLSetConnectAttr**和類似的值已被取代。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08001|無法建立連線的用戶端|驅動程式無法建立與資料來源的連接。|  
|08002|使用中的連接名稱|(DM) 指定*ConnectionHandle*必須已經用來建立與資料來源的連線和連線是仍處於開啟狀態，或使用者已瀏覽的連線。|  
|08004|伺服器拒絕連線|資料來源會拒絕連線建立實作定義的原因。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和資料來源的驅動程式在嘗試連線之間的通訊連結失敗。|  
|28000|無效的授權規格|指定的引數的值*使用者名稱*或是指定的引數的值*驗證*違反了資料來源所定義的限制。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式管理員 」 (DM) 無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*ConnectionHandle*。 **SQLConnect**呼叫函式，和之前執行，完成[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上呼叫*ConnectionHandle*，並接著**SQLConnect**上一次呼叫函式*ConnectionHandle*。<br /><br /> 或者， **SQLConnect**呼叫函式，和之前執行，完成**SQLCancelHandle**上呼叫*ConnectionHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *ConnectionHandle*和仍在呼叫此函式時所執行。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|(DM) 引數指定的值*NameLength1*， *NameLength2*，或*NameLength3*小於 0，但不是等於 SQL_NTS。<br /><br /> (DM) 引數指定的值*NameLength1*超過資料來源名稱的最大長度。|  
|HYT00|已超過逾時的設定|查詢逾時期限過期之前完成的資料來源的連接。 透過設定的逾時期限**SQLSetConnectAttr**，SQL_ATTR_LOGIN_TIMEOUT。|  
|HY114|驅動程式不支援連接層級的非同步函式執行|(DM) 應用程式啟用連接控制代碼上非同步作業之前建立的連接。 不過，此驅動程式不支援連接控制代碼上的非同步作業。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 的資料來源名稱所指定的驅動程式不支援此函式。|  
|IM002|找不到資料來源並沒有指定的預設驅動程式|(DM) 的資料來源的引數所指定的名稱*ServerName*找不到系統的資訊，或是否有預設的驅動程式規格。|  
|IM003|指定的驅動程式無法連接到|(DM) 資料中列出的驅動程式來源規格，在 系統資訊中的找不到或無法連線到某些其他原因。|  
|IM004|在 SQL_HANDLE_ENV 的驅動程式的 SQLAllocHandle 失敗|(DM) 期間**SQLConnect**，驅動程式管理員呼叫駕**SQLAllocHandle**函式搭配*HandleType* SQL_HANDLE_ENV 和驅動程式傳回錯誤。|  
|IM005|在利用 SQL_HANDLE_DBC 的驅動程式的 SQLAllocHandle 失敗|(DM) 期間**SQLConnect**，驅動程式管理員呼叫駕**SQLAllocHandle**函式搭配*HandleType*利用 SQL_HANDLE_DBC 和驅動程式傳回錯誤。|  
|IM006|驅動程式的 SQLSetConnectAttr 無法|期間**SQLConnect**，驅動程式管理員呼叫駕**SQLSetConnectAttr**函式和驅動程式傳回錯誤。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|IM009|無法連線到轉譯 DLL|驅動程式無法連線到轉譯的資料來源所指定的 DLL。|  
|IM010|資料來源名稱太長|(DM)  *\*ServerName*超過 SQL_MAX_DSN_LENGTH 字元。|  
|IM014|指定的 DSN 包含在驅動程式和應用程式之間的架構不相符|(DM) 32 位元應用程式使用 DSN 連接至 64 位元驅動程式;反之亦然。|  
|IM015|驅動程式的 SQLConnect SQL_HANDLE_DBC_INFO_HANDLE 上失敗|如果驅動程式會傳回 SQL_ERROR，驅動程式管理員將會傳回 SQL_ERROR，應用程式，而且連接會失敗。<br /><br /> 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊，請參閱[ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
|S1118|驅動程式不支援非同步通知|當驅動程式不支援非同步通知時，您無法對 SQL_ATTR_ASYNC_DBC_EVENT 或 SQL_ATTR_ASYNC_DBC_RETCODE_PTR 進行設定。|  
  
## <a name="comments"></a>註解  
 應用程式所使用之原因的相關資訊**SQLConnect**，請參閱[使用 sqlconnect 進行連接](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)。  
  
 驅動程式管理員不會連線至驅動程式應用程式呼叫函式之前 (**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**) 連接到驅動程式。 該時間點之前，驅動程式管理員會搭配它自己的控制代碼，並管理連接資訊。 當應用程式呼叫的連線函式時，驅動程式管理員會檢查驅動程式目前是否已連接到指定之*ConnectionHandle*:  
  
-   如果驅動程式未連線到，驅動程式管理員會連接到驅動程式，然後呼叫**SQLAllocHandle**具有*HandleType* SQL_HANDLE_ENV 的**SQLAllocHandle**與*HandleType*利用 SQL_HANDLE_DBC 的**SQLSetConnectAttr** （如果應用程式指定任何連接屬性），以及驅動程式中的連線函式。 驅動程式管理員會傳回 SQLSTATE IM006 (駕**SQLSetConnectOption**失敗) 和連接函式，如果驅動程式傳回的錯誤 SQL_SUCCESS_WITH_INFO **SQLSetConnectAttr**。 如需詳細資訊，請參閱 <<c0> [ 連接到資料來源或驅動程式](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)。  
  
-   如果指定的驅動程式已連線到在*ConnectionHandle*，驅動程式管理員驅動程式中呼叫連線函式。 在此情況下，驅動程式必須先確定所有的連接屬性的*ConnectionHandle*維護其目前的設定。  
  
-   如果不同的驅動程式連接到，驅動程式管理員會呼叫**SQLFreeHandle**具有*HandleType*利用 SQL_HANDLE_DBC 的然後，如果沒有其他的驅動程式已連線到該環境中，呼叫**SQLFreeHandle**具有*HandleType*已連線的驅動程式中利用 SQL_HANDLE_ENV 的然後斷線該驅動程式。 然後，它會執行與驅動程式時未連線到相同的作業。  
  
 驅動程式再配置控制代碼，並初始化本身。  
  
 當應用程式呼叫**SQLDisconnect**，此驅動程式管理員會呼叫**SQLDisconnect**驅動程式中。 不過，它不會中斷驅動程式。 這會在重複連接到和從資料來源中斷連接的應用程式的記憶體中保留驅動程式。 當應用程式呼叫**SQLFreeHandle**具有*HandleType*利用 SQL_HANDLE_DBC，驅動程式管理員呼叫**SQLFreeHandle**具有*HandleType*利用 SQL_HANDLE_DBC 的然後**SQLFreeHandle**具有*HandleType*中驅動程式，利用 SQL_HANDLE_ENV 的然後斷線的驅動程式。  
  
 ODBC 應用程式可以建立一個以上的連線。  
  
## <a name="driver-manager-guidelines"></a>驅動程式管理員的指導方針  
 內容 **ServerName*會影響如何驅動程式管理員和驅動程式一起運作以建立資料來源的連接。  
  
-   如果\* *ServerName*包含有效的資料來源名稱，驅動程式管理員在系統資訊中找出對應的資料來源規格，並連接到相關聯的驅動程式。 驅動程式管理員會將傳遞每**SQLConnect**驅動程式的引數。  
  
-   如果找不到資料來源名稱或*ServerName*為 null 指標，驅動程式管理員會找出預設資料來源的規格，並連接到相關聯的驅動程式。 驅動程式管理員會將傳遞至驅動程式*使用者名稱*並*驗證*未經修改的引數和 「 預設 」，如*ServerName*引數。  
  
-   如果*ServerName*引數為"DEFAULT"，驅動程式管理員會找出預設資料來源的規格，並連接到相關聯的驅動程式。 驅動程式管理員會將傳遞每**SQLConnect**驅動程式的引數。  
  
-   如果找不到資料來源名稱或*ServerName*是 null 指標，以及資料來源的規格不存在的預設值，驅動程式管理員會傳回 sql_error，其中包含 SQLSTATE IM002 （資料來源找不到名稱，沒有預設值指定驅動程式）。  
  
 它連線到透過驅動程式管理員之後，驅動程式可以在 系統資訊中找出其對應的資料來源規格，並使用從指定的驅動程式特定資訊來完成它需要的連接資訊的組。  
  
 如果在資料來源的系統資訊中指定的預設轉譯程式庫，則驅動程式連接到它。 不同的轉譯程式庫可以藉由呼叫連線到**SQLSetConnectAttr** SQL_ATTR_TRANSLATE_LIB 屬性。 轉譯選項可以指定藉由呼叫**SQLSetConnectAttr** SQL_ATTR_TRANSLATE_OPTION 屬性。  
  
 如果驅動程式支援**SQLConnect**，必須包含的驅動程式的系統資訊的 [驅動程式關鍵字] 區段**ConnectFunctions**的第一個字元的關鍵字設定為"Y"。  
  
### <a name="connection-pooling"></a>連接共用  
 連接共用，可讓應用程式重複使用已建立的連接。 當啟用連線共用並**SQLConnect**呼叫時，驅動程式管理員會嘗試以進行連線，使用屬於指定的連接共用的環境中的連接集區的連線。 此環境是使用連接集區中的所有應用程式所使用的共用的環境。  
  
 啟用連線共用的環境藉由呼叫配置之前**SQLSetEnvAttr**設 SQL_ATTR_CONNECTION_POOLING SQL_CP_ONE_PER_DRIVER （可指定每個驅動程式的一個集區的最大值） 或 SQL_CP_ONE_PER_HENV（指定每個環境的一個集區的最大的值）。 **SQLSetEnvAttr**在此情況下以呼叫*EnvironmentHandle*設為 null，讓處理序層級屬性的屬性。 如果 SQL_ATTR_CONNECTION_POOLING 設 SQL_CP_OFF，已停用連接共用。  
  
 啟用連接共用之後， **SQLAllocHandle**具有*HandleType*利用 SQL_HANDLE_ENV 的呼叫來配置環境。 這個呼叫所配置的環境是在共用的環境，因為已啟用連線共用。 不過，將使用的環境之前不會決定**SQLAllocHandle**具有*HandleType*利用 SQL_HANDLE_DBC 的呼叫。  
  
 **SQLAllocHandle**具有*HandleType*利用 SQL_HANDLE_DBC 的呼叫來配置的連接。 驅動程式管理員會嘗試尋找現有的共用的環境符合應用程式設定的環境屬性。 如果不存在此環境，其中會建立為隱含*共用的環境*。 如果找到相符的共用的環境，則環境控制代碼傳回給應用程式和其參考計數會漸增。  
  
 不過，將使用的連接之前不會決定**SQLConnect**呼叫。 此時，驅動程式管理員會嘗試尋找符合準則的應用程式所要求的連接集區中的現有連接。 這類準則包括要求呼叫中的連線選項**SQLConnect** (值*ServerName*， *UserName*，和*驗證*關鍵字) 和任何連接屬性組，因為**Handletype**具有*HandleType*利用 SQL_HANDLE_DBC 的呼叫。 驅動程式管理員會檢查這些準則，針對對應的連接關鍵字和集區中的連接中的屬性。 如果找到相符項目，則使用連接集區中。 如果找到相符項目，則會建立新的連接。  
  
 如果 SQL_ATTR_CP_MATCH 環境屬性設定為 SQL_CP_STRICT_MATCH，比對必須是完全可使用的集區中連接的。 如果 SQL_ATTR_CP_MATCH 環境屬性設定為 SQL_CP_RELAXED_MATCH，連接選項呼叫**SQLConnect**必須符合，但並非所有的連接屬性必須比對。  
  
 會套用下列規則時連線屬性所設定的應用程式，再**SQLConnect**呼叫時，不符合集區中連接的連接屬性：  
  
-   如果之前已連線，則必須設定連接屬性：  
  
     如果 SQL_ATTR_CP_MATCH SQL_CP_STRICT_MATCH，SQL_ATTR_PACKET_SIZE 中共用的連接必須與相同應用程式所設定的屬性。 如果 SQL_CP_RELAXED_MATCH，SQL_ATTR_PACKET_SIZE 的值可能會不同。  
  
     SQL_ATTR_LOGIN_VALUE 的值不會影響比對。  
  
-   如果之前或之後建立連接，則可以設定連接屬性：  
  
     如果連接屬性尚未設定應用程式，但已設定連線集區，而且沒有預設值，在共用連接的連接屬性設回預設值，並宣告相符項目。 如果沒有預設值，共用的連接不會視為相符項目。  
  
     如果連接屬性已經設定了應用程式，但尚未設定連接集區中，在集區上的連接屬性的變更時的應用程式，並宣告相符項目。  
  
     如果連接屬性已經設定了應用程式，且也已設定連線集區中，但值不同時，會使用應用程式的連接屬性的值，並宣告相符項目。  
  
-   如果驅動程式特有的連接屬性的值不相同，而且 SQL_ATTR_CP_MATCH 設 SQL_CP_STRICT_MATCH，不會使用集區中的連接。  
  
 當應用程式呼叫**SQLDisconnect**中斷連線，連線會傳回連接集區，也有可重複使用。  
  
### <a name="optimizing-connection-pooling-performance"></a>最佳化連線集區效能  
 當涉及分散式的交易時，就可以將連接共用所使用的效能最佳化**SQL_DTC_TRANSITION_COST**，這是 SQLUINTEGER 位元遮罩。 參考的轉換會連接屬性會從 0 的值為非零，SQL_ATTR_ENLIST_IN_DTC 的轉換，反之亦然。 這是從連線未編列在分散式交易編列在分散式交易中，反之亦然。 取決於驅動程式如何實作登錄 （設定連接屬性 SQL_ATTR_ENLIST_IN_DTC），這些轉換可能很昂貴，因此應避免為了達到最佳效能。  
  
 驅動程式所傳回的值會包含下列的位元的任何組合：  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**，當設定，表示非零值轉換為零會比從非零值轉換到另一個非零的值 （登錄在其下一個交易中的先前已登錄的連線）。  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**，當設定，表示零的零轉換的費用會比使用其 SQL_ATTR_ENLIST_IN_DTC 屬性已經設定為零的連線。  
  
 沒有與連接使用方式的權衡取捨的效能。 如果驅動程式會指出一或多個這些轉換會耗費資源，驅動程式管理員連接共用器會回應此集區中保留更多連線。 會用於非交易式，偏好使用的部分連線集區中，而有些則適合異動使用。 不過，如果驅動程式會指出這些轉換不昂貴，較少的連線可用，或許交替非交易式和交易式的使用。  
  
 不支援 SQL_ATTR_ENLIST_IN_DTC 的驅動程式不需要支援 SQL_DTC_TRANSITION_COST。 支援 SQL_ATTR_ENLIST_IN_DTC，但不是 SQL_DTC_TRANSITION_COST 的驅動程式，它會假設，轉換不是高成本，因為如果驅動程式會傳回此值為 0 （沒有位元集）。  
  
 雖然 SQL_DTC_TRANSITION_COST 引進在 ODBC 3.5 中，ODBC 2。*x*驅動程式也可以支援它因為驅動程式管理員會查詢此驅動程式版本不限的資訊。  
  
### <a name="code-example"></a>程式碼範例  
 在下列範例中，應用程式配置環境和連接控制代碼。 然後，它會連接到與使用者識別碼 JohnS SalesOrders 資料來源 」 和 「 密碼 Sesame 並處理資料。 當它完成處理資料時，它會從資料來源中斷連線的連線，並釋放控制代碼。  
  
```  
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
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|配置控制代碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|探索及列舉值，才能連接到資料來源|[SQLBrowseConnect 函式](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|從資料來源中斷連接|[SQLDisconnect 函式](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|連接到資料來源使用的連接字串或對話方塊方塊|[SQLDriverConnect 函式](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|傳回連接屬性的設定|[SQLGetConnectAttr 函式](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函式](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
