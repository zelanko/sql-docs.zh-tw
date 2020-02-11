---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2960c42690a9528763321bc882bb788b437cb66a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036197"
---
# <a name="sqlbrowseconnect-function"></a>SQLBrowseConnect 函數
**標準**  
 引進的版本： ODBC 1.0 標準合規性： ODBC  
  
 **摘要**  
 **SQLBrowseConnect**支援一種反復的方法，可探索及列舉連接至資料來源所需的屬性和屬性值。 **SQLBrowseConnect**的每個呼叫都會傳回連續的屬性和屬性值層級。 當所有層級都已列舉時，與資料來源的連接會完成，而且**SQLBrowseConnect**會傳回完整的連接字串。 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 的傳回碼指出已指定所有連接資訊，而且應用程式現在已連接至資料來源。  
  
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
 源流覽要求連接字串（請參閱「批註」中的「*InConnectionString*引數」）。  
  
 *StringLength1*  
 源**InConnectionString*的長度（以字元為單位）。  
  
 *OutConnectionString*  
 輸出要在其中傳回流覽結果連接字串之字元緩衝區的指標（請參閱「批註」中的「*OutConnectionString*引數」）。  
  
 如果*OutConnectionString*為 Null， *StringLength2Ptr*仍會傳回*OutConnectionString*所指向的緩衝區中可傳回的字元總數（不包括字元資料的 Null 終止字元）。  
  
 *BufferLength*  
 源**OutConnectionString*緩衝區的長度（以字元為單位）。  
  
 *StringLength2Ptr*  
 輸出可在\* *OutConnectionString*中傳回的字元總數（不包括 null 終止）。 如果可傳回的字元數大於或等於*BufferLength*， \* *OutConnectionString*中的連接字串會截斷為*BufferLength*減去 null 終止字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_ERROR、SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLBrowseConnect**傳回 SQL_ERROR、SQL_SUCCESS_WITH_INFO 或 SQL_NEED_DATA 時，可以藉由呼叫**SQLGetDiagRec**與*HandleType*的 SQL_HANDLE_STMT 和*ConnectionHandle 的控制碼*來取得相關聯的 SQLSTATE 值。 下表列出**SQLBrowseConnect**常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|緩衝區\* *OutConnectionString*不夠大，無法傳回整個流覽結果連接字串，因此字串已被截斷。 Buffer **StringLength2Ptr*包含 untruncated 流覽結果連接字串的長度。 （函數會傳回 SQL_NEED_DATA）。|  
