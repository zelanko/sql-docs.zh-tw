---
description: SQLConnect 函數
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 714bc6f69a72609ee266effff71f1898d62ec7d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461200"
---
# <a name="sqlconnect-function"></a>SQLConnect 函數
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLConnect** 會建立與驅動程式和資料來源的連接。 連接控制碼會參考與資料來源之連接相關的所有資訊的儲存，包括狀態、交易狀態和錯誤資訊。  
  
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
 *ConnectionHandle*  
 [輸入] 連線控制代碼。  
  
 *ServerName*  
 輸出資料來源名稱。 資料可能位於與程式相同的電腦上，或位於網路上某處的另一部電腦上。 如需應用程式如何選擇資料來源的詳細資訊，請參閱 [選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 *NameLength1*  
 輸出**ServerName* 的長度（以字元為單位）。  
  
 *使用者名稱*  
 輸出使用者識別碼。  
  
 *NameLength2*  
 輸出**UserName* 的長度（以字元為單位）。  
  
 *驗證*  
 輸出驗證字串 (通常是) 密碼。  
  
 *NameLength3*  
 輸出**驗證* 的長度（以字元為單位）。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLConnect**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_DBC）和*ConnectionHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLConnect** 通常會傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01S02|選項值已變更|驅動程式不支援在**SQLSetConnectAttr**中指定的*ValuePtr*引數值，並取代類似的值。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|08001|用戶端無法建立連接|驅動程式無法建立與資料來源的連接。|  
|08002|使用中的連接名稱| (DM) 指定的 *ConnectionHandle* 已經用來建立與資料來源的連接，而且連接仍然開啟或使用者正在流覽連接。|  
|08004|伺服器拒絕連接|資料來源因為執行定義的原因而拒絕建立連接。|  
|08S01|通訊連結失敗|在函數完成處理之前，驅動程式與驅動程式嘗試連接的資料來源之間的通訊連結失敗。|  
|28000|不正確授權規格|為引數使用者 *名稱* 指定的值或為引數 *驗證* 指定的值違反了資料來源所定義的限制。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤| (DM) 驅動程式管理員無法配置支援執行或完成函式所需的記憶體。|  
|HY008|已取消作業|*ConnectionHandle*已啟用非同步處理。 已**呼叫 SQLConnect**函式，在它完成執行之前，已在*ConnectionHandle*上呼叫[SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)函式，然後在*ConnectionHandle*上再次呼叫**SQLConnect**函數。<br /><br /> 或者，呼叫**SQLConnect**函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒在*ConnectionHandle*上呼叫**SQLCancelHandle** 。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式 (不是針對 *ConnectionHandle* 呼叫這個) ，而且在呼叫此函式時仍在執行。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY090|不正確字串或緩衝區長度| (DM) 引數 *NameLength1*、 *NameLength2*或 *NameLength3* 指定的值小於0，但不等於 SQL_NTS。<br /><br />  (DM) 引數 *NameLength1* 指定的值超過資料來源名稱的最大長度。|  
|HYT00|已超過逾時的設定|查詢超時時間已在與資料來源的連接完成之前過期。 Timeout 期限是透過 **SQLSetConnectAttr**、SQL_ATTR_LOGIN_TIMEOUT 設定。|  
|HY114|驅動程式不支援連接層級的非同步函式執行| (DM) 應用程式在進行連接之前，已啟用連接控制碼上的非同步作業。 不過，驅動程式不支援在連接控制碼上進行非同步作業。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 資料來源名稱所指定的驅動程式不支援此函數。|  
|IM002|找不到資料來源，且未指定預設驅動程式| (DM) 在系統資訊中找不到引數 *ServerName* 中指定的資料來源名稱，也沒有預設的驅動程式規格。|  
|IM003|無法連接指定的驅動程式| (DM) 找不到系統資訊中的資料來源規格中所列的驅動程式，或由於某些其他原因而無法連接到該驅動程式。|  
|IM004|SQL_HANDLE_ENV 上的驅動程式 SQLAllocHandle 失敗|在 **SQLConnect**期間 (DM) ，驅動程式管理員會呼叫驅動程式的 **SQLAllocHandle** 函式，並使用 *HandleType* 的 SQL_HANDLE_ENV，而驅動程式會傳回錯誤。|  
|IM005|SQL_HANDLE_DBC 上的驅動程式 SQLAllocHandle 失敗|在 **SQLConnect**期間 (DM) ，驅動程式管理員會呼叫驅動程式的 **SQLAllocHandle** 函式，並使用 *HandleType* 的 SQL_HANDLE_DBC，而驅動程式會傳回錯誤。|  
|IM006|驅動程式的 SQLSetConnectAttr 失敗|在 **SQLConnect**期間，驅動程式管理員會呼叫驅動程式的 **SQLSetConnectAttr** 函式，而驅動程式會傳回錯誤。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|IM009|無法連接到轉譯 DLL|驅動程式無法連接到針對資料來源指定的轉譯 DLL。|  
|IM010|資料來源名稱太長| (DM) * \* ServerName*的長度超過 SQL_MAX_DSN_LENGTH 個字元。|  
|IM014|指定的 DSN 包含驅動程式和應用程式之間的架構不相符| (DM) 32 位應用程式使用連接到64位驅動程式的 DSN;反之亦然。|  
|IM015|SQL_HANDLE_DBC_INFO_HANDLE 上的驅動程式 SQLConnect 失敗|如果驅動程式傳回 SQL_ERROR，驅動程式管理員會將 SQL_ERROR 傳回給應用程式，且連接將會失敗。<br /><br /> 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊，請參閱 [在 ODBC 驅動程式中開發連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，而且如果啟用了通知模式，則必須在控制碼上呼叫 **SQLCompleteAsync** ，以進行後置處理，並完成作業。|  
|S1118|驅動程式不支援非同步通知|當驅動程式不支援非同步通知時，您無法設定 SQL_ATTR_ASYNC_DBC_EVENT 或 SQL_ATTR_ASYNC_DBC_RETCODE_PTR。|  
  
## <a name="comments"></a>註解  
 如需應用程式為何使用 **SQLConnect**的相關資訊，請參閱 [使用 SQLConnect 連接](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)。  
  
 驅動程式管理員不會連接到驅動程式，直到應用程式呼叫函式 (**SQLConnect**、 **SQLDriverConnect**或 **SQLBrowseConnect**) 連接到驅動程式為止。 在那之前，驅動程式管理員會使用它自己的控點，並管理連接資訊。 當應用程式呼叫連接函式時，驅動程式管理員會檢查驅動程式目前是否已針對指定的 *ConnectionHandle*連接到：  
  
-   如果驅動程式未連接到，驅動程式管理員會連線到驅動程式，並使用*HandleType*的 SQL_HANDLE_ENV、 **SQLAllocHandle**與 HandleType SQL_HANDLE_DBC 的*HandleType* 、 **SQLSetConnectAttr** (（如果應用程式指定了任何連接屬性) ，以及驅動程式中的連接函數）來呼叫**SQLAllocHandle** 。 如果驅動程式傳回**SQLSetConnectAttr**的錯誤，驅動程式管理員會傳回 SQLSTATE IM006 (驅動程式的**SQLSetConnectOption**失敗) 和 SQL_SUCCESS_WITH_INFO。 如需詳細資訊，請參閱 [連接到資料來源或驅動程式](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)。  
  
-   如果指定的驅動程式已連接到 *ConnectionHandle*上，驅動程式管理員只會呼叫驅動程式中的連接功能。 在此情況下，驅動程式必須確定 *ConnectionHandle* 的所有連接屬性都維持其目前的設定。  
  
-   如果有不同的驅動程式連線到，驅動程式管理員會以 SQL_HANDLE_DBC 的*HandleType*呼叫**SQLFreeHandle** ，然後，如果在該環境中沒有其他驅動程式連線到，它就會在連接的驅動程式中呼叫具有*HandleType* SQL_HANDLE_ENV 的**SQLFreeHandle** ，然後中斷該驅動程式的連線。 然後，它會執行與驅動程式未連接時相同的作業。  
  
 然後，驅動程式會配置控制碼並初始化本身。  
  
 當應用程式呼叫 **SQLDisconnect**時，驅動程式管理員會在驅動程式中呼叫 **SQLDisconnect** 。 但是，它不會中斷連接驅動程式。 這可將驅動程式保留在記憶體中，以供重複連接和中斷資料來源的應用程式使用。 當應用程式以 SQL_HANDLE_DBC 的*HandleType*呼叫**SQLFreeHandle**時，驅動程式管理員會以 SQL_HANDLE_DBC *HandleType*來呼叫**SQLFreeHandle** ，然後在驅動程式**中使用** *SQLFreeHandle SQL_HANDLE_ENV HandleType* ，然後將驅動程式中斷連線。  
  
 ODBC 應用程式可以建立一個以上的連接。  
  
## <a name="driver-manager-guidelines"></a>驅動程式管理員指導方針  
 **ServerName* 的內容會影響驅動程式管理員和驅動程式如何一起運作，以建立與資料來源的連接。  
  
-   如果 \* *ServerName*包含有效的資料來源名稱，驅動程式管理員會在系統資訊中尋找對應的資料來源規格，並連接到相關聯的驅動程式。 驅動程式管理員會將每個 **SQLConnect** 引數傳遞至驅動程式。  
  
-   如果找不到資料來源名稱，或 *ServerName* 是 null 指標，驅動程式管理員會尋找預設的資料來源規格，並連接到相關聯的驅動程式。 驅動程式管理員*會將使用者名稱和**驗證*引數原封不動地傳遞至驅動程式，並將*ServerName*引數的「預設值」傳遞給驅動程式。  
  
-   如果 *ServerName* 引數是 "default"，驅動程式管理員會尋找預設的資料來源規格，並連接到相關聯的驅動程式。 驅動程式管理員會將每個 **SQLConnect** 引數傳遞至驅動程式。  
  
-   如果找不到資料來源名稱，或 *ServerName* 為 null 指標，且預設的資料來源規格不存在，驅動程式管理員會傳回 SQL_ERROR，其中包含 SQLSTATE IM002 (找不到資料來源名稱，且) 未指定預設驅動程式。  
  
 驅動程式管理員連接到之後，驅動程式可以在系統資訊中找到其對應的資料來源規格，並使用規格中的驅動程式特定資訊來完成其必要的連接資訊。  
  
 如果在資料來源的系統資訊中指定了預設的翻譯程式庫，驅動程式就會連接到它。 藉由呼叫 **SQLSetConnectAttr** 與 SQL_ATTR_TRANSLATE_LIB 屬性，可以連接不同的翻譯程式庫。 您可以使用 SQL_ATTR_TRANSLATE_OPTION 屬性呼叫 **SQLSetConnectAttr** 來指定翻譯選項。  
  
 如果驅動程式支援 **SQLConnect**，則驅動程式系統資訊的驅動程式關鍵字區段必須包含 **ConnectFunctions** 關鍵字，並將第一個字元設定為 "Y"。  
  
### <a name="connection-pooling"></a>連接共用  
 連接共用可讓應用程式重複使用已經建立的連接。 當連接共用已啟用並呼叫 **SQLConnect** 時，驅動程式管理員會嘗試使用屬於連接共用的環境中連接集區一部分的連接來建立連接。 此環境是共用環境，可供所有使用集區中連接的應用程式使用。  
  
 連接共用會在配置環境之前啟用，方法是呼叫 **SQLSetEnvAttr** ，將 SQL_ATTR_CONNECTION_POOLING 設定為 SQL_CP_ONE_PER_DRIVER (指定每個驅動程式最多一個集區) 或 SQL_CP_ONE_PER_HENV (指定每個環境) 最多一個集區。 在此情況下， **SQLSetEnvAttr**會呼叫*EnvironmentHandle*設為 null 的，讓屬性成為進程層級的屬性。 如果 SQL_ATTR_CONNECTION_POOLING 設定為 SQL_CP_OFF，則會停用連接共用。  
  
 啟用連接共用之後，會呼叫具有 SQL_HANDLE_ENV *HandleType*的**SQLAllocHandle**來配置環境。 此呼叫所配置的環境是共用的環境，因為已啟用連接共用。 不過，在呼叫具有 SQL_HANDLE_DBC *HandleType*的**SQLAllocHandle**之前，將不會決定要使用的環境。  
  
 會呼叫具有 SQL_HANDLE_DBC *HandleType*的**SQLAllocHandle** ，以配置連接。 驅動程式管理員會嘗試尋找符合應用程式所設定之環境屬性的現有共用環境。 如果沒有這樣的環境，則會建立一個作為隱含 *共用環境*。 如果找到相符的共用環境，環境控制碼會傳回至應用程式，而且其參考計數會遞增。  
  
 不過，在呼叫 **SQLConnect** 之前，將不會決定要使用的連接。 屆時，驅動程式管理員會嘗試在連接集區中尋找符合應用程式所要求準則的現有連接。 這些準則包括呼叫 **SQLConnect** 時要求的連接選項 (*伺服器名稱*、使用者 *名稱*和 *驗證* 關鍵字的值) 以及自 **SQLAllocHandle** 加上 *HandleType* 為 SQL_HANDLE_DBC 的任何連接屬性設定。 驅動程式管理員會根據集區中連接的對應連接關鍵字和屬性來檢查這些準則。 如果找到相符的，則會使用集區中的連接。 如果找不到相符項，則會建立新的連接。  
  
 如果 SQL_ATTR_CP_MATCH 環境屬性設定為 SQL_CP_STRICT_MATCH，則比對要使用的集區中的連接必須是完全相符的。 如果 SQL_ATTR_CP_MATCH 的環境屬性設定為 SQL_CP_RELAXED_MATCH，則呼叫 **SQLConnect** 的連接選項必須相符，但並非所有的連接屬性都必須相符。  
  
 在呼叫 **SQLConnect** 之前，應用程式所設定的連接屬性不符合集區中連接的連接屬性時，會套用下列規則：  
  
-   如果必須在連接完成之前設定連接屬性：  
  
     如果 SQL_CP_STRICT_MATCH SQL_ATTR_CP_MATCH，則共用連接中的 SQL_ATTR_PACKET_SIZE 必須與應用程式所設定的屬性相同。 如果 SQL_CP_RELAXED_MATCH，SQL_ATTR_PACKET_SIZE 的值可能會不同。  
  
     SQL_ATTR_LOGIN_VALUE 的值不會影響相符項。  
  
-   如果連接屬性可以在建立連接之前或之後設定：  
  
     如果連接屬性尚未由應用程式設定，但在集區中已設定連接，而且有預設值，則會將共用連接中的連接屬性設定回預設值，並宣告相符的結果。 如果沒有預設值，則不會將共用的連接視為相符。  
  
     如果連接屬性已由應用程式設定，但未在集區的連接上設定，則集區上的連接屬性會變更為應用程式所設定的，而且會宣告相符的屬性。  
  
     如果連接屬性已由應用程式設定，而且也已在集區中的連接上設定，但值不同，則會使用應用程式的連接屬性值並宣告相符的結果。  
  
-   如果驅動程式特定的連接屬性值不相同，且 SQL_ATTR_CP_MATCH 設定為 SQL_CP_STRICT_MATCH，則不會使用集區中的連接。  
  
 當應用程式呼叫 **SQLDisconnect** 中斷連線時，連接會傳回連接集區，而且可供重複使用。  
  
### <a name="optimizing-connection-pooling-performance"></a>優化連接共用效能  
 牽涉到分散式交易時，您可以使用 **SQL_DTC_TRANSITION_COST**（也就是 SQLUINTEGER 位元遮罩）來將連接共用效能優化。 參考的轉換是連接屬性的轉換 SQL_ATTR_ENLIST_IN_DTC 從值0到非零，反之亦然。 這是從未登錄在分散式交易中，並在分散式交易中登記的連接，反之亦然。 根據驅動程式如何實行登記 (設定 SQL_ATTR_ENLIST_IN_DTC) 的連接屬性，這些轉換可能會很耗費資源，因此為了獲得最佳效能，應予以避免。  
  
 驅動程式所傳回的值包含下列位的任意組合：  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**，當設定時，表示零到非零的轉換比從非零到另一個非零值的轉換更昂貴， (在下一個交易) 登記先前登錄的連接。  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**，當設定時，表示非零到零的轉換比使用 SQL_ATTR_ENLIST_IN_DTC 屬性已設定為零的連接高得多。  
  
 效能與連接使用方式的取捨相同。 如果驅動程式指出其中一或多個轉換的成本很高，驅動程式管理員的連接共用器會藉由在集區中保留更多連接來回應此情況。 集區中的某些連接偏好非交易式使用，而有些則是交易式使用的偏好。 但是，如果驅動程式指出這些轉換不是昂貴的，則可以使用較少的連接，可能會在非交易式和交易式使用之間交替。  
  
 不支援 SQL_ATTR_ENLIST_IN_DTC 的驅動程式不需要支援 SQL_DTC_TRANSITION_COST。 針對支援 SQL_ATTR_ENLIST_IN_DTC 但未 SQL_DTC_TRANSITION_COST 的驅動程式，會假設轉換的成本不高，如同驅動程式傳回 0 (未針對此值設定) 。  
  
 雖然 SQL_DTC_TRANSITION_COST 是在 ODBC 3.5 中引進的，但是 ODBC 2。*x* 驅動程式也可以支援它，因為驅動程式管理員會查詢這項資訊，而不論驅動程式版本為何。  
  
### <a name="code-example"></a>程式碼範例  
 在下列範例中，應用程式會配置環境和連接控制碼。 然後，它會使用使用者識別碼聖約翰和密碼 Sesame 和處理資料，連接到 SalesOrders 資料來源。 完成資料的處理之後，就會中斷與資料來源的連線，並釋放控制碼。  
  
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
|配置控制碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|探索和列舉連接到資料來源所需的值|[SQLBrowseConnect 函式](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|中斷與資料來源的連接|[SQLDisconnect 函式](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|使用連接字串或對話方塊連接到資料來源|[SQLDriverConnect 函式](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|傳回連接屬性的設定|[SQLGetConnectAttr 函數](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
