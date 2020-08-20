---
description: SQLAllocHandle 函式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9488e5d8d627feac2877878cc2d10a52ec15e4e6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487291"
---
# <a name="sqlallochandle-function"></a>SQLAllocHandle 函式
**一致性**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLAllocHandle** 會配置環境、連接、語句或描述項控制碼。  
  
> [!NOTE]  
>  這個函式是用來配置可取代 ODBC 2.0 函式 **SQLAllocConnect**、 **SQLAllocEnv**和 **SQLAllocStmt**之控制碼的泛型函數。 允許呼叫 **SQLAllocHandle** 的應用程式使用 ODBC 2。*x* 驅動程式時， **SQLAllocHandle** 的呼叫會在驅動程式管理員中對應到 **SQLAllocConnect**、 **SQLAllocEnv**或 **SQLAllocStmt**。 如需詳細資訊，請參閱「批註」。 如需有關驅動程式管理員如何將此函式對應至 ODBC 3 的詳細資訊。*x* 應用程式正在使用 ODBC 2。*x* 驅動程式，請參閱對應取代函式 [以提供應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 輸出要由 **SQLAllocHandle**配置的控制碼類型。 必須為下列其中一個值：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN 控制碼只能由驅動程式管理員和驅動程式使用。 應用程式不應該使用這個控制碼類型。 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊，請參閱 [在 ODBC 驅動程式中開發連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *InputHandle*  
 輸出在其內容中要配置新控制碼的輸入控制碼。 如果 *HandleType* 為 SQL_HANDLE_ENV，則 SQL_Null_HANDLE。 如果 *HandleType* 是 SQL_HANDLE_DBC，這必須是環境控制碼，如果是 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC，它必須是連接控制碼。  
  
 *OutputHandlePtr*  
 出緩衝區的指標，此緩衝區會將控制碼傳回至新配置的資料結構。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_INVALID_HANDLE 或 SQL_ERROR。  
  
 配置環境控制碼以外的控制碼時，如果**SQLAllocHandle**傳回 SQL_ERROR，則會根據*HandleType*的值，將*OutputHandlePtr*設定為 SQL_Null_HDBC、SQL_Null_HSTMT 或 SQL_Null_HDESC，除非 output 引數為 Null 指標。 然後，應用程式可以從與 *InputHandle* 引數中的控制碼相關聯的診斷資料結構取得其他資訊。  
  
## <a name="environment-handle-allocation-errors"></a>環境處理配置錯誤  
 環境配置是在驅動程式管理員和每個驅動程式內進行。 **SQLAllocHandle**所傳回的錯誤與*HandleType*的 SQL_HANDLE_ENV 取決於發生錯誤的層級。  
  
 如果在呼叫具有 SQL_HANDLE_ENV 之*HandleType*的**SQLAllocHandle**時，驅動程式管理員無法配置* \* OutputHandlePtr*的記憶體，或應用程式為*OutputHandlePtr*提供 null 指標， **SQLAllocHandle**會傳回 SQL_ERROR。 驅動程式管理員會將 **OutputHandlePtr* 設定為 SQL_Null_HENV (，除非應用程式提供的 Null 指標傳回 SQL_ERROR) 。 沒有可與其他診斷資訊相關聯的控制碼。  
  
 在應用程式呼叫 **SQLConnect**、 **SQLBrowseConnect**或 **SQLDriverConnect**之前，驅動程式管理員不會呼叫驅動層級的環境控制碼配置函數。 如果驅動層級 **SQLAllocHandle** 函式中發生錯誤，驅動程式管理員層級的 **SQLConnect**、 **SQLBrowseConnect**或 **SQLDriverConnect** 函數會傳回 SQL_ERROR。 診斷資料結構包含 SQLSTATE IM004 (驅動程式的 **SQLAllocHandle** 失敗) 。 此錯誤會在連接控制碼上傳回。  
  
 如需驅動程式管理員和驅動程式之間的函式呼叫流程的詳細資訊，請參閱 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)函式。  
  
## <a name="diagnostics"></a>診斷  
 當 **SQLAllocHandle** 傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，藉由呼叫 **SQLGetDiagRec** 並將適當的 *HandleType* 和 *控制碼* 設定為 *INPUTHANDLE*的值，即可取得相關聯的 SQLSTATE 值。 SQL_SUCCESS_WITH_INFO (但不能針對 *OutputHandle* 引數傳回 SQL_ERROR) 。 下表列出 **SQLAllocHandle** 通常會傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|08003|連接未開啟| (DM) *HandleType* 引數是 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC，但 *InputHandle* 引數指定的連接尚未開啟。 連接程式必須順利完成 (而且必須開啟連接) ，驅動程式才能配置語句或描述項控制碼。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **MessageText*緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤| (DM) 驅動程式管理員無法為指定的控制碼配置記憶體。<br /><br /> 驅動程式無法為指定的控制碼配置記憶體。|  
|HY009|Null 指標的用法無效| (DM) *OutputHandlePtr* 引數為 null 指標。|  
|HY010|函數順序錯誤| (DM) *HandleType* 引數是 SQL_HANDLE_DBC 的，而且尚未呼叫 **SQLSetEnvAttr** 來設定 SQL_ODBC_VERSION 的環境屬性。<br /><br />  (DM) 以非同步方式執行的函式是針對 **InputHandle** 呼叫的，而且當呼叫 **SQLAllocHandle** 函式時， **HandleType** 設定為 SQL_HANDLE_STMT 或 SQL_HANDLE_DESC 時，仍在執行。|  
|HY013|記憶體管理錯誤|*HandleType*引數為 SQL_HANDLE_DBC、SQL_HANDLE_STMT 或 SQL_HANDLE_DESC;因為無法存取基礎記憶體物件，所以無法處理函式呼叫，可能是因為記憶體不足的情況。|  
|HY014|超過的控制碼數目限制|針對可針對 *HandleType* 引數所表示之控制碼類型配置的控制碼數目，驅動程式定義的限制。|  
|HY092|不正確屬性/選項識別碼| (DM) *HandleType* 引數不是： SQL_HANDLE_ENV、SQL_HANDLE_DBC、SQL_HANDLE_STMT 或 SQL_HANDLE_DESC。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未執行選用功能|*HandleType*引數已 SQL_HANDLE_DESC，且驅動程式是 ODBC 2。*x*驅動程式。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) *HandleType* 引數是 SQL_HANDLE_STMT 的，而驅動程式並不是有效的 ODBC 驅動程式。<br /><br />  (DM) *HandleType* 引數是 SQL_HANDLE_DESC 的，而且驅動程式不支援配置描述項控制碼。|  
  