|01S00|不正確連接字串屬性|在流覽要求連接字串（*InConnectionString*）中指定了不正確屬性關鍵字。 （函數會傳回 SQL_NEED_DATA）。<br /><br /> 在不會套用至目前連接層級的流覽要求連接字串（*InConnectionString*）中指定了 attribute 關鍵字。 （函數會傳回 SQL_NEED_DATA）。|  
|01S02|值已變更|驅動程式不支援在**SQLSetConnectAttr**中指定的*valueptr 是*引數值，並會取代類似的值。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08001|用戶端無法建立連接|驅動程式無法與資料來源建立連接。|  
|08002|使用中的連接名稱|（DM）指定的連接已經用來與資料來源建立連接，且連接已開啟。|  
|08004|伺服器已拒絕連接|資料來源因為執行定義的原因，而拒絕建立連接。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與驅動程式嘗試連接的資料來源之間的通訊連結失敗。|  
|28000|不正確授權規格|使用者識別碼或授權字串，或兩者（如流覽要求連接字串（*InConnectionString*）中所指定）都會違反資料來源所定義的限制。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|（DM）驅動程式管理員無法配置支援執行或完成函數所需的記憶體。<br /><br /> 驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步作業已藉由呼叫[SQLCancelHandle 函數](../../../odbc/reference/syntax/sqlcancelhandle-function.md)來取消。 然後，在*ConnectionHandle*上再次呼叫原始函數。<br /><br /> 已取消作業，方法是從多執行緒應用程式中的不同執行緒呼叫*ConnectionHandle*上的**SQLCancelHandle** 。|  
|HY010|函數順序錯誤|（DM）已針對*ConnectionHandle*呼叫非同步執行的函式（而非這個函式），而且在呼叫這個函數時仍在執行中。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|（DM）為引數*StringLength1*指定的值小於0，而且不等於 SQL_NTS。<br /><br /> （DM）為引數*BufferLength*指定的值小於0。|  
|HY114|驅動程式不支援連接層級的非同步函式執行|（DM）應用程式在建立連接之前，已在連接控制碼上啟用非同步作業。 不過，此驅動程式不支援在連接控制碼上進行非同步作業。|  
|HYT00|已超過逾時的設定|在資料來源的連接完成之前，登入超時時間已過期。 超時期間是透過**SQLSetConnectAttr**設定，SQL_ATTR_LOGIN_TIMEOUT。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）對應至指定資料來源名稱的驅動程式不支援函數。|  
|IM002|找不到資料來源，且未指定任何預設驅動程式|（DM）在系統資訊中找不到流覽要求連接字串（*InConnectionString*）中指定的資料來源名稱，也沒有預設的驅動程式規格。<br /><br /> （DM）在系統資訊中找不到 ODBC 資料來源和預設驅動程式資訊。|  
|IM003|無法載入指定的驅動程式|（DM） [系統資訊] 或 [**驅動程式**] 關鍵字所指定的資料來源規格中所列的驅動程式，或因某些原因而無法載入。|  
|IM004|SQL_HANDLE _ENV 上的驅動程式**SQLAllocHandle**失敗|（DM）在**SQLBrowseConnect**期間，驅動程式管理員會以 SQL_HANDLE_ENV 的*HandleType*呼叫驅動程式的**SQLAllocHandle**函數，而驅動程式會傳回錯誤。|  
|IM005|SQL_HANDLE_DBC 上的驅動程式**SQLAllocHandle**失敗|（DM）在**SQLBrowseConnect**期間，驅動程式管理員會以 SQL_HANDLE_DBC 的*HandleType*呼叫驅動程式的**SQLAllocHandle**函數，而驅動程式會傳回錯誤。|  
|IM006|驅動程式的**SQLSetConnectAttr**失敗|（DM）在**SQLBrowseConnect**期間，驅動程式管理員會呼叫驅動程式的**SQLSetConnectAttr**函式，而驅動程式會傳回錯誤。|  
|IM009|無法載入轉譯 DLL|驅動程式無法載入為數據源或連接所指定的轉譯 DLL。|  
|IM010|資料來源名稱太長|（DM） DSN 關鍵字的屬性值長度超過 SQL_MAX_DSN_LENGTH 個字元。|  
|IM011|驅動程式名稱太長|（DM） DRIVER 關鍵字的屬性值長度超過255個字元。|  
|IM012|驅動程式關鍵字語法錯誤|（DM） DRIVER 關鍵字的關鍵字-值配對包含語法錯誤。|  
|IM014|指定的 DSN 包含驅動程式與應用程式之間的架構不相符|（DM）32位應用程式使用連接到64位驅動程式的 DSN;或反之亦然。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 而且如果啟用通知模式，則必須在控制碼上呼叫**SQLCompleteAsync** ，才能執行後置處理並完成作業。|  
|S1118|驅動程式不支援非同步通知|當驅動程式不支援非同步通知時，您無法設定 SQL_ATTR_ASYNC_DBC_EVENT 或 SQL_ATTR_ASYNC_DBC_RETCODE_PTR。|  
  
