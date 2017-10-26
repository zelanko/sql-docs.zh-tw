---
title: "SQLDriverConnect 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLDriverConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDriverConnect
helpviewer_keywords:
- SQLDriverConnect function [ODBC]
ms.assetid: e299be1d-5c74-4ede-b6a3-430eb189134f
caps.latest.revision: 50
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8b9576bf21c922c1e8d223710210a1703f1cbec3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqldriverconnect-function"></a>SQLDriverConnect 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ODBC  
  
 **摘要**  
 **SQLDriverConnect**替代**SQLConnect**。 它支援資料來源需要更多的連接資訊中的三個引數比**SQLConnect**，提示使用者輸入所有連接資訊和系統中未定義的資料來源對話方塊資訊。  
  
 **SQLDriverConnect**提供下列連接屬性：  
  
-   建立資料來源所使用的連接字串，其中包含資料來源名稱、 一或多個使用者識別碼、 一或多個密碼，以及所需的其他資訊的連接。  
  
-   建立連線，使用部分連接字串或沒有其他資訊。在此情況下，驅動程式管理員和驅動程式可以每個提示使用者輸入連接資訊。  
  
-   連接到資料來源不是定義在 系統資訊。 如果應用程式提供部分連接字串，此驅動程式可以提示使用者輸入連接資訊。  
  
-   連接到資料來源使用.dsn 檔案中的資訊從建構連接字串。  
  
 建立連接之後， **SQLDriverConnect**傳回的完整的連接字串。 應用程式可以使用這個字串的後續連接要求。 如需詳細資訊，請參閱[使用 SQLDriverConnect 連接](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLDriverConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLHWND         WindowHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr,  
     SQLUSMALLINT    DriverCompletion);  
