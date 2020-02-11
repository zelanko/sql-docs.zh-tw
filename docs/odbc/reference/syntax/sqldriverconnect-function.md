---
title: SQLDriverConnect 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9528280514be2eb2424b15a39ded3206aaca112f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104699"
---
# <a name="sqldriverconnect-function"></a>SQLDriverConnect 函數
**標準**  
 引進的版本： ODBC 1.0 標準合規性： ODBC  
  
 **摘要**  
 **SQLDriverConnect**是**SQLConnect**的替代方式。 它支援的資料來源需要比**SQLConnect**中的三個引數更多的連接資訊，而對話方塊會提示使用者輸入所有連接資訊，以及系統資訊中未定義的資料來源。  
  
 **SQLDriverConnect**提供下列連接屬性：  
  
-   使用包含資料來源名稱的連接字串、一或多個使用者識別碼、一個或多個密碼，以及資料來源所需的其他資訊，建立連接。  
  
-   使用部分連接字串建立連接，或不提供其他資訊;在這種情況下，驅動程式管理員和驅動程式都可以提示使用者輸入連接資訊。  
  
-   建立未在系統資訊中定義的資料來源連接。 如果應用程式提供部分連接字串，驅動程式可能會提示使用者輸入連接資訊。  
  
-   使用從 .dsn 檔案中的資訊所構成的連接字串，建立與資料來源的連接。  
  
 建立連接之後， **SQLDriverConnect**會傳回已完成的連接字串。 應用程式可以針對後續的連接要求使用此字串。 如需詳細資訊，請參閱[使用 SQLDriverConnect 連接](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
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
 [輸入] 連線控制代碼。  
  
 *WindowHandle*  
 源視窗控制碼。 應用程式可以傳遞父視窗的控制碼（如果適用的話），或如果視窗控制碼不適用或**SQLDriverConnect**不會顯示任何對話方塊，則為 null 指標。  
  
 *InConnectionString*  
 源完整的連接字串（請參閱「批註」中的語法）、部分連接字串或空字串。  
  
 *StringLength1*  
 源**InConnectionString*的長度（如果字串是 Unicode，則以字元為單位）; 如果 STRING 為 ANSI 或 DBCS，則為位元組。  
  
 *OutConnectionString*  
 輸出已完成連接字串之緩衝區的指標。 成功連接到目標資料來源之後，此緩衝區會包含已完成的連接字串。 應用程式應該為這個緩衝區配置至少1024個字元。  
  
 如果*OutConnectionString*為 Null， *StringLength2Ptr*仍會傳回*OutConnectionString*所指向的緩衝區中可傳回的字元總數（不包括字元資料的 Null 終止字元）。  
  
 *BufferLength*  
 源**OutConnectionString*緩衝區的長度（以字元為單位）。  
  
 *StringLength2Ptr*  
 輸出緩衝區的指標，要在其中傳回\* *OutConnectionString*中可傳回的字元總數（不包括 null 終止字元）。 如果可傳回的字元數大於或等於*BufferLength*，則\* *OutConnectionString*中已完成的連接字串會截斷為*BufferLength*減去 null 終止字元的長度。  
  
 *DriverCompletion*  
 源指出驅動程式管理員或驅動程式是否必須提示取得更多連線資訊的旗標：  
  
 SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE、SQL_DRIVER_COMPLETE_REQUIRED 或 SQL_DRIVER_NOPROMPT。  
  
 （如需詳細資訊，請參閱「留言」）。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR、SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDriverConnect**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec** （ *fHandleType*為 SQL_HANDLE_DBC）和 hHandle *ConnectionHandle*來取得相關聯的 SQLSTATE*值。* 下表列出**SQLDriverConnect**常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|緩衝區\* *OutConnectionString*不夠大，無法傳回整個連接字串，因此連接字串已被截斷。 Untruncated 連接字串的長度會以 **StringLength2Ptr*傳回。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S00|不正確連接字串屬性|在連接字串（*InConnectionString*）中指定了不正確屬性關鍵字，但驅動程式仍然能夠連接到資料來源。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S02|選項值已變更|驅動程式不支援**SQLSetConnectAttr**中的*valueptr 是*引數所指向的指定值，並且會取代類似的值。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S08|儲存檔案 DSN 時發生錯誤|* \*InConnectionString*中的字串包含**FILEDSN**關鍵字，但尚未儲存該 dsn 檔案。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S09|不正確關鍵字|（DM） * \*InConnectionString*中的字串包含**SAVEFILE**關鍵字，但不含**驅動程式**或**FILEDSN**關鍵字。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08001|用戶端無法建立連接|驅動程式無法與資料來源建立連接。|  
|08002|使用中的連接名稱|（DM）已使用指定的*ConnectionHandle*來建立與資料來源的連接，且該連接仍為開啟狀態。|  
|08004|伺服器已拒絕連接|資料來源因為執行定義的原因，而拒絕建立連接。|  
|08S01|通訊連結失敗|在**SQLDriverConnect**函數完成處理之前，驅動程式與驅動程式嘗試連接的資料來源之間的通訊連結失敗。|  
|28000|不正確授權規格|使用者識別碼或授權字串，或兩者（如連接字串（*InConnectionString*）中所指定）都會違反資料來源所定義的限制。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 SzMessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY000|一般錯誤：不正確檔案 dsn|（DM） **InConnectionString*中的字串包含 FILEDSN 關鍵字，但找不到該 dsn 檔案的名稱。|  
|HY000|一般錯誤：無法建立檔案緩衝區|（DM） **InConnectionString*中的字串包含 FILEDSN 關鍵字，但無法讀取該 dsn 檔案。|  
|HY001|記憶體配置錯誤|驅動程式管理員無法配置支援執行或完成**SQLDriverConnect**函數所需的記憶體。<br /><br /> 驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|已啟用*ConnectionHandle*的非同步處理。 已呼叫函式，在完成執行之前，會在*ConnectionHandle*上呼叫[SQLCancelHandle 函數](../../../odbc/reference/syntax/sqlcancelhandle-function.md)，然後在*ConnectionHandle*上再次呼叫**SQLDriverConnect**函數。<br /><br /> 或者，已呼叫**SQLDriverConnect**函式，在完成執行之前，會從多執行緒應用程式中的不同執行緒在*ConnectionHandle*上呼叫**SQLCancelHandle** 。|  
|HY010|函數順序錯誤|（DM）已針對*ConnectionHandle*呼叫另一個非同步執行的函式（非**SQLDriverConnect**），而且在呼叫**SQLDriverConnect**函式時仍在執行中。|  
|HY013|記憶體管理錯誤|無法處理**SQLDriverConnect**函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|（DM）為引數*StringLength1*指定的值小於0，而且不等於 SQL_NTS。<br /><br /> （DM）為引數*BufferLength*指定的值小於0。|  
|HY092|不正確屬性/選項識別碼|（DM）已 SQL_DRIVER_PROMPT *DriverCompletion*引數，且*WindowHandle*引數為 null 指標。|  
|HY110|驅動程式完成無效|（DM）為引數*DriverCompletion*指定的值不等於 SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE、SQL_DRIVER_COMPLETE_REQUIRED 或 SQL_DRIVER_NOPROMPT。<br /><br /> （DM）已啟用連接共用，且為引數*DriverCompletion*指定的值不等於 SQL_DRIVER_NOPROMPT。|  
|HYC00|未執行的選擇性功能|此驅動程式不支援應用程式所要求的 ODBC 行為版本。|  
|HYT00|已超過逾時的設定|在資料來源的連接完成之前，登入超時時間已過期。 超時期間是透過**SQLSetConnectAttr**設定，SQL_ATTR_LOGIN_TIMEOUT。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）對應至指定資料來源名稱的驅動程式不支援函數。|  
|IM002|找不到資料來源，且未指定任何預設驅動程式|（DM）在系統資訊中找不到連接字串（*InConnectionString*）中指定的資料來源名稱，而且沒有預設的驅動程式規格。<br /><br /> （DM）在系統資訊中找不到 ODBC 資料來源和預設驅動程式資訊。|  
|IM003|無法載入指定的驅動程式|（DM） [系統資訊] 或 [**驅動程式**] 關鍵字所指定的資料來源規格中所列的驅動程式，或因某些原因而無法載入。|  
|IM004|SQL_HANDLE_ENV 上的驅動程式**SQLAllocHandle**失敗|（DM）在**SQLDriverConnect**期間，驅動程式管理員會以 SQL_HANDLE_ENV 的*fHandleType*呼叫驅動程式的**SQLAllocHandle**函數，而驅動程式會傳回錯誤。|  
|IM005|SQL_HANDLE_DBC 上的驅動程式**SQLAllocHandle**失敗。|（DM）在**SQLDriverConnect**期間，驅動程式管理員會以 SQL_HANDLE_DBC 的*fHandleType*呼叫驅動程式的**SQLAllocHandle**函數，而驅動程式會傳回錯誤。|  
|IM006|驅動程式的**SQLSetConnectAttr**失敗|（DM）在**SQLDriverConnect**期間，驅動程式管理員會呼叫驅動程式的**SQLSetConnectAttr**函式，而驅動程式會傳回錯誤。|  
|IM007|未指定任何資料來源或驅動程式;禁止的對話方塊|連接字串中未指定任何資料來源名稱或驅動程式，而且*DriverCompletion*已 SQL_DRIVER_NOPROMPT。|  
|IM008|對話方塊失敗|驅動程式嘗試顯示其登入對話方塊，但失敗。<br /><br /> *WindowHandle*是 null 指標，而且未 SQL_DRIVER_NO_PROMPT *DriverCompletion* 。|  
|IM009|無法載入轉譯 DLL|驅動程式無法載入為數據源或連接所指定的轉譯 DLL。|  
|IM010|資料來源名稱太長|（DM） DSN 關鍵字的屬性值長度超過 SQL_MAX_DSN_LENGTH 個字元。|  
|IM011|驅動程式名稱太長|（DM） **DRIVER**關鍵字的屬性值長度超過255個字元。|  
|IM012|驅動程式關鍵字語法錯誤|（DM） **DRIVER**關鍵字的關鍵字-值配對包含語法錯誤。<br /><br /> （DM） * \*InConnectionString*中的字串包含**FILEDSN**關鍵字，但此 .dsn 檔案未包含**DRIVER**關鍵字或**dsn**關鍵字。|  
|IM014|指定的 DSN 包含驅動程式與應用程式之間的架構不相符|（DM）32位應用程式使用連接到64位驅動程式的 DSN;或反之亦然。|  
|IM015|SQL_HANDLE_DBC_INFO_HANDLE 上的驅動程式 SQLDriverConnect 失敗|如果驅動程式傳回 SQL_ERROR，驅動程式管理員會傳回 SQL_ERROR 給應用程式，連線將會失敗。<br /><br /> 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊，請參閱[在 ODBC 驅動程式中開發連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 而且如果啟用通知模式，則必須在控制碼上呼叫**SQLCompleteAsync** ，才能執行後置處理並完成作業。|  
|S1118|驅動程式不支援非同步通知|當驅動程式不支援非同步通知時，您無法設定 SQL_ATTR_ASYNC_DBC_EVENT 或 SQL_ATTR_ASYNC_DBC_RETCODE_PTR。|  
  
## <a name="comments"></a>註解  
 連接字串的語法如下：  
  
 *連接字串*：： =*空字串*[;] &#124;*屬性*[;] &#124;*屬性*;*連接字串*  
  
 *empty 字串*：： =*attribute* ：： = *attribute-關鍵字*=*屬性-值*&#124; DRIVER = [{]*屬性-值*[}]  
  
 *attribute-關鍵字*：： = DSN &#124; UID &#124; PWD &#124;*驅動程式定義-attribute-關鍵字*  
  
 *屬性-值*：： =*字元字串*  
  
 *驅動程式定義-attribute-關鍵字*：： = *identifier*  
  
 其中，*字元字串*包含零或多個字元;*識別碼*有一或多個字元;*attribute-關鍵字*不區分大小寫;*屬性值*可能會區分大小寫;而**DSN**關鍵字的值不只包含空白。  
  
 由於連接字串和初始化檔文法的關係，包含字元 **[]{}（），;？的關鍵字和屬性值。= \*！** 不應避免以大括弧括住的 @。 **DSN**關鍵字的值不能只包含空格，且不應包含開頭空白。 由於系統資訊的文法，關鍵字和資料來源名稱不能包含反斜線（\\）字元。  
  
 應用程式不需要在**驅動程式**關鍵字後面加上大括弧，除非屬性包含分號（;)，在此情況下需要大括弧。 如果驅動程式收到的屬性值包含大括弧，驅動程式就不應該移除它們，但它們應該是所傳回連接字串的一部分。  
  
 以大括弧（{}）括住的 DSN 或連接字串值，其中包含任何字元 **[]{}（）、;？= \*！ @** 會原封不動地傳遞至驅動程式。 不過，在關鍵字中使用這些字元時，驅動程式管理員會在使用 file Dsn 時傳回錯誤，但會將連接字串傳遞至一般連接字串的驅動程式。 避免在關鍵字值中使用內嵌的大括弧。  
  
 連接字串可以包含任何數目的驅動程式定義的關鍵字。 由於**driver**關鍵字不會使用系統資訊中的資訊，因此驅動程式必須定義足夠的關鍵字，讓驅動程式只能使用連接字串中的資訊來連接到資料來源。 （如需詳細資訊，請參閱本節稍後的「驅動程式方針」）。驅動程式會定義連接至資料來源所需的關鍵字。  
  
 下表描述**DSN**、 **FILEDSN**、 **DRIVER**、 **UID**、 **PWD**和**SAVEFILE**關鍵字的屬性值。  
  
|關鍵字|屬性值描述|  
|-------------|---------------------------------|  
|**網上**|**SQLDataSources**或**SQLDriverConnect**的 [資料來源] 對話方塊所傳回之資料來源的名稱。|  
|**FILEDSN**|將為數據源建立連接字串之 dsn 檔案的名稱。 這些資料來源稱為「檔案資料來源」。|  
|**DRIVER**|**SQLDrivers**函數所傳回之驅動程式的描述。 例如，Rdb 或 SQL Server。|  
|**UID**|使用者識別碼。|  
|**PWD**|對應至使用者識別碼的密碼，如果沒有使用者識別碼（PWD =;) 的密碼，則為空字串。|  
|**SAVEFILE**|Dsn 檔案的檔案名，其中所使用之關鍵字的屬性值會在其中儲存、成功的連接。|  
  
 如需應用程式如何選擇資料來源或驅動程式的相關資訊，請參閱[選擇資料來源或驅動](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)程式。  
  
 如果連接字串中有重複的任何關鍵字，驅動程式會使用與第一次出現關鍵字相關聯的值。 如果**DSN**和**驅動程式**關鍵字包含在相同的連接字串中，驅動程式管理員和驅動程式會先使用任何出現的關鍵字。  
  
 **FILEDSN**和**DSN**關鍵字是互斥的：第一次出現的關鍵字會被使用，而第二個的則會被忽略。 另一方面， **FILEDSN**和**DRIVER**關鍵字並不會互斥。 如果有任何關鍵字出現在具有**FILEDSN**的連接字串中，則會使用連接字串中關鍵字的屬性值，而不是在 .dsn 檔案中的相同關鍵字的屬性值。  
  
 如果使用**FILEDSN**關鍵字，則會使用在 .dsn 檔案中指定的關鍵字來建立連接字串。 （如需詳細資訊，請參閱本節稍後的「檔案資料來源」）。**UID**關鍵字是選擇性的;只能使用**DRIVER**關鍵字建立一個. dsn 檔案。 **PWD**關鍵字不會儲存在 .dsn 檔案中。 儲存和載入 dsn 檔案的預設目錄會是**CommonFileDir**在 HKEY_LOCAL_MACHINE \software\microsoft\ Windows\CurrentVersion 和 "ODBC\DataSources" 中所指定路徑的組合。 （如果 CommonFileDir 是 "C:\Program Files\Common Files"，則預設目錄會是 "C:\Program Files\Common Files\ODBC\Data 來源"）。  
  
