---
description: SQLBrowseConnect 函數
title: SQLBrowseConnect 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBrowseConnect
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBrowseConnect
helpviewer_keywords:
- SQLBrowseConnect function [ODBC]
ms.assetid: b7f1be66-e6c7-4790-88ec-62b7662103c0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 712dbb366e25098c7956ffbb9c8733a437339297
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499631"
---
# <a name="sqlbrowseconnect-function"></a>SQLBrowseConnect 函數
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ODBC  
  
 **總結**  
 **SQLBrowseConnect** 支援一種反復的方法，來探索和列舉連接到資料來源所需的屬性和屬性值。 每次呼叫 **SQLBrowseConnect** 時，都會傳回屬性和屬性值的連續層級。 列舉所有層級之後，就會完成與資料來源的連接，而且 **SQLBrowseConnect**會傳回完整的連接字串。 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 的傳回碼表示已指定所有連接資訊，而且應用程式現在已連接至資料來源。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
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
 [輸入] 連線控制代碼。  
  
 *InConnectionString*  
 輸出流覽要求連接字串 (請參閱「批註」 ) 中的「*InConnectionString* 引數」。  
  
 *StringLength1*  
 輸出**InConnectionString* 的長度（以字元為單位）。  
  
 *OutConnectionString*  
 出要在其中傳回流覽結果連接字串之字元緩衝區的指標 (請參閱「批註」 ) 中的「*OutConnectionString* 引數」。  
  
 如果 *OutConnectionString* 是 Null， *StringLength2Ptr* 仍會傳回字元總數 (排除字元資料的 Null 終止字元) 可在 *OutConnectionString*所指向的緩衝區中傳回。  
  
 *BufferLength*  
 輸出**OutConnectionString* 緩衝區的長度（以字元為單位）。  
  
 *StringLength2Ptr*  
 出 (排除 null 終止) 可在 OutConnectionString 中傳回的字元總數 \* * *。 如果可傳回的字元數大於或等於*BufferLength*，OutConnectionString 中的連接字串 \* *OutConnectionString*會截斷為*BufferLength*減去 null 終止字元的長度。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_ERROR、SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLBrowseConnect**傳回 SQL_ERROR、SQL_SUCCESS_WITH_INFO 或 SQL_NEED_DATA 時，可以藉由呼叫 SQLGetDiagRec 和*HandleType* SQL_HANDLE_STMT 的**SQLGetDiagRec**以及*ConnectionHandle 的控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLBrowseConnect** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01004|字串資料，右邊已截斷|緩衝區 \* *OutConnectionString*不夠大，無法傳回整個流覽結果連接字串，因此字串已被截斷。 Buffer **StringLength2Ptr* 包含 untruncated 流覽結果連接字串的長度。  (函數會傳回 SQL_NEED_DATA。 ) |  
