---
title: "SQLBrowseConnect 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLBrowseConnect
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLBrowseConnect
helpviewer_keywords: SQLBrowseConnect function [ODBC]
ms.assetid: b7f1be66-e6c7-4790-88ec-62b7662103c0
caps.latest.revision: "36"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 839cf9ec1e802d0bce8da8cc0134bf89b0646bb2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="sqlbrowseconnect-function"></a>SQLBrowseConnect 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ODBC  
  
 **摘要**  
 **SQLBrowseConnect**支援反覆方法探索，並列舉的屬性和連接到資料來源所需的屬性值。 每次呼叫**SQLBrowseConnect**傳回後續的層級的屬性和屬性值。 當已經列舉所有層級、 資料來源的連接完成並傳回完整的連線字串**SQLBrowseConnect**。 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 傳回碼表示已指定所有連接資訊，而且應用程式現在已連線到資料來源。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLBrowseConnect(  
     SQLHDBC         ConnectionHandle,  
     SQLCHAR *       InConnectionString,  
     SQLSMALLINT     StringLength1,  
     SQLCHAR *       OutConnectionString,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLength2Ptr);  
```  
  
## <a name="arguments"></a>引數  
 *ConnectionHandle*  
 [輸入]連接控制代碼。  
  
 *InConnectionString*  
 [輸入]瀏覽要求連接字串 (請參閱 「*InConnectionString*引數 」 中的 [意見])。  
  
 *StringLength1*  
 [輸入]長度 **InConnectionString*以字元為單位。  
  
 *OutConnectionString*  
 [輸出]這是要傳回瀏覽結果連接字串中字元緩衝區的指標 (請參閱"*OutConnectionString*引數 」 中 [意見])。  
  
 如果*OutConnectionString*是 NULL， *StringLength2Ptr*仍會傳回的總字元數 （不含字元資料 null 結束字元） 可用來傳回緩衝區中所指*OutConnectionString*。  
  
 *Columnsize*  
 [輸入]長度，以字元為單位的 **OutConnectionString*緩衝區。  
  
 *StringLength2Ptr*  
 [輸出]的總字元數 （不含 null 終止） 可用來傳回中\* *OutConnectionString*。 可傳回的字元數目是否大於或等於*Columnsize*中的連接字串\* *OutConnectionString*會被截斷成*Columnsize*減去 null 結束字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NEED_DATA、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLBrowseConnect**傳回 SQL_ERROR、 SQL_SUCCESS_WITH_INFO 或 SQL_NEED_DATA，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType*利用 SQL_HANDLE_STMT 的和*ConnectionHandle 的控制代碼*。 下表列出通常所傳回的 SQLSTATE 值**SQLBrowseConnect** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|緩衝區\* *OutConnectionString*仍不夠大，無法傳回整個瀏覽結果連接字串，所以已截斷字串。 緩衝區 **StringLength2Ptr*包含未截斷的瀏覽結果連接字串的長度。 （函式會傳回 SQL_NEED_DATA）。|  
|01S00|無效的連接字串屬性|瀏覽要求的連接字串中指定無效的屬性關鍵字 (*InConnectionString*)。 （函式會傳回 SQL_NEED_DATA）。<br /><br /> 瀏覽要求的連接字串中指定一個屬性的關鍵字 (*InConnectionString*) 時，不適用於目前的連接層級。 （函式會傳回 SQL_NEED_DATA）。|  
|01S02 的警告|值已變更|驅動程式不支援指定的值*ValuePtr*引數中的**SQLSetConnectAttr**置換相似的值。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08001|無法建立連線的用戶端|驅動程式無法建立與資料來源的連接。|  
|08002|使用中的連接名稱|(DM) 指定的連接必須已經用來建立與資料來源的連接和連接為開啟。|  
|08004|伺服器拒絕連線|資料來源的拒絕連線的建立實作定義理由。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式的驅動程式在嘗試連接資料來源之間的通訊連結失敗。|  
|28000|無效的授權規格|使用者識別碼或授權字串，或兩者都指定在瀏覽要求的連接字串 (*InConnectionString*)，違反了資料來源所定義的限制。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|(DM) 驅動程式管理員無法配置記憶體，才能支援執行或完成的函式。<br /><br /> 驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY008|已取消操作|已取消非同步作業，藉由呼叫[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)。 然後，原始函式一次上呼叫*ConnectionHandle*。<br /><br /> 已取消作業，藉由呼叫**SQLCancelHandle**上*ConnectionHandle*從不同的執行緒在多執行緒應用程式。|  
|HY010|函數順序錯誤|以非同步方式執行的函式 （不是這一個） 已呼叫 (DM) *ConnectionHandle*和還在執行時呼叫此函式。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY090|字串或緩衝區長度無效|(DM) 引數指定的值*StringLength1*小於 0，且不等於 SQL_NTS。<br /><br /> (DM) 引數指定的值*Columnsize*小於 0。|  
|HY114|驅動程式不支援連接層級的非同步函式執行|(DM) 應用程式啟用連接控制代碼上非同步作業之前建立的連接。 不過，驅動程式不支援連接控制代碼上的非同步作業。|  
|HYT00|已超過逾時的設定|登入逾時期限過期之前完成資料來源的連接。 逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_LOGIN_TIMEOUT。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 對應到指定的資料來源名稱的驅動程式不支援此函式。|  
|IM002|找不到資料來源並指定預設驅動程式|(DM) 的資料來源瀏覽要求的連接字串中指定的名稱 (*InConnectionString*) 找不到在系統資訊，或是否有預設的驅動程式規格。<br /><br /> (DM) 的系統資訊中找不到 ODBC 資料來源及預設驅動程式的資訊。|  
|IM003|無法載入指定的驅動程式|(DM) 驅動程式的系統資訊的資料來源規格中所列，或所指定**驅動程式**關鍵字找不到或無法載入某些其他原因。|  
|IM004|驅動程式的**SQLAllocHandle**上 SQL_HANDLE _ENV 失敗|(DM) 期間**SQLBrowseConnect**，稱為 「 驅動程式的驅動程式管理員**SQLAllocHandle**函式與*HandleType* SQL_HANDLE_ENV 和驅動程式傳回發生錯誤。|  
|IM005|驅動程式的**SQLAllocHandle**上利用 SQL_HANDLE_DBC 失敗|(DM) 期間**SQLBrowseConnect**，稱為 「 驅動程式的驅動程式管理員**SQLAllocHandle**函式與*HandleType*利用 SQL_HANDLE_DBC 的驅動程式傳回發生錯誤。|  
|IM006|驅動程式的**SQLSetConnectAttr**失敗|(DM) 期間**SQLBrowseConnect**，稱為 「 驅動程式的驅動程式管理員**SQLSetConnectAttr**函式和驅動程式傳回錯誤。|  
|IM009|無法載入轉譯 DLL|驅動程式無法載入轉譯 DLL 所指定資料來源或連接。|  
|IM010|資料來源名稱太長|(DM) DSN 關鍵字的屬性值已超過 SQL_MAX_DSN_LENGTH 個字元。|  
|IM011|驅動程式名稱太長|(DM) 驅動程式關鍵字的屬性值已超過 255 個字元。|  
|IM012|驅動程式關鍵字的語法錯誤|(DM) 驅動程式關鍵字的關鍵字-值配對包含語法錯誤。|  
|IM014|指定的資料來源名稱包含驅動程式和應用程式之間的架構不相符|(DM) 32 位元應用程式使用的 DSN 連接至 64 位元驅動程式。反之亦然。|  
|IM017|中的非同步通知模式已停用輪詢|每當通知模型使用時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，且如果已啟用通知模式， **SQLCompleteAsync**必須在後續處理作業，並完成此作業的控制代碼上呼叫。|  
|S1118|驅動程式不支援非同步通知|當驅動程式不支援非同步通知時，您無法對 SQL_ATTR_ASYNC_DBC_EVENT 或 SQL_ATTR_ASYNC_DBC_RETCODE_PTR 進行設定。|  
  
## <a name="inconnectionstring-argument"></a>InConnectionString 引數  
 瀏覽要求的連接字串的語法如下：  
  
 *連接字串*:: =*屬性*[;] &#124;*屬性*;*連接 stringattribute* :: =*屬性關鍵字*=*屬性值*&#124;驅動程式 = [{]*屬性值 [*}]*屬性關鍵字*:: = DSN &#124;UID &#124;PWD &#124;*驅動程式-定義-屬性-keywordattribute-值*:: =*字元-stringdriver-定義-屬性-關鍵字*:: =*識別碼*  
  
 其中*字元字串*有零個或多個字元。*識別碼*有一或多個字元。*屬性關鍵字*不區分大小寫。*屬性值*可能會區分大小寫，以及值**DSN**關鍵字並沒有包含單獨的空白個數。 因為連接字串和初始設定檔案文法、 關鍵字和屬性值包含字元**[] {} （)，;？\*= ！ @**應該予以避免。 在 系統資訊的文法，因為關鍵字和資料來源名稱不能包含反斜線 (\\) 字元。 ODBC 2。*x*驅動程式，驅動程式關鍵字的屬性值前後需要加括號。  
  
 如果瀏覽要求的連接字串中重複任何關鍵字，驅動程式會使用第一個出現的關鍵字相關聯的值。 如果**DSN**和**驅動程式**關鍵字包含在相同的瀏覽要求連接字串、 驅動程式管理員和驅動程式會使用第一個出現任何關鍵字。  
  
 應用程式如何選擇資料來源或驅動程式的相關資訊，請參閱[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
## <a name="outconnectionstring-argument"></a>OutConnectionString 引數  
 瀏覽結果連接字串是連接屬性的清單。 連接屬性是由屬性關鍵字和對應的屬性值所組成。 瀏覽結果連接字串的語法如下：  
  
 *連接字串*:: =*屬性*[;] &#124;*屬性*;*連接 stringattribute* :: = [\*]*屬性關鍵字 = 屬性 valueattribute 關鍵字*:: = *ODBC 屬性關鍵字*&#124;*driver-defined-attribute-keywordODBC-attribute-keyword* = {UID &#124;PWD} [:*當地語系化識別碼*]*驅動程式-定義-屬性-關鍵字*:: =*識別碼*[:*當地語系化識別碼*]*屬性值*:: = {*屬性值清單*} &#124; 嗎？ （大括號是常值，驅動程式傳回）。*屬性值清單*:: =*字元字串*[:*當地語系化的字元字串*] &#124;*字元字串*[:*當地語系化的字元字串*]，*屬性值清單*  
  
 其中*字元字串*和*當地語系化的字元字串*有零個或多個字元。*識別碼*和*當地語系化識別碼*有一或多個字元。*屬性關鍵字*不區分大小寫; 和*屬性值*可能區分大小寫。 因為連接字串和初始設定檔案文法、 關鍵字、 當地語系化的識別項，與屬性值包含字元**[] {} （)，;？\*= ！ @**應該予以避免。 在 系統資訊的文法，因為關鍵字和資料來源名稱不能包含反斜線 (\\) 字元。  
  
 瀏覽結果連接字串語法是根據下列的語意規則：  
  
-   如果使用星號 (\*) 位於*屬性關鍵字*、*屬性*是選擇性的而且可以在下一個呼叫中省略**SQLBrowseConnect**。  
  
-   屬性關鍵字**UID**和**PWD**中所定義，具有相同的意義**SQLDriverConnect**。  
  
-   A*驅動程式-定義-屬性-關鍵字*名稱可能會提供屬性值之屬性的種類。 例如，它可能是**伺服器**，**資料庫**，**主機**，或**DBMS**。  
  
-   *ODBC 屬性關鍵字*和*驅動程式-定義-屬性-關鍵字*包含關鍵字的當地語系化或易記版本。 這可能會使用應用程式做為對話方塊中的標籤。 不過， **UID**， **PWD**，或*識別碼*單獨時，必須使用瀏覽要求字串傳遞至驅動程式。  
  
-   {*屬性值清單*} 無效，實際值的列舉型別對應*屬性關鍵字*。 請注意，大括號 （{}） 不會指出選項; 清單則會傳回由驅動程式。 例如，它可能是伺服器名稱的清單或清單的資料庫名稱。  
  
-   如果*屬性值*是一個單一的問號 （？），單一值會對應至*屬性關鍵字*。 例如，UID = JohnS;PWD = 色的芝麻。  
  
-   每次呼叫**SQLBrowseConnect**傳回只有滿足的連線程序的下一個層級所需的資訊。 驅動程式將使的內容一律可以決定在每次呼叫，與連接控制代碼關聯狀態資訊。  
  
## <a name="using-sqlbrowseconnect"></a>使用 SQLBrowseConnect  
 **SQLBrowseConnect**需要配置的連接。 驅動程式管理員會載入驅動程式中指定，或對應至初始瀏覽要求連接字串; 中指定的資料來源名稱當發生這種情況的相關資訊，請參閱中的 「 註解 」 一節[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)。 驅動程式可能會建立在瀏覽處理序與資料來源連接。 如果**SQLBrowseConnect**會傳回 SQL_ERROR，未處理的連接都會結束，而且連接會傳回到未連接的狀態。  
  
> [!NOTE]  
>  **SQLBrowseConnect**不支援連接共用。 如果**SQLBrowseConnect**時啟用連接共用時，會呼叫 SQLSTATE HY000 （一般的錯誤） 會傳回。  
  
 當**SQLBrowseConnect**稱為瀏覽要求的連接字串必須包含在連接上第一次， **DSN**關鍵字或**驅動程式**關鍵字。 如果瀏覽要求的連接字串包含**DSN**關鍵字，驅動程式管理員在 系統資訊中找出對應的資料來源規格：  
  
-   如果驅動程式管理員會尋找對應的資料來源規格，則會載入相關聯的驅動程式 DLL。驅動程式可以擷取系統資訊的資料來源的相關資訊。  
  
-   如果驅動程式管理員找不到對應的資料來源規格，它會找出預設資料來源的規格，並載入相關聯的驅動程式 DLL;驅動程式可以擷取系統資訊的預設資料來源的相關資訊。 「 預設 」 會傳遞至驅動程式之 dsn。  
  
-   如果驅動程式管理員找不到對應的資料來源規格，而且沒有任何預設資料來源的規格，它會傳回 sql_error，其中包含 SQLSTATE IM002 （找不到資料來源並指定預設驅動程式）。  
  
 如果瀏覽要求的連接字串包含**驅動程式**關鍵字，驅動程式管理員會載入指定的驅動程式; 它不會嘗試尋找資料來源中的系統資訊。 因為**驅動程式**關鍵字不使用系統資訊的資訊、 驅動程式必須定義足夠的關鍵字，讓驅動程式可以連接到資料來源瀏覽要求的連接字串中使用的資訊。  
  
 每次呼叫**SQLBrowseConnect**，應用程式瀏覽要求的連接字串中指定的連接屬性值。 驅動程式會傳回連續層級的屬性和屬性值中瀏覽結果連接字串。只要尚未列舉瀏覽要求的連接字串中的連接屬性，它會傳回 SQL_NEED_DATA。 應用程式會使用瀏覽結果連接字串的內容來建置瀏覽要求的連接字串的下一個呼叫**SQLBrowseConnect**。 所有必要的屬性 (未加上星號中那些*OutConnectionString*引數) 必須包含在下次呼叫**SQLBrowseConnect**。 請注意應用程式在建置目前的瀏覽要求連接字串; 時，無法使用先前瀏覽結果連接字串的內容也就是說，不能指定不同的值，在先前的層級中設定的屬性。  
  
 當已經列舉所有層級的連接和其相關聯的屬性時，驅動程式傳回 SQL_SUCCESS、 資料來源的連接已完成且完整的連接字串會傳回到應用程式。 連接字串是適合用來搭配使用**SQLDriverConnect**，SQL_DRIVER_NOPROMPT 選項來建立另一個連接。 完整的連接字串不能在另一個呼叫**SQLBrowseConnect**，不過，如果**SQLBrowseConnect**再次呼叫，將整個之呼叫的序列可能會重複。  
  
 **SQLBrowseConnect**如果在瀏覽處理序; 例如，無效密碼或應用程式所提供的屬性關鍵字發生可復原的、 非嚴重錯誤也會傳回 SQL_NEED_DATA。 時，會傳回 SQL_NEED_DATA 和瀏覽結果連線字串並未變更，發生錯誤以及應用程式可以呼叫**SQLGetDiagRec**来傳回的 SQLSTATE 瀏覽時間錯誤。 這可讓以更正該屬性，並繼續瀏覽應用程式。  
  
 應用程式可以終止隨時瀏覽處理序藉由呼叫**SQLDisconnect**。 驅動程式將會終止任何未處理的連接，並將連接傳回未連接的狀態。  
  
 如果非同步作業已啟用連接控制代碼上**SQLBrowseConnect**也可能會傳回 SQL_STILL_EXECUTING。 應用程式時，它會傳回 SQL_NEED_DATA，必須使用**SQLDisconnect**取消瀏覽程序。 如果**SQLBrowseConnect**傳回 SQL_STILL_EXECUTING，應用程式應該使用**SQLCancelHandle**取消進行中的作業。 呼叫**SQLCancelHandle**之後函式會傳回 SQL_NEED_DATA 沒有任何作用。  
  
 如需詳細資訊，請參閱[連接 SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)。  
  
 如果驅動程式支援**SQLBrowseConnect**，驅動程式的系統資訊中的驅動程式關鍵字區段必須包含**ConnectFunctions**關鍵字與第三個字元設為"Y"。  
  
## <a name="code-example"></a>程式碼範例  
  
> [!NOTE]  
>  如果您要連接至資料來源提供者支援 Windows 驗證，您應該指定`Trusted_Connection=yes`而不是在連接字串中的使用者識別碼和密碼資訊。  
  
 在下列範例中，應用程式呼叫**SQLBrowseConnect**重複。 每次**SQLBrowseConnect**傳回 SQL_NEED_DATA，它會傳回它所需之資料的相關資訊的傳遞\* *OutConnectionString*。 在應用程式通過*OutConnectionString*其常式**GetUserInput** （未顯示）。 **GetUserInput**剖析資訊、 建置和顯示對話方塊，並傳回在使用者所輸入的資訊\* *InConnectionString*。 應用程式會將使用者的資訊傳遞到下一個呼叫中的驅動程式**SQLBrowseConnect**。 應用程式有提供需要的驅動程式連接到資料來源，所有資訊之後**SQLBrowseConnect**傳回 SQL_SUCCESS 和應用程式會繼續。  
  
 如需更詳細的連接到 SQL Server 驅動程式，藉由呼叫範例**SQLBrowseConnect**，請參閱[SQL Server 瀏覽範例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)。  
  
 例如，若要連接至資料來源銷售，下列動作可能會發生。 首先，應用程式傳遞到下列字串**SQLBrowseConnect**:  
  
```  
"DSN=Sales"  
```  
  
 驅動程式管理員會載入驅動程式與資料來源銷售相關聯。 然後它會呼叫驅動程式的**SQLBrowseConnect**它收到來自應用程式的相同引數的函式。 驅動程式會傳回下列字串中的 **OutConnectionString*:  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 應用程式傳遞此字串，以便其**GetUserInput**常式，哪些組建的對話方塊，詢問使用者選取紅色、 藍色或綠色的伺服器，並輸入使用者識別碼和密碼。 常式傳遞的使用者指定的下列資訊回\* *InConnectionString*，這在應用程式傳遞給**SQLBrowseConnect**:  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect**使用這項資訊連接到紅色伺服器為 Smith 色的芝麻，密碼，則會傳回下列字串中的 **OutConnectionString*:  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 應用程式傳遞此字串，以便其**GetUserInput**常式，哪些組建的對話方塊，詢問使用者是否要選取的資料庫。 使用者選取 empdata 和應用程式會呼叫**SQLBrowseConnect**與這個字串的最後一次：  
  
```  
"DATABASE=SalesOrders"  
```  
  
 這是最後一則資訊驅動程式必須連接到資料來源;**SQLBrowseConnect**都會傳回 SQL_SUCCESS，和 **OutConnectionString*包含完整的連接字串：  
  
```  
// SQLBrowseConnect_Function.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define BRWS_LEN 100  
SQLHENV henv;  
SQLHDBC hdbc;  
SQLHSTMT hstmt;  
SQLRETURN retcode;  
SQLCHAR szConnStrIn[BRWS_LEN], szConnStrOut[BRWS_LEN];  
SQLSMALLINT cbConnStrOut;  
  