> [!NOTE]  
>  您可以呼叫安裝程式 DLL 中的[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)和[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)函式，直接操作 dsn 檔案。  
  
 如果使用**SAVEFILE**關鍵字，則用來讓目前的連線成功的關鍵字屬性值會以**SAVEFILE**關鍵字的屬性值名稱的形式儲存為. dsn 檔案。 **SAVEFILE**關鍵字必須與**DRIVER**關鍵字、 **FILEDSN**關鍵字或兩者一起使用，否則函式會傳回具有 SQLSTATE 01S09 （無效關鍵字） SQL_SUCCESS_WITH_INFO。 **SAVEFILE**關鍵字必須出現在連接字串的**DRIVER**關鍵字之前，否則結果會是未定義的。  
  
## <a name="driver-manager-guidelines"></a>驅動程式管理員指導方針  
 驅動程式管理員會在驅動程式的**SQLDriverConnect**函式的*InConnectionString*引數中，建立要傳遞至驅動程式的連接字串。 [驅動程式管理員] 不會修改應用程式傳遞給它的*InConnectionString*引數。  
  
 驅動程式管理員的動作是以*DriverCompletion*引數的值為基礎：  
  
-   SQL_DRIVER_PROMPT：如果連接字串不包含**DRIVER**、 **DSN**或**FILEDSN**關鍵字，驅動程式管理員就會顯示 [資料來源] 對話方塊。 它會從對話方塊所傳回的資料來源名稱，以及應用程式傳遞給它的任何其他關鍵字，來建立連接字串。 如果對話方塊所傳回的資料來源名稱是空的，則驅動程式管理員會指定「關鍵字-值組」 DSN = 預設值。 （此對話方塊不會顯示名稱為 "Default" 的資料來源）。  
  
