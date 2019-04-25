---
title: SQLAllocHandle 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLAllocHandle
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLAllocHandle
helpviewer_keywords:
- SQLAllocHandle function [ODBC]
ms.assetid: 6e7fe420-8cf4-4e72-8dad-212affaff317
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0a075b96e7a29cef4a10f034147732bf03f64b2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62761779"
---
# <a name="sqlallochandle-function"></a>SQLAllocHandle 函式
**合規性**  
 導入的版本：ODBC 3.0 版的標準合規性：ISO 92  
  
 **摘要**  
 **SQLAllocHandle**會配置環境、 連接、 陳述式或描述元控制代碼。  
  
> [!NOTE]  
>  此函式會配置控制代碼會取代 ODBC 2.0 函式的泛型函式**SQLAllocConnect**， **SQLAllocEnv**，並**SQLAllocStmt**。 若要允許呼叫的應用程式**SQLAllocHandle**才能使用 ODBC 2。*x*驅動程式，呼叫**Handletype**會對應至在驅動程式管理員**SQLAllocConnect**， **SQLAllocEnv**，或**SQLAllocStmt**視需要。 如需詳細資訊，請參閱 「 註解。 」 如需哪些驅動程式管理員的詳細資訊時 ODBC 3 會對應到此函式。*x*應用程式正在使用的 ODBC 2。*x*驅動程式，請參閱[對應取代函式應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 [輸入]所配置的控制代碼的型別**SQLAllocHandle**。 必須是下列值之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 只在驅動程式管理員和驅動程式會使用 SQL_HANDLE_DBC_INFO_TOKEN 控制代碼。 應用程式不應使用此控制代碼型別。 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊，請參閱[ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *InputHandle*  
 [輸入]輸入控制代碼，新的控制代碼會配置其內容中。 如果*HandleType*為 SQL_HANDLE_ENV，這是 SQL_NULL_HANDLE。 如果*HandleType*是利用 SQL_HANDLE_DBC，這必須是環境控制代碼，如果是利用 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC，它必須是在連接控制代碼。  
  
 *OutputHandlePtr*  
 [輸出]在其中傳回的控制代碼的新配置的資料結構的緩衝區指標。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_INVALID_HANDLE 或 SQL_ERROR。  
  
 如果配置環境控制代碼以外的控制代碼時**SQLAllocHandle**會傳回 SQL_ERROR，它會設定*OutputHandlePtr* SQL_NULL_HDBC、 SQL_NULL_HSTMT，或 SQL_NULL_HDESC，取決於值*HandleType*，除非您的輸出引數為 null 指標。 應用程式接著可以從與中的控制代碼相關聯的診斷資料結構取得其他資訊*InputHandle*引數。  
  
## <a name="environment-handle-allocation-errors"></a>環境控制代碼配置錯誤  
 在驅動程式管理員和每個驅動程式中，就會發生環境配置。 傳回的錯誤**SQLAllocHandle**具有*HandleType*利用 SQL_HANDLE_ENV 的取決於發生錯誤的層級。  
  
 如果驅動程式管理員無法配置記憶體 *\*OutputHandlePtr*當**SQLAllocHandle**具有*HandleType*利用 SQL_HANDLE_ENV 的呼叫，或應用程式提供了 null 指標*OutputHandlePtr*， **SQLAllocHandle**會傳回 SQL_ERROR。 驅動程式管理員會將 **OutputHandlePtr*至 SQL_NULL_HENV （除非應用程式提供了 null 指標，它會傳回 SQL_ERROR）。 沒有任何控制代碼與相關聯的其他診斷資訊。  
  
 驅動程式管理員不會呼叫的驅動程式層級環境控制代碼配置函式，直到應用程式會呼叫**SQLConnect**， **SQLBrowseConnect**，或**SQLDriverConnect**. 如果驅動程式層級中發生錯誤**SQLAllocHandle**函式，則驅動程式管理員層級**SQLConnect**， **SQLBrowseConnect**，或**SQLDriverConnect**函式會傳回 SQL_ERROR。 診斷資料結構包含 SQLSTATE IM004 (駕**SQLAllocHandle**失敗)。 在連接控制代碼會傳回錯誤。  
  
 如需驅動程式管理員和驅動程式之間的函式呼叫的流程的詳細資訊，請參閱[SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLAllocHandle**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**適當*HandleType*並*處理*的值設*InputHandle*。 可針對傳回 SQL_SUCCESS_WITH_INFO （但不是 SQL_ERROR） *OutputHandle*引數。 下表列出通常所傳回的 SQLSTATE 值**SQLAllocHandle** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08003|未開啟連接|(DM) *HandleType*引數為 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC，但藉由指定連接*InputHandle*引數未開啟。 必須已成功完成連線程序 （和連線必須開啟） 來配置陳述式或描述元的驅動程式處理。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**在 **MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式管理員 」 (DM) 無法配置指定的控制代碼的記憶體。<br /><br /> 驅動程式無法配置指定的控制代碼的記憶體。|  
|HY009|使用無效的 null 指標|(DM) *OutputHandlePtr*引數是 null 指標。|  
|HY010|函數順序錯誤|(DM) *HandleType*引數是利用 SQL_HANDLE_DBC，及**SQLSetEnvAttr** se nevolala 設定 SQL_ODBC_VERSION 環境屬性。<br /><br /> (DM) 的呼叫以非同步方式執行的函式**InputHandle**仍執行時並**SQLAllocHandle**呼叫函式與**HandleType**設定利用 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC。|  
|HY013|記憶體管理錯誤|*HandleType*引數已利用 SQL_HANDLE_DBC、 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC;，因為基礎記憶體的物件無法存取，可能是因為記憶體不足，無法處理函式呼叫條件。|  
|HY014|超出處理數目限制|所指定的驅動程式定義可獲配置的控制代碼類型的控制代碼的數目限制*HandleType*已達到引數。|  
|HY092|屬性/選項識別碼無效|(DM) *HandleType*引數不是：SQL_HANDLE_ENV、 利用 SQL_HANDLE_DBC、 SQL_HANDLE_STMT，還是 SQL_HANDLE_DESC。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|*HandleType*引數是 SQL_HANDLE_DESC，且驅動程式的 ODBC 2。*x*驅動程式。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) *HandleType*引數為 SQL_HANDLE_STMT，和驅動程式不是有效的 ODBC 驅動程式。<br /><br /> (DM) *HandleType*引數為 SQL_HANDLE_DESC，且驅動程式不支援配置描述項控制代碼。|  
  
## <a name="comments"></a>註解  
 **SQLAllocHandle**用以配置控制代碼的環境、 連接、 陳述式，以及描述元，如下列各節中所述。 如需控制代碼的一般資訊，請參閱[控制代碼](../../../odbc/reference/develop-app/handles.md)。  
  
 一次應用程式可以配置一個以上的環境、 連線或陳述式控制代碼，如果驅動程式支援多個配置。 在 ODBC 中，沒有限制定義的環境、 連接、 陳述式或一次可配置描述項控制代碼數目。 驅動程式可能會限制特定類型可以一次; 配置的控制代碼的數目如需詳細資訊，請參閱驅動程式文件。  
  
 如果應用程式會呼叫**SQLAllocHandle**具有 *\*OutputHandlePtr*設為環境、 連接、 陳述式或已經存在的描述項控制代碼，驅動程式會覆寫資訊與相關聯*處理*，除非您的應用程式使用連接共用 （請參閱 「 配置環境屬性的連線共用 」 本節稍後的）。 驅動程式管理員不會檢查以查看是否*處理*進入 *\*OutputHandlePtr*已在使用，也不會覆寫之前檢查先前的內容的控制代碼.  
  
> [!NOTE]  
>  它會呼叫不正確的 ODBC 應用程式開發**SQLAllocHandle**使用相同的應用程式變數定義的兩倍 *\*OutputHandlePtr*而不需呼叫**SQLFreeHandle**之前它重新配置釋放控制代碼。 覆寫 ODBC 控制代碼的方式可能會導致不一致的行為或部分的 ODBC 驅動程式的錯誤。  
  
 在作業系統上支援多個執行緒，應用程式可以在不同執行緒上使用相同的環境、 連接、 陳述式或描述元控制代碼。 驅動程式因此必須支援 「 安全、 多執行緒存取此資訊;其中一種方式達到這個目的，比方說，是使用重要區段或號誌。 如需有關執行緒的詳細資訊，請參閱[進行多執行緒處理](../../../odbc/reference/develop-app/multithreading.md)。  
  
 **SQLAllocHandle**未設定 SQL_ATTR_ODBC_VERSION 環境屬性時呼叫它來配置環境控制代碼; 必須由應用程式或 SQLSTATE HY010 設定環境屬性會 （函數順序錯誤）時，傳回**SQLAllocHandle**呼叫來配置連接控制代碼。  
  
 符合標準的應用程式，如**SQLAllocHandle**對應至**SQLAllocHandleStd**在編譯時期。 這兩個函數之間的差異在於**SQLAllocHandleStd**時呼叫，SQL_ATTR_ODBC_VERSION 環境屬性設定為 SQL_OV_ODBC3 *HandleType*引數設定為 SQL_HANDLE_ENV。 這是因為標準相容的應用程式永遠會 ODBC 3。*x*應用程式。 此外，標準不需要註冊應用程式版本。 這是這兩個函數; 唯一的差別否則，它們是完全相同。 **SQLAllocHandleStd**對應至**Handletype**內的驅動程式管理員。 因此，協力廠商驅動程式就不必實作**SQLAllocHandleStd**。  
  
 應該使用 ODBC 3.8 應用程式：  
  
-   **SQLAllocHandle 和不 SQLAllocHandleStd**配置環境控制代碼。  
  
-   **SQLSetEnvAttr**設 SQL_OV_ODBC3_80 SQL_ATTR_ODBC_VERSION 環境屬性。  
  
## <a name="allocating-an-environment-handle"></a>配置環境控制代碼  
 環境控制代碼提供有效的連接控制代碼和作用中連接控制代碼等全域資訊的存取權。 一般環境控制代碼的詳細資訊，請參閱[環境控制代碼](../../../odbc/reference/develop-app/environment-handles.md)。  
  
 若要要求環境控制代碼，應用程式會呼叫**SQLAllocHandle**具有*HandleType*利用 SQL_HANDLE_ENV 的和*InputHandle* SQL_NULL_HANDLE。 驅動程式會為會在傳回的相關聯的控制代碼的值與環境資訊來配置記憶體 *\*OutputHandlePtr*引數。 在應用程式通過 *\*OutputHandle*需要環境控制代碼引數的所有後續呼叫中的值。 如需詳細資訊，請參閱 <<c0> [ 配置環境處理](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 在驅動程式管理員環境控制代碼，如果已經有驅動程式的環境控制代碼，然後**SQLAllocHandle**具有*HandleType*該驅動程式中不會呼叫利用 SQL_HANDLE_ENV 的時建立的連線，只有**SQLAllocHandle**具有*HandleType*利用 SQL_HANDLE_DBC。 如果驅動程式的環境控制代碼不存在在驅動程式管理員環境控制代碼，呼叫與 SQL_HANDLE_ENV HandleType SQLAllocHandle 和 SQLAllocHandle HandleType 的利用 SQL_HANDLE_DBC 的驅動程式中時的第一個連線環境的控制代碼會連接到驅動程式。  
  
 驅動程式管理員會處理當**SQLAllocHandle**函式搭配*HandleType*的 SQL_HANDLE_ENV，它會檢查**追蹤**系統的 [ODBC] 區段中的關鍵字資訊。 如果它設定為 1，驅動程式管理員可讓目前的應用程式的追蹤。 如果設定追蹤旗標，已配置的第一個環境控制代碼，以及最後一個環境控制代碼已釋放時結束時，也會啟動追蹤。 如需詳細資訊，請參閱 <<c0> [ 設定資料來源](../../../odbc/reference/install/configuring-data-sources.md)。  
  
 在配置環境控制代碼之後, 應用程式必須呼叫**SQLSetEnvAttr**環境控制代碼設定 SQL_ATTR_ODBC_VERSION 環境屬性。 如果這個屬性未設定之前**SQLAllocHandle**呼叫來配置連接控制代碼的環境中，配置連接的呼叫將傳回 SQLSTATE HY010 （函數順序錯誤）。 如需詳細資訊，請參閱 <<c0> [ 宣告應用程式的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)。  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>配置的連接集區在共用環境  
 環境，可在單一處理序上的多個元件之間共用。 共用的環境可供多個元件在相同的時間。 當元件會使用共用的環境時，它可以使用共用的連接，讓它配置，並使用現有的連接，而不需要重新建立該連線。  
  
 應用程式配置共用的環境，可用來連接共用之前，必須呼叫**SQLSetEnvAttr**設 SQL_CP_ONE_PER_DRIVER 或 SQL_CP_ONE_PER_ SQL_ATTR_CONNECTION_POOLING 環境屬性HENV。 **SQLSetEnvAttr**在此情況下以呼叫*EnvironmentHandle*設為 null，讓處理序層級屬性的屬性。  
  
 啟用連接共用之後，應用程式會呼叫**SQLAllocHandle**具有*HandleType*引數設定為 SQL_HANDLE_ENV。 這個呼叫所配置的環境將會隱含的共用的環境，因為已啟用連線共用。  
  
 當配置共用的環境時，會使用的環境之前不會決定**SQLAllocHandle**具有*HandleType*利用 SQL_HANDLE_DBC 的呼叫。 此時，驅動程式管理員會嘗試尋找現有的環境符合應用程式所要求的環境屬性。 如果不存在此環境，做為共用的環境會建立一個。 驅動程式管理員會維護每個共用的環境; 的參考計數第一次建立環境時，計數是設定為 1。 如果找到相符的環境，該環境的控制代碼傳回應用程式，並參考計數會漸增。 以這種方式配置環境控制代碼可以用於任何 ODBC 函數可接受做為輸入引數環境控制代碼。  
  
## <a name="allocating-a-connection-handle"></a>配置連接控制代碼  
 連接控制代碼提供有效的陳述式等資訊的存取，並描述項控制代碼上連接和交易是否目前已開啟。 一般連接控制代碼的詳細資訊，請參閱[連接控制代碼](../../../odbc/reference/develop-app/connection-handles.md)。  
  
 若要要求在連接控制代碼，應用程式會呼叫**SQLAllocHandle**具有*HandleType*利用 SQL_HANDLE_DBC。 *InputHandle*引數設定為要呼叫所傳回的環境控制代碼**SQLAllocHandle** ，配置該控制代碼。 驅動程式會針對連接資訊和會在傳回的相關聯的控制代碼的值來配置記憶體 *\*OutputHandlePtr*。 在應用程式通過 *\*OutputHandlePtr*需要連接控制代碼的所有後續呼叫中的值。 如需詳細資訊，請參閱 <<c0> [ 配置連接處理](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)。  
  
 驅動程式管理員會處理**SQLAllocHandle**函式，並呼叫駕**SQLAllocHandle**函式應用程式呼叫時**SQLConnect**， **SQLBrowseConnect**，或**SQLDriverConnect**。 (如需詳細資訊，請參閱 < [SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)。)  
  
 如果之前未設定 SQL_ATTR_ODBC_VERSION 環境屬性**SQLAllocHandle**呼叫來配置連接控制代碼的環境中，配置連接的呼叫將傳回 SQLSTATE HY010 （函式的順序錯誤）。  
  
 當應用程式呼叫**SQLAllocHandle**具有*InputHandle*引數設定為 SQL_HANDLE_DBC 的而且也設為共用的環境控制代碼，驅動程式管理員會嘗試尋找現有的共用比對應用程式設定的環境屬性的環境。 如果沒有這類環境存在，會建立一個，1 參考計數 （在驅動程式管理員所維護）。 如果比對共用環境位於該控制代碼傳回給應用程式，其參考計數會漸增。  
  
 實際將使用的連接不會決定透過驅動程式管理員直到**SQLConnect**或是**SQLDriverConnect**呼叫。 驅動程式管理員的呼叫中使用的連線選項**SQLConnect** (或連接關鍵字，在呼叫**SQLDriverConnect**) 和之後連接配置的連接屬性設定決定應使用哪個集區中的連接。 如需詳細資訊，請參閱 < [SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="allocating-a-statement-handle"></a>配置陳述式控制代碼  
 陳述式控制代碼提供陳述式的資訊，例如錯誤訊息、 資料指標名稱，以及狀態資訊的存取權，來處理 SQL 陳述式。 一般陳述式控制代碼的詳細資訊，請參閱[陳述式控制代碼](../../../odbc/reference/develop-app/statement-handles.md)。  
  
 若要要求陳述式控制代碼，應用程式連接到資料來源，然後呼叫**SQLAllocHandle**提交 SQL 陳述式之前。 在此呼叫中， *HandleType*應該設定為 SQL_HANDLE_STMT 並*InputHandle*應該設定為要呼叫所傳回的連接控制代碼**SQLAllocHandle**所配置的控制代碼。 驅動程式會配置陳述式資訊的記憶體，與指定的連接，並會在傳回的相關聯的控制代碼的值產生關聯的陳述式控制代碼 *\*OutputHandlePtr*。 在應用程式通過 *\*OutputHandlePtr*需要陳述式控制代碼的所有後續呼叫中的值。 如需詳細資訊，請參閱 <<c0> [ 配置陳述式控制代碼](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)。  
  
 當配置陳述式控制代碼時，驅動程式自動配置一組的四個描述項，並將這些描述元控制代碼指派給 SQL_ATTR_APP_ROW_DESC、 SQL_ATTR_APP_PARAM_DESC、 SQL_ATTR_IMP_ROW_DESC 和 SQL_ATTR_IMP_PARAM_DESC陳述式屬性。 這些指*隱含*配置描述元。 若要明確配置應用程式描述項，請參閱下一節 「 配置描述項控制代碼 」。  
  
## <a name="allocating-a-descriptor-handle"></a>配置描述項控制代碼  
 當應用程式呼叫**SQLAllocHandle**具有*HandleType*的 SQL_HANDLE_DESC，驅動程式會配置應用程式描述項。 這些指*明確*配置描述元。 應用程式會引導驅動程式來呼叫，而不是自動配置指定的陳述式控制代碼使用的應用程式明確配置描述元**SQLSetStmtAttr** SQL_ATTR_APP_ROW_DESC 函式或 SQL_ATTR_APP_PARAM_DESC 屬性。 無法明確地配置實作描述項也可以實作描述項中指定**SQLSetStmtAttr**函式呼叫。  
  
 明確配置描述項是在連接控制代碼，而不是陳述式控制代碼相關聯 （如同自動配置描述項）。 只有在應用程式實際連接到資料庫時，才會維持配置描述元。 因為明確配置描述項與連接控制代碼相關聯，應用程式可以關聯的連接中的多個陳述式的明確配置描述項。 以隱含方式配置應用程式描述項，相反地，不能與一個以上的陳述式控制代碼相關聯。 （它不能與不是其配置的任何陳述式控制代碼相關聯。）明確配置描述項控制代碼可以明確地釋放應用程式，或藉由呼叫**SQLFreeHandle**具有*HandleType* SQL_HANDLE_DESC，或以隱含方式連線時已關閉。  
  
 明確配置描述元會釋出，隱含配置描述元時，再次陳述式相關聯。 （該陳述式的 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC 屬性一次是設為隱含配置描述項控制代碼）。這是針對已在連接上的明確配置描述元相關聯的所有陳述式，則為 true。  
  
 如需描述項的詳細資訊，請參閱[描述元](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[範例 ODBC 程式](../../../odbc/reference/sample-odbc-program.md)， [SQLBrowseConnect 函式](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)， [SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)，以及[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|執行 SQL 陳述式|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|釋放環境、 連接、 陳述式或描述元控制代碼|[SQLFreeHandle 函式](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|準備執行陳述式|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函式](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定描述項欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定環境屬性|[SQLSetEnvAttr 函式](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|設定陳述式屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