## <a name="comments"></a>註解  
 **SQLAllocHandle** 可用來配置環境、連接、語句和描述項的控制碼，如下列各節所述。 如需控制碼的一般資訊，請參閱 [控制碼](../../../odbc/reference/develop-app/handles.md)。  
  
 如果驅動程式支援多個配置，則應用程式一次可以配置一個以上的環境、連接或語句控制碼。 在 ODBC 中，不會定義任何一次可以配置的環境、連接、語句或描述項控制碼數目的限制。 驅動程式可能會限制特定類型的控制碼數目，可一次配置;如需詳細資訊，請參閱驅動程式檔集。  
  
 如果應用程式呼叫**SQLAllocHandle** ，並將* \* OutputHandlePtr*設定為已存在的環境、連接、語句或描述項控制碼，則驅動程式會覆寫與*控制碼*相關聯的資訊，除非應用程式使用連接共用 (請參閱本節後面的「配置連接共用的環境屬性」) 。 驅動程式管理員不會檢查* \* OutputHandlePtr*中輸入的*控制碼*是否已在使用中，也不會在覆寫之前檢查控制碼的先前內容。  
  
> [!NOTE]  
>  這是不正確的 ODBC 應用程式設計，可使用為* \* OutputHandlePtr*定義的相同應用程式變數來呼叫**SQLAllocHandle**兩次，而不需要呼叫**SQLFreeHandle**來釋放控制碼，然後再重新配置。 以這種方式覆寫 ODBC 控制碼可能會導致 ODBC 驅動程式部分的行為不一致或發生錯誤。  
  
 在支援多個執行緒的作業系統上，應用程式可以在不同的執行緒上使用相同的環境、連接、語句或描述項控制碼。 因此，驅動程式必須支援安全的多執行緒存取此資訊;例如，用來達成此目的的方法之一，是使用重要區段或信號。 如需執行緒的詳細資訊，請參閱 [多執行緒](../../../odbc/reference/develop-app/multithreading.md)。  
  
 **SQLAllocHandle** 在呼叫以配置環境控制碼時，不會設定 SQL_ATTR_ODBC_VERSION 環境屬性;環境屬性必須由應用程式設定，或在呼叫 **SQLAllocHandle** 來配置連接控制碼時，會傳回 SQLSTATE HY010 (函數順序錯誤) 。  
  
 針對符合標準的應用程式， **SQLAllocHandle** 會在編譯時期對應至 **SQLAllocHandleStd** 。 這兩個函式之間的差異在於， **SQLAllocHandleStd** 會在呼叫時將 SQL_ATTR_ODBC_VERSION 環境屬性設定為 SQL_OV_ODBC3，並將 *HandleType* 引數設定為 SQL_HANDLE_ENV。 這是因為符合標準的應用程式一律是 ODBC 3。*x* 應用程式。 此外，標準不需要註冊應用程式版本。 這是這兩個函式之間的唯一差異;否則，它們是相同的。 **SQLAllocHandleStd** 會對應至驅動程式管理員內的 **SQLAllocHandle** 。 因此，協力廠商驅動程式不需要執行 **SQLAllocHandleStd**。  
  
 ODBC 3.8 應用程式應該使用：  
  