void GetUserInput(SQLCHAR * szConnStrOut, SQLCHAR * szConnStrIn) {}  
  
int main() {  
   // Allocate the environment handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);        
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
      // Set the version environment attribute.  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
         // Allocate the connection handle.  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            // Call SQLBrowseConnect until it returns a value other than SQL_NEED_DATA   
            // (pass data source name the first time).  If SQL_NEED_DATA is returned, call GetUserInput   
            // (not shown) to build a dialog from the values in szConnStrOut.  The user-supplied values   
            // are returned in szConnStrIn, which is passed in the next call to SQLBrowseConnect.  
  
            strcpy_s((char*)szConnStrIn, _countof(szConnStrIn), "DSN=Sales");  
            do {  
               retcode = SQLBrowseConnect(hdbc, szConnStrIn, SQL_NTS,  
                  szConnStrOut, BRWS_LEN, &cbConnStrOut);  
               if (retcode == SQL_NEED_DATA)  
                  GetUserInput(szConnStrOut, szConnStrIn);  
            } while (retcode == SQL_NEED_DATA);  
  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
               // Allocate the statement handle.  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                  // Process data after successful connection  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               SQLDisconnect(hdbc);  
            }  
         }  
         SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
      }  
   }  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|配置連接控制代碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|連接到資料來源|[SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|從資料來源中斷連線|[SQLDisconnect 函式](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|連接到資料來源使用的連接字串或對話方塊方塊|[SQLDriverConnect 函式](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|傳回的驅動程式描述和屬性|[SQLDrivers 函式](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|釋放連接控制代碼|[SQLFreeHandle 函式](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>請參閱＜  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