-   SQL_DRIVER_COMPLETE 或 SQL_DRIVER_COMPLETE_REQUIRED：如果應用程式所指定的連接字串包含**DSN**關鍵字，驅動程式管理員就會複製應用程式所指定的連接字串。 否則，它會採取與*DriverCompletion* SQL_DRIVER_PROMPT 時相同的動作。  
  
-   SQL_DRIVER_NOPROMPT：驅動程式管理員會複製應用程式所指定的連接字串。  
  
 如果應用程式所指定的連接字串包含**DRIVER**關鍵字，驅動程式管理員就會複製應用程式所指定的連接字串。  
  
 驅動程式管理員會使用它所建立的連接字串，判斷要使用的驅動程式，連接到該驅動程式，並將它所結構化的連接字串傳遞給驅動程式;如需驅動程式管理員和驅動程式互動的詳細資訊，請參閱[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)函式中的「批註」一節。 如果連接字串不包含**driver**關鍵字，驅動程式管理員會決定要使用哪一個驅動程式，如下所示：  
  
1.  如果連接字串包含**DSN**關鍵字，驅動程式管理員會從系統資訊抓取與資料來源相關聯的驅動程式。  
  
2.  如果連接字串不包含**DSN**關鍵字，或找不到資料來源，驅動程式管理員會從系統資訊抓取與預設資料來源相關聯的驅動程式。 （如需詳細資訊，請參閱[預設](../../../odbc/reference/install/default-subkey.md)子機碼）。驅動程式管理員會將連接字串中的**DSN**關鍵字值變更為 "DEFAULT"。  
  
