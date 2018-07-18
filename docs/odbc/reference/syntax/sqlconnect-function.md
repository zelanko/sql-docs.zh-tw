---
title: SQLConnect 函數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c125516f2cc46c1391f74e016b3d4e9487c8dc57
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32922743"
---
# <a name="sqlconnect-function"></a>SQLConnect 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ISO 92  
  
 **摘要**  
 **SQLConnect**建立驅動程式和資料來源的連接。 連接控制代碼會參考儲存體的所有資訊連接到資料來源，包括狀態、 交易狀態及資訊時發生錯誤。  
  
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
 [輸入]資料來源名稱。 資料可能會位於與程式，相同的電腦或網路上的某個地方的另一部電腦上。 如需應用程式如何選擇資料來源資訊，請參閱[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
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
 當**SQLConnect**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType* SQL_ 的HANDLE_DBC 和*處理*的*ConnectionHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLConnect** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S02|選項值已變更|驅動程式不支援指定的值*ValuePtr*引數中的**SQLSetConnectAttr**置換相似的值。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08001|無法建立連線的用戶端|驅動程式無法建立與資料來源的連接。|  
|08002|使用中的連接名稱|(DM) 指定*ConnectionHandle*必須已經用來建立與資料來源的連線，而連接是仍保持開啟，或使用者已瀏覽的連接。|  
|08004|伺服器拒絕連線|資料來源的拒絕連線的建立實作定義理由。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和資料來源的驅動程式在嘗試連線之間的通訊連結失敗。|  
|28000|無效的授權規格|指定的引數的值*UserName*或是指定的引數的值*驗證*違反了資料來源所定義的限制。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|(DM) 驅動程式管理員無法配置記憶體，才能支援執行或完成的函式。|  
|HY008|已取消操作|非同步處理已啟用*ConnectionHandle*。 **SQLConnect**呼叫函式，和之前已完成執行， [SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上呼叫*ConnectionHandle*，並接著**SQLConnect**上一次呼叫函式*ConnectionHandle*。<br /><br /> 或者， **SQLConnect**呼叫函式，和之前已完成執行， **SQLCancelHandle**上呼叫*ConnectionHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|以非同步方式執行的函式 （不是這一個） 已呼叫 (DM) *ConnectionHandle*和還在執行時呼叫此函式。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY090|字串或緩衝區長度無效|(DM) 引數指定的值*NameLength1*， *NameLength2*，或*NameLength3*小於 0，但不是等於 SQL_NTS。<br /><br /> (DM) 引數指定的值*NameLength1*超過資料來源名稱的最大長度。|  
|HYT00|已超過逾時的設定|查詢逾時期限過期之前完成資料來源的連接。 逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_LOGIN_TIMEOUT。|  
|HY114|驅動程式不支援連接層級的非同步函式執行|(DM) 應用程式啟用連接控制代碼上非同步作業之前建立的連接。 不過，驅動程式不支援連接控制代碼上的非同步作業。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 資料來源名稱所指定的驅動程式不支援此函式。|  
|IM002|找不到資料來源並指定預設驅動程式|(DM) 的資料來源的引數中指定名稱*ServerName*找不到在系統資訊，或是否有預設的驅動程式規格。|  
|IM003|指定的驅動程式不會連接到|(DM) 資料中列出的驅動程式在 系統資訊的來源規格找不到或無法連線至其他原因。|  
|IM004|驅動程式的 SQLAllocHandle SQL_HANDLE_ENV 上失敗|(DM) 期間**SQLConnect**，稱為 「 驅動程式的驅動程式管理員**SQLAllocHandle**函式與*HandleType* SQL_HANDLE_ENV 和驅動程式傳回錯誤。|  
|IM005|利用 SQL_HANDLE_DBC 上的驅動程式的 SQLAllocHandle 失敗|(DM) 期間**SQLConnect**，稱為 「 驅動程式的驅動程式管理員**SQLAllocHandle**函式與*HandleType*利用 SQL_HANDLE_DBC 的驅動程式傳回錯誤。|  
|IM006|驅動程式的 SQLSetConnectAttr 無法|期間**SQLConnect**，稱為 「 驅動程式的驅動程式管理員**SQLSetConnectAttr**函式和驅動程式傳回錯誤。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|IM009|無法連線至轉譯 DLL|驅動程式無法連接到轉譯的資料來源所指定的 DLL。|  
|IM010|資料來源名稱太長|(DM)  *\*ServerName*超過 SQL_MAX_DSN_LENGTH 字元。|  
|IM014|指定的資料來源名稱包含驅動程式和應用程式之間的架構不相符|(DM) 32 位元應用程式使用的 DSN 連接至 64 位元驅動程式。反之亦然。|  
|IM015|驅動程式的 SQLConnect SQL_HANDLE_DBC_INFO_HANDLE 上失敗|如果驅動程式會傳回 SQL_ERROR，驅動程式管理員將會傳回 SQL_ERROR，應用程式，則連接會失敗。<br /><br /> 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊，請參閱[開發 ODBC 驅動程式中的連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。|  
|IM017|中的非同步通知模式已停用輪詢|每當通知模型使用時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，且如果已啟用通知模式， **SQLCompleteAsync**必須在後續處理作業，並完成此作業的控制代碼上呼叫。|  
|S1118|驅動程式不支援非同步通知|當驅動程式不支援非同步通知時，您無法對 SQL_ATTR_ASYNC_DBC_EVENT 或 SQL_ATTR_ASYNC_DBC_RETCODE_PTR 進行設定。|  
  
## <a name="comments"></a>註解  
 應用程式所使用之原因的資訊如**SQLConnect**，請參閱[使用 SQLConnect 連接](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)。  
  
 驅動程式管理員不會連線到驅動程式的應用程式呼叫函式之前 (**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**) 連接到驅動程式。 該時間點之前，驅動程式管理員會與它自己的控點，並管理連接資訊。 當應用程式呼叫連線函式時，驅動程式管理員會檢查驅動程式目前是否已連接至指定*ConnectionHandle*:  
  
-   如果驅動程式未連線到，驅動程式管理員會連接到驅動程式，然後呼叫**SQLAllocHandle**與*HandleType* SQL_HANDLE_ENV 的**SQLAllocHandle**與*HandleType*利用 SQL_HANDLE_DBC 的**SQLSetConnectAttr** （如果應用程式指定任何連接屬性），以及驅動程式中的連線函式。 驅動程式管理員會傳回 SQLSTATE IM006 (驅動程式的**SQLSetConnectOption**失敗) 和連接函式，如果驅動程式傳回的錯誤 SQL_SUCCESS_WITH_INFO **SQLSetConnectAttr**。 如需詳細資訊，請參閱[連接到資料來源或驅動程式](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)。  
  
-   如果指定的驅動程式已經連接為開啟*ConnectionHandle*，驅動程式管理員驅動程式中呼叫連線函式。 在此情況下，驅動程式必須確定所有的連接屬性的*ConnectionHandle*維護其目前的設定。  
  
-   如果不同的驅動程式連接到，驅動程式管理員會呼叫**SQLFreeHandle**與*HandleType*的利用 SQL_HANDLE_DBC，然後，如果沒有其他驅動程式連接到該環境中，呼叫**SQLFreeHandle**與*HandleType*已連線的驅動程式中利用 SQL_HANDLE_ENV 的然後中斷連接該驅動程式。 然後，它會執行為驅動程式時未連線到相同的作業。  
  
 驅動程式再配置控制代碼，並初始化本身。  
  
 當應用程式呼叫**SQLDisconnect**，驅動程式管理員呼叫**SQLDisconnect**驅動程式中。 不過，它不會中斷驅動程式。 如此一來，重複連接及中斷資料來源的應用程式所需記憶體中驅動程式。 當應用程式呼叫**SQLFreeHandle**與*HandleType*利用 SQL_HANDLE_DBC 的驅動程式管理員呼叫**SQLFreeHandle**與*HandleType*利用 SQL_HANDLE_DBC 的然後**SQLFreeHandle**與*HandleType*中驅動程式，利用 SQL_HANDLE_ENV 的然後中斷連接，驅動程式。  
  
 ODBC 應用程式可以建立一個以上的連線。  
  
## <a name="driver-manager-guidelines"></a>驅動程式管理員指導方針  
 內容 **ServerName*會影響如何驅動程式管理員和驅動程式一起運作以建立資料來源的連接。  
  
-   如果\* *ServerName*包含有效的資料來源名稱，驅動程式管理員在系統資訊中找出對應的資料來源規格，並連接到相關聯的驅動程式。 驅動程式管理員會將傳遞每個**SQLConnect**驅動程式的引數。  
  
-   如果找不到資料來源名稱或*ServerName*為 null 指標，驅動程式管理員找出預設資料來源的規格，並連接到相關聯的驅動程式。 驅動程式管理員會將傳遞至驅動程式*UserName*和*驗證*未經修改的引數和 「 預設 」 的*ServerName*引數。  
  
-   如果*ServerName*引數為"DEFAULT"，驅動程式管理員找出預設資料來源的規格，並連接到相關聯的驅動程式。 驅動程式管理員會將傳遞每個**SQLConnect**驅動程式的引數。  
  
-   如果找不到資料來源名稱或*ServerName*是 null 指標，以及預設的資料來源的規格不存在，驅動程式管理員會傳回 sql_error，其中包含 SQLSTATE IM002 （資料來源找不到名稱，沒有預設值指定驅動程式）。  
  
 它連接到驅動程式管理員之後，驅動程式就可以找到其對應的資料來源規格系統資訊，並使用規格的驅動程式特定資訊來完成其一組必要的連接資訊。  
  
 如果在資料來源的系統資訊中指定預設轉譯程式庫，則驅動程式會連接到它。 不同轉譯程式庫可以藉由呼叫連線到**SQLSetConnectAttr** SQL_ATTR_TRANSLATE_LIB 屬性。 轉譯選項可以指定藉由呼叫**SQLSetConnectAttr** SQL_ATTR_TRANSLATE_OPTION 屬性。  
  
 如果驅動程式支援**SQLConnect**，驅動程式的系統資訊的驅動程式關鍵字區段必須包含**ConnectFunctions**關鍵字的第一個字元設為"Y"。  
  
### <a name="connection-pooling"></a>連接共用  
 連接共用可讓應用程式重複使用已建立的連線。 當啟用連接共用和**SQLConnect**呼叫時，驅動程式管理員嘗試進行連接使用屬於指定給連接共用的環境中的連接集區的連接。 這個環境是共用的環境中所使用的連接集區中的所有應用程式使用。  
  
 會啟用連接共用的環境藉由呼叫配置之前**SQLSetEnvAttr**設 SQL_ATTR_CONNECTION_POOLING SQL_CP_ONE_PER_DRIVER （可指定每個驅動程式的一個集區的最大值） 或 SQL_CP_ONE_PER_HENV（指定每個環境的一個集區的最大值）。 **SQLSetEnvAttr**在此情況下呼叫*EnvironmentHandle*設為 null，讓屬性程序層級屬性。 如果 SQL_ATTR_CONNECTION_POOLING 設 SQL_CP_OFF，已停用連接共用。  
  
 啟用連接共用之後， **SQLAllocHandle**與*HandleType*利用 SQL_HANDLE_ENV 的呼叫來配置環境。 這個呼叫所配置的環境是在共用的環境，因為已啟用連接共用。 不過，將使用的環境不會決定直到**SQLAllocHandle**與*HandleType*利用 SQL_HANDLE_DBC 的呼叫。  
  
 **SQLAllocHandle**與*HandleType*利用 SQL_HANDLE_DBC 的呼叫來配置連接。 驅動程式管理員會嘗試尋找現有的共用的環境符合應用程式所設定的環境屬性。 如果沒有這類環境存在，則會建立為隱含*共用的環境*。 如果找到相符的共用的環境，則環境控制代碼傳回至應用程式和其參考計數會遞增。  
  
 不過，如果將使用的連接不決定直到**SQLConnect**呼叫。 此時，驅動程式管理員會嘗試尋找符合準則的應用程式所要求之連線集區中現有的連接。 這類準則包括要求呼叫中的連接選項**SQLConnect** (值*ServerName*， *UserName*，和*驗證*關鍵字) 和任何連接屬性組，因為**SQLAllocHandle**與*HandleType*利用 SQL_HANDLE_DBC 的被呼叫。 驅動程式管理員會檢查這些準則的對應連接關鍵字和連接集區中的屬性。 如果找到相符項目，則會使用連接集區中。 如果找到相符項目，就會建立新的連接。  
  
 如果 SQL_ATTR_CP_MATCH 環境屬性設定為 SQL_CP_STRICT_MATCH，比對必須是完全使用集區中的連接。 如果 SQL_ATTR_CP_MATCH 環境屬性設定為 SQL_CP_RELAXED_MATCH，連接選項的呼叫中**SQLConnect**必須符合，但並非所有連接屬性必須相符。  
  
 下列規則會套用時連線屬性所設定的應用程式之前**SQLConnect**呼叫時，不符合連接集區中的 「 連接 」 屬性：  
  
-   如果之前已連線，則必須設定連接屬性：  
  
     如果 SQL_ATTR_CP_MATCH SQL_CP_STRICT_MATCH，SQL_ATTR_PACKET_SIZE 中共用的連接必須是相同的應用程式所設定的屬性。 如果 SQL_CP_RELAXED_MATCH，SQL_ATTR_PACKET_SIZE 的值可能會不同。  
  
     SQL_ATTR_LOGIN_VALUE 的值不會影響比對。  
  
-   如果之前或在建立連接之後，可以設定連接屬性：  
  
     如果連接屬性尚未設定應用程式，但已在資料庫中，設定在連接上，而且沒有預設值，共用連接的 「 連接 」 屬性設回預設值，並宣告相符項目。 如果沒有預設值，共用的連接不視為相符項目。  
  
     如果連接屬性已經設定了應用程式，但尚未設定連接集區中，應用程式集區上的 「 連接 」 屬性變更到該集合，並宣告相符項目。  
  
     如果連接屬性已經設定了應用程式，並也已在設定連接集區中，但值不相同，會使用應用程式的連接屬性的值宣告，且相符項目。  
  
-   如果驅動程式特有的連接屬性的值並不相同，因此 SQL_ATTR_CP_MATCH 設 SQL_CP_STRICT_MATCH，不使用連接集區中。  
  
 當應用程式呼叫**SQLDisconnect**中斷連接，連接傳回連接集區，供重複使用。  
  
### <a name="optimizing-connection-pooling-performance"></a>最佳化連線集區效能  
 當涉及分散式的交易時，便可將連接共用所使用的效能最佳化**SQL_DTC_TRANSITION_COST**，這是 SQLUINTEGER 位元遮罩。 參考轉換是的連接屬性會從 0 的值為非零的 SQL_ATTR_ENLIST_IN_DTC，反之亦然。 這是從連線不在分散式異動中登記編列在分散式交易，反之亦然。 根據此驅動程式已實作方式編列 （設定連接屬性 SQL_ATTR_ENLIST_IN_DTC），這些轉換可能會耗費資源，並因此應避免為了達到最佳效能。  
  
 驅動程式所傳回的值包含下列的位元的任何組合：  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**，當設定時，表示轉換為非零，零費用會比從零到另一個則為非零值 （登記中其下一個交易的先前編列的連接） 的轉換。  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**，當設定，表示轉換為零的非零的費用會比使用其 SQL_ATTR_ENLIST_IN_DTC 屬性已設為零的連接。  
  
 沒有效能及連線使用量上取捨。 如果驅動程式會指出一或多個這些轉換是相當費時，驅動程式管理員連接共用器會回應此集區中保留更多的連線。 連接集區中有些非交易式使用的慣用發佈點，而有些是交易式使用的慣用發佈點。 不過，如果驅動程式會指出這些轉換不是相當費時，較少的連線可用，或許交替執行非交易式和交易式的使用。  
  
 不支援 SQL_ATTR_ENLIST_IN_DTC 的驅動程式不需要支援 SQL_DTC_TRANSITION_COST。 支援 SQL_ATTR_ENLIST_IN_DTC，但不是 SQL_DTC_TRANSITION_COST 的驅動程式，它會假設轉換不是高度耗費資源，因為驅動程式會傳回此值為 0 （未設定位元為單位）。  
  
 雖然 SQL_DTC_TRANSITION_COST 推出的 ODBC 3.5，ODBC 2。*x*驅動程式也可以支援它因為驅動程式管理員會查詢此驅動程式版本不限的資訊。  
  
### <a name="code-example"></a>程式碼範例  
 在下列範例中，應用程式配置環境和連接控制代碼。 然後，連接到與使用者識別碼 JohnS SalesOrders 資料來源和密碼的芝麻並處理資料。 當它完成處理資料時，它會中斷資料來源的連接，並釋放控制代碼。  
  
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
|探索和列舉值連接到資料來源所需|[SQLBrowseConnect 函式](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|從資料來源中斷連線|[SQLDisconnect 函式](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|連接到資料來源使用的連接字串或對話方塊方塊|[SQLDriverConnect 函式](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|傳回連接屬性的設定|[SQLGetConnectAttr 函式](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函式](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
