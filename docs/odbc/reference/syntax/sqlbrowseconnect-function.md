---
title: SQLBrowse連接功能 |微軟文件
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
ms.openlocfilehash: 607b0d764a694098a23111e9d7f4ce9755ea982d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301338"
---
# <a name="sqlbrowseconnect-function"></a>SQLBrowseConnect 函數
**一致性**  
 版本介紹: ODBC 1.0 標準合規性: ODBC  
  
 **摘要**  
 **SQLBrowseConnect**支援一種反覆運算方法,用於發現和枚舉連接到數據源所需的屬性和屬性值。 對**SQLBrowseConnect**的每個調用都返回連續的屬性和屬性值級別。 枚舉所有級別後,完成與數據源的連接 **,SQLBrowseConnect**傳回完整的連接字串。 SQL_SUCCESS或SQL_SUCCESS_WITH_INFO的返回代碼表示已指定所有連接資訊,並且應用程式現在已連接到數據源。  
  
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
 *連接句柄*  
 [輸入] 連線控制代碼。  
  
 *連接字串*  
 [輸入]瀏覽請求連接字串(請參閱"註解"中的'*連接字串*參數")。  
  
 *字串長度1*  
 [輸入]字元中的 *「連接字串」* 的長度。  
  
 *外連線字串*  
 【輸出]指向要返回瀏覽結果連接字串的字元緩衝區的指標(請參閱"註釋"中的 *「OutConnectString*參數」)。  
  
 如果*OutConnectString*為 NULL,*則 StringLength2Ptr*仍將返回字元總數(不包括字元數據的空終止字元),這些字元可在*OutConnectionString*指向的緩衝區中返回。  
  
 *緩衝區長度*  
 [輸入]**外連接字串*緩衝區的長度(以字元表示)。  
  
 *字串長度2Ptr*  
 【輸出]可在\**OutConnectionString*中返回的字元總數(不包括空終止)。 如果可用於返回的字元數大於或等於*BufferLength,* 則\**OutConnectionString*中的連接字串將截斷為*BufferLength*減去空終止字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_ERROR、SQL_INVALID_HANDLE或SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLBrowseConnect**傳回SQL_ERROR、SQL_SUCCESS_WITH_INFO 或SQL_NEED_DATA時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*連接句柄的句柄*。 下表列出了**SQLBrowseConnect**通常返回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|緩衝區\* *OutConnectionString*不夠大,無法返回整個流覽結果連接字串,因此該字串被截斷。 緩衝區 =*StringLength2Ptr*包含未壓縮的瀏覽結果連接字串的長度。 (函數返回SQL_NEED_DATA。|  
|01S00|不合法的連線字串屬性|在瀏覽請求連接字串 *(InConnectString)* 中指定了無效的屬性關鍵字。 (函數返回SQL_NEED_DATA。<br /><br /> 在瀏覽請求連接字串(*InConnectionString)* 中指定了不適用於當前連接等級的屬性關鍵字。 (函數返回SQL_NEED_DATA。|  
|01S02|值已變更|驅動程式不支援**SQLSetConnectAttr**中*ValuePtr*參數的指定值,並替換了類似的值。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08001|用戶端無法建立連線|驅動程式無法與數據源建立連接。|  
|08002|使用的連線名稱|(DM) 指定的連接已用於與數據源建立連接,並且連接已打開。|  
|08004|伺服器拒絕連接|數據源出於實現定義的原因拒絕建立連接。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程序嘗試連接到的數據源之間的通信鏈路失敗。|  
|28000|不合法的授權規範|用戶標識碼或授權字串或兩者(如瀏覽請求連接字串 *(InConnectionString)* 中指定)都違反了數據來源定義的限制。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|(DM) 驅動程式管理員無法分配支援執行或完成函數所需的記憶體。<br /><br /> 驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|通過調用[SQLCancelHandle 函數](../../../odbc/reference/syntax/sqlcancelhandle-function.md),非同步操作被取消。 然後,在*ConnectHandle*上再次調用原始函數。<br /><br /> 通過在*連接句柄*上從多線程應用程式中的不同線程調用**SQLCancelHandle,** 操作被取消。|  
|HY010|函式序列錯誤|(DM) 為*ConnectHandle*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) 為參數*StringLength1*指定的值小於 0,不等於SQL_NTS。<br /><br /> (DM) 為參數*BufferLength*指定的值小於 0。|  
|HY114|驅動程式不支援連接層級功能執行|(DM) 在進行連接之前,應用程式在連接句柄上啟用了非同步操作。 但是,驅動程式不支援對連接句柄進行非同步操作。|  
|HYT00|已超過逾時的設定|與數據源的連接完成之前,登錄超時期限已過期。 超時期間通過**SQLSetConnectAttr**SQL_ATTR_LOGIN_TIMEOUT設置。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 對應於指定數據來源名稱的驅動程式不支援該函數。|  
|IM002|找不到資料來源,未指定預設驅動程式|(DM) 在系統資訊中找不到瀏覽請求連接字串 *(InConnectionString)* 中指定的數據源名稱,也沒有預設驅動程式規範。<br /><br /> (DM) ODBC 資料來源和預設驅動程式資訊在系統資訊中找不到。|  
|IM003|無法載入指定的驅動程式|(DM) 由於其他原因找不到或無法載入**DRIVER**關鍵字中數據來源規範中列出的驅動程式。|  
|IM004|驅動程式的**SQLAllocHandle**上SQL_HANDLE_ENV失敗|(DM) 在**SQLBrowseConnect**期間,驅動程式管理器呼叫驅動程式的**SQLAllocHandle**函數,該*函數的句柄類型*為 SQL_HANDLE_ENV,驅動程式返回了錯誤。|  
|IM005|驅動程式的**SQLAllocHandle**上 SQL_HANDLE_DBC 失敗|(DM) 在**SQLBrowseConnect**期間,驅動程式管理器呼叫驅動程式的**SQLAllocHandle**函數,具有SQL_HANDLE_DBC的*句柄類型*,驅動程式返回了錯誤。|  
|IM006|驅動程式的**SQLSetConnectAttr**失敗|(DM) 在**SQLBrowseConnect**期間,驅動程式管理器呼叫驅動程式的**SQLSetConnectAttr**函數,驅動程式返回錯誤。|  
|IM009|無法載入轉換 DLL|驅動程式無法載入為資料來源或連接指定的轉換 DLL。|  
|IM010|資料來源名稱太長|(DM) DSN 關鍵字的屬性值大於SQL_MAX_DSN_LENGTH個字元。|  
|IM011|驅動程式名稱太長|(DM) DRIVER 關鍵字的屬性值超過 255 個字元。|  
|IM012|驅動程式關鍵字語法錯誤|(DM) DRIVER 關鍵字的關鍵字值對包含語法錯誤。|  
|IM014|指定的 DSN 包含驅動程式與應用程式之間的架構結構不符合|(DM) 32 位元應用程式使用 DSN 連接到 64 位元驅動程式;反之亦然。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
|S1118|驅動程式不支援非同步通知|當驅動程式不支援非同步通知時,無法設置SQL_ATTR_ASYNC_DBC_EVENT或SQL_ATTR_ASYNC_DBC_RETCODE_PTR。|  
  
## <a name="inconnectionstring-argument"></a>連接字串參數  
 瀏覽要求連接字串具有以下語法:  
  
 *連接字串*::**屬性*`;`= &#124;*屬性*`;`*連接字串*;<br>
 *屬性*::**屬性關鍵字*`=``DRIVER=`*屬性值*&#124;`}` =`{`屬性*值*|<br>
 *屬性關鍵字*`DSN``UID`::* &#124;&#124;&#124;`PWD`*驅動程式定義的屬性關鍵字*<br>
 *屬性值*::**字元字串*<br>
 *驅動程式定義的屬性關鍵字*::**識別子*<br>
  
 *其中字元字串*具有零個或多個字元;*標識符*具有一個或多個字元;*屬性關鍵字*不區分大小寫;*屬性值*可能區分大小寫;**DSN**關鍵字的值不只包含空白。 由於連接字串與初始化檔案語法,包含字串的關鍵字和屬性值 ***()、??{}應\*避免[!]** 。 由於系統資訊中的語法,關鍵字和數據源名稱不能包含反斜杠\\( ) 字元。 對於 ODBC 2。*x*驅動程式,在 DRIVER 關鍵字的屬性值周圍需要大括弧。  
  
 如果在瀏覽請求連接字串中重複任何關鍵字,驅動程式將使用與關鍵字的第一次出現關聯的值。 如果**DSN**和**DRIVER**關鍵字包含在相同的流覽請求連接字串中,則驅動程式管理器和驅動程式首先使用哪個關鍵字出現。  
  
 有關應用程式如何選擇資料來源或驅動程式的資訊,請參閱[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
## <a name="outconnectionstring-argument"></a>外連線字串參數  
 瀏覽結果連接字串是連接屬性的清單。 連接屬性由屬性關鍵字和相應的屬性值組成。 瀏覽結果連接字串具有以下語法:  
  
 *連接字串*::**attribute*`;`屬性 = &#124;*屬性*`;`*連接字串*<br>
 *屬性*::*`*`=*屬性關鍵字*`=`*屬性值*<br>
 *屬性關鍵字*::* *ODBC 屬性關鍵字*&#124;*驅動程式定義屬性關鍵字*<br>
 *ODBC 屬性關鍵字*`UID` `PWD`=`:`&#124; =*本地化識別符*=*驅動程式定義的屬性關鍵字*:::**識別符*`:`=*本地化識別符*=*屬性值*`{`:::**屬性值列表*`}`&#124;(`?`大括弧是文字的;它們由驅動程式返回。<br>
 *屬性值清單*::**字串*`:`=*本地化字串*= &#124;*字串*`:`=`,`*本地化字串*=*屬性值清單*<br>
  
 *其中字元字串*和*本地化字串*具有零個或多個字元;*標識碼*和*本地化識別碼*具有一個或多個字元;*屬性關鍵字*不區分大小寫;和*屬性值*可能區分大小寫。 由於連接字串與初始化檔案語法、關鍵字、本地化識別碼和包含字元 ***()、??{}應\*避免[!]** 。 由於系統資訊中的語法,關鍵字和數據源名稱不能包含反斜杠\\( ) 字元。  
  
 瀏覽結果連接字串語法根據以下文意規則使用:  
  
-   如果星號\*( ) 在*屬性關鍵字*之前,*則屬性*是選擇的,可以在**SQLBrowseConnect**的下一次呼叫中省略 。  
  
-   屬性關鍵字**UID**和**PWD**的含義與**SQLDriverConnect**中定義的含義相同。  
  
-   *驅動程式定義的屬性關鍵字*為可以提供屬性值的屬性類型命名。 例如,它可能是**伺服器**、**資料庫**、**主機**或**DBMS**。  
  
-   *ODBC 屬性關鍵字*和*驅動程式定義的屬性關鍵字*包括關鍵字的當地語系化或使用者友好版本。 應用程式可能會將其用作對話方塊中的標籤。 但是,在將瀏覽請求字串傳遞給驅動程式時,必須單獨使用**UID、PWD**或**UID***識別碼*。  
  
-   [*屬性-值清單*] 是對相應*屬性關鍵字*有效的實際值的枚舉。 請注意,大括弧({}) 不指示選項清單;因此,如果大括弧 ( ) 不指示選項清單。它們由司機返回。 例如,它可能是伺服器名稱的清單或資料庫名稱的清單。  
  
-   如果*屬性值*是單一問號 (?),則單個值對應於*屬性關鍵字*。 例如,UID_JohnS;PWD_芝麻。  
  
-   每次對**SQLBrowseConnect**的調用都僅返回滿足連接過程下一個級別所需的資訊。 驅動程式將狀態資訊與連接句柄關聯,以便始終可以在每次調用時確定上下文。  
  
## <a name="using-sqlbrowseconnect"></a>使用 SQLBrowse 連線  
 **SQLBrowseConnect**需要分配的連接。 驅動程式管理器載入在初始瀏覽請求連接字串中指定或對應於初始流覽請求連接字串中指定的資料來源名稱的驅動程式;有關發生這種情況的資訊,請參閱[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)中的"註釋"部分。 在流覽過程中,驅動程式可能與數據源建立連接。 如果**SQLBrowseConnect**傳回SQL_ERROR,則未完成的連接將終止,連接將返回到未連接狀態。  
  
> [!NOTE]  
>  **SQLBrowseConnect**不支援連接池。 如果在啟用連接池時調用**SQLBrowseConnect,** 則傳回 SQLSTATE HY000(一般錯誤)。  
  
 首次在連接上調用**SQLBrowseConnect**時,流覽請求連接字串必須包含**DSN**關鍵字或**DRIVER**關鍵字。 如果瀏覽要求連接字串包含**DSN**關鍵字,驅動程式管理員在系統資訊中找到相應的資料來源規範:  
  
-   如果驅動程式管理員找到相應的數據源規範,它將載入關聯的驅動程式 DLL;如果驅動程式管理員找到相應的資料來源規範,則載入相應的驅動程式 DLL。驅動程式可以從系統資訊中檢索有關數據來源的資訊。  
  
-   如果驅動程式管理員找不到相應的資料源規範,它將查找預設數據源規範並載入關聯的驅動程式 DLL;驅動程式可以從系統資訊中檢索有關預設數據源的資訊。 "DEFAULT"傳遞給 DSN 的驅動程式。  
  
-   如果驅動程式管理員找不到相應的資料來源規範,並且沒有預設資料源規範,它將返回 SQL_ERROR SQLSTATE IM002(找不到資料來源,未指定預設驅動程式)。  
  
 如果瀏覽請求連接字串包含 DRIVER 關鍵字,則驅動程式管理員將載入指定的驅動程式;如果瀏覽請求連接字串包含**DRIVER**關鍵字,則驅動程式管理員將載入指定的驅動程式。它不嘗試在系統資訊中查找數據源。 由於**DRIVER**關鍵字不使用系統資訊中的資訊,因此驅動程式必須定義足夠的關鍵字,以便驅動程式只能使用流覽請求連接字串中的資訊連接到數據源。  
  
 每次調用**SQLBrowseConnect**時,應用程式都會在流覽請求連接字串中指定連接屬性值。 驅動程式返回流覽結果連接字串中連續的屬性和屬性值級別;如果驅動程式,則返回這些值和屬性值。只要流覽請求連接字串中尚未枚舉連接屬性,它SQL_NEED_DATA返回。 應用程式使用流覽結果連接字串的內容來構建下一次調用**SQLBrowseConnect**的流覽請求連接字串。 所有必需屬性(在*OutConnectionString*參數中未帶有星號的屬性)必須包含在**SQLBrowseConnect**的下一次調用中。 請注意,在生成當前流覽請求連接字串時,應用程式無法使用以前的流覽結果連接字串的內容;也就是說,它不能為以前級別中設置的屬性指定不同的值。  
  
 枚舉所有級別的連接及其關聯屬性後,驅動程式將返回SQL_SUCCESS,與數據源的連接已完成,並且將返回一個完整的連接字串到應用程式。 連接字串適合與**SQLDriverConnect**結合使用,SQL_DRIVER_NOPROMPT選項來建立另一個連接。 但是,在**SQLBrowseConnect**的另一個調用中,無法使用完整的連接字串;如果再次調用**SQLBrowseConnect,** 則必須重複整個調用序列。  
  
 如果瀏覽過程中存在可恢復的非致命錯誤 **,SQLBrowseConnect**還會返回SQL_NEED_DATA;例如,應用程式提供的無效密碼或屬性關鍵字。 返回SQL_NEED_DATA且流覽結果連接字串保持不變時,將發生錯誤,應用程式可以調用**SQLGetDiagRec**返回 SQLSTATE 以獲取流覽時間錯誤。 這允許應用程式更正屬性並繼續流覽。  
  
 應用程式可以隨時透過調用**SQLDisconnect**終止瀏覽過程。 驅動程式將終止任何未完成的連接,並將連接返回到未連接狀態。  
  
 如果在連接句柄上啟用了非同步操作 **,SQLBrowseConnect**也可能返回SQL_STILL_EXECUTING。 當它返回SQL_NEED_DATA時,應用程式必須使用**SQLDisconnect**來取消瀏覽過程。 如果**SQLBrowseConnect**返回SQL_STILL_EXECUTING,則應用程式應使用**SQLCancelHandle**取消正在進行的操作。 在函數返回SQL_NEED_DATA返回後調用**SQLCancelHandle**不起作用。  
  
 有關詳細資訊,請參閱使用[SQLBrowse 連接連接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)。  
  
 如果驅動程式支援**SQLBrowseConnect,** 則驅動程式的系統資訊中的驅動程式關鍵字部分必須包含**ConnectFunctions**關鍵字,第三個字元設置為「Y」。。  
  
## <a name="code-example"></a>程式碼範例  
  
> [!NOTE]  
>  如果要連接到支援 Windows 身份驗證的資料來源提供者,則應在連接字串`Trusted_Connection=yes`中指定 而不是使用者 ID 和密碼資訊。  
  
 在下面的示例中,應用程式重複調用**SQLBrowseConnect。** 每次**SQLBrowseConnect**返回SQL_NEED_DATA時,它都會\*傳遞有關*OutConnectString*中所需數據的資訊。 應用程式將*OutConnectString*傳遞給其例程**GetUserInput(** 未顯示)。 **GetUserInput**解析資訊,生成並顯示一個對話框,並返回使用者\*在*InConnectionString*中輸入的資訊。 應用程式在下一次調用**SQLBrowseConnect**時將使用者的資訊傳遞給驅動程式。 在應用程式為驅動程式連接到數據源提供了所有必要的資訊後 **,SQLBrowseConnect**返回SQL_SUCCESS,應用程式將繼續。  
  
 有關透過呼叫**SQLBrowseConnect**連線到 SQL Server 驅動程式的詳細的範例,請參考[SQL Server 瀏覽範例](../../../odbc/reference/develop-app/sql-server-browsing-example.md)。  
  
 例如,要連接到數據源 Sales,可能會執行以下操作。 首先,應用程式將以下字串傳遞給**SQLBrowseConnect**:  
  
```  
"DSN=Sales"  
```  
  
 驅動程式管理器載入與數據源銷售關聯的驅動程式。 然後,它將調用驅動程式的**SQLBrowseConnect**函數,其參數與從應用程式接收的相同參數相同。 驅動程式傳回以下字串在 +*外連線字串*:  
  
```  
"HOST:Server={red,blue,green};UID:ID=?;PWD:Password=?"  
```  
  
 應用程式將此字串傳遞給其**GetUserInput**例程,該例程生成一個對話方塊,要求使用者選擇紅色、藍色或綠色伺服器並輸入使用者 ID 和密碼。 例程式將以下使用者指定的資訊傳\*回*InConnectionString*中,應用程式將這些資訊傳遞給**SQLBrowseConnect**:  
  
```  
"HOST=red;UID=Smith;PWD=Sesame"  
```  
  
 **SQLBrowseConnect**使用此資訊以 Smith 密碼芝麻的身份連線到紅色伺服器,然後在 +*OutConnectString*中傳回以下字串 :  
  
```  
"*DATABASE:Database={SalesEmployees,SalesGoals,SalesOrders}"  
```  
  
 應用程式將此字串傳遞給其**GetUserInput**例程,該例程生成一個對話框,要求使用者選擇資料庫。 使用者選擇 empdata,應用程式使用此字串呼叫**SQLBrowse 連接**最後一次:  
  
```  
"DATABASE=SalesOrders"  
```  
  
 這是驅動程式連接到數據源所需的最後一條資訊;**SQLBrowseConnect**傳回SQL_SUCCESS, 與 **外連線字串*包含已完成的連接字串:  
  
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
|配置連接句柄|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|連接到資料來源|[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|與資料源斷線連線|[SQLDisconnect 函式](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|使用連接字串或對話框連接到資料來源|[SQLDriverConnect 函數](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|傳回驅動程式描述與屬性|[SQLDrivers 函式](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|釋放連接句柄|[SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