-   **SQLAllocHandle 而不是 SQLAllocHandleStd** 來配置環境控制碼。  
  
-   **SQLSetEnvAttr** ，將 SQL_ATTR_ODBC_VERSION 環境屬性設定為 SQL_OV_ODBC3_80。  
  
## <a name="allocating-an-environment-handle"></a>配置環境控制代碼  
 環境控制碼可讓您存取全域資訊，例如有效的連接控制碼和使用中的連接控制碼。 如需環境控制碼的一般資訊，請參閱 [環境控制碼](../../../odbc/reference/develop-app/environment-handles.md)。  
  
 若要要求環境控制碼，應用程式會以 SQL_HANDLE_ENV 的*HandleType*和 SQL_Null_HANDLE 的*InputHandle*來呼叫**SQLAllocHandle** 。 驅動程式會為環境資訊配置記憶體，並將相關聯的控制碼值傳遞回* \* OutputHandlePtr*引數。 應用程式會在需要環境控制碼引數的所有後續呼叫中傳遞* \* OutputHandle*值。 如需詳細資訊，請參閱配置 [環境控制碼](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)。  
  
 在驅動程式管理員的環境控制碼下，如果已有驅動程式的環境控制碼，則在建立連線時，不會在該驅動程式中呼叫具有 SQLAllocHandle *HandleType* SQL_HANDLE_ENV 的**SQLAllocHandle** ，而只會**SQLAllocHandle** *HandleType*為 SQL_HANDLE_DBC。 如果驅動程式的環境控制碼不存在於驅動程式管理員的環境控制碼下，當該環境的第一個連接控制碼連接到驅動程式時，就會在驅動程式中呼叫 SQLAllocHandle HandleType 為 SQL_HANDLE_ENV，且 SQLAllocHandle 具有 HandleType SQL_HANDLE_DBC 的。  
  
 當驅動程式管理員以 SQL_HANDLE_ENV 的*HandleType*處理**SQLAllocHandle**函式時，它會檢查系統資訊 [ODBC] 區段中的**Trace**關鍵字。 如果設定為1，驅動程式管理員就會針對目前的應用程式啟用追蹤。 如果已設定追蹤旗標，則會在配置第一個環境控制碼時啟動追蹤，並且在最後一個環境控制碼釋放時結束。 如需詳細資訊，請參閱設定 [資料來源](../../../odbc/reference/install/configuring-data-sources.md)。  
  
 配置環境控制碼之後，應用程式必須在環境控制碼上呼叫 **SQLSetEnvAttr** ，以設定 SQL_ATTR_ODBC_VERSION 環境屬性。 如果在呼叫 **SQLAllocHandle** 之前未設定此屬性以配置環境上的連接控制碼，則配置連接的呼叫將會傳回 SQLSTATE HY010 (函式順序錯誤) 。 如需詳細資訊，請參閱宣告 [應用程式的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)。  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>配置共用環境以進行連接共用  
 您可以在單一進程上的多個元件之間共用環境。 共用的環境可以同時用於多個元件。 當某個元件使用共用環境時，它可以使用共用的連接，讓它能夠配置和使用現有的連線，而不需要重新建立該連線。  
  
 在配置可用於連接共用的共用環境之前，應用程式必須呼叫 **SQLSetEnvAttr** ，以將 SQL_ATTR_CONNECTION_POOLING 環境屬性設定為 SQL_CP_ONE_PER_DRIVER 或 SQL_CP_ONE_PER_HENV。 在此情況下， **SQLSetEnvAttr**會呼叫*EnvironmentHandle*設為 null 的，讓屬性成為進程層級的屬性。  
  
 啟用連接共用之後，應用程式會呼叫 **SQLAllocHandle** ，並將 *HandleType* 引數設定為 SQL_HANDLE_ENV。 此呼叫所配置的環境將會是隱含的共用環境，因為已啟用連接共用。  
  
 配置共用的環境時，將不會決定要使用的環境，除非 **SQLAllocHandle** 會呼叫 *HandleType* 的 SQL_HANDLE_DBC。 屆時，驅動程式管理員會嘗試找出符合應用程式所要求之環境屬性的現有環境。 如果沒有這樣的環境，則會建立一個共用環境作為共用環境。 驅動程式管理員會維護每個共用環境的參考計數;當您第一次建立環境時，計數會設定為1。 如果找到相符的環境，就會將該環境的控制碼傳回給應用程式，而參考計數會遞增。 以這種方式配置的環境控制碼，可用於接受環境控制碼做為輸入引數的任何 ODBC 函數。  
  
