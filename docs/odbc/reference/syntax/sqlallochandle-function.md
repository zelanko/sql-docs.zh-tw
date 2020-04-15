---
title: SQLAllocHandle 函數 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 178e3fad1ec062dd7f812125da66b7e21a7a4f4b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290207"
---
# <a name="sqlallochandle-function"></a>SQLAllocHandle 函式
**一致性**  
 推出版本: ODBC 3.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLAllocHandle**分配環境、連接、語句或描述符句柄。  
  
> [!NOTE]  
>  此函數是用於分配句柄的通用函數,用於替換 ODBC 2.0 函數**SQLAllocConnect、SQLAllocEnv**和**SQLAllocStmt。** **SQLAllocEnv** 允許調用**SQLAllocHandle 的應用程式**使用 ODBC 2。*x*驅動程式,對**SQLAllocHandle 的**調用在驅動程式管理器中對應到**SQLAllocConnect、SQLAllocEnv**或**SQLAllocStmt(** 視情況而定)。 **SQLAllocEnv** 有關詳細資訊,請參閱"註釋"。 有關驅動程式管理員將此功能映射到 ODBC 3 時的詳細資訊。*x*應用程式使用 ODBC 2。*x*驅動程式,請參閱[映射應用程式向後相容性的替代函數](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 [輸入]要由**SQLAllocHandle**分配的句柄的類型。 必須為下列其中一個值：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN句柄僅由驅動程式管理器和驅動程式使用。 應用程式不應使用此句柄類型。 有關SQL_HANDLE_DBC_INFO_TOKEN的詳細資訊,請參閱在[ODBC 驅動程式中開發連接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *輸入手柄*  
 [輸入]要在上下文中分配新句柄的輸入句柄。 如果*HandleType*是SQL_HANDLE_ENV,則這是SQL_NULL_HANDLE。 如果*HandleType* SQL_HANDLE_DBC,則它必須是環境句柄,如果是SQL_HANDLE_STMT或SQL_HANDLE_DESC,則必須是連接句柄。  
  
 *輸出手柄*  
 【輸出]指向要將句柄返回到新分配的數據結構的緩衝區的指標。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_INVALID_HANDLE 或SQL_ERROR。  
  
 分配環境句柄以外的句柄時,如果**SQLAllocHandle**返回SQL_ERROR,它將*OutputHandlePtr*設置為SQL_NULL_HDBC、SQL_NULL_HSTMT或SQL_NULL_HDESC,具體取決於*HandleType 的值*,除非輸出參數是空指標。 然後,應用程式可以從與*InputHandle*參數中的句柄關聯的診斷數據結構獲取其他資訊。  
  
## <a name="environment-handle-allocation-errors"></a>環境處理分配錯誤  
 環境分配既發生在驅動程式管理器內,也發生在每個驅動程式中。 **SQLAllocHandle**傳回的錯誤帶有SQL_HANDLE_ENV*的句柄類型*,具體取決於發生錯誤的級別。  
  
 如果調用具有*SQL_HANDLE_ENV的***SQLAllocHandle**時驅動程式管理器無法為*\*輸出句柄分配*記憶體,或者應用程式為*OutputHandlePtr*提供空指標, 則**SQLAllocHandle**返回SQL_ERROR。 驅動程式管理員將輸出*句柄設置*到SQL_NULL_HENV(除非應用程式提供了一個空指標,該指標返回SQL_ERROR)。 沒有關聯其他診斷資訊的句柄。  
  
 在應用程式呼叫**SQLConnect、SQLBrowseConnect**或**SQLDriverConnect**之前**SQLConnect**,驅動程式管理員不會調用驅動程式級環境句柄分配函數。 如果驅動程式級**SQLAllocHandle**函數中出現錯誤,則驅動程式管理器級別的**SQLConnect、SQLBrowseConnect**或**SQLDriverConnect****SQLBrowseConnect**函數將返回SQL_ERROR。 診斷資料結構包含 SQLSTATE IM004(驅動程式的**SQLAllocHandle**失敗)。 在連接句柄上返回錯誤。  
  
 有關驅動程式管理員和驅動程式之間函數呼叫流的詳細資訊,請參閱[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLAllocHandle**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以通過調用**SQLGetDiagRec**獲得關聯的 SQLSTATE 值,並將相應的*句柄Type*和*句柄*設置為*InputHandle*的值。 可以為*輸出處理*參數返回SQL_SUCCESS_WITH_INFO(但不是SQL_ERROR)。 下表列出了**SQLAllocHandle**通常返回的 SQLSTATE 值,並在此函數的上下文中解釋每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08003|連線未開啟|(DM) *HandleType*參數SQL_HANDLE_STMT或SQL_HANDLE_DESC,但*InputHandle*參數指定的連接未打開。 連接過程必須成功完成(連接必須打開),驅動程式才能分配語句或描述符句柄。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在 @*MessageText*緩衝區中返回的錯誤消息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|(DM) 驅動程式管理員無法為指定的句柄分配記憶體。<br /><br /> 驅動程式無法為指定的句柄分配記憶體。|  
|HY009|不合法的空白指標|(DM)*輸出句柄Ptr*參數是一個空指標。|  
|HY010|函式序列錯誤|(DM) *handleType*參數SQL_HANDLE_DBC,並且尚未調用**SQLSetEnvAttr**來設置SQL_ODBC_VERSION環境屬性。<br /><br /> (DM) 為**InputHandle**調用了非同步執行函數,並且在使用**HandleType**設定為SQL_HANDLE_STMT或SQL_HANDLE_DESC調用**SQLAllocHandle**函數時仍在執行。|  
|HY013|記憶體管理錯誤|*HandleType*參數SQL_HANDLE_DBC、SQL_HANDLE_STMT 或SQL_HANDLE_DESC;無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY014|超過控制點的控制點數量限制|已達到為*HandleType*參數指示的句柄類型可分配的句柄數的驅動程式定義限制。|  
|HY092|不合法屬性/選項識別碼|(DM) *HandleType*參數不是:SQL_HANDLE_ENV、SQL_HANDLE_DBC、SQL_HANDLE_STMT 或SQL_HANDLE_DESC。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|*HandleType*參數SQL_HANDLE_DESC,驅動程式是 ODBC 2。*x*驅動程式。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) *HandleType*參數SQL_HANDLE_STMT,驅動程式不是有效的 ODBC 驅動程式。<br /><br /> (DM) *handleType*參數SQL_HANDLE_DESC,驅動程式不支援分配描述符句柄。|  
  
## <a name="comments"></a>註解  
 **SQLAllocHandle**用於為環境、連接、語句和描述符分配句柄,如以下各節所述。 有關句柄的一般資訊,請參閱[句柄](../../../odbc/reference/develop-app/handles.md)。  
  
 如果驅動程式支援多個分配,應用程式可以一次分配多個環境、連接或語句句柄。 在 ODBC 中,對可在任何時間分配的環境、連接、語句或描述符句柄的數量不定義任何限制。 驅動程式可能會限制一次可以分配的某種類型的句柄的數量;有關詳細資訊,請參閱驅動程序文檔。  
  
 如果應用程式使用*\*OutputHandlePtr*調用**SQLAllocHandle,** 並將該句柄設置為已經存在的環境、連接、語句或描述符句柄,則驅動程式將覆蓋與*句柄*關聯的資訊,除非應用程式正在使用連接池(請參閱本節後面的"為連接池分配環境屬性")。 驅動程式管理員不檢查在*\*OutputHandlePtr*中輸入的*句柄*是否已被使用,也不會在覆蓋句柄之前檢查句柄的先前內容。  
  
> [!NOTE]  
>  使用為*\*OutputHandlePtr*定義的相同應用程式變數調用**SQLAllocHandle**兩次,而不調用**SQLFreeHandle**以釋放句柄,然後再重新分配它,這是不正確的 ODBC 應用程式程式設計。 以這種方式覆蓋 ODBC 句柄可能會導致 ODBC 驅動程式的行為不一致或錯誤。  
  
 在支援多個線程的作業系統上,應用程式可以在不同的線程上使用相同的環境、連接、語句或描述符句柄。 因此,驅動程式必須支援對此資訊的安全多線程訪問;例如,實現此目的的一種方法是使用關鍵部分或信號量。 有關執行緒的詳細資訊,請參閱[多線程](../../../odbc/reference/develop-app/multithreading.md)。  
  
 **SQLAllocHandle**在調用環境句柄時不設置SQL_ATTR_ODBC_VERSION環境屬性;但是,在調用它時,它未設置該屬性。環境屬性必須由應用程式設置,或者當調用**SQLAllocHandle**分配連接句柄時,將返回 SQLSTATE HY010(函數序列錯誤)。  
  
 對於符合標準的應用程式 **,SQLAllocHandle**在編譯時映射到**SQLAllocHandleStd。** 這兩個函數之間的區別是 **,SQLAllocHandleStd**將SQL_ATTR_ODBC_VERSION環境屬性設置為SQL_OV_ODBC3,當使用*HandleType*參數設置為SQL_HANDLE_ENV時,將環境屬性設置為SQL_OV_ODBC3。 之所以這樣做,是因為符合標準的應用程式始終是 ODBC 3。*x*應用程式。 此外,標準不要求註冊應用程式版本。 這是這兩個函數之間的唯一區別;否則,它們是相同的。 **SQLAllocHandleStd**映射到驅動程式管理器內的**SQLAllocHandle。** 因此,第三方驅動程式不必實現**SQLAllocHandleStd**。  
  
 ODBC 3.8 應用程式應使用:  
  
-   **SQLAllocHandle 而不是 SQLAllocHandleStd**來分配環境句柄。  
  
-   **SQLSetEnvAttr**將SQL_ATTR_ODBC_VERSION環境屬性設置為SQL_OV_ODBC3_80。  
  
## <a name="allocating-an-environment-handle"></a>配置環境控制代碼  
 環境句柄提供對全域資訊(如有效連接句柄和活動連接句柄)的訪問。 有關環境句柄的一般資訊,請參閱[環境句柄](../../../odbc/reference/develop-app/environment-handles.md)。  
  
 要請求環境句柄,應用程式呼叫**SQLAllocHandle,** 具有 SQL_HANDLE_ENV的*句柄類型*和 SQL_NULL_HANDLE的*輸入句柄*。 驅動程式為環境資訊分配記憶體,並將關聯的句柄的值傳回*\*OutputHandlePtr*參數中。 應用程式在所有需要環境句柄參數的後續調用中傳遞*\*OutputHandle*值。 有關詳細資訊,請參閱[分配環境句柄](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 在驅動程式管理器的環境句柄下,如果已存在驅動程式的環境句柄,則在建立連接時,該驅動程式中不會調用具有*句柄類型的*SQL_HANDLE_ENV **SQLAllocHandle,** 只有具有*SQL_HANDLE_DBC的* **SQLAllocHandle。** 如果驅動程式的環境句柄在驅動程式管理器的環境句柄下不存在,則當環境的第一個連接句柄連接到驅動程式時,驅動程式中會調用具有SQL_HANDLE_ENV句柄類型的 SQLAllocHandle 和具有 SQL_HANDLE_DBC的 SQLAllocHandle。  
  
 當驅動程式管理器使用 SQL_HANDLE_ENV 的*句柄類型*處理**SQLAllocHandle**函數時,它會檢查系統資訊 [ODBC] 部分中的**Trace**關鍵字。 如果設置為 1,驅動程式管理員將啟用對當前應用程式的追蹤。 如果設置了跟蹤標誌,則跟蹤在分配第一個環境句柄時開始,並在釋放最後一個環境句柄時結束。 有關詳細資訊,請參考[設定資料來源](../../../odbc/reference/install/configuring-data-sources.md)。  
  
 分配環境句柄后,應用程式必須在環境句柄上調用**SQLSetEnvAttr**來設置SQL_ATTR_ODBC_VERSION環境屬性。 如果在調用**SQLAllocHandle**在環境中分配連接句柄之前未設置此屬性,則分配連接的調用將返回 SQLSTATE HY010(函數序列錯誤)。 關於詳細資訊,請參閱[此應用程式的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)。  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>連線池配置共享環境  
 環境可以在單個進程中在多個元件之間共用。 共用環境可以同時由多個元件使用。 當元件使用共享環境時,它可以使用池連接,從而允許它分配和使用現有連接,而無需重新創建該連接。  
  
 在分配可用於連接池的共用環境之前,應用程式必須調用**SQLSetEnvAttr**將SQL_ATTR_CONNECTION_POOLING環境屬性設置為SQL_CP_ONE_PER_DRIVER或SQL_CP_ONE_PER_HENV。 在這種情況下 **,SQLSetEnvAttr**調用*環境處理設置為*null,這使得屬性成為進程級屬性。  
  
 啟用連接池後,應用程式將**SQLAllocHandle**調用,*句柄類型*參數設置為SQL_HANDLE_ENV。 此調用分配的環境將是隱式共用環境,因為連接池已啟用。  
  
 分配共用環境后,在調用具有*SQL_HANDLE_DBC*的**SQLAllocHandle**之前,不會確定將使用的環境。 此時,驅動程式管理員嘗試查找與應用程式請求的環境屬性匹配的現有環境。 如果不存在此類環境,則創建一個環境作為共用環境。 驅動程式管理員維護每個共用環境的引用計數;首次創建環境時,計數設置為1。 如果找到匹配的環境,該環境的句柄將返回到應用程式,並且引用計數將遞增。 以這種方式分配的環境句柄可用於接受環境句柄作為輸入參數的任何 ODBC 函數。  
  
## <a name="allocating-a-connection-handle"></a>配置連接控制代碼  
 連接句柄提供對連接上的有效語句和描述符句柄以及事務當前是否打開等資訊的訪問。 有關連接句柄的一般資訊,請參閱[連接句柄](../../../odbc/reference/develop-app/connection-handles.md)。  
  
 要請求連接句柄,應用程式使用*SQL_HANDLE_DBC的句柄類型*調用**SQLAllocHandle。** *InputHandle*參數設置為調用分配給該句柄的**SQLAllocHandle**返回的環境句柄。 驅動程式為連接資訊分配記憶體,並將關聯的句柄的值傳回*\*OutputHandlePtr*中。 應用程式在所有*\** 需要連接句柄的後續調用中傳遞 OutputHandlePtr 值。 有關詳細資訊,請參閱[分配連接句柄](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)。  
  
 驅動程式管理員處理**SQLAllocHandle**函數,並在應用程式呼叫**SQLConnect、SQLBrowseConnect**或**SQLDriverConnect****SQLBrowseConnect**時調用驅動程式的**SQLAllocHandle**函數。 (有關詳細資訊,請參閱[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
 如果在調用**SQLAllocHandle**在環境中分配連接句柄之前未設置SQL_ATTR_ODBC_VERSION環境屬性,則分配連接的調用將返回 SQLSTATE HY010(函數序列錯誤)。  
  
 當應用程式呼叫**SQLAllocHandle**時,*輸入句柄*參數設定為SQL_HANDLE_DBC並設置為共用環境句柄,驅動程式管理器將嘗試查找與應用程式設定的環境屬性匹配的現有共享環境。 如果不存在此類環境,則創建一個環境,引用計數(由驅動程式管理器維護)為 1。 如果找到匹配的共用環境,該句柄將返回到應用程式,其引用計數將遞增。  
  
 在調用**SQLConnect**或**SQLDriverConnect**之前,驅動程式管理員不會確定將使用的實際連接。 驅動程式管理員在調用**SQLConnect**時使用連接選項(或**SQLDriverConnect**呼叫中的連接關鍵字)和連接分配後設定的連接屬性來確定應在池中使用哪個連接。 有關詳細資訊,請參閱[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="allocating-a-statement-handle"></a>配置陳述式控制代碼  
 語句句柄提供對語句資訊(如錯誤消息、游標名稱和 SQL 語句處理的狀態資訊)的訪問。 有關語句句柄的一般資訊,請參閱[語句句柄](../../../odbc/reference/develop-app/statement-handles.md)。  
  
 要請求語句句柄,應用程式連接到數據源,然後在提交 SQL 語句之前調用**SQLAllocHandle。** 在此調用中 *,HandleType*應設定為SQL_HANDLE_STMT,*並且輸入句柄*應設置為調用分配給該句柄的**SQLAllocHandle**返回的連接句柄。 驅動程式為語句資訊分配記憶體,將語句句柄與指定的連接關聯,並在*\*OutputHandlePtr*中傳遞關聯句柄的值。 應用程式在所有*\** 需要語句句柄的後續調用中傳遞 OutputHandlePtr 值。 有關詳細資訊,請參閱[分配敘述的句柄](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)。  
  
 分配語句句柄時,驅動程式會自動分配一組四個描述符,並將這些描述符的句柄分配給SQL_ATTR_APP_ROW_DESC、SQL_ATTR_APP_PARAM_DESC、SQL_ATTR_IMP_ROW_DESC 和SQL_ATTR_IMP_PARAM_DESC語句屬性。 這些稱為*隱式*分配的描述符。 要顯式分配應用程式描述符,請參閱以下部分"分配描述符句柄"。  
  
## <a name="allocating-a-descriptor-handle"></a>配置描述符句柄  
 當應用程式使用 SQL_HANDLE_DESC 的*句柄類型*調用**SQLAllocHandle**時,驅動程式分配應用程式描述符。 這些稱為*顯式*分配的描述符。 應用程式指示驅動程式使用顯式分配的應用程式描述符,而不是透過使用SQL_ATTR_APP_ROW_DESC或SQL_ATTR_APP_PARAM_DESC 屬性呼叫**SQLSetStmtAttr**函數來為給定語句句柄自動分配的應用程式描述符。 不能顯式分配實現描述符,也不能在**SQLSetStmtAttr**函數調用中指定實現描述符。  
  
 顯式分配的描述符與連接句柄而不是語句句柄相關聯(自動分配的描述符是)。 僅當應用程式實際連接到資料庫時,才會分配描述符。 由於顯式分配的描述符與連接句柄相關聯,因此應用程式可以將顯式分配的描述符與連接中的多個語句相關聯。 另一方面,隱式分配的應用程式描述符不能與多個語句句柄關聯。 (它不能與分配給它的任何語句句柄以外的任何語句句柄相關聯。顯式分配的描述符句柄可以通過應用程式或使用SQL_HANDLE_DESC*的句柄類型*調用**SQLFreeHandle**或連接關閉時隱式釋放。  
  
 釋放顯式分配的描述符時,隱式分配的描述符將再次與語句關聯。 (該語句SQL_ATTR_APP_ROW_DESC或SQL_ATTR_APP_PARAM_DESC屬性將再次設置為隱式分配的描述符句柄。對於與連接上顯式分配的描述符關聯的所有語句,這都是如此。  
  
 有關描述符的詳細資訊,請參閱[描述子](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="code-example"></a>程式碼範例  
 請參考[範例 ODBC 程式](../../../odbc/reference/sample-odbc-program.md)[、SQLBrowseConnect 函數](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)[、SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)與[SQLSetCursor 名稱函數](../../../odbc/reference/syntax/sqlsetcursorname-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行準備好的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|釋放環境、連線、語句或描述符句柄|[SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|準備執行敘述|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|設定連線屬性|[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定描述符位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定環境屬性|[SQLSetEnvAttr 函式](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|設定敘述屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