## <a name="inconnectionstring-argument"></a>InConnectionString 引數  
 流覽要求連接字串具有下列語法：  
  
 *connection 字串*：： = *attribute*[`;`] &#124;*屬性* `;` *連接字串*;<br>
 *attribute* ：： = *attribute-關鍵字*`=`*屬性-值*&#124; `DRIVER=`[`{`]*屬性-值*[`}`]<br>
 *attribute-關鍵字*：： = `DSN` &#124; `UID` &#124; `PWD` &#124;*驅動程式定義-attribute-關鍵字*<br>
 *屬性-值*：： =*字元字串*<br>
 *驅動程式定義-attribute-關鍵字*：： = *identifier*<br>
  
 其中，*字元字串*包含零或多個字元;*識別碼*有一或多個字元;*attribute-關鍵字*不區分大小寫;*屬性值*可能會區分大小寫;而**DSN**關鍵字的值不只包含空白。 由於連接字串和初始化檔文法的關係，包含字元 **[]{}（），;？的關鍵字和屬性值。= \*！ @** 應該避免。 由於系統資訊中的文法，關鍵字和資料來源名稱不能包含反斜線（\\）字元。 適用于 ODBC 2。*x*驅動程式，driver 關鍵字的屬性值周圍需要有大括弧。  
  
 如果流覽要求連接字串中有重複的任何關鍵字，驅動程式會使用與第一次出現關鍵字相關聯的值。 如果**DSN**和**驅動程式**關鍵字包含在相同的流覽要求連接字串中，驅動程式管理員和驅動程式會先使用任何出現的關鍵字。  
  
 如需應用程式如何選擇資料來源或驅動程式的相關資訊，請參閱[選擇資料來源或驅動](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)程式。  
  