3.  如果連接字串中的**DSN**關鍵字設定為 "DEFAULT"，驅動程式管理員會從系統資訊抓取與預設資料來源相關聯的驅動程式。  
  
4.  如果找不到資料來源，而且找不到預設資料來源，驅動程式管理員會傳回具有 SQLSTATE IM002 的 SQL_ERROR （找不到資料來源，且未指定預設驅動程式）。  
  
## <a name="file-data-sources"></a>檔案資料來源  
 如果應用程式在**SQLDriverConnect**的呼叫中所指定的連接字串包含**FILEDSN**關鍵字，且此關鍵字未被**dsn**或**驅動程式**關鍵字取代，則驅動程式管理員會使用此 .dsn 檔案中的資訊和*InConnectionString*引數來建立連接字串。 驅動程式管理員會繼續進行，如下所示：  
  
1.  檢查 dsn 檔案的檔案名是否有效。 如果不是，則會傳回 SQLSTATE IM014 的 SQL_ERROR （檔案 DSN 的名稱無效）。 如果檔案名是空字串（""），而且未指定 SQL_DRIVER_NOPROMPT，則會顯示 [**開啟**檔案] 對話方塊。 如果檔案名包含有效路徑，但沒有檔案名或檔案名無效，而且未指定 SQL_DRIVER_NOPROMPT，則會顯示 [**開啟**檔案] 對話方塊，並將目前的目錄設定為檔案名中指定的檔案。 如果檔案名是空字串（""），或檔案名包含有效的路徑，但沒有檔案名或不正確檔案名，而且指定了 SQL_DRIVER_NOPROMPT，則 SQL_ERROR 會傳回 SQLSTATE IM014 （不正確 file DSN 名稱）。  
  