|01S00|不正確連接字串屬性|在流覽要求連接字串中指定了不正確 attribute 關鍵字 (*InConnectionString*) 。  (函數會傳回 SQL_NEED_DATA。 ) <br /><br /> 在流覽要求連接字串中指定了 attribute 關鍵字， (*InConnectionString*) 不會套用至目前的連接層級。  (函數會傳回 SQL_NEED_DATA。 ) |  
|01S02|值已變更|驅動程式不支援在**SQLSetConnectAttr**中指定的*ValuePtr*引數值，並取代類似的值。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|08001|用戶端無法建立連接|驅動程式無法建立與資料來源的連接。|  
|08002|使用中的連接名稱| (DM) 指定的連接已經用來建立與資料來源的連接，且連接已開啟。|  
|08004|伺服器拒絕連接|資料來源因為執行定義的原因而拒絕建立連接。|  
|08S01|通訊連結失敗|在函數完成處理之前，驅動程式與驅動程式嘗試連接的資料來源之間的通訊連結失敗。|  
|28000|不正確授權規格|使用者識別碼或授權字串（或兩者）（如流覽要求連接字串中所指定 (*InConnectionString*) ）違反了資料來源所定義的限制。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤| (DM) 驅動程式管理員無法配置支援執行或完成函式所需的記憶體。<br /><br /> 驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY008|已取消作業|藉由呼叫 [SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)函式來取消非同步作業。 然後，在 *ConnectionHandle*上再次呼叫原始函數。<br /><br /> 從多執行緒應用程式中的不同執行緒呼叫*ConnectionHandle*上的**SQLCancelHandle** ，以取消作業。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式 (不是針對 *ConnectionHandle* 呼叫這個) ，而且在呼叫此函式時仍在執行。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY090|不正確字串或緩衝區長度| (DM) 引數 *StringLength1* 指定的值小於0且不等於 SQL_NTS。<br /><br />  (DM) 引數 *BufferLength* 指定的值小於0。|  
|HY114|驅動程式不支援連接層級的非同步函式執行| (DM) 應用程式在進行連接之前，已啟用連接控制碼上的非同步作業。 不過，驅動程式不支援在連接控制碼上進行非同步作業。|  
|HYT00|已超過逾時的設定|資料來源連接完成之前，登入超時時間已過期。 Timeout 期限是透過 **SQLSetConnectAttr**、SQL_ATTR_LOGIN_TIMEOUT 設定。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 對應至指定資料來源名稱的驅動程式不支援此函數。|  
|IM002|找不到資料來源，且未指定預設驅動程式| (DM) 在系統資訊中找不到流覽要求連接字串中所指定的資料來源名稱 (*InConnectionString*) ，也沒有預設的驅動程式規格。<br /><br /> 在系統資訊中找不到 (DM) ODBC 資料來源和預設驅動程式資訊。|  
|IM003|無法載入指定的驅動程式| (DM) 在系統資訊中所列的驅動程式，或由 **驅動程式** 關鍵字指定的驅動程式，找不到或因為某些其他原因而無法載入。|  
|IM004|SQL_HANDLE _ENV 上的驅動程式 **SQLAllocHandle** 失敗|在 **SQLBrowseConnect**期間 (DM) ，驅動程式管理員會呼叫驅動程式的 **SQLAllocHandle** 函式，並使用 *HandleType* 的 SQL_HANDLE_ENV，而驅動程式會傳回錯誤。|  
|IM005|SQL_HANDLE_DBC 上的驅動程式 **SQLAllocHandle** 失敗|在 **SQLBrowseConnect**期間 (DM) ，驅動程式管理員會呼叫驅動程式的 **SQLAllocHandle** 函式，並使用 *HandleType* 的 SQL_HANDLE_DBC，而驅動程式會傳回錯誤。|  
|IM006|驅動程式的 **SQLSetConnectAttr** 失敗|在 **SQLBrowseConnect**期間 (DM) ，驅動程式管理員會呼叫驅動程式的 **SQLSetConnectAttr** 函式，而驅動程式會傳回錯誤。|  
|IM009|無法載入轉譯 DLL|驅動程式無法載入為數據源或連接所指定的轉譯 DLL。|  
|IM010|資料來源名稱太長| (DM) DSN 關鍵字的屬性值超過 SQL_MAX_DSN_LENGTH 個字元。|  
|IM011|驅動程式名稱太長| (DM) 驅動程式關鍵字的屬性值超過255個字元。|  
|IM012|驅動程式關鍵字語法錯誤| (DM) DRIVER 關鍵字的關鍵字-值組包含語法錯誤。|  
|IM014|指定的 DSN 包含驅動程式和應用程式之間的架構不相符| (DM) 32 位應用程式使用連接到64位驅動程式的 DSN;反之亦然。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，而且如果啟用了通知模式，則必須在控制碼上呼叫 **SQLCompleteAsync** ，以進行後置處理，並完成作業。|  
|S1118|驅動程式不支援非同步通知|當驅動程式不支援非同步通知時，您無法設定 SQL_ATTR_ASYNC_DBC_EVENT 或 SQL_ATTR_ASYNC_DBC_RETCODE_PTR。|  
  