## <a name="outconnectionstring-argument"></a>OutConnectionString 引數  
 流覽結果連接字串是連接屬性的清單。 連接屬性包含屬性關鍵字和對應的屬性值。 流覽結果連接字串具有下列語法：  
  
 *connection 字串*：： = *attribute*[`;`] &#124;*屬性* `;` *連接字串*<br>
 *attribute* ：： = [`*`]*屬性-關鍵字*`=`*屬性-值*<br>
 *attribute-關鍵字*：： = *ODBC-attribute-關鍵字*&#124;*驅動程式定義-attribute-關鍵字*<br>
 *ODBC-attribute-關鍵字*= {`UID` &#124; `PWD`} [`:`*當地語系化識別碼*]*驅動程式定義-attribute-關鍵字*：： = *identifier*[`:`*當地語系化識別碼*]*屬性-值*：： = `{` *屬性-值-清單* `}` &#124; `?` （大括弧為常值，驅動程式會傳回）。<br>
 *屬性-值-list* ：： =*字元字串*[`:`*當地語系化的字元字串*] &#124;*字元字串*[`:`*當地語系化的字元字串*] `,` *屬性-值清單*<br>
  
 其中，*字元字串*和*當地語系化字元字串*有零或多個字元;*識別碼*和*當地語系化識別碼*有一或多個字元;*attribute-關鍵字*不區分大小寫;和*屬性值*可能會區分大小寫。 由於連接字串和初始化檔文法、關鍵字、當地語系化識別碼和包含字元 **[]{}（）、; 的屬性值？= \*！ @** 應該避免。 由於系統資訊中的文法，關鍵字和資料來源名稱不能包含反斜線（\\）字元。  
  
 根據下列語義規則，會使用流覽結果連接字串語法：  
  
-   \*如果星號（）在*屬性關鍵字*之前，*屬性*是選擇性的，而且可以在下一次呼叫**SQLBrowseConnect**時省略。  
  
-   屬性關鍵字**UID**和**PWD**具有與**SQLDriverConnect**中所定義相同的意義。  
  
-   *驅動程式定義的-attribute 關鍵字*會命名可提供屬性值的屬性類型。 例如，它可能是**伺服器**、**資料庫**、**主機**或**DBMS**。  
  
-   *ODBC-attribute-關鍵字*和*驅動程式定義-attribute-關鍵字*包含關鍵字的當地語系化或方便使用的版本。 應用程式可能會使用此功能做為對話方塊中的標籤。 不過，在將流覽要求字串傳遞至驅動程式時，必須單獨使用**UID**、 **PWD**或*識別碼*。  
  
-   {*屬性-值-list*} 是對對應的*屬性-關鍵字*有效的實際值列舉。 請注意，大括弧{}（）並不表示挑選清單;驅動程式會傳回它們。 例如，它可能是伺服器名稱的清單或資料庫名稱清單。  
  
-   如果*屬性-值*是單一問號（？），則單一值會對應至*屬性（attribute）關鍵字*。 例如，UID = 聖約翰;PWD = Sesame。  
  
-   每次呼叫**SQLBrowseConnect**時，只會傳回滿足連接程式下一個層級所需的資訊。 驅動程式會將狀態資訊與連接控制碼產生關聯，以便一律可以在每次呼叫時判斷內容。  
  
## <a name="using-sqlbrowseconnect"></a>使用 SQLBrowseConnect  
 **SQLBrowseConnect**需要已配置的連接。 驅動程式管理員會載入或中指定的驅動程式，其對應于初始流覽要求連接字串中所指定的資料來源名稱;如需何時發生這種情況的詳細資訊，請參閱[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)函式中的「批註」一節。 在流覽過程中，驅動程式可能會與資料來源建立連接。 如果**SQLBrowseConnect**傳回 SQL_ERROR，就會終止未完成的連接，而且連接會回到未連線的狀態。  
  
> [!NOTE]  
>  **SQLBrowseConnect**不支援連接共用。 如果在啟用連接共用時呼叫**SQLBrowseConnect** ，則會傳回 SQLSTATE HY000 （一般錯誤）。  
  
 第一次在連接上呼叫**SQLBrowseConnect**時，流覽要求連接字串必須包含**DSN**關鍵字或**DRIVER**關鍵字。 如果流覽要求連接字串包含**DSN**關鍵字，驅動程式管理員會在系統資訊中尋找對應的資料來源規格：  
  
-   如果驅動程式管理員找到對應的資料來源規格，就會載入關聯的驅動程式 DLL;驅動程式可以從系統資訊取得資料來源的相關資訊。  
  
-   如果驅動程式管理員找不到對應的資料來源規格，它會尋找預設的資料來源規格，並載入相關聯的驅動程式 DLL。驅動程式可以從系統資訊取得預設資料來源的相關資訊。 "DEFAULT" 會傳遞給 DSN 的驅動程式。  
  
-   如果驅動程式管理員找不到對應的資料來源規格，而且沒有預設的資料來源規格，它會傳回具有 SQLSTATE IM002 的 SQL_ERROR （找不到資料來源，且未指定預設驅動程式）。  
  
 如果流覽要求連接字串包含**DRIVER**關鍵字，驅動程式管理員會載入指定的驅動程式;它不會嘗試找出系統資訊中的資料來源。 由於**driver**關鍵字不會使用系統資訊中的資訊，因此驅動程式必須定義足夠的關鍵字，讓驅動程式只能使用流覽要求連接字串中的資訊來連接到資料來源。  
  
 在每次呼叫**SQLBrowseConnect**時，應用程式會在流覽要求連接字串中指定連接屬性值。 驅動程式會在流覽結果連接字串中傳回連續的屬性和屬性值層級;只要有尚未在流覽要求連接字串中列舉的連接屬性，它就會傳回 SQL_NEED_DATA。 應用程式會使用流覽結果連接字串的內容，來建立下一個呼叫**SQLBrowseConnect**的流覽要求連接字串。 下一次呼叫**SQLBrowseConnect**時，必須包含所有必要屬性（前面加上星號的*OutConnectionString*引數）。 請注意，建立目前的流覽要求連接字串時，應用程式無法使用先前流覽結果連接字串的內容;也就是說，它無法為先前層級中設定的屬性指定不同的值。  
  
 當所有連線層級和其相關聯的屬性都已列舉時，驅動程式會傳回 SQL_SUCCESS、資料來源的連接已完成，而且完整的連接字串會傳回到應用程式。 連接字串適用于與**SQLDriverConnect**搭配使用，以建立另一個連接的 SQL_DRIVER_NOPROMPT 選項。 不過，在另一個呼叫**SQLBrowseConnect**時，不能使用完整的連接字串。如果再次呼叫**SQLBrowseConnect** ，則必須重複呼叫的整個順序。  
  
 如果流覽進程期間有可復原的非嚴重錯誤， **SQLBrowseConnect**也會傳回 SQL_NEED_DATA;例如，應用程式所提供的無效密碼或屬性關鍵字。 當傳回 SQL_NEED_DATA，且流覽結果連接字串未變更時，就會發生錯誤，而且應用程式可以呼叫**SQLGetDiagRec** ，以傳回 SQLSTATE 的流覽時間錯誤。 這允許應用程式更正屬性並繼續流覽。  
  
 應用程式可以隨時呼叫**SQLDisconnect**來終止流覽進程。 驅動程式會終止任何未處理的連接，並將連線傳回未連線的狀態。  
  
 如果已在連接控制碼上啟用非同步作業， **SQLBrowseConnect**也可能會傳回 SQL_STILL_EXECUTING。 當它傳回 SQL_NEED_DATA 時，應用程式必須使用**SQLDisconnect**來取消流覽進程。 如果**SQLBrowseConnect**傳回 SQL_STILL_EXECUTING，應用程式應該使用**SQLCancelHandle**來取消進行中的作業。 在函式傳回 SQL_NEED_DATA 之後呼叫**SQLCancelHandle**沒有任何作用。  
  
 如需詳細資訊，請參閱[使用 SQLBrowseConnect 連接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)。  
  
 如果驅動程式支援**SQLBrowseConnect**，驅動程式的系統資訊中的 driver 關鍵字區段必須包含**ConnectFunctions**關鍵字，而第三個字元設定為 "Y"。  
  
## <a name="code-example"></a>程式碼範例  
  
> [!NOTE]  
>  如果您要連接到支援 Windows 驗證的資料來源提供者，您應該在`Trusted_Connection=yes`連接字串中指定而不是使用者識別碼和密碼資訊。  
  
 在下列範例中，應用程式會重複呼叫**SQLBrowseConnect** 。 每次**SQLBrowseConnect**傳回 SQL_NEED_DATA，它就會在\* *OutConnectionString*中傳遞所需資料的相關資訊。 應用程式會將*OutConnectionString*傳遞至其常式**GetUserInput** （未顯示）。 **GetUserInput**會剖析資訊、建立並顯示對話方塊，並傳回使用者在\* *InConnectionString*中輸入的資訊。 應用程式會在下一次呼叫**SQLBrowseConnect**時，將使用者的資訊傳遞給驅動程式。 在應用程式提供所有必要的資訊以讓驅動程式連接到資料來源之後， **SQLBrowseConnect**會傳回 SQL_SUCCESS 並繼續執行應用程式。  
  
 如需藉由呼叫**SQLBrowseConnect**來連接到 SQL Server 驅動程式的更詳細範例，請參閱[SQL Server 流覽範例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)。  
  
 例如，若要連接到資料來源銷售，可能會發生下列動作。 首先，應用程式會將下列字串傳遞至**SQLBrowseConnect**：  
  
```  
"DSN=Sales"  
```  
  
 驅動程式管理員會載入與資料來源銷售相關聯的驅動程式。 然後，它會使用從應用程式收到的相同引數來呼叫驅動程式的**SQLBrowseConnect**函式。 驅動程式會在 **OutConnectionString*中傳回下列字串：  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 應用程式會將此字串傳遞至其**GetUserInput**常式，這會建立一個對話方塊，要求使用者選取紅色、藍色或綠色伺服器，並輸入使用者識別碼和密碼。 此常式會將下列使用者指定的資訊傳回\*給應用程式傳遞給**SQLBrowseConnect**的*InConnectionString*：  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect**會使用此資訊以 Smith 與密碼 Sesame 連接到 red server，然後在 **OutConnectionString*中傳回下列字串：  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 應用程式會將此字串傳遞至其**GetUserInput**常式，這會建立一個對話方塊，要求使用者選取資料庫。 使用者選取 empdata，應用程式會使用此字串來呼叫**SQLBrowseConnect**的最後時間：  
  
```  
"DATABASE=SalesOrders"  
```  
  
 這是驅動程式連接到資料來源所需的最後一項資訊;**SQLBrowseConnect**會傳回 SQL_SUCCESS，而 **OutConnectionString*包含已完成的連接字串：  
  
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
|連接到資料來源|[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|中斷與資料來源的連線|[SQLDisconnect 函式](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|使用連接字串或對話方塊連接到資料來源|[SQLDriverConnect 函數](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|傳回驅動程式描述和屬性|[SQLDrivers 函式](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|釋放連接控制碼|[SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
