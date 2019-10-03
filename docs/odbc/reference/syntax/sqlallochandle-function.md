---
title: SQLAllocHandle 函式 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLAllocHandle
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLAllocHandle
helpviewer_keywords:
- SQLAllocHandle function [ODBC]
ms.assetid: 6e7fe420-8cf4-4e72-8dad-212affaff317
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2fcf08a4a55a7c65dbc94219ac908da83ea15bad
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344277"
---
# <a name="sqlallochandle-function"></a>SQLAllocHandle 函式
**標準**  
 引進的版本:ODBC 3.0 標準合規性:ISO 92  
  
 **摘要**  
 **SQLAllocHandle**會配置環境、連接、語句或描述項控制碼。  
  
> [!NOTE]  
>  此函式是用來配置控制碼的泛型函式, 會取代 ODBC 2.0 函數**SQLAllocConnect**、 **SQLAllocEnv**和**SQLAllocStmt**。 允許呼叫**SQLAllocHandle**的應用程式與 ODBC 2 搭配使用。*x*驅動程式, **SQLAllocHandle**的呼叫會適當地對應到**SQLAllocConnect**、 **SQLAllocEnv**或**SQLAllocStmt**的驅動程式管理員。 如需詳細資訊, 請參閱「批註」。 如需在 ODBC 3 時, 驅動程式管理員將此函式對應至哪個功能的詳細資訊。*x*應用程式正在使用 ODBC 2。*x*驅動程式, 請參閱[對應取代函式以取得應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 源要由**SQLAllocHandle**配置的控制碼類型。 必須是下列其中一個值:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN 控制碼僅供驅動程式管理員和驅動程式使用。 應用程式不應使用此控制碼類型。 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊, 請參閱[在 ODBC 驅動程式中開發連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *InputHandle*  
 源中的輸入控制碼, 其內容是要配置新的控制碼。 如果*HandleType*為 SQL_HANDLE_ENV, 則此為 SQL_Null_HANDLE。 如果*HandleType*是 SQL_HANDLE_DBC, 這必須是環境控制碼, 如果是 HANDLETYPE 來或 SQL_HANDLE_DESC, 它必須是連接控制碼。  
  
 *OutputHandlePtr*  
 輸出緩衝區的指標, 在其中將控制碼傳回至新配置的資料結構。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_INVALID_HANDLE 或 SQL_ERROR。  
  
 在配置環境控制碼以外的控制碼時, 如果**SQLAllocHandle**傳回 SQL_ERROR, 它會將*OUTPUTHANDLEPTR*設定為 SQL_Null_HDBC、SQL_Null_HSTMT 或 SQL_Null_HDESC, 這取決於*HandleType*的值, 除非output 引數為 null 指標。 然後, 應用程式可以從與*InputHandle*引數中的控制碼相關聯的診斷資料結構中取得其他資訊。  
  
## <a name="environment-handle-allocation-errors"></a>環境控制碼配置錯誤  
 環境配置會同時在驅動程式管理員和每個驅動程式內發生。 **SQLAllocHandle**傳回*HandleType*為 SQL_HANDLE_ENV 的錯誤取決於發生錯誤的層級。  
  
 如果在呼叫*HandleType*為 SQL_HANDLE_ENV 的**SQLAllocHandle**時, 驅動程式管理員無法為 *\*OutputHandlePtr*配置記憶體, 或應用程式為*OutputHandlePtr*提供 null 指標, **SQLAllocHandle**會傳回 SQL_ERROR。 驅動程式管理員會將 *OutputHandlePtr*設定為 SQL_Null_HENV (除非應用程式提供了 Null 指標, 這會傳回 SQL_ERROR)。 沒有用來與其他診斷資訊產生關聯的控制碼。  
  
 在應用程式呼叫**SQLConnect**、 **SQLBrowseConnect**或**SQLDriverConnect**之前, 驅動程式管理員不會呼叫驅動層級的環境控制碼配置函式。 如果驅動程式層級的**SQLAllocHandle**函式中發生錯誤, 驅動程式管理員層級的**SQLConnect**、 **SQLBrowseConnect**或**SQLDriverConnect**函數會傳回 SQL_ERROR。 診斷資料結構包含 SQLSTATE IM004 (驅動程式的**SQLAllocHandle**失敗)。 此錯誤會在連接控制碼上傳回。  
  
 如需驅動程式管理員和驅動程式之間的函式呼叫流程的詳細資訊, 請參閱[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)函式。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLAllocHandle**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時, 可以藉由呼叫**SQLGetDiagRec**並將適當的*HandleType*和*Handle*設定為 InputHandle 的值, 來取得相關聯的 SQLSTATE 值。 可以針對*OutputHandle*引數傳回 SQL_SUCCESS_WITH_INFO (但不是 SQL_ERROR)。 下表列出通常由**SQLAllocHandle**所傳回的 SQLSTATE 值, 並在此函式的內容中說明每一個值;「(DM)」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明, 否則, 與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|Error|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|08003|連接未開啟|(DM) *HandleType*引數為 HANDLETYPE 來或 SQL_HANDLE_DESC, 但*InputHandle*引數所指定的連接未開啟。 連接程式必須成功完成 (而且必須開啟連接), 驅動程式才能配置語句或描述項控制碼。|  
|HY000|一般錯誤|發生錯誤, 但沒有任何特定 SQLSTATE, 且未定義任何執行特定的 SQLSTATE。 \* *MessageText*緩衝區中的 **SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|(DM) 驅動程式管理員無法為指定的控制碼配置記憶體。<br /><br /> 驅動程式無法為指定的控制碼配置記憶體。|  
|HY009|Null 指標的使用不正確|(DM) *OutputHandlePtr*引數為 null 指標。|  
|HY010|函數順序錯誤|(DM) *HandleType*引數是 SQL_HANDLE_DBC, 而且尚未呼叫**SQLSETEN加值稅TR**來設定 SQL_ODBC_VERSION 環境屬性。<br /><br /> (DM) 已針對**InputHandle**呼叫非同步執行的函式, 而且當呼叫**SQLAllocHandle**函數時, 如果**HANDLETYPE**設定為 handletype 來或 SQL_HANDLE_DESC, 仍在執行中。|  
|HY013|記憶體管理錯誤|*HandleType*引數為 SQL_HANDLE_DBC、HANDLETYPE 來或 SQL_HANDLE_DESC;無法處理函數呼叫, 因為無法存取基礎記憶體物件, 可能是因為記憶體不足的狀況。|  
|HY014|超過控制碼數目限制|已達到針對*HandleType*引數所表示的控制碼類型, 可以配置的控制碼數目的驅動程式定義限制。|  
|HY092|不正確屬性/選項識別碼|(DM) *HandleType*引數不是:SQL_HANDLE_ENV、SQL_HANDLE_DBC、HANDLETYPE 來或 SQL_HANDLE_DESC。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|(DM) 如需暫停狀態的詳細資訊, 請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|*HandleType*引數是 SQL_HANDLE_DESC, 而驅動程式是 ODBC 2。*x*驅動程式。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前, 連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 來設定。|  
|IM001|驅動程式不支援此功能|(DM) *HandleType*引數是 handletype 來, 而驅動程式不是有效的 ODBC 驅動程式。<br /><br /> (DM) *HandleType*引數已 SQL_HANDLE_DESC, 而驅動程式不支援配置描述項控制碼。|  
  
## <a name="comments"></a>註解  
 **SQLAllocHandle**是用來配置環境、連接、語句和描述元的控制碼, 如下列各節所述。 如需控制碼的一般資訊, 請參閱[控制碼](../../../odbc/reference/develop-app/handles.md)。  
  
 如果驅動程式支援多個配置, 應用程式一次可以配置一個以上的環境、連接或語句控制碼。 在 ODBC 中, 不會在任何一次可以配置的環境、連接、語句或描述項控制碼數目上定義任何限制。 驅動程式可能會限制一次可配置的特定控制碼類型數目;如需詳細資訊, 請參閱驅動程式檔集。  
  
 如果應用程式呼叫**SQLAllocHandle** ,  *\** 並將 OutputHandlePtr 設定為已存在的環境、連接、語句或描述項控制碼, 驅動程式會覆寫與*控制碼相關聯的資訊*, 除非應用程式使用連接共用 (請參閱本節稍後的「配置連接共用的環境屬性」)。 驅動程式管理員不會檢查 *\*OutputHandlePtr*中輸入的*控制碼*是否已在使用中, 也不會在覆寫之前檢查控制碼的先前內容。  
  
> [!NOTE]  
>  這不是不正確的 ODBC 應用程式設計, 而是使用為 *\*OutputHandlePtr*定義的相同應用程式變數呼叫**SQLAllocHandle**兩次, 而不需要呼叫**SQLFreeHandle**來釋放控制碼, 然後再重新配置. 以這種方式覆寫 ODBC 控制碼, 可能會導致 ODBC 驅動程式不一致的行為或錯誤。  
  
 在支援多個執行緒的作業系統上, 應用程式可以在不同的執行緒上使用相同的環境、連接、語句或描述項控制碼。 因此, 驅動程式必須支援安全的多執行緒存取此資訊;例如, 其中一種方法是使用關鍵區段或信號來達成此目的。 如需執行緒的詳細資訊, 請參閱[多執行緒](../../../odbc/reference/develop-app/multithreading.md)。  
  
 **SQLAllocHandle**不會在呼叫以配置環境控制碼時, 設定 SQL_ATTR_ODBC_VERSION 環境屬性。環境屬性必須由應用程式設定, 否則當呼叫**SQLAllocHandle**來配置連接控制碼時, 將會傳回 SQLSTATE HY010 (函數序列錯誤)。  
  
 針對符合標準的應用程式, **SQLAllocHandle**會在編譯時期對應至**SQLAllocHandleStd** 。 這兩個函式之間的差異在於, **SQLAllocHandleStd**會在呼叫時將 SQL_ATTR_ODBC_VERSION 環境屬性設定為 SQL_OV_ODBC3, 並將*HandleType*引數設為 SQL_HANDLE_ENV。 這麼做是因為符合標準的應用程式一律是 ODBC 3。*x*應用程式。 此外, 標準不需要註冊應用程式版本。 這是這兩個函數之間的唯一差異;否則, 它們完全相同。 **SQLAllocHandleStd**會對應到驅動程式管理員內的**SQLAllocHandle** 。 因此, 協力廠商驅動程式不需要執行**SQLAllocHandleStd**。  
  
 ODBC 3.8 應用程式應該使用:  
  
-   **SQLAllocHandle 和 Not SQLAllocHandleStd**以配置環境控制碼。  
  
-   **SQLSetEnvAttr** , 將 SQL_ATTR_ODBC_VERSION 環境屬性設定為 SQL_OV_ODBC3_80。  
  
## <a name="allocating-an-environment-handle"></a>配置環境控制代碼  
 環境控制碼提供全域資訊的存取權, 例如有效的連接控制碼和作用中的連接控制碼。 如需環境控制碼的一般資訊, 請參閱[環境控制碼](../../../odbc/reference/develop-app/environment-handles.md)。  
  
 若要要求環境控制碼, 應用程式會呼叫*HandleType*為 SQL_HANDLE_ENV 且*InputHandle*為 SQL_Null_HANDLE 的**SQLAllocHandle** 。 驅動程式會為環境資訊配置記憶體, 並將相關聯的控制碼值傳遞回 *\*OutputHandlePtr*引數中。 應用程式會在所有需要環境控制碼引數的後續呼叫中傳遞 *\*OutputHandle*值。 如需詳細資訊, 請參閱配置[環境控制碼](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 在驅動程式管理員的環境控制碼之下, 如果已有驅動程式的環境控制碼, 則在建立連線時, 不會在該驅動程式中呼叫具有 SQL_HANDLE_ENV *HandleType*的**SQLAllocHandle** , 只會**SQLAllocHandle** *HandleType*為 SQL_HANDLE_DBC。 驅動程式管理員的環境控制碼若驅動程式的環境控制碼不存在, 則會在第一次連線時于驅動程式中呼叫具有 HandleType SQL_HANDLE_ENV 和 SQLAllocHandle HandleType SQL_HANDLE_DBC 的 SQLAllocHandle環境的控制碼已連接到驅動程式。  
  
 當驅動程式管理員以 SQL_HANDLE_ENV 的*HandleType*處理**SQLAllocHandle**函數時, 它會檢查系統資訊 [ODBC] 區段中的**Trace**關鍵字。 如果設定為 1, 驅動程式管理員就會啟用目前應用程式的追蹤。 如果已設定追蹤旗標, 則會在配置第一個環境控制碼時開始追蹤, 並在最後一個環境控制碼釋放時結束。 如需詳細資訊, 請參閱設定[資料來源](../../../odbc/reference/install/configuring-data-sources.md)。  
  
 配置環境控制碼之後, 應用程式必須在環境控制碼上呼叫**SQLSetEnvAttr** , 以設定 SQL_ATTR_ODBC_VERSION 環境屬性。 如果未在呼叫**SQLAllocHandle**之前設定此屬性來配置環境上的連接控制碼, 則配置連接的呼叫將會傳回 SQLSTATE HY010 (函數序列錯誤)。 如需詳細資訊, 請參閱宣告[應用程式的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)。  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>配置共用環境以進行連接共用  
 在單一進程中, 可以在多個元件之間共用環境。 共用環境可以同時由一個以上的元件使用。 當元件使用共用環境時, 它可以使用集區連接, 讓它能夠配置和使用現有的連接, 而不需要重新建立該連線。  
  
 在配置可用於連接共用的共用環境之前, 應用程式必須呼叫**SQLSetEnvAttr** , 將 SQL_ATTR_CONNECTION_POOLING 環境屬性設定為 SQL_CP_ONE_PER_DRIVER 或 SQL_CP_ONE_PER_HENV。 在此情況下, 會呼叫**SQLSetEnvAttr** , 並將*EnvironmentHandle*設為 null, 讓屬性成為進程層級屬性。  
  
 啟用連接共用之後, 應用程式會呼叫**SQLAllocHandle** , 並將*HandleType*引數設定為 SQL_HANDLE_ENV。 此呼叫所配置的環境將會是隱含的共用環境, 因為已啟用連接共用。  
  
 配置共用環境時, 除非呼叫具有 SQL_HANDLE_DBC *HandleType*的**SQLAllocHandle** , 否則不會決定要使用的環境。 此時, 驅動程式管理員會嘗試找出符合應用程式所要求之環境屬性的現有環境。 如果這類環境不存在, 則會建立一個共用環境。 驅動程式管理員會維護每個共用環境的參考計數;第一次建立環境時, 計數會設定為1。 如果找到相符的環境, 該環境的控制碼會傳回給應用程式, 而參考計數會遞增。 以這種方式配置的環境控制碼, 可以用於接受環境控制碼做為輸入引數的任何 ODBC 函數。  
  
## <a name="allocating-a-connection-handle"></a>配置連接控制代碼  
 連接控制碼提供資訊的存取權, 例如連接上的有效語句和描述項控制碼, 以及交易目前是否開啟。 如需連接控制碼的一般資訊, 請參閱[連接控制碼](../../../odbc/reference/develop-app/connection-handles.md)。  
  
 若要要求連接控制碼, 應用程式會以 SQL_HANDLE_DBC 的*HandleType*呼叫**SQLAllocHandle** 。 *InputHandle*引數會設定為**SQLAllocHandle**呼叫所傳回的環境控制碼, 該處理常式會配置給該處理。 驅動程式會為連接資訊配置記憶體, 並在 *\*OutputHandlePtr*中傳遞相關聯之控制碼的值。 應用程式會在所有需要連接控制碼的後續呼叫中傳遞 *\*OutputHandlePtr*值。 如需詳細資訊, 請參閱配置[連接控制碼](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)。  
  
 當應用程式呼叫**SQLConnect**、 **SQLBrowseConnect**或**SQLDriverConnect**時, 驅動程式管理員會處理**SQLAllocHandle**函數, 並呼叫驅動程式的**SQLAllocHandle**函式。 (如需詳細資訊, 請參閱[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md))。  
  
 如果在呼叫**SQLAllocHandle**之前未設定 SQL_ATTR_ODBC_VERSION 環境屬性來配置環境上的連接控制碼, 則配置連接的呼叫將會傳回 SQLSTATE HY010 (函數序列錯誤)。  
  
 當應用程式呼叫**SQLAllocHandle** , 並將*InputHandle*引數設為 SQL_HANDLE_DBC, 同時將設定為共用的環境控制碼時, 驅動程式管理員會嘗試尋找符合環境屬性的現有共用環境。由應用程式設定。 如果沒有這類環境存在, 則會建立一個, 其中會有1個參考計數 (由驅動程式管理員維護)。 如果找到相符的共用環境, 則會將該控制碼傳回給應用程式, 而且其參考計數會遞增。  
  
 在呼叫**SQLConnect**或**SQLDriverConnect**之前, 驅動程式管理員不會決定要使用的實際連接。 驅動程式管理員會使用**SQLConnect**呼叫中的連接選項 (或**SQLDriverConnect**呼叫中的連接關鍵字), 以及連線配置之後所設定的連接屬性來判斷集區中的哪個連接應該使用。 如需詳細資訊, 請參閱[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="allocating-a-statement-handle"></a>配置陳述式控制代碼  
 語句控制碼提供語句資訊的存取權, 例如錯誤訊息、資料指標名稱, 以及 SQL 語句處理的狀態資訊。 如需語句控制碼的一般資訊, 請參閱[語句控制碼](../../../odbc/reference/develop-app/statement-handles.md)。  
  
 若要要求語句控制碼, 應用程式會連接到資料來源, 然後在提交 SQL 語句之前呼叫**SQLAllocHandle** 。 在此呼叫中, *HandleType*應該設定為 handletype 來, 而*InputHandle*應設定為呼叫**SQLAllocHandle**所傳回的連接控制碼, 該控制碼會配置給該處理常式。 驅動程式會為語句資訊配置記憶體、將語句控制碼與指定的連接建立關聯, 並將相關聯的控制碼值傳遞回 *\*OutputHandlePtr*。 應用程式會在所有需要語句控制碼的後續呼叫中傳遞 *\*OutputHandlePtr*值。 如需詳細資訊, 請參閱配置[語句控制碼](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)。  
  
 配置語句控制碼時, 驅動程式會自動設定一組四個描述元, 並將這些描述元的控制碼指派給 SQL_ATTR_APP_ROW_DESC、SQL_ATTR_APP_PARAM_DESC、SQL_ATTR_IMP_ROW_DESC 和 SQL_ATTR_IMP_PARAM_DESC語句屬性。 這些稱為*隱含*配置的描述元。 若要明確配置應用程式描述項, 請參閱下一節「配置描述項控制碼」。  
  
## <a name="allocating-a-descriptor-handle"></a>配置描述元控制碼  
 當應用程式以 SQL_HANDLE_DESC 的*HandleType*呼叫**SQLAllocHandle**時, 驅動程式會配置應用程式描述項。 這些稱為*明確*配置的描述元。 應用程式會指示驅動程式使用明確配置的應用程式描述元, 而不是透過呼叫**SQLSetStmtAttr**函數與 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_, 針對指定的語句控制碼自動設定一個PARAM_DESC 屬性。 無法明確配置執行描述項, 也不能在**SQLSetStmtAttr**函式呼叫中指定執行描述元。  
  
 明確配置的描述元與連接控制碼相關聯, 而不是語句控制碼 (如自動設定的描述元)。 只有當應用程式實際連接到資料庫時, 描述元才會保持配置。 由於明確配置的描述元與連接控制碼相關聯, 因此應用程式可以將明確配置的描述元與連接中的一個以上的語句產生關聯。 另一方面, 隱含配置的應用程式描述項無法與一個以上的語句控制碼建立關聯。 (它無法與配置給它的任何語句控制碼建立關聯)。明確配置的描述元控制碼可以由應用程式明確釋放, 或藉由呼叫*HandleType*為 SQL_HANDLE_DESC 的**SQLFreeHandle** , 或在連接關閉時隱含地釋出。  
  
 釋放明確配置的描述元時, 隱含配置的描述元會再次與語句相關聯。 (該語句的 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC 屬性會再次設定為隱含配置的描述項控制碼)。這適用于與連接上明確配置的描述元相關聯的所有語句。  
  
 如需描述項的詳細資訊, 請參閱[描述](../../../odbc/reference/develop-app/descriptors.md)元。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[範例 ODBC 程式](../../../odbc/reference/sample-odbc-program.md)、 [SQLBrowseConnect 函數](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)、 [SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)函式。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|釋放環境、連接、語句或描述項控制碼|[SQLFreeHandle 函式](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|準備語句以執行|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函式](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定描述項欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定環境屬性|[SQLSetEnvAttr 函式](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|設定語句屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