2.  讀取 .dsn 檔案的 [ODBC] 區段中的所有關鍵詞。 如果**驅動程式**關鍵字不存在，則會傳回具有 SQLSTATE IM012 （驅動程式關鍵字語法錯誤）的 SQL_ERROR，但不含 dsn 檔案的 unshareable，因此只會包含**dsn**關鍵字。  
  
     如果檔案資料來源是 unshareable，驅動程式管理員會讀取**DSN**關鍵字的值，並視需要連接到 unshareable 檔案資料來源所指向的使用者或系統資料來源。 不會執行步驟3到5。  
  
3.  為驅動程式建立連接字串。 驅動程式連接字串是在 .dsn 檔案中指定的關鍵字與原始應用程式連接字串中所指定的聯集。 在結構中，關鍵字重迭的驅動程式連接字串的規則如下所示：  
  
    -   如果**driver**關鍵字存在於應用程式連接字串中，而**驅動**程式關鍵字所指定的驅動程式在 .dsn 檔案和應用程式連接字串中並不相同，則會忽略該 dsn 檔案中的驅動程式資訊，並使用應用程式連接字串中的驅動程式資訊。 如果**驅動程式**關鍵字所指定的驅動程式在 .dsn 檔案和應用程式的連接字串中是相同的，則所有關鍵詞都會重迭，而在應用程式連接字串中指定的則會優先于在 .dsn 檔案中指定的位置。  
  
    -   在新的連接字串中，會排除**FILEDSN**關鍵字。  
  