## <a name="inconnectionstring-argument"></a>InConnectionString 引數  
 流覽要求連接字串具有下列語法：  
  
 *connection-string* ：： = *attribute*[ `;` ] &#124; *屬性* `;` *連接-字串*;<br>
 *attribute* ：： = *attribute-關鍵字* `=` *屬性-value* &#124; `DRIVER=` [ `{` ]*attribute-value*[ `}` ]<br>
 *attribute-關鍵字* ：： = `DSN` &#124; `UID` &#124; `PWD` &#124; *驅動程式定義-attribute-關鍵字*<br>
 *屬性-值* ：： = *字元-字串*<br>
 *驅動程式定義-attribute-關鍵字* ：： = *識別碼*<br>
  
 其中 *字元字串* 包含零或多個字元; *識別碼* 有一或多個字元; *attribute-關鍵字* 不區分大小寫; *屬性-值* 可能會區分大小寫;而 **DSN** 關鍵字的值並不只包含空白。 由於連接字串和初始化檔文法，包含字元 [] 的關鍵字和屬性值 ** {} ( # A1，;？ \*=！ @** 應予以避免。 由於系統資訊中的文法，關鍵字和資料來源名稱不能包含反斜線 (\\) 字元。 適用于 ODBC 2。*x* 驅動程式，驅動程式關鍵字的屬性值周圍需要有大括弧。  
  
 如果在流覽要求連接字串中重複出現任何關鍵字，驅動程式會使用與第一次出現關鍵字相關聯的值。 如果 **DSN** 和 **驅動程式** 關鍵字包含在相同的流覽要求連接字串中，驅動程式管理員和驅動程式就會使用第一個出現的任何關鍵字。  
  
 如需應用程式如何選擇資料來源或驅動程式的相關資訊，請參閱 [選擇資料來源或驅動](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)程式。  
  
## <a name="outconnectionstring-argument"></a>OutConnectionString 引數  
 [流覽結果連接字串] 是連接屬性的清單。 連接屬性是由 attribute 關鍵字和對應的屬性值所組成。 流覽結果連接字串的語法如下：  
  
 *connection-string* ：： = *attribute*[ `;` ] &#124; *屬性* `;` *連接-字串*<br>
 *attribute* ：： = [ `*` ]*attribute-關鍵字* `=` *屬性-值*<br>
 *attribute-關鍵字* ：： = *ODBC-attribute-關鍵字* &#124; *驅動程式定義-attribute-關鍵字*<br>
 *ODBC-attribute-關鍵字*= { `UID` &#124; `PWD` } [ `:` *當地語系化識別碼*]*驅動程式定義-attribute-關鍵字*：： = *identifier*[ `:` *當地語系化識別碼*]*屬性-value* ：： = `{` *屬性-值清單* `}` &#124; `?` (大括弧是常值; 驅動程式會傳回它們。 ) <br>
 *attribute-value-list* ：： = *character 字串*[ `:` *當地語系化的字元字串*] &#124;*字元*字串 [ `:` *當地語系化的字元字串*] `,` *屬性-值-清單*<br>
  
 其中的 *字元字串* 和 *當地語系化字元字串* 包含零或多個字元; *識別碼* 和 *當地語系化識別碼* 有一或多個字元; *attribute-關鍵字* 不區分大小寫;和 *屬性值* 可能會區分大小寫。 由於連接字串和初始化檔文法、關鍵字、當地語系化識別碼以及包含字元 [] 的屬性值 ** {} ( # A1，;？ \*=！ @** 應予以避免。 由於系統資訊中的文法，關鍵字和資料來源名稱不能包含反斜線 (\\) 字元。  
  
 根據下列語義規則，使用流覽結果連接字串語法：  
  
-   如果星號 (\*) 在 *attribute 關鍵字*的前面，則 *屬性* 是選擇性的，而且可以在下一次呼叫 **SQLBrowseConnect**時省略。  
  
-   Attribute 關鍵字 **UID** 和 **PWD** 具有與 **SQLDriverConnect**中所定義相同的意義。  
  
-   *驅動程式定義的屬性-關鍵字*會命名可以提供屬性值的屬性類型。 例如，它可能是 **伺服器**、 **資料庫**、 **主機**或 **DBMS**。  
  
-   *ODBC-attribute-關鍵字* 和 *驅動程式定義-attribute-關鍵字* 包含當地語系化或便於使用的關鍵字版本。 應用程式可能會在對話方塊中將其當做標籤使用。 但是，當您將流覽要求字串傳遞至驅動程式時，必須使用 **UID**、 **PWD**或 *識別碼* 單獨。  
  
-   {*Attribute-value-list*} 是對對應的 *attribute 關鍵字*有效的實際值列舉。 請注意，大括弧 () 不會 {} 指出選項清單; 驅動程式會傳回這些選項。 例如，它可能是伺服器名稱的清單或資料庫名稱清單。  
  
-   如果 *屬性值* 是單一問號 (？ ) ，則單一值會對應至 *attribute 關鍵字*。 例如，UID = 聖約翰;PWD = Sesame。  
  
-   每次呼叫 **SQLBrowseConnect** 時，只會傳回滿足下一層連接程式所需的資訊。 驅動程式會將狀態資訊與連接控制碼建立關聯，以便隨時都能在每次呼叫時判斷內容。  
  
## <a name="using-sqlbrowseconnect"></a>使用 SQLBrowseConnect  
 **SQLBrowseConnect** 需要配置的連接。 驅動程式管理員會載入或中所指定的驅動程式，該驅動程式會對應至初始流覽要求連接字串中指定的資料來源名稱;如需發生此情況的詳細資訊，請參閱 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)函式中的「批註」一節。 驅動程式可能會在流覽程式期間建立與資料來源的連接。 如果 **SQLBrowseConnect** 傳回 SQL_ERROR，則會終止未完成的連接，且連接會返回未連接的狀態。  
  
> [!NOTE]  
>  **SQLBrowseConnect** 不支援連接共用。 如果在啟用連接共用時呼叫 **SQLBrowseConnect** ，將會傳回 SQLSTATE HY000 (一般錯誤) 。  
  
 當您第一次在連接上呼叫 **SQLBrowseConnect** 時，流覽要求連接字串必須包含 **DSN** 關鍵字或 **DRIVER** 關鍵字。 如果流覽要求連接字串包含 **DSN** 關鍵字，驅動程式管理員會在系統資訊中尋找對應的資料來源規格：  
  
-   如果驅動程式管理員找到對應的資料來源規格，則會載入相關聯的驅動程式 DLL;驅動程式可以從系統資訊取得資料來源的相關資訊。  
  
-   如果驅動程式管理員找不到對應的資料來源規格，則會找出預設的資料來源規格，並載入相關聯的驅動程式 DLL;驅動程式可以從系統資訊取得預設資料來源的相關資訊。 "DEFAULT" 會傳遞給 DSN 的驅動程式。  
  
-   如果驅動程式管理員找不到對應的資料來源規格，而且沒有預設的資料來源規格，則會傳回 SQL_ERROR，其中包含 SQLSTATE IM002 (找不到資料來源，且未) 指定預設驅動程式。  
  
 如果流覽要求連接字串包含 **driver** 關鍵字，驅動程式管理員會載入指定的驅動程式。它不會嘗試在系統資訊中尋找資料來源。 由於 **driver** 關鍵字不會使用系統資訊中的資訊，因此驅動程式必須定義足夠的關鍵字，讓驅動程式只能使用流覽要求連接字串中的資訊連接到資料來源。  
  
 在每次呼叫 **SQLBrowseConnect**時，應用程式會在流覽要求連接字串中指定連接屬性值。 驅動程式會在流覽結果連接字串中傳回連續的屬性和屬性值層級;只要有尚未在流覽要求連接字串中列舉的連接屬性，它就會傳回 SQL_NEED_DATA。 應用程式會使用流覽結果連接字串的內容，建立 **SQLBrowseConnect**下一個呼叫的流覽要求連接字串。 所有必要屬性 (前面沒有星號的 *OutConnectionString* 引數) 必須包含在 **SQLBrowseConnect**的下一個呼叫中。 請注意，在建立目前的流覽要求連接字串時，應用程式無法使用先前流覽結果連接字串的內容;也就是說，它無法為先前層級中設定的屬性指定不同的值。  
  
 列舉所有的連接層級和其相關聯的屬性時，驅動程式會傳回 SQL_SUCCESS、與資料來源的連接已完成，而且會將完整的連接字串傳回給應用程式。 連接字串適合與 **SQLDriverConnect**搭配使用，並使用 SQL_DRIVER_NOPROMPT 選項來建立另一個連接。 但是，無法在 **SQLBrowseConnect**的另一個呼叫中使用完整的連接字串。如果再次呼叫 **SQLBrowseConnect** ，就必須重複呼叫的整個順序。  
  
 如果流覽進程期間有可復原的非嚴重錯誤， **SQLBrowseConnect**也會傳回 SQL_NEED_DATA;例如，應用程式所提供的無效密碼或屬性關鍵字。 當傳回 SQL_NEED_DATA，且流覽結果連接字串未變更時，就會發生錯誤，應用程式可以呼叫 **SQLGetDiagRec** 來傳回瀏覽器錯誤的 SQLSTATE。 這可讓應用程式更正屬性，並繼續流覽。  
  
 應用程式可以在任何時間呼叫 **SQLDisconnect**來終止流覽進程。 驅動程式將會終止任何未處理的連線，並將連接傳回未連線的狀態。  
  
 如果在連接控制碼上啟用非同步作業， **SQLBrowseConnect** 可能也會傳回 SQL_STILL_EXECUTING。 當它傳回 SQL_NEED_DATA 時，應用程式必須使用 **SQLDisconnect** 來取消流覽處理常式。 如果 **SQLBrowseConnect** 傳回 SQL_STILL_EXECUTING，應用程式應該使用 **SQLCancelHandle** 來取消進行中的作業。 在函數傳回 SQL_NEED_DATA 之後呼叫 **SQLCancelHandle** 沒有任何作用。  
  
 如需詳細資訊，請參閱 [使用 SQLBrowseConnect 連接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)。  
  
 如果驅動程式支援 **SQLBrowseConnect**，則驅動程式系統資訊中的 driver 關鍵字區段必須包含 **ConnectFunctions** 關鍵字，並將第三個字元設定為 "Y"。  
  
## <a name="code-example"></a>程式碼範例  
  
> [!NOTE]  
>  如果您要連接到支援 Windows 驗證的資料來源提供者，您應該 `Trusted_Connection=yes` 在連接字串中指定，而不是使用者識別碼和密碼資訊。  
  
 在下列範例中，應用程式會重複呼叫 **SQLBrowseConnect** 。 每次**SQLBrowseConnect**傳回 SQL_NEED_DATA 時，它會在 OutConnectionString 中傳回所需資料的相關資訊 \* * *。 應用程式會將 *OutConnectionString* 傳遞至其常式 **GetUserInput** (不會顯示) 。 **GetUserInput**會剖析資訊、建立並顯示對話方塊，並傳回使用者在 InConnectionString 中輸入的資訊 \* * *。 應用程式會在下一次呼叫 **SQLBrowseConnect**時，將使用者的資訊傳遞至驅動程式。 在應用程式提供所有必要資訊，讓驅動程式連接到資料來源之後， **SQLBrowseConnect** 會傳回 SQL_SUCCESS，然後應用程式會繼續進行。  
  
 如需更詳細的範例，以藉由呼叫 **SQLBrowseConnect**來連接到 SQL Server 的驅動程式，請參閱 [SQL Server 流覽範例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)。  
  
 例如，若要連接到資料來源銷售，可能會發生下列動作。 首先，應用程式會將下列字串傳遞給 **SQLBrowseConnect**：  
  
```  
"DSN=Sales"  
```  
  
 驅動程式管理員會載入與資料來源銷售相關聯的驅動程式。 然後，它會使用從應用程式收到的相同引數來呼叫驅動程式的 **SQLBrowseConnect** 函式。 驅動程式會在 **OutConnectionString*中傳回下列字串：  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 應用程式會將此字串傳遞至其 **GetUserInput** 常式，其會建立一個對話方塊，要求使用者選取紅色、藍色或綠色伺服器，並輸入使用者識別碼和密碼。 常式會在 InConnectionString 中傳遞下列使用者指定的資訊 \* * *，應用程式會將這些資訊傳遞給**SQLBrowseConnect**：  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect** 會使用這項資訊以 Smith 的密碼 Sesame 連接到 red server，然後在 **OutConnectionString*中傳回下列字串：  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 應用程式會將此字串傳遞至其 **GetUserInput** 常式，此常式會建立要求使用者選取資料庫的對話方塊。 使用者選取 empdata，而應用程式會使用此字串來呼叫 **SQLBrowseConnect** 最後一次：  
  
```  
"DATABASE=SalesOrders"  
```  
  
 這是驅動程式連接到資料來源所需的最後一項資訊; **SQLBrowseConnect** 會傳回 SQL_SUCCESS，而 **OutConnectionString* 包含已完成的連接字串：  
  
```cpp  
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
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|配置連接控制碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|連線到資料來源|[SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|中斷與資料來源的連接|[SQLDisconnect 函式](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|使用連接字串或對話方塊連接到資料來源|[SQLDriverConnect 函式](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|傳回驅動程式描述和屬性|[SQLDrivers 函式](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|釋放連接控制碼|[SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