## <a name="allocating-a-connection-handle"></a>配置連接控制代碼  
 連接控制碼可讓您存取訊號，例如連接上的有效語句和描述項控制碼，以及交易目前是否開啟。 如需連接控制碼的一般資訊，請參閱 [連接控制碼](../../../odbc/reference/develop-app/connection-handles.md)。  
  
 若要要求連接控制碼，應用程式會呼叫 **SQLAllocHandle** ，並使用 *HandleType* 的 SQL_HANDLE_DBC。 *InputHandle*引數會設定為環境控制碼，該控制碼是由配置該控制碼之**SQLAllocHandle**的呼叫所傳回。 驅動程式會針對連接資訊配置記憶體，並在* \* OutputHandlePtr*中將相關聯的控制碼值傳遞回來。 應用程式會在所有需要連接控制碼的後續呼叫中傳遞* \* OutputHandlePtr*值。 如需詳細資訊，請參閱配置 [連接控制碼](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)。  
  
 當應用程式呼叫**SQLConnect**、 **SQLBrowseConnect**或**SQLDriverConnect**時，驅動程式管理員會處理**SQLAllocHandle**函式，並呼叫驅動程式的**SQLAllocHandle**函式。  (需詳細資訊，請參閱 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)函式。 )   
  
 如果在呼叫 **SQLAllocHandle** 之前未設定 SQL_ATTR_ODBC_VERSION 環境屬性，以在環境上配置連接控制碼，則配置連接的呼叫將會傳回 SQLSTATE HY010 (函數順序錯誤) 。  
  
 當應用程式呼叫 **SQLAllocHandle** 時，如果 *InputHandle* 引數設定為 SQL_HANDLE_DBC，同時也設為共用環境控制碼，驅動程式管理員會嘗試尋找符合應用程式所設定之環境屬性的現有共用環境。 如果沒有這樣的環境，則會建立一個，其中有參考計數 (由驅動程式管理員) 1。 如果找到相符的共用環境，則會將該控制碼傳回給應用程式，且其參考計數會遞增。  
  
 在呼叫 **SQLConnect** 或 **SQLDriverConnect** 之前，驅動程式管理員不會決定要使用的實際連接。 驅動程式管理員會在呼叫中使用連接選項 **SQLConnect** (或) **SQLDriverConnect** 呼叫中的連接關鍵字，以及連接配置之後設定的連接屬性，以決定應該使用集區中的哪個連接。 如需詳細資訊，請參閱 [SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="allocating-a-statement-handle"></a>配置陳述式控制代碼  
 語句控制碼可提供語句資訊的存取權，例如，錯誤訊息、資料指標名稱，以及 SQL 語句處理的狀態資訊。 如需語句控制碼的一般資訊，請參閱 [語句控制碼](../../../odbc/reference/develop-app/statement-handles.md)。  
  
 若要要求語句控制碼，應用程式會連接到資料來源，然後在提交 SQL 語句之前呼叫 **SQLAllocHandle** 。 在此呼叫中， *HandleType* 應該設定為 SQL_HANDLE_STMT 而且 *InputHandle* 應該設定為配置給該控制碼之 **SQLAllocHandle** 的呼叫所傳回的連接控制碼。 驅動程式會為語句資訊配置記憶體、將語句控制碼與指定的連接產生關聯，然後將相關聯的控制碼值傳遞回* \* OutputHandlePtr*。 應用程式會在所有需要語句控制碼的後續呼叫中傳遞* \* OutputHandlePtr*值。 如需詳細資訊，請參閱配置 [語句控制碼](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)。  
  
 配置語句控制碼時，驅動程式會自動設定一組四個描述項，並將這些描述項的控制碼指派給 SQL_ATTR_APP_ROW_DESC、SQL_ATTR_APP_PARAM_DESC、SQL_ATTR_IMP_ROW_DESC 和 SQL_ATTR_IMP_PARAM_DESC 語句屬性。 這些稱為 *隱含* 配置的描述項。 若要明確配置應用程式描述項，請參閱下一節「配置描述項控制碼」。  
  
## <a name="allocating-a-descriptor-handle"></a>配置描述項控制碼  
 當應用程式以 SQL_HANDLE_DESC 的*HandleType*呼叫**SQLAllocHandle**時，驅動程式會配置應用程式描述項。 這些稱為 *明確* 配置的描述項。 應用程式會指示驅動程式使用明確配置的應用程式描述項，而不是使用 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC 屬性來呼叫 **SQLSetStmtAttr** 函數，以使用明確配置的應用程式描述項，而不是針對指定的語句控制碼自動 無法明確配置執行描述項，也不能在 **SQLSetStmtAttr** 函式呼叫中指定執行描述項。  
  
 明確配置的描述元會與連接控制碼相關聯，而不是語句控制碼 (因為系統會) 自動設定的描述項。 只有當應用程式實際連接到資料庫時，才會維持配置描述項。 因為明確配置的描述項與連接控制碼相關聯，所以應用程式可以將明確配置的描述項與連接內的多個語句產生關聯。 另一方面，隱含配置的應用程式描述項無法與多個語句控制碼建立關聯。  (它無法與配置給它的任何語句控制碼相關聯。 ) 明確配置的描述項控制碼可以由應用程式明確釋放，也可以透過*HandleType*的 SQL_HANDLE_DESC 呼叫**SQLFreeHandle** ，或是在關閉連接時隱含地釋放。  
  
 釋放明確配置的描述項時，隱含配置的描述元會再次與語句相關聯。  (，該語句的 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC 屬性會再次設定為隱含配置的描述項控制碼 ) 。對於與連接上明確配置的描述項相關聯的所有語句，這是正確的。  
  
 如需描述項的詳細資訊，請參閱 [描述](../../../odbc/reference/develop-app/descriptors.md)項。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱 [ODBC 程式](../../../odbc/reference/sample-odbc-program.md)、 [SQLBrowseConnect 函數](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)、 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)函式和 [SQLSetCursorName 函數](../../../odbc/reference/syntax/sqlsetcursorname-function.md)範例。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|釋放環境、連接、語句或描述項控制碼|[SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|準備要執行的語句|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定描述項欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定環境屬性|[SQLSetEnvAttr 函式](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|設定語句屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