4.  藉由查看登錄專案 HKEY_LOCAL_MACHINE \SOFTWARE\ODBC\ODBCINST. 來載入驅動程式INI\\<驅動程式\>名稱 \Driver \<，其中 driver name> 是由**driver**關鍵字指定。  
  
5.  將新的連接字串傳遞給驅動程式。  
  
 如需 dsn 檔案的範例，請參閱[使用檔案資料來源連接](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)。  
  
## <a name="savefile-keyword"></a>SAVEFILE 關鍵字  
 如果應用程式所指定的連接字串包含**SAVEFILE**關鍵字，則驅動程式管理員會將連接字串儲存在 .dsn 檔案中。 驅動程式管理員會繼續進行，如下所示：  
  
1.  檢查包含做為**SAVEFILE**關鍵字之屬性值的 dsn 檔案的檔案名是否有效。 如果不是，則會傳回 SQLSTATE IM014 的 SQL_ERROR （檔案 DSN 的名稱無效）。 檔案名的有效性是由標準系統命名規則所決定。 如果檔案名是空字串（""），而且未 SQL_DRIVER_NOPROMPT *DriverCompletion*引數，則檔案名會是有效的。 如果檔案名已經存在，則如果 SQL_DRIVER_NOPROMPT *DriverCompletion* ，則會覆寫檔案。 如果*DriverCompletion* SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE 或 SQL_DRIVER_COMPLETE_REQUIRED，對話方塊會提示使用者指定是否應該覆寫檔案。 如果未輸入，則會顯示 [檔案 **-儲存**] 對話方塊。  
  