```  
  
## <a name="arguments"></a>引數  
 *ConnectionHandle*  
 [輸入]連接控制代碼。  
  
 *Sqldriverconnect*  
 [輸入]視窗控制代碼。 應用程式可以將傳遞的父視窗控制代碼，如果適用的話，或如果任一個為 null 指標的視窗控制代碼不適用或**SQLDriverConnect**不會顯示任何對話方塊。  
  
 *InConnectionString*  
 [輸入]完整連接字串 （請參閱 [意見] 中的語法），部分連接字串或空字串。  
  
 *StringLength1*  
 [輸入]長度 **InConnectionString*，如果字串為 Unicode 或位元組如果字串為 ANSI 或 DBCS 字元。  
  
 *OutConnectionString*  
 [輸出]已完成的連接字串緩衝區的指標。 目標資料來源的連接成功，這個緩衝區會包含完整的連接字串。 應用程式應該為這個緩衝區配置至少 1024 個字元。  
  
 如果*OutConnectionString*是 NULL， *StringLength2Ptr*仍會傳回的總字元數 （不含字元資料 null 結束字元） 可用來傳回緩衝區中所指*OutConnectionString*。  
  
 *Columnsize*  
 [輸入]長度 **OutConnectionString*緩衝區，以字元為單位。  
  
 *StringLength2Ptr*  
 [輸出]這是要傳回的總字元數 （不包括 null 結束字元） 中的緩衝區指標可用來傳回中\* *OutConnectionString*。 可傳回的字元數目是否大於或等於*Columnsize*，完成連接字串中的\* *OutConnectionString*會被截斷成*Columnsize*減去 null 結束字元的長度。  
  
 *DriverCompletion*  
 [輸入]旗標，表示驅動程式管理員或驅動程式必須提示輸入連接的詳細資訊：  
  
 SQL_DRIVER_PROMPT、 SQL_DRIVER_COMPLETE、 SQL_DRIVER_COMPLETE_REQUIRED 時或 SQL_DRIVER_NOPROMPT。  
  
 （如需詳細資訊，請參閱 「 註解。"）  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDriverConnect**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可能會取得藉由呼叫**SQLGetDiagRec**與*fHandleType*利用 SQL_HANDLE_DBC 的和*hHandle*的*ConnectionHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLDriverConnect** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|緩衝區\* *OutConnectionString*仍不夠大，無法傳回整個連接字串中，因此連接字串已遭截斷。 中會傳回未截斷的連接字串的長度 **StringLength2Ptr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S00|無效的連接字串屬性|連接字串中指定無效的屬性關鍵字 (*InConnectionString*)，但仍然連接到資料來源驅動程式。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S02 的警告|選項值已變更|驅動程式不支援指定的值所指向*ValuePtr*引數中的**SQLSetConnectAttr**置換相似的值。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S08|儲存檔案 DSN 時發生錯誤|中的字串* \*InConnectionString*包含**FILEDSN**關鍵字，但.dsn 檔案未儲存。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S09|無效的關鍵字|(DM) 中的字串* \*InConnectionString*包含**SAVEFILE**關鍵字，但不是**驅動程式**或**FILEDSN**關鍵字。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08001|無法建立連線的用戶端|驅動程式無法建立與資料來源的連接。|  
|08002|使用中的連接名稱|(DM) 指定*ConnectionHandle*必須已經用來與資料來源，建立連線，而仍開啟的連接。|  
|08004|伺服器拒絕連線|資料來源的拒絕連線的建立實作定義理由。|  
|08S01|通訊連結失敗|驅動程式的驅動程式在嘗試連接資料來源之間的通訊連結失敗之前**SQLDriverConnect**函式已完成的處理。|  
|28000|無效的授權規格|使用者識別碼或授權字串，或兩者的連接字串中所指定 (*InConnectionString*)，違反了資料來源所定義的限制。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中* \*szMessageText*緩衝區描述錯誤和其原因。|  
|HY000|一般的錯誤： 無效的檔案 dsn|(DM) 中的字串 **InConnectionString*包含 FILEDSN 關鍵字，但找不到.dsn 檔案的名稱。|  
|HY000|一般的錯誤： 無法建立緩衝區|(DM) 中的字串 **InConnectionString*包含 FILEDSN 關鍵字，但無法讀取.dsn 檔案。|  
|HY001|記憶體配置錯誤|驅動程式管理員無法配置記憶體，才能支援執行或完成**SQLDriverConnect**函式。<br /><br /> 驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY008|已取消操作|非同步處理已啟用*ConnectionHandle*。 呼叫此函式，和之前已完成執行， [SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上呼叫*ConnectionHandle*，然後**SQLDriverConnect**上一次呼叫函式*ConnectionHandle*。<br /><br /> 或者， **SQLDriverConnect**呼叫函式，和之前已完成執行， **SQLCancelHandle**上呼叫*ConnectionHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 另一個以非同步方式執行的函式 (不**SQLDriverConnect**) 針對呼叫*ConnectionHandle*還在執行時和**SQLDriverConnect**呼叫函式。|  
|HY013|記憶體管理錯誤|**SQLDriverConnect**因為基礎記憶體的物件無法存取，可能是因為記憶體不足，無法處理函式呼叫。|  
|HY090|字串或緩衝區長度無效|(DM) 引數指定的值*StringLength1*小於 0，且不等於 SQL_NTS。<br /><br /> (DM) 引數指定的值*Columnsize*小於 0。|  
|HY092|屬性/選項識別碼無效|(DM) *DriverCompletion*引數為 SQL_DRIVER_PROMPT，而*Sqldriverconnect*引數為 null 指標。|  
|HY110|無效的驅動程式完成|(DM) 指定的引數的值*DriverCompletion*不等於 SQL_DRIVER_PROMPT、 SQL_DRIVER_COMPLETE、 SQL_DRIVER_COMPLETE_REQUIRED 時或 SQL_DRIVER_NOPROMPT。<br /><br /> (DM) 連接共用已啟用，而且引數指定的值*DriverCompletion*不等於 SQL_DRIVER_NOPROMPT。|  
|HYC00|未實作選擇性功能|驅動程式不支援要求的應用程式的 ODBC 行為的版本。|  
|HYT00|已超過逾時的設定|登入逾時期限過期之前完成資料來源的連接。 逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_LOGIN_TIMEOUT。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 對應到指定的資料來源名稱的驅動程式不支援此函式。|  
|IM002|找不到資料來源並指定預設驅動程式|(DM) 的資料來源連接字串中指定的名稱 (*InConnectionString*) 在系統資訊中，找不到，而且已經沒有預設的驅動程式規格。<br /><br /> (DM) 的系統資訊中找不到 ODBC 資料來源及預設驅動程式的資訊。|  
|IM003|無法載入指定的驅動程式|(DM) 驅動程式的系統資訊的資料來源規格中所列，或所指定**驅動程式**關鍵字找不到或無法載入某些其他原因。|  
|IM004|驅動程式的**SQLAllocHandle**上 SQL_HANDLE_ENV 失敗|(DM) 期間**SQLDriverConnect**，稱為 「 驅動程式的驅動程式管理員**SQLAllocHandle**函式與*fHandleType* SQL_HANDLE_ENV 和驅動程式傳回發生錯誤。|  
|IM005|驅動程式的**SQLAllocHandle**上利用 SQL_HANDLE_DBC 失敗。|(DM) 期間**SQLDriverConnect**，稱為 「 驅動程式的驅動程式管理員**SQLAllocHandle**函式與*fHandleType*利用 SQL_HANDLE_DBC 的驅動程式傳回發生錯誤。|  
|IM006|驅動程式的**SQLSetConnectAttr**失敗|(DM) 期間**SQLDriverConnect**，稱為 「 驅動程式的驅動程式管理員**SQLSetConnectAttr**函式和驅動程式傳回錯誤。|  
|IM007|沒有資料來源或驅動程式指定;禁止使用的對話方塊|連接字串中指定任何資料來源名稱或驅動程式和*DriverCompletion*已 SQL_DRIVER_NOPROMPT。|  
|IM008|對話失敗|驅動程式會嘗試顯示其登入 對話方塊，而失敗。<br /><br /> *Sqldriverconnect*是 null 指標，和*DriverCompletion*未 SQL_DRIVER_NO_PROMPT。|  
|IM009|無法載入轉譯 DLL|驅動程式無法載入轉譯 DLL 所指定資料來源或連接。|  
|IM010|資料來源名稱太長|(DM) DSN 關鍵字的屬性值已超過 SQL_MAX_DSN_LENGTH 個字元。|  
|IM011|驅動程式名稱太長|(DM) 屬性值**驅動程式**關鍵字已超過 255 個字元。|  
|IM012|驅動程式關鍵字的語法錯誤|(DM) 關鍵字-值配對的**驅動程式**關鍵字包含語法錯誤。<br /><br /> (DM) 中的字串* \*InConnectionString*包含**FILEDSN**關鍵字，但.dsn 檔案未包含**驅動程式**關鍵字或**DSN**關鍵字。|  
|IM014|指定的資料來源名稱包含驅動程式和應用程式之間的架構不相符|(DM) 32 位元應用程式使用的 DSN 連接至 64 位元驅動程式。反之亦然。|  
|IM015|驅動程式的 SQLDriverConnect SQL_HANDLE_DBC_INFO_HANDLE 上失敗|如果驅動程式會傳回 SQL_ERROR，驅動程式管理員將會傳回 SQL_ERROR，應用程式，則連接會失敗。<br /><br /> 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊，請參閱[開發 ODBC 驅動程式中的連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。|  
|IM017|中的非同步通知模式已停用輪詢|每當通知模型使用時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，且如果已啟用通知模式， **SQLCompleteAsync**必須在後續處理作業，並完成此作業的控制代碼上呼叫。|  
|S1118|驅動程式不支援非同步通知|當驅動程式不支援非同步通知時，您無法對 SQL_ATTR_ASYNC_DBC_EVENT 或 SQL_ATTR_ASYNC_DBC_RETCODE_PTR 進行設定。|  
  
## <a name="comments"></a>註解  
 連接字串具有下列語法：  
  
 *連接字串*:: =*空白字串*[;] &#124;*屬性*[;] &#124;*屬性*;*連接字串*  
  
 *空白字串*:: =*屬性*:: =*屬性關鍵字*=*屬性值*&#124;驅動程式 = [{}]*屬性值*[}]  
  
 *屬性關鍵字*:: = DSN &#124;UID &#124;PWD &#124;*驅動程式-定義-屬性-關鍵字*  
  
 *屬性值*:: =*字元字串*  
  
 *驅動程式-定義-屬性-關鍵字*:: =*識別碼*  
  
 其中*字元字串*有零個或多個字元。*識別碼*有一或多個字元。*屬性關鍵字*不區分大小寫。*屬性值*可能會區分大小寫，以及值**DSN**關鍵字並沒有包含單獨的空白個數。  
  
 因為連接字串和初始設定檔案文法、 關鍵字和屬性值包含字元**[] {} （)，;？\*= ！ @**不括在大括號應予以避免。 值**DSN**關鍵字不能只包含空格，且不能包含前置的空白。 系統資訊的文法，因為關鍵字和資料來源名稱不能包含反斜線 (\\) 字元。  
  
 應用程式不需要將大括號括住屬性值之後,**驅動程式**關鍵字屬性包含分號 （;），除非這種情況下在大括號是必要。 如果驅動程式收到的屬性值包含大括號，驅動程式不應該移除它們，但它們應該傳回的連接字串的一部分。  
  
 括在大括號 （{}） 包含任何字元的 DSN 或連接字串值**[] {} （)，;？\*= ！ @**便會傳遞至驅動程式。 不過，當關鍵字中使用這些字元，驅動程式管理員使用檔案名稱 （dsn） 會傳回錯誤，但將連接字串傳遞至規則的連接字串的驅動程式。 請避免使用內嵌的大括號中關鍵字值。  
  
 連接字串可能包含任意數目的驅動程式定義的關鍵字。 因為**驅動程式**關鍵字不會使用系統資訊的資訊，此驅動程式必須定義足夠的關鍵字，讓驅動程式可以連接到資料來源連接字串中使用的資訊。 （如需詳細資訊，請參閱 < 驅動程式指導方針，> 本節後面）。驅動程式會定義哪些關鍵字，才能連接到資料來源。  
  
 下表描述的屬性值**DSN**， **FILEDSN**，**驅動程式**， **UID**， **PWD**，和**SAVEFILE**關鍵字。  
  
|關鍵字|屬性值描述|  
|-------------|---------------------------------|  
|**資料來源名稱**|所傳回的資料來源名稱**SQLDataSources**或資料來源 對話方塊的**SQLDriverConnect**。|  
|**FILEDSN**|資料來源的.dsn 檔案內建的連接字串的名稱。 檔案資料來源時，會呼叫這些資料來源。|  
|**驅動程式**|描述驅動程式所傳回的**SQLDrivers**函式。 例如，Rdb 或 SQL Server。|  
|**UID**|使用者識別碼。|  
|**PWD**|對應到使用者識別碼或空字串，如果沒有密碼的使用者識別碼的密碼 (PWD =;）。|  
|**利用 SAVEFILE**|.Dsn 檔案應該儲存關鍵字進行存在、 成功連線所使用的屬性值的檔案名稱。|  
  
 應用程式如何選擇資料來源或驅動程式的相關資訊，請參閱[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果連接字串中重複任何關鍵字，驅動程式會使用第一個出現的關鍵字相關聯的值。 如果**DSN**和**驅動程式**相同的連接字串中包含關鍵字、 驅動程式管理員和驅動程式會使用第一個出現任何關鍵字。  
  
 **FILEDSN**和**DSN**關鍵字是互斥： 使用第一個出現任何關鍵字，且出現第二個會被忽略。 **FILEDSN**和**驅動程式**關鍵字，相反地，不會互斥。 如果任何關鍵字出現在連接字串中使用**FILEDSN**，那麼在連接字串關鍵字的屬性值會使用而不是相同的關鍵字.dsn 檔案中的屬性值。  
  
 如果**FILEDSN**關鍵字，則.dsn 檔案中指定的關鍵字用來建立連接字串。 （如需詳細資訊，請參閱 < 檔案資料來源，> 本節後面）。**UID**關鍵字是選擇性的;.dsn 檔案可能以建立只**驅動程式**關鍵字。 **PWD**關鍵字不會儲存在.dsn 檔案。 儲存及載入.dsn 檔案的預設目錄將會是所指定之路徑的組合**CommonFileDir** HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ Windows\CurrentVersion 和"ODBC\DataSources 」 中。 （如果 CommonFileDir"C:\Program Files\Common Files"，預設目錄是 「 C:\Program Files\Common Files\ODBC\Data 來源 」。）  
  
> [!NOTE]  
>  間隔.dsn 檔案可以直接透過呼叫[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)和[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)安裝程式 DLL 中的函式。  
  
 如果**SAVEFILE**關鍵字時，關鍵字進行存在、 成功連線所使用的屬性值會儲存為.dsn 檔案的屬性值的名稱取代**SAVEFILE**關鍵字。 **SAVEFILE**關鍵字必須用於搭配**驅動程式**關鍵字， **FILEDSN**關鍵字，或兩者，或函式會傳回 SQL_SUCCESS_WITH_INFO 與SQLSTATE 01S09 （無效的關鍵字）。 **SAVEFILE**關鍵字必須出現在之前**驅動程式**關鍵字的連接字串或結果會是未定義。  
  
## <a name="driver-manager-guidelines"></a>驅動程式管理員指導方針  
 驅動程式管理員所建構的連接字串將傳遞至驅動程式*InConnectionString*驅動程式的引數**SQLDriverConnect**函式。 驅動程式管理員不會修改*InConnectionString*引數傳遞給它的應用程式。  
  
 動作驅動程式管理員 的值為基礎的*DriverCompletion*引數：  
  
-   SQL_DRIVER_PROMPT： 如果連接字串未包含**驅動程式**， **DSN**，或**FILEDSN**關鍵字，驅動程式管理員會顯示 [資料來源] 對話方塊。 它會建構連接字串從對話方塊所傳回的資料來源名稱和由應用程式傳遞給它的任何其他關鍵字。 驅動程式管理員 對話方塊所傳回的資料來源名稱是空的如果指定的關鍵字-值組 DSN = 預設值。 （這個對話方塊不會顯示具有名稱為 「 預設 」 的資料來源）。  
  
-   SQL_DRIVER_COMPLETE 或 SQL_DRIVER_COMPLETE_REQUIRED： 如果應用程式所指定的連接字串包含**DSN**關鍵字，驅動程式管理員會將複製應用程式所指定的連接字串。 否則，它會將相同的動作當做會*DriverCompletion*為 SQL_DRIVER_PROMPT。  
  
-   SQL_DRIVER_NOPROMPT： 驅動程式管理員會將複製應用程式所指定的連接字串。  
  
 如果應用程式所指定的連接字串包含**驅動程式**關鍵字，驅動程式管理員會將複製應用程式所指定的連接字串。  
  
 使用它已建構的連接字串，驅動程式管理員決定要使用哪一個驅動程式、 連接到該驅動程式，以及將它已建構的連接字串傳遞至驅動程式;驅動程式管理員和驅動程式的互動之相關詳細資訊，請參閱中的 「 註解 」 一節[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)。 如果連接字串不包含**驅動程式**關鍵字，驅動程式管理員會決定哪些驅動程式使用，如下所示：  
  
1.  如果連接字串包含**DSN**關鍵字，驅動程式管理員擷取系統資訊的資料來源相關聯的驅動程式。  
  
2.  如果連接字串不包含**DSN**關鍵字或資料來源找不到，驅動程式管理員擷取系統資訊的預設資料來源相關聯的驅動程式。 (如需詳細資訊，請參閱[預設子機碼](../../../odbc/reference/install/default-subkey.md)。)值變更的驅動程式管理員**DSN**中 「 預設 」 的連接字串關鍵字。  
  
3.  如果**DSN**中的連接字串關鍵字設為 「 預設 」，驅動程式管理員擷取系統資訊的預設資料來源相關聯的驅動程式。  
  
4.  如果找不到資料來源，而且找不到預設的資料來源，驅動程式管理員會傳回 sql_error，其中包含 SQLSTATE IM002 （找不到資料來源並指定預設驅動程式）。  
  
## <a name="file-data-sources"></a>檔案資料來源  
 如果應用程式的呼叫中指定的連接字串**SQLDriverConnect**包含**FILEDSN**關鍵字，且此關鍵字並未被取代之**DSN**或**驅動程式**關鍵字，則驅動程式管理員會建立連接字串使用.dsn 檔案中的資訊和*InConnectionString*引數。 驅動程式管理員程序如下：  
  
1.  檢查.dsn 檔案的檔案名稱是否有效。 如果沒有，它會傳回 sql_error，其中包含 SQLSTATE IM014 （無效的檔案名稱的檔案 DSN）。 如果檔案名稱是空字串 ("") 而且 SQL_DRIVER_NOPROMPT 不指定，則**檔案開啟**對話方塊隨即出現。 如果檔案名稱中包含有效的路徑，但沒有任何檔案名稱或檔名無效，而且未指定 SQL_DRIVER_NOPROMPT，則**檔案開啟**對話方塊會顯示與目前設定為其中的檔案名稱中指定的目錄。 如果檔案名稱是空字串 ("") 或檔案名稱中包含有效的路徑，但沒有任何檔案名稱或檔名無效，並指定 SQL_DRIVER_NOPROMPT 時，然後使用 SQLSTATE IM014 就會傳回 SQL_ERROR （無效的檔案名稱的檔案 DSN）。  
  
2.  讀取.dsn 檔案的 [ODBC] 區段中的所有關鍵字。 如果**驅動程式**關鍵字不存在，它會傳回 sql_error，其中包含 SQLSTATE IM012 （驅動程式關鍵字的語法錯誤），除了其中.dsn 檔案是是非共用，而因此僅包含**DSN**關鍵字。  
  
     如果是非共用檔案資料來源，驅動程式管理員讀取值**DSN**關鍵字，並視需要指向自檔案資料來源的使用者或系統資料來源連接。 不會執行步驟 3 到 5。  
  
3.  建構此驅動程式的連接字串。 驅動程式連接字串是.dsn 檔案中指定的關鍵字和原始的應用程式連接字串中所指定的 union。 驅動程式連接字串關鍵字個重疊的建構函式的規則如下所示：  
  
    -   如果**驅動程式**關鍵字存在於應用程式連接字串和所指定的驅動程式**驅動程式**關鍵字不相同的.dsn 檔案和應用程式連接字串，然後在系統會忽略.dsn 檔案中的驅動程式資訊和應用程式連接字串中的驅動程式資訊時使用。 如果所指定的驅動程式**驅動程式**關鍵字相同.dsn 檔案和應用程式的連接字串，則所有關鍵字都重疊，在應用程式連接字串中所指定的優先順序高於這些.dsn 檔案中指定。  
  
    -   在 新的連接字串**FILEDSN**關鍵字會被刪除。  
  
4.  在登錄項目 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST 中尋找會載入驅動程式。INI\\< 驅動程式名稱\>\Driver 其中\<驅動程式名稱 > 所指定**驅動程式**關鍵字。  
  
5.  將驅動程式傳遞新的連接字串。  
  
 如需.dsn 檔案的範例，請參閱[連接使用的檔案資料來源](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)。  
  
## <a name="savefile-keyword"></a>利用 SAVEFILE 關鍵字  
 如果應用程式所指定的連接字串包含**SAVEFILE**關鍵字，則驅動程式管理員將連接字串儲存於.dsn 檔案。 驅動程式管理員程序如下：  
  
1.  檢查是否.dsn 檔案的檔案名稱包含的屬性值為**SAVEFILE**關鍵字無效。 如果沒有，它會傳回 sql_error，其中包含 SQLSTATE IM014 （無效的檔案名稱的檔案 DSN）。 檔案名稱的有效性取決於標準的系統命名規則。 如果檔案名稱是空字串 ("") 和*DriverCompletion*引數不是 SQL_DRIVER_NOPROMPT，則檔案名稱是否有效。 如果檔案名稱已經存在，則如果*DriverCompletion*為 SQL_DRIVER_NOPROMPT，則會覆寫檔案。 如果*DriverCompletion* SQL_DRIVER_PROMPT、 SQL_DRIVER_COMPLETE 或 SQL_DRIVER_COMPLETE_REQUIRED 時，會出現對話方塊提示使用者指定是否應該覆寫該檔案。 如果不是輸入，然後在**檔案儲存** 對話方塊隨即出現。  
  
2.  如果驅動程式傳回 SQL_SUCCESS，而且找不到檔案名稱是空的字串，則驅動程式管理員寫入中傳回的連接資訊*OutConnectionString*引數中指定的格式與指定的檔案本節稍早的 「 連接字串 」 一節。  
  
3.  如果驅動程式傳回 SQL_SUCCESS，而檔案名稱是空字串 ("")，則驅動程式管理員會呼叫**檔案儲存**通用對話方塊中，與*hwnd*指定，並將連接資訊傳回在*OutConnectionString*本節稍早的 「 連接字串 」 區段中指定的格式與檔案儲存通用對話方塊中指定的檔案。  
  
4.  如果驅動程式傳回 SQL_SUCCESS，它會傳回*OutConnectionString*包含應用程式的連接字串引數。  
  
5.  如果驅動程式會傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR，驅動程式管理員會傳回 SQLSTATE 應用程式。  
  
## <a name="driver-guidelines"></a>驅動程式的指導方針  
 驅動程式會檢查傳遞給它的驅動程式管理員的連接字串是否包含**DSN**或**驅動程式**關鍵字。 如果連接字串包含**驅動程式**關鍵字，驅動程式無法擷取系統資訊的資料來源的相關資訊。 如果連接字串包含**DSN**關鍵字或未包含**DSN**或**驅動程式**關鍵字，驅動程式可以擷取資料來源的相關資訊從系統的資訊，如下所示：  
  
1.  如果連接字串包含**DSN**關鍵字，驅動程式會擷取指定的資料來源的資訊。  
  
2.  如果連接字串不包含**DSN**關鍵字，找不到指定的資料來源，或**DSN**關鍵字設定為 「 預設 」 時，驅動程式會擷取預設資料來源的資訊.  
  
 驅動程式會使用它會從系統資訊來增強連接字串中傳遞給它的資訊擷取任何資訊。 如果系統資訊中的資訊重複的連接字串中的資訊，此驅動程式會使用連接字串中的資訊。  
  
 根據值*DriverCompletion*，驅動程式會提示使用者輸入連接資訊，例如使用者識別碼和密碼，並連接到資料來源：  
  
-   SQL_DRIVER_PROMPT： 驅動程式會顯示一個對話方塊，使用做為初始的值中的連接字串和系統資訊的值 （如果有的話）。 當使用者結束對話方塊中時，驅動程式會連接到資料來源。 它也會建構連接字串的值從**DSN**或**驅動程式**關鍵字\* *InConnectionString*和從傳回的資訊對話方塊。 在此連接字串就會將 **OutConnectionString*緩衝區。  
  
-   SQL_DRIVER_COMPLETE 或 SQL_DRIVER_COMPLETE_REQUIRED： 如果連接字串包含足夠的資訊，且該資訊正確，驅動程式會連接到資料來源和複製\* *InConnectionString*至\* *OutConnectionString*。 如果任何資訊遺失或不正確，驅動程式會將相同的動作會當做*DriverCompletion*為 SQL_DRIVER_PROMPT，除非該*DriverCompletion*是 SQL_DRIVER_COMPLETE_所需，驅動程式會停用不需要連接到資料來源的任何資訊的控制項。  
  
-   SQL_DRIVER_NOPROMPT： 如果連接字串包含足夠的資訊，此驅動程式會連接到資料來源和複製\* *InConnectionString*至\* *OutConnectionString*. 否則，驅動程式會傳回 SQL_ERROR，如**SQLDriverConnect**。  
  
 在成功連接到資料來源之後，驅動程式也會設定\* *StringLength2Ptr*可用來傳回中輸出連接字串的長度 **OutConnectionString*。  
  
 如果使用者取消驅動程式管理員] 或 [驅動程式時，所顯示的對話方塊**SQLDriverConnect**傳回 sql_no_data 為止。  
  
 如需驅動程式管理員和驅動程式在連線程序互動的方式，請參閱[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
 如果驅動程式支援**SQLDriverConnect**，驅動程式的系統資訊的驅動程式關鍵字區段必須包含**ConnectFunctions**關鍵字與第二個字元設為"Y"。  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>連接時啟用了連接共用  
 連接共用可讓應用程式重複使用已建立的連線。 當**SQLDriverConnect**呼叫時，則驅動程式管理員會嘗試進行連接使用屬於指定給連接共用的環境中的連接集區的連接。 如需連接共用的詳細資訊，請參閱[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
 應用程式可以設定 SQL_ATTR_RESET_CONNECTION 位置啟用共用的連接上呼叫 SQLDisconnect 之前。 如需詳細資訊，請參閱[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 當應用程式呼叫時，適用下列限制**SQLDriverConnect**連接到共用的連接：  
  
-   沒有連接共用處理執行時**SAVEFILE**關鍵字指定連接字串中。  
  
-   如果已啟用連接共用， **SQLDriverConnect**可以只使用呼叫*DriverCompletion* SQL_DRIVER_NOPROMPT 引數; 如果**SQLDriverConnect**稱為與任何其他*DriverCompletion*，SQLSTATE HY110 會傳回 （不正確的驅動程式完成）。  
  
## <a name="connection-attributes"></a>連接屬性  
 使用所設定的 SQL_ATTR_LOGIN_TIMEOUT 連接屬性**SQLSetConnectAttr**，定義要等候的驅動程式所完成成功連接後再傳回至應用程式的登入要求的秒數。 如果系統會提示使用者完成連接字串，每個登入要求的等待期間開始時啟動的驅動程式的連線程序。  
  
 驅動程式預設會開啟連接 SQL_MODE_READ_WRITE 存取模式。 若要設定 SQL_MODE_READ_ONLY 存取模式，應用程式必須呼叫**SQLSetConnectAttr** SQL_ATTR_ACCESS_MODE 屬性，然後才呼叫**SQLDriverConnect**。  
  
 如果在資料來源的系統資訊中指定預設轉譯程式庫，則驅動程式會載入它。 可以藉由呼叫載入不同轉譯程式庫**SQLSetConnectAttr** SQL_ATTR_TRANSLATE_LIB 屬性。 轉譯選項可以指定藉由呼叫**SQLSetConnectAttr** SQL_ATTR_TRANSLATE_OPTION 選項。  
  
 如需詳細資訊，請參閱[使用 SQLDriverConnect 連接](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)。  
  
```  
// SQLDriverConnect_ref.cpp  
// compile with: odbc32.lib user32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR OutConnStr[255];  
   SQLSMALLINT OutConnStrLen;  
  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            retcode = SQLDriverConnect( // SQL_NULL_HDBC  
               hdbc,   
               desktopHandle,   
               (SQLCHAR*)"driver=SQL Server",   
               _countof("driver=SQL Server"),  
               OutConnStr,  
               255,   
               &OutConnStrLen,  
               SQL_DRIVER_PROMPT );  
  
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
  
 另請參閱[範例 ODBC 程式](../../../odbc/reference/sample-odbc-program.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|配置控制代碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|探索和列舉值連接到資料來源所需|[SQLBrowseConnect 函式](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|連接到資料來源|[SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|從資料來源中斷連線|[SQLDisconnect 函式](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|傳回的驅動程式描述和屬性|[SQLDrivers 函式](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|釋放控制代碼|[SQLFreeHandle 函式](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函式](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)

