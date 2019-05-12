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
manager: craigg
ms.openlocfilehash: 3af78971a17035091ab8a72bf0c9a8fe90250dd3
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/11/2019
ms.locfileid: "65538183"
---
# <a name="sqlbrowseconnect-function"></a>SQLBrowseConnect 函數
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ODBC  
  
 **摘要**  
 **SQLBrowseConnect**支援探索和列舉的屬性和屬性值連接到資料來源所需的反覆式方法。 每次呼叫**SQLBrowseConnect**傳回後續的層級的屬性和屬性值。 當已經列舉所有層級時，在完成資料來源的連接而完整連接字串由**SQLBrowseConnect**。 傳回碼為 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，指出已指定所有連接資訊，以及應用程式現在已連接到資料來源。  
  
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
 [輸入]連接控制代碼。  
  
 *InConnectionString*  
 [輸入]瀏覽要求的連接字串 (請參閱 「*InConnectionString*引數""註解"中)。  
  
 *StringLength1*  
 [輸入]長度 **InConnectionString*以字元為單位。  
  
 *OutConnectionString*  
 [輸出]在其中傳回瀏覽結果連接字串的字元緩衝區的指標 (請參閱 「*OutConnectionString*引數""註解"中)。  
  
 如果*OutConnectionString*為 NULL，就*StringLength2Ptr*仍會傳回 （不含字元資料的 null 終止字元） 的字元總數可傳回緩衝區中指向*OutConnectionString*。  
  
 *BufferLength*  
 [輸入]長度，以字元為單位的 **OutConnectionString*緩衝區。  
  
 *StringLength2Ptr*  
 [輸出]字元 （不含 null 終止） 可用來傳回中總數\* *OutConnectionString*。 可用來傳回字元的數目是否大於或等於*Columnsize*中的連接字串\* *OutConnectionString*會被截斷成*BufferLength*減去 null 結束字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NEED_DATA、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLBrowseConnect**可以藉由呼叫取得傳回 SQL_ERROR、 SQL_SUCCESS_WITH_INFO 或 SQL_NEED_DATA，相關聯的 SQLSTATE 值**SQLGetDiagRec**使用*HandleType*利用 SQL_HANDLE_STMT 的並*控制代碼的 ConnectionHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLBrowseConnect** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|緩衝區\* *OutConnectionString*仍不夠大，無法傳回整個瀏覽結果連接字串，所以已截斷字串。 緩衝區 **StringLength2Ptr*包含未截斷的瀏覽結果連接字串的長度。 （函式會傳回 SQL_NEED_DATA）。|  
|01S00|連接字串屬性無效|瀏覽要求的連接字串中指定一個屬性無效的關鍵字 (*InConnectionString*)。 （函式會傳回 SQL_NEED_DATA）。<br /><br /> 瀏覽要求的連接字串中指定一個屬性的關鍵字 (*InConnectionString*) 時，不適用於目前的連接層級。 （函式會傳回 SQL_NEED_DATA）。|  
|01S02|值已變更|驅動程式不支援指定的值*ValuePtr*中的引數**SQLSetConnectAttr**和類似的值已被取代。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08001|無法建立連線的用戶端|驅動程式無法建立與資料來源的連接。|  
|08002|使用中的連接名稱|(DM) 指定的連接必須已經用來建立與資料來源的連接和連接為開啟。|  
|08004|伺服器拒絕連線|資料來源會拒絕連線建立實作定義的原因。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和資料來源的驅動程式已嘗試連線之間的通訊連結失敗。|  
|28000|無效的授權規格|使用者識別碼或授權字串或兩者，指定在瀏覽要求的連接字串 (*InConnectionString*)，違反了資料來源所定義的限制。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式管理員 」 (DM) 無法配置記憶體，才能支援執行或完成函式。<br /><br /> 驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步作業已取消藉由呼叫[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)。 然後，原始的函式一次上呼叫*ConnectionHandle*。<br /><br /> 已取消作業，藉由呼叫**SQLCancelHandle**上*ConnectionHandle*從不同的執行緒，多執行緒應用程式中。|  
|HY010|函數順序錯誤|以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *ConnectionHandle*和仍在呼叫此函式時所執行。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|(DM) 引數指定的值*StringLength1*為小於 0，且不等於 SQL_NTS。<br /><br /> (DM) 引數指定的值*Columnsize*為小於 0。|  
|HY114|驅動程式不支援連接層級的非同步函式執行|(DM) 應用程式啟用連接控制代碼上非同步作業之前建立的連接。 不過，此驅動程式不支援連接控制代碼上的非同步作業。|  
|HYT00|已超過逾時的設定|登入逾時期限過期之前完成的資料來源的連接。 透過設定的逾時期限**SQLSetConnectAttr**，SQL_ATTR_LOGIN_TIMEOUT。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 對應到指定的資料來源名稱的驅動程式不支援此函式。|  
|IM002|找不到資料來源並沒有指定的預設驅動程式|(DM) 的資料來源瀏覽要求的連接字串中指定的名稱 (*InConnectionString*) 找不到系統的資訊，或是否有預設的驅動程式規格。<br /><br /> (DM) 的系統資訊中找不到 ODBC 資料來源和預設驅動程式資訊。|  
|IM003|無法載入指定的驅動程式|(DM) 驅動程式中的系統資訊的資料來源規格中所列，或所指定**驅動程式**關鍵字找不到或無法載入某些其他原因。|  
|IM004|駕**SQLAllocHandle**上失敗的 SQL_HANDLE _ENV|(DM) 期間**SQLBrowseConnect**，驅動程式管理員呼叫駕**SQLAllocHandle**函式搭配*HandleType* SQL_HANDLE_ENV 和驅動程式傳回發生錯誤。|  
|IM005|駕**SQLAllocHandle**上利用 SQL_HANDLE_DBC 失敗|(DM) 期間**SQLBrowseConnect**，驅動程式管理員呼叫駕**SQLAllocHandle**函式搭配*HandleType*利用 SQL_HANDLE_DBC 和驅動程式傳回發生錯誤。|  
|IM006|駕**SQLSetConnectAttr**失敗|(DM) 期間**SQLBrowseConnect**，驅動程式管理員呼叫駕**SQLSetConnectAttr**函式和驅動程式傳回錯誤。|  
|IM009|無法載入轉譯 DLL|驅動程式無法載入轉譯 DLL 所指定的資料來源或連接。|  
|IM010|資料來源名稱太長|(DM) DSN 關鍵字的屬性值已超過 SQL_MAX_DSN_LENGTH 個字元。|  
|IM011|驅動程式名稱太長|(DM) 驅動程式關鍵字的屬性值已超過 255 個字元。|  
|IM012|驅動程式關鍵字的語法錯誤|(DM) 驅動程式關鍵字的關鍵字-值配對包含語法錯誤。|  
|IM014|指定的 DSN 包含在驅動程式和應用程式之間的架構不相符|(DM) 32 位元應用程式使用 DSN 連接至 64 位元驅動程式;反之亦然。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
|S1118|驅動程式不支援非同步通知|當驅動程式不支援非同步通知時，您無法對 SQL_ATTR_ASYNC_DBC_EVENT 或 SQL_ATTR_ASYNC_DBC_RETCODE_PTR 進行設定。|  
  
## <a name="inconnectionstring-argument"></a>InConnectionString 引數  
 瀏覽要求的連接字串的語法如下：  
  
 *connection-string* ::= *attribute*[`;`] &#124; *attribute* `;` *connection-string*;<br>
 *attribute* ::= *attribute-keyword*`=`*attribute-value* &#124; `DRIVER=`[`{`]*attribute-value*[`}`]<br>
 *attribute-keyword* ::= `DSN` &#124; `UID` &#124; `PWD` &#124; *driver-defined-attribute-keyword*<br>
 *attribute-value* ::= *character-string*<br>
 *driver-defined-attribute-keyword* ::= *identifier*<br>
  
 何處*字元字串*有零個或多個字元;*識別碼*有一或多個字元;*屬性關鍵字*不區分大小寫;*屬性值*可能會區分大小寫，而**DSN**關鍵字並沒有包含單獨的空白。 因為連接字串和初始設定檔案文法、 關鍵字和屬性值包含字元 **[]{}(）; 嗎？\*= ！ @** 應該予以避免。 在 系統資訊的文法，因為關鍵字和資料來源名稱不能包含反斜線 (\\) 字元。 ODBC 2。*x*驅動程式、 驅動程式關鍵字的屬性值前後需要括號。  
  
 如果瀏覽要求的連接字串中重複任何關鍵字，驅動程式會使用第一個出現的關鍵字相關聯的值。 如果**DSN**並**驅動程式**相同的瀏覽要求連接字串中包含關鍵字、 驅動程式與驅動程式管理員會使用任何關鍵字會出現第一次。  
  
 如需應用程式如何選擇資料來源或驅動程式的資訊，請參閱[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
## <a name="outconnectionstring-argument"></a>OutConnectionString 引數  
 瀏覽結果連接字串是連接屬性的清單。 連接屬性是由屬性關鍵字和對應的屬性值所組成。 瀏覽結果連接字串的語法如下：  
  
 *connection-string* ::= *attribute*[`;`] &#124; *attribute* `;` *connection-string*<br>
 *attribute* ::= [`*`]*attribute-keyword*`=`*attribute-value*<br>
 *attribute-keyword* ::= *ODBC-attribute-keyword* &#124; *driver-defined-attribute-keyword*<br>
 *ODBC 屬性關鍵字*= {`UID` &#124; `PWD`} [`:`*當地語系化識別碼*]*驅動程式-定義-屬性-關鍵字*:: = *識別項*[`:`*當地語系化識別碼*]*屬性值*:: = `{` *屬性值清單* `}` &#124; `?` （大括號是常值，由驅動程式）。<br>
 *attribute-value-list* ::= *character-string* [`:`*localized-character string*] &#124; *character-string* [`:`*localized-character string*] `,` *attribute-value-list*<br>
  
 何處*字元字串*並*當地語系化的字元字串*有零個或多個字元;*識別碼*並*當地語系化識別碼*有一或多個字元;*屬性關鍵字*不區分大小寫，並*屬性值*可能區分大小寫。 連線字串和初始設定檔案文法、 關鍵字、 當地語系化的識別項，與屬性值包含字元 **[]{}(）; 嗎？\*= ！ @** 應該予以避免。 在 系統資訊的文法，因為關鍵字和資料來源名稱不能包含反斜線 (\\) 字元。  
  
 瀏覽結果連接字串語法是根據下列的語意規則來使用：  
  
-   如果使用星號 (\*) 前面*屬性關鍵字*，則*屬性*是選擇性的可以在下一個呼叫中省略**SQLBrowseConnect**。  
  
-   屬性關鍵字**UID**並**PWD**中所定義，具有相同的意義**SQLDriverConnect**。  
  
-   A*驅動程式-定義-屬性-關鍵字*名稱可能會提供屬性值之屬性的類型。 比方說，它可能**伺服器**，**資料庫**，**主機**，或**DBMS**。  
  
-   *ODBC 屬性關鍵字*並*驅動程式-定義-屬性-關鍵字*包含關鍵字的當地語系化或使用者易記版本。 這可能會使用應用程式為在對話方塊中的標籤。 不過， **UID**， **PWD**，或有*識別碼*單獨時，必須使用瀏覽要求字串傳遞至驅動程式。  
  
-   {*屬性值清單*} 是實際值的列舉型別對應的有效值*屬性關鍵字*。 請注意，在大括號 ({}) 並不表示選擇清單，它們會傳回由驅動程式。 比方說，它可能是一份伺服器名稱或資料庫名稱的清單。  
  
-   如果*屬性值*是一個單一的問號 （？），單一值會對應至*屬性關鍵字*。 例如，UID = JohnS;PWD = 街。  
  
-   每次呼叫**SQLBrowseConnect**傳回只將符合連線程序的下一個層級所需的資訊。 驅動程式與連接控制代碼關聯的狀態資訊，以便的內容一律可以決定在每次呼叫。  
  
## <a name="using-sqlbrowseconnect"></a>使用 SQLBrowseConnect  
 **SQLBrowseConnect**需要配置的連接。 驅動程式管理員載入驅動程式中指定，或對應至初始瀏覽要求連接字串; 中指定的資料來源名稱當發生這種情況的相關資訊，請參閱 「 註解 」 一節[SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)。 驅動程式可能會建立與資料來源的連線，在瀏覽的程序期間。 如果**SQLBrowseConnect**會傳回 SQL_ERROR，連線已終止，而且連接會傳回未連接的狀態未完成。  
  
> [!NOTE]  
>  **SQLBrowseConnect**不支援連接共用。 如果**SQLBrowseConnect**稱為啟用連接共用時，SQLSTATE HY000 會傳回 （也就是一般錯誤）。  
  
 當**SQLBrowseConnect**呼叫連接上第一次，瀏覽要求的連接字串必須包含**DSN**關鍵字或**驅動程式**關鍵字。 如果瀏覽要求的連接字串包含**DSN**關鍵字，驅動程式管理員會尋找對應的資料來源規格中的系統資訊：  
  
-   如果驅動程式管理員找到對應的資料來源規格，它會載入相關聯的驅動程式 DLL;驅動程式可以擷取系統資訊的資料來源的相關資訊。  
  
-   如果驅動程式管理員找不到對應的資料來源規格，它會找出預設資料來源的規格，並載入相關聯的驅動程式 DLL;驅動程式可以擷取系統資訊的預設資料來源的相關資訊。 「 預設 」 會傳遞至驅動程式之 dsn。  
  
-   如果驅動程式管理員找不到對應的資料來源規格，而且沒有任何預設資料來源的規格，它會傳回 sql_error，其中包含 SQLSTATE IM002 （找不到資料來源和指定的任何預設驅動程式）。  
  
 如果瀏覽要求的連接字串包含**驅動程式**關鍵字，驅動程式管理員會載入指定的驅動程式; 它不會嘗試找出資料來源中的系統資訊。 因為**驅動程式**關鍵字不會使用資訊的系統資訊、 驅動程式必須定義足夠的關鍵字，讓驅動程式可以連接到資料來源瀏覽要求的連接字串中使用的資訊。  
  
 在每次呼叫**SQLBrowseConnect**，應用程式瀏覽要求的連接字串中指定的連接屬性值。 驅動程式傳回屬性和屬性值的連續層的級中瀏覽結果連接字串;只要有尚未列舉瀏覽要求的連接字串中的連接屬性，它會傳回 SQL_NEED_DATA。 應用程式會使用瀏覽結果連接字串的內容來建置下一個呼叫的瀏覽要求連接字串**SQLBrowseConnect**。 所有必要的屬性 (這些未加上星號*OutConnectionString*引數) 必須包含在下一個呼叫**SQLBrowseConnect**。 請注意應用程式在建置目前的瀏覽要求連接字串; 時，無法使用先前的瀏覽結果連接字串的內容也就是它不能指定不同的值，在先前的層級中設定的屬性。  
  
 當所有層級的連接和其相關聯的屬性皆已列舉時，驅動程式傳回 SQL_SUCCESS、 資料來源的連接已完成，而且完整連接字串會傳回到應用程式。 連接字串是適用於搭配**SQLDriverConnect**，SQL_DRIVER_NOPROMPT 選項，以建立另一個連線。 完整連接字串不能在另一個呼叫**SQLBrowseConnect**，不過，如果**SQLBrowseConnect**所呼叫的同樣地，在整個系列的呼叫必須重複執行。  
  
 **SQLBrowseConnect**期間瀏覽程序; 例如，無效密碼或應用程式所提供的屬性關鍵字可復原的、 非嚴重錯誤時，也會傳回 SQL_NEED_DATA。 時，會傳回 SQL_NEED_DATA 和瀏覽結果連接字串會變更，發生錯誤，而應用程式可以呼叫**SQLGetDiagRec**返回瀏覽階段錯誤的 SQLSTATE。 這可讓更正該屬性，並繼續瀏覽應用程式。  
  
 應用程式可以終止隨時瀏覽程序藉由呼叫**SQLDisconnect**。 驅動程式會終止任何未處理的連接，並將連接傳回未連接的狀態。  
  
 如果非同步作業已啟用連接控制代碼上**SQLBrowseConnect**也可能會傳回 SQL_STILL_EXECUTING。 應用程式時，它會傳回 SQL_NEED_DATA，必須使用**SQLDisconnect**取消瀏覽程序。 如果**SQLBrowseConnect**傳回 SQL_STILL_EXECUTING，應用程式應該使用**SQLCancelHandle**取消進行中的作業。 呼叫**SQLCancelHandle**之後函式會傳回 SQL_NEED_DATA 沒有任何作用。  
  
 如需詳細資訊，請參閱 <<c0> [ 使用 sqldriverconnect 進行連接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)。  
  
 如果驅動程式支援**SQLBrowseConnect**，必須包含驅動程式的系統資訊中的 [驅動程式關鍵字] 區段**ConnectFunctions**關鍵字與第三個字元設為"Y"。  
  
## <a name="code-example"></a>程式碼範例  
  
> [!NOTE]  
>  如果您要連接到資料來源提供者支援 Windows 驗證，您應該指定`Trusted_Connection=yes`而不是在連接字串中的使用者識別碼和密碼資訊。  
  
 在下列範例中，應用程式會呼叫**SQLBrowseConnect**重複。 每次**SQLBrowseConnect**會傳回 SQL_NEED_DATA，它會傳遞它所需的資料後的資訊\* *OutConnectionString*。 在應用程式通過*OutConnectionString*其常式**GetUserInput** （未顯示）。 **GetUserInput**剖析的資訊、 建置和顯示對話方塊，並傳回使用者所輸入的資訊\* *InConnectionString*。 應用程式會將使用者的資訊傳遞到下一個呼叫中的驅動程式**SQLBrowseConnect**。 應用程式提供的驅動程式連接到資料來源的所有必要資訊之後**SQLBrowseConnect**傳回 SQL_SUCCESS 和應用程式會繼續。  
  
 如需更詳細的範例，連接到 SQL Server 驅動程式呼叫的**SQLBrowseConnect**，請參閱[SQL Server 瀏覽範例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)。  
  
 比方說，若要連接到資料來源的銷售，可能會執行下列動作。 首先，應用程式傳遞下列字串**SQLBrowseConnect**:  
  
```  
"DSN=Sales"  
```  
  
 驅動程式管理員會載入驅動程式與資料來源銷售相關聯。 然後它會呼叫駕**SQLBrowseConnect**與來自應用程式的相同引數的函式。 驅動程式會傳回下列字串中的 **OutConnectionString*:  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 應用程式傳遞此字串，以其**GetUserInput**例行，哪些組建的對話方塊，要求使用者選取的紅色、 藍色或綠色的伺服器，並輸入使用者識別碼和密碼。 中的常式傳遞的使用者指定的下列資訊回\* *InConnectionString*，應用程式將傳遞**SQLBrowseConnect**:  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect** Smith 以連接到紅色的伺服器密碼街，會使用此資訊，然後傳回 在下列字串 **OutConnectionString*:  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 應用程式傳遞此字串，以其**GetUserInput**例行，哪些組建的對話方塊，詢問使用者是否要選取的資料庫。 使用者選取 empdata 和應用程式會呼叫**SQLBrowseConnect**以這個字串的最後一個時間：  
  
```  
"DATABASE=SalesOrders"  
```  
  
 這是資訊的最終的一段的驅動程式必須連接到資料來源**SQLBrowseConnect**都會傳回 SQL_SUCCESS，和 **OutConnectionString*包含完整的連接字串：  
  
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
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|配置連接控制代碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|連接到資料來源|[SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|從資料來源中斷連接|[SQLDisconnect 函式](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|連接到資料來源使用的連接字串或對話方塊方塊|[SQLDriverConnect 函式](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|傳回的驅動程式描述和屬性|[SQLDrivers 函式](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|釋放連接控制代碼|[SQLFreeHandle 函式](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