2.  如果驅動程式傳回 SQL_SUCCESS 而且檔案名不是空字串，則驅動程式管理員會將*OutConnectionString*引數中所傳回的連接資訊，寫入至指定的檔案，並使用本節稍早的「連接字串」一節中所指定的格式。  
  
3.  如果驅動程式傳回 SQL_SUCCESS 而且檔案名是空字串（""），則驅動程式管理員會呼叫具有指定之*hwnd*的 [檔案 **-儲存**通用] 對話方塊，並將*OutConnectionString*中傳回的連接資訊寫入至 [檔案-儲存通用] 對話方塊中所指定的檔案，並使用本節稍早的「連接字串」一節中所指定的格式。  
  
4.  如果驅動程式傳回 SQL_SUCCESS，它會傳回包含應用程式之連接字串的*OutConnectionString*引數。  
  
5.  如果驅動程式傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR，則驅動程式管理員會將 SQLSTATE 傳回至應用程式。  
  
## <a name="driver-guidelines"></a>驅動程式指導方針  
 此驅動程式會檢查驅動程式管理員傳遞給它的連接字串是否包含**DSN**或**驅動程式**關鍵字。 如果連接字串包含**DRIVER**關鍵字，驅動程式就無法從系統資訊取得資料來源的相關資訊。 如果連接字串包含**dsn**關鍵字，或不包含**dsn**或**DRIVER**關鍵字，則驅動程式可以從系統資訊抓取資料來源的相關資訊，如下所示：  
  
1.  如果連接字串包含**DSN**關鍵字，驅動程式會抓取指定之資料來源的資訊。  
  
2.  如果連接字串不包含**DSN**關鍵字、找不到指定的資料來源，或**DSN**關鍵字設定為 "DEFAULT"，則驅動程式會抓取預設資料來源的資訊。  
  
 驅動程式會使用它從系統資訊中抓取的任何資訊，來擴大在連接字串中傳遞給它的資訊。 如果系統資訊中的資訊與連接字串中的資訊重複，驅動程式會使用連接字串中的資訊。  
  
 根據*DriverCompletion*的值，驅動程式會提示使用者輸入連接資訊，例如使用者識別碼和密碼，並連接到資料來源：  
  
-   SQL_DRIVER_PROMPT：驅動程式會顯示一個對話方塊，使用連接字串中的值和系統資訊（如果有的話）做為初始值。 當使用者離開對話方塊時，驅動程式會連接到資料來源。 它也會從*InConnectionString*中\*的**DSN**或**驅動程式**關鍵字值，以及從對話方塊傳回的資訊，來建立連接字串。 它會將這個連接字串放在 **OutConnectionString*緩衝區中。  
  
-   SQL_DRIVER_COMPLETE 或 SQL_DRIVER_COMPLETE_REQUIRED：如果連接字串包含足夠的資訊，而且該資訊是正確的，則驅動程式會連接到資料來源\*，並將*InConnectionString*複製到\* *OutConnectionString*。 如果遺失或不正確的資訊，驅動程式會採取與*DriverCompletion* SQL_DRIVER_PROMPT 時相同的動作，但如果*DriverCompletion*是 SQL_DRIVER_COMPLETE_REQUIRED，驅動程式會停用控制項，找出連接至資料來源時不需要的任何資訊。  
  
-   SQL_DRIVER_NOPROMPT：如果連接字串包含足夠的資訊，驅動程式會連接到資料來源，並\*將*InConnectionString*複製到\* *OutConnectionString*。 否則，驅動程式會傳回**SQLDriverConnect**的 SQL_ERROR。  
  
 成功連接到資料來源時，驅動程式也會將\* *StringLength2Ptr*設定為輸出連接字串的長度，以供在 **OutConnectionString*中傳回。  
  
 如果使用者取消驅動程式管理員或驅動程式所顯示的對話方塊， **SQLDriverConnect**會傳回 SQL_NO_DATA。  
  
 如需驅動程式管理員和驅動程式如何在連接過程中互動的相關資訊，請參閱[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)函式。  
  
 如果驅動程式支援**SQLDriverConnect**，驅動程式之系統資訊的 driver 關鍵字區段必須包含**ConnectFunctions**關鍵字，並將第二個字元集設定為 "Y"。  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>連接共用啟用時連線  
 連接共用可讓應用程式重複使用已建立的連接。 當呼叫**SQLDriverConnect**時，驅動程式管理員會嘗試使用連接共用的環境中連接集區的連線來建立連接。 如需連接共用的詳細資訊，請參閱[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
 應用程式可以在已啟用共用的連接上呼叫 SQLDisconnect 之前，先設定 SQL_ATTR_RESET_CONNECTION。 如需詳細資訊，請參閱[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 下列限制適用于應用程式呼叫**SQLDriverConnect**以連線到共用連接時：  
  
-   當連接字串中指定了**SAVEFILE**關鍵字時，不會執行任何連接共用處理。  
  
-   如果已啟用連接共用，則只能使用 SQL_DRIVER_NOPROMPT 的*DriverCompletion*引數來呼叫**SQLDriverConnect** 。如果使用任何其他*DriverCompletion*呼叫**SQLDriverConnect** ，則會傳回 SQLSTATE HY110 （不正確驅動程式完成）。  
  
## <a name="connection-attributes"></a>連接屬性  
 SQL_ATTR_LOGIN_TIMEOUT 連接屬性（使用**SQLSetConnectAttr**設定）會定義在傳回應用程式之前，驅動程式成功連接的等候登入要求完成的秒數。 如果系統提示使用者完成連接字串，每個登入要求的等待期間都會在驅動程式啟動連接進程時開始。  
  
 驅動程式預設會在 SQL_MODE_READ_WRITE 存取模式中開啟連接。 若要將存取模式設定為 SQL_MODE_READ_ONLY，應用程式必須先呼叫具有 SQL_ATTR_ACCESS_MODE 屬性的**SQLSetConnectAttr** ，然後再呼叫**SQLDriverConnect**。  
  
 如果在資料來源的系統資訊中指定預設轉譯程式庫，驅動程式會將它載入。 藉由使用 SQL_ATTR_TRANSLATE_LIB 屬性呼叫**SQLSetConnectAttr** ，可以載入不同的翻譯程式庫。 您可以使用 SQL_ATTR_TRANSLATE_OPTION 選項呼叫**SQLSetConnectAttr**來指定翻譯選項。  
  
 如需詳細資訊，請參閱[使用 SQLDriverConnect 連接](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)。  
  
```cpp  
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
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|配置控制碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|探索和列舉連接至資料來源所需的值|[SQLBrowseConnect 函數](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|連接到資料來源|[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|中斷與資料來源的連線|[SQLDisconnect 函式](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|傳回驅動程式描述和屬性|[SQLDrivers 函式](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|釋放控制碼|[SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
