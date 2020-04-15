---
title: SQLDriver連接功能 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 88ec70d68b46beca97fd6b0d758e21aab5d4f4b2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302769"
---
# <a name="sqldriverconnect-function"></a>SQLDriverConnect 函數
**一致性**  
 版本介紹: ODBC 1.0 標準合規性: ODBC  
  
 **摘要**  
 **SQLDriverConnect**是**SQLConnect**的替代方法。 它支援比**SQLConnect**中的三個參數(用於提示使用者所有連接資訊的對話方塊)和系統資訊中未定義的資料來源需要更多的連接資訊的資料來源。  
  
 **SQLDriverConnect**提供以下連線屬性:  
  
-   使用包含數據源名稱、一個或多個用戶密碼、一個或多個密碼以及數據源所需的其他資訊的連接字串建立連接。  
  
-   使用部分連接字串或沒有附加資訊建立連接;在這種情況下,驅動程式管理器和驅動程式可以分別提示使用者提供連接資訊。  
  
-   建立與系統資訊中未定義的數據源的連接。 如果應用程式提供部分連接字串,驅動程式可以提示使用者提供連接資訊。  
  
-   使用從 .dsn 檔案中的資訊建構的連接字串建立與數據源的連接。  
  
 建立連接後 **,SQLDriverConnect**將傳回已完成的連接字串。 應用程式可以使用此字串執行後續連接請求。 有關詳細資訊,請參閱使用[SQLDriverConnect 連線](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)。  
  
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
 *連接句柄*  
 [輸入] 連線控制代碼。  
  
 *視窗控點*  
 [輸入]視窗句柄。 如果視窗句柄不適用或**SQLDriverConnect**不會顯示任何對話框,則應用程式可以傳遞父視窗的句柄(如果適用)或空指標。  
  
 *連接字串*  
 [輸入]完整的連接字串(請參閱"註釋"中的語法)、部分連接字串或空字串。  
  
 *字串長度1*  
 [輸入]如果字串為 Unicode,則長度 =*連接字串*,或字串為 ANSI 或 DBCS 的位元組。  
  
 *外連線字串*  
 【輸出]指向已完成連接字串的緩衝區。 成功連接到目標資料來源後,此緩衝區包含已完成的連接字串。 應用程式應為此緩衝區分配至少 1,024 個字元。  
  
 如果*OutConnectString*為 NULL,*則 StringLength2Ptr*仍將返回字元總數(不包括字元數據的空終止字元),這些字元可在*OutConnectionString*指向的緩衝區中返回。  
  
 *緩衝區長度*  
 [輸入]**外連接字串*緩衝區的長度(以字元表示)。  
  
 *字串長度2Ptr*  
 【輸出]指向緩衝區的指標,其中返回可在\**OutConnectString*中返回的字元總數(不包括空終止字元)。 如果可用於返回的字元數大於或等於*BufferLength,* 則\**OutConnectionString*中已完成的連接字串將截斷為*BufferLength*減去空終止字元的長度。  
  
 *驅動程式完成*  
 [輸入]指示驅動程式管理員或驅動程式是否必須提示更多連線資訊的標誌:  
  
 SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE、SQL_DRIVER_COMPLETE_REQUIRED或SQL_DRIVER_NOPROMPT。  
  
 (有關其他資訊,請參閱"註釋"。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR、SQL_INVALID_HANDLE 或SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDriverConnect**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有 SQL_HANDLE_DBC的*fHandleType*和*連接句柄*的*hHandle。* 下表列出了**SQLDriverConnect**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|緩衝區\* *OutConnectionString*不夠大,無法返回整個連接字串,因此連接字串被截斷。 未壓縮的連接字串的長度在 [*字串長度2Ptr*中傳回】 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01S00|不合法的連線字串屬性|在連接字串 *(InConnectionString)* 中指定了無效屬性關鍵字,但驅動程式無論如何都能夠連接到數據來源。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01S02|選項值已變更|驅動程式不支援**SQLSetConnectAttr**中的*ValuePtr*參數指向的指定值,並替換了類似的值。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01S08|錯誤儲存檔案 DSN|InConnectString 中的字串包含一個**FILESN**關鍵字,但 .dsn 檔未儲存。 * \** (函數返回SQL_SUCCESS_WITH_INFO。|  
|01S09|無效關鍵字|(DM) * \*InConnectString*中的字串包含**SAVEFILE**關鍵字,但不包含**驅動程式**或**FILESN**關鍵字。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08001|用戶端無法建立連線|驅動程式無法與數據源建立連接。|  
|08002|使用的連線名稱|(DM) 指定的*ConnectHandle*已用於與資料源建立連接,並且連接仍處於打開狀態。|  
|08004|伺服器拒絕連接|數據源出於實現定義的原因拒絕建立連接。|  
|08S01|通訊連結|在**SQLDriverConnect**函數完成處理之前,驅動程式與驅動程式嘗試連接到的數據源之間的通訊鏈路失敗。|  
|28000|不合法的授權規範|用戶識別碼或授權字串或連接字串 *(InConnectionString)* 中指定的兩者都違反了數據來源定義的限制。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*szMessageText*緩衝區中返回的錯誤消息描述了錯誤及其原因。|  
|HY000|一般錯誤:檔案 dsn 無效|(DM) =*InConnectString*中的字串包含一個 FILESN 關鍵字,但找不到 .dsn 檔案的名稱。|  
|HY000|一般錯誤:無法建立檔案緩衝區|(DM) =*InConnectString*中的字串包含一個 FILESN 關鍵字,但 .dsn 檔不可讀。|  
|HY001|記憶體配置錯誤|驅動程式管理員無法分配支援執行或完成**SQLDriverConnect**函數所需的記憶體。<br /><br /> 驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|為*連接句柄*啟用了非同步處理。 呼叫該函數,在完成執行之前,在*ConnectHandle*上調用[SQLCancelHandle 函數](../../../odbc/reference/syntax/sqlcancelhandle-function.md),然後在*ConnectHandle*上再次調用**SQLDriverConnect**函數。<br /><br /> 或者 **,SQLDriverConnect**函數被調用,在完成執行之前,SQLCancelHandle 是從多線程應用程式中的不同線程調用的**ConnectHandle。** *ConnectionHandle*|  
|HY010|函式序列錯誤|(DM) 另一個非同步執行函數(不是**SQLDriverConnect)** 被呼叫為*ConnectHandle,* 並且在呼叫**SQLDriverConnect**函數時仍在執行。|  
|HY013|記憶體管理錯誤|無法處理**SQLDriverConnect**函數呼叫,因為無法存取基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) 為參數*StringLength1*指定的值小於 0,不等於SQL_NTS。<br /><br /> (DM) 為參數*BufferLength*指定的值小於 0。|  
|HY092|不合法屬性/選項識別碼|(DM)*驅動程式完成*參數*SQL_DRIVER_PROMPT,WindowHandle*參數為空指標。|  
|HY110|驅動程式完成無效|(DM) 為參數 *「驅動程式完成」* 指定的值不等於SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE、SQL_DRIVER_COMPLETE_REQUIRED或SQL_DRIVER_NOPROMPT。<br /><br /> (DM) 連接池已啟用,為參數*Driver 完成*指定的值不等於SQL_DRIVER_NOPROMPT。|  
|HYC00|沒有選擇選擇功能|驅動程式不支援應用程式請求的 ODBC 行為版本。|  
|HYT00|已超過逾時的設定|與數據源的連接完成之前,登錄超時期限已過期。 超時期間通過**SQLSetConnectAttr**SQL_ATTR_LOGIN_TIMEOUT設置。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 對應於指定數據來源名稱的驅動程式不支援該函數。|  
|IM002|找不到資料來源,未指定預設驅動程式|(DM) 在系統資訊中找不到連接字串 *(InConnectionString)* 中指定的數據源名稱,並且沒有預設驅動程式規範。<br /><br /> (DM) ODBC 資料來源和預設驅動程式資訊在系統資訊中找不到。|  
|IM003|無法載入指定的驅動程式|(DM) 由於其他原因找不到或無法載入**DRIVER**關鍵字中數據來源規範中列出的驅動程式。|  
|IM004|驅動程式的**SQLAllocHandle**上 SQL_HANDLE_ENV 失敗|(DM) 在**SQLDriverConnect**期間,驅動程式管理器呼叫驅動程式的**SQLAllocHandle**函數,該函數具有*fHandleType* SQL_HANDLE_ENV,驅動程式傳回了錯誤。|  
|IM005|驅動程式的**SQLAllocHandle**上SQL_HANDLE_DBC失敗。|(DM) 在**SQLDriverConnect**期間,驅動程式管理器呼叫驅動程式的**SQLAllocHandle**函數,該函數具有*fHandleType* SQL_HANDLE_DBC,驅動程式傳回了錯誤。|  
|IM006|驅動程式的**SQLSetConnectAttr**失敗|(DM) 在**SQLDriverConnect**期間,驅動程式管理器呼叫驅動程式的**SQLSetConnectAttr**函數,驅動程式傳回錯誤。|  
|IM007|未指定數據源或驅動程式;禁止對話|連接字串中未指定資料來源名稱或驅動程式,並且*驅動程式完成*SQL_DRIVER_NOPROMPT。|  
|IM008|對話失敗|驅動程序嘗試顯示其登錄對話框,但失敗。<br /><br /> *WindowHandle*是一個空指標,*並且驅動程式完成*不是SQL_DRIVER_NO_PROMPT。|  
|IM009|無法載入轉換 DLL|驅動程式無法載入為資料來源或連接指定的轉換 DLL。|  
|IM010|資料來源名稱太長|(DM) DSN 關鍵字的屬性值大於SQL_MAX_DSN_LENGTH個字元。|  
|IM011|驅動程式名稱太長|(DM) **DRIVER**關鍵字的屬性值超過 255 個字元。|  
|IM012|驅動程式關鍵字語法錯誤|(DM) **DRIVER**關鍵字的關鍵字值對包含語法錯誤。<br /><br /> (DM) * \*InConnectString*中的字串包含**一個 FILESN**關鍵字,但 .dsn 檔不包含**DRIVER**關鍵字或**DSN**關鍵字。|  
|IM014|指定的 DSN 包含驅動程式與應用程式之間的架構結構不符合|(DM) 32 位元應用程式使用 DSN 連接到 64 位元驅動程式;反之亦然。|  
|IM015|驅動程式的 SQLDriver 連線SQL_HANDLE_DBC_INFO_HANDLE失敗|如果驅動程式返回SQL_ERROR,驅動程式管理員將返回SQL_ERROR到應用程式,連接將失敗。<br /><br /> 有關SQL_HANDLE_DBC_INFO_TOKEN的詳細資訊,請參閱在[ODBC 驅動程式中開發連接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
|S1118|驅動程式不支援非同步通知|當驅動程式不支援非同步通知時,無法設置SQL_ATTR_ASYNC_DBC_EVENT或SQL_ATTR_ASYNC_DBC_RETCODE_PTR。|  
  
## <a name="comments"></a>註解  
 連接字串有以下語法:  
  
 *連接字串*::**空字串*{;&#124;*屬性*{;] &#124;*屬性*;*連接字串*  
  
 *空字串*::**屬性*:::**屬性關鍵字*=*屬性值*&#124; DRIVER_*屬性值*{}}  
  
 *屬性關鍵字*::* DSN &#124; UID &#124; PWD &#124;*驅動程式定義的屬性關鍵字*  
  
 *屬性值*::**字元字串*  
  
 *驅動程式定義的屬性關鍵字*::**識別子*  
  
 *其中字元字串*具有零個或多個字元;*標識符*具有一個或多個字元;*屬性關鍵字*不區分大小寫;*屬性值*可能區分大小寫;**DSN**關鍵字的值不只包含空白。  
  
 由於連接字串與初始化檔案語法,包含字串的關鍵字和屬性值 ***()、??{}應避免\*** 用大括弧括起來的 [!] 。 **DSN**關鍵字的值不能僅包含空白,並且不應包含前導空格。 由於系統資訊的語法,關鍵字和數據源名稱不能包含反斜杠\\( ) 字元。  
  
 應用程式不必在**DRIVER**關鍵字之後在屬性值周圍添加大括弧,除非該屬性包含分號(;),在這種情況下需要大括弧。 如果驅動程式接收的屬性值包括大括弧,則驅動程式不應刪除它們,但它們應是返回的連接字串的一部分。  
  
 包含任何字元的{}**{}DSN 或連接字串值,包含括弧 (;?\**!]** 完好無損地傳遞給驅動程式。 但是,在關鍵字中使用這些字元時,驅動程式管理器在使用檔案 DSN 時返回一個錯誤,但將連接字串傳遞給驅動程式以進行常規連接字串。 避免在關鍵字值中使用嵌入大括弧。  
  
 連接字串可能包括任意數量的驅動程式定義的關鍵字。 由於**DRIVER**關鍵字不使用系統資訊中的資訊,因此驅動程式必須定義足夠的關鍵字,以便驅動程式只能使用連接字串中的資訊連接到資料來源。 (有關詳細資訊,請參閱本節後面的"駕駛員指南"。驅動程式定義連接到數據源所需的關鍵字。  
  
 下表描述了 DSN、FILEDSN、DRIVER、UID、PWD**UID**和**SAVEFILE**關鍵字**DSN****FILEDSN****DRIVER****PWD**的屬性值。  
  
|關鍵字|屬性值描述|  
|-------------|---------------------------------|  
|**Dsn**|**SQLDataSources**或**SQLDriverConnect**的數據源對話框返回的數據源的名稱。|  
|**備案**|.dsn 檔案的名稱,從中將為數據源生成連接字串。 這些數據源稱為文件數據源。|  
|**司機**|**SQLDriver**函數傳回的驅動程式的說明。 例如,Rdb或 SQL 伺服器。|  
|**UID**|使用者 ID。|  
|**Pwd**|與使用者ID對應的密碼,或空字串(如果使用者ID沒有密碼)(PWD=;)。|  
|**儲存檔案**|應保存 .dsn 檔的檔名,其中應儲存用於建立當前成功連接時使用的關鍵字的屬性值。|  
  
 有關應用程式如何選擇資料來源或驅動程式的資訊,請參閱[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 如果在連接字串中重複任何關鍵字,驅動程式將使用與關鍵字的第一次出現關聯的值。 如果**DSN**和**DRIVER**關鍵字包含在相同的連接字串中,則驅動程式管理器和驅動程式首先使用哪個關鍵字出現。  
  
 **FILEDSN**和**DSN**關鍵字是互斥的:使用哪個關鍵字先出現,而出現第二個關鍵字的關鍵字將被忽略。 另一方面 **,FILEDSN**和**DRIVER**關鍵字不是相互排斥的。 如果任何關鍵字出現在與**FILESN**的連接字串中,則使用連接字串中關鍵字的屬性值,而不是 .dsn 檔中同一關鍵字的屬性值。  
  
 如果使用**FILESN**關鍵字,則 .dsn 檔中指定的關鍵字將用於創建連接字串。 (有關詳細資訊,請參閱本節後面的"文件數據源"。**UID**關鍵字是可選的;但是,UID 關鍵字是可選的。可以僅使用**DRIVER**關鍵字創建 .dsn 檔。 **PWD**關鍵字不儲存在 .dsn 檔中。 保存和載入 .dsn 檔的預設目錄是 HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_Windows_Windows_當前版本和"ODBC_資料來源"中**由 CommonFileDir**指定的路徑的組合。 (如果通用 FileDir 是"C:*程式檔\公共檔",則默認目錄為"C:程式檔\常見檔\ODBC_數據來源"。  
  
> [!NOTE]  
>  通過調用安裝程式 DLL 中的[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)和[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)函數,可以直接操作 .dsn 檔。  
  
 如果使用**SAVEFILE**關鍵字,則用於進行當前成功連接的關鍵字的屬性值將保存為 .dsn 檔,該檔的名稱為**SAVEFILE**關鍵字的屬性值。 **SAVEFILE**關鍵字必須與**DRIVER**關鍵字 **、FILESN**關鍵字或兩者結合使用,否則函數返回SQL_SUCCESS_WITH_INFO SQLSTATE 01S09(無效關鍵字)。 **SAVEFILE**關鍵字必須出現在連接字串中的**DRIVER**關鍵字之前,否則結果將未定義。  
  
## <a name="driver-manager-guidelines"></a>駕駛員經理指南  
 驅動程式管理員建構一個連接字串,以傳遞給驅動程式的**SQLDriverConnect**函數的*InConnectionString*參數中的驅動程式。 驅動程式管理員不會修改應用程式傳遞給它的*InConnectionString*參數。  
  
 驅動程式管理員的操作基於*驅動程式完成*參數的值:  
  
-   SQL_DRIVER_PROMPT:如果連接字串不包含**DRIVER、DSN****DRIVER**或 **「已提交」** 關鍵字,則驅動程式管理員將顯示「資料源」對話方塊。 它建構一個連接字串,從對話框返回的數據源名稱以及應用程式傳遞給它的任何其他關鍵字。 如果對話框返回的數據源名稱為空,則驅動程式管理器指定關鍵字值對 DSN_Default。 (此對話框不會顯示名稱為"預設"的數據源。  
  
-   SQL_DRIVER_COMPLETE或SQL_DRIVER_COMPLETE_REQUIRED:如果應用程式指定的連接字串包含**DSN**關鍵字,則驅動程式管理員將複製應用程式指定的連接字串。 否則,它採取的操作與*SQL_DRIVER_PROMPT驅動程式完成*時相同的操作。  
  
-   SQL_DRIVER_NOPROMPT:驅動程式管理員複製應用程式指定的連接字串。  
  
 如果應用程式指定的連接字串包含**DRIVER**關鍵字,則驅動程式管理器將複製應用程式指定的連接字串。  
  
 使用它建構的連接字串,驅動程式管理員確定要使用的驅動程式,連接到該驅動程式,並將它建構的連接字串傳遞給驅動程式;有關驅動程式管理器和驅動程式交互的詳細資訊,請參閱[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)中的"註釋"部分。 如果連線字串不包含**DRIVER**關鍵字,驅動程式管理員將確定要使用的驅動程式,如下所示:  
  
1.  如果連接字串包含**DSN**關鍵字,驅動程式管理員將從系統資訊中檢索與數據源關聯的驅動程式。  
  
2.  如果連接字串不包含**DSN**關鍵字或找不到數據源,驅動程式管理器將從系統資訊中檢索與預設數據源關聯的驅動程式。 (關於詳細資訊,請參考[預設子鍵](../../../odbc/reference/install/default-subkey.md)。驅動程式管理員將連接字串中的**DSN**關鍵字的值更改為"DEFAULT"。  
  
3.  如果連接字串中的**DSN**關鍵字設定為"DEFAULT",驅動程式管理器將從系統資訊中檢索與預設數據源關聯的驅動程式。  
  
4.  如果未找到資料源,並且找不到預設數據源,則驅動程式管理器將返回 SQL_ERROR SQLSTATE IM002(找不到資料來源,未指定預設驅動程式)。  
  
## <a name="file-data-sources"></a>檔案資料來源  
 如果應用程式在調用**SQLDriverConnect**中指定的連接字串包含**FILESN**關鍵字,並且此關鍵字未被**DSN**或**DRIVER**關鍵字取代,則驅動程式管理器將使用 .dsn 檔和*InConnectString*參數中的資訊創建連接字串。 驅動程式管理員繼續如下:  
  
1.  檢查 .dsn 檔的檔名是否有效。 如果沒有,它將返回SQL_ERROR SQLSTATE IM014(文件 DSN 的無效名稱)。 如果檔案名是空字串 ("")且未指定SQL_DRIVER_NOPROMPT,則顯示 **「檔案打開」** 對話方塊。 如果檔名包含有效的路徑但沒有檔名或無效的檔名,並且未指定SQL_DRIVER_NOPROMPT,則「**檔案打開**」對話框將顯示目前的目錄設定為檔名中指定的目錄。 如果檔名是空字串 ("")或檔名包含有效的路徑,但沒有檔名或無效的檔名,並且SQL_DRIVER_NOPROMPT指定,則使用 SQLSTATE IM014(檔案 DSN 的無效名稱)返回SQL_ERROR。  
  
2.  讀取 .dsn 檔的 [ODBC] 部分中的所有關鍵字。 如果**DRIVER**關鍵字不存在,則傳回 SQL_ERROR SQLSTATE IM012(驅動程式關鍵字語法錯誤),除非 .dsn 檔不可共用,因此僅包含**DSN**關鍵字。  
  
     如果檔案資料來源不可分享,驅動程式管理員將讀取**DSN**關鍵字的值,並根據需要連接到不可分享檔案資料來源指向的使用者或系統數據來源。 步驟 3 到 5 未執行。  
  
3.  為驅動程式建構連接字串。 驅動程式連接字串是 .dsn 檔中指定的關鍵字和原始應用程式連接字串中指定的關鍵字的合併。 關鍵字重疊的驅動程式連接字串的建構規則如下所示:  
  
    -   如果應用程式連接字串中存在**DRIVER**關鍵字,並且**DRIVER**關鍵字指定的驅動程式在 .dsn 檔案和應用程式連接字串中不同,則忽略 .dsn 檔案中的驅動程式資訊,並使用應用程式連接字串中的驅動程式資訊。 如果**DRIVER**關鍵字指定的驅動程式在 .dsn 檔案和應用程式的連接字串中相同,則當所有關鍵字重疊時,應用程式連接字串中指定的驅動程式優先於 .dsn 檔中指定的驅動程式。  
  
    -   在新的連接字串中,將消除 **「已提交」** 關鍵字。  
  
4.  通過在註冊表項HKEY_LOCAL_MACHINE_軟體_ODBC_ODBCINST 中查找驅動程式。INI\\ \><驱动程序\<名稱 \ 驅動程式,其中驅動程式名稱>由**DRIVER**關鍵字指定。  
  
5.  傳遞驅動程式的新連接字串。  
  
 有關 .dsn 檔案的範例,請參考[檔案資料來源 。](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)  
  
## <a name="savefile-keyword"></a>儲存檔案關鍵字  
 如果應用程式指定的連接字串包含**SAVEFILE**關鍵字,則驅動程式管理器將連接字串儲存在 .dsn 檔中。 驅動程式管理員繼續如下:  
  
1.  檢查作為**SAVEFILE**關鍵字的屬性值包含的 .dsn 檔的檔名是否有效。 如果沒有,它將返回SQL_ERROR SQLSTATE IM014(文件 DSN 的無效名稱)。 檔名的有效性由標準系統命名規則確定。 如果檔名是空字串 ("")並且*驅動程式完成*參數不SQL_DRIVER_NOPROMPT,則檔名有效。 如果檔名已存在,則如果*SQL_DRIVER_NOPROMPT驅動程式完成*,則檔將被覆蓋。 如果 *「驅動程式完成」* 是SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE或SQL_DRIVER_COMPLETE_REQUIRED,則一個對話方塊會提示使用者指定是否應覆蓋該檔。 如果輸入"否",則將顯示 **"檔案儲存**"對話方塊。  
  
2.  如果驅動程式返回SQL_SUCCESS並且檔名不是空字串,則驅動程式管理器將*OutConnectionString*參數中傳回的連接資訊寫入指定檔,其格式位於本節前面的「連接字串」部分中。  
  
3.  如果驅動程式返回SQL_SUCCESS並且檔名是空字串 ("),則驅動程式管理器調用指定*hwnd* **的檔保存**公共對話框,並將 在*OutConnectString 中*傳回的連接資訊寫入「檔保存公共對話框」中指定的檔案,該格式在本節中稍早的「連接字串」部分中指定。  
  
4.  如果驅動程式返回SQL_SUCCESS,它將返回包含與應用程式的連接字串*的OutConnectString*參數。  
  
5.  如果驅動程式返回SQL_SUCCESS_WITH_INFO或SQL_ERROR,則驅動程式管理器將 SQLSTATE 返回到應用程式。  
  
## <a name="driver-guidelines"></a>駕駛員指南  
 驅動程式檢查驅動程式管理器傳遞給它的連接字串是否包含**DSN**或**DRIVER**關鍵字。 如果連接字串包含**DRIVER**關鍵字,則驅動程式無法從系統資訊中檢索有關數據來源的資訊。 如果連線字串包含**DSN**關鍵字或不包含**DSN**或**DRIVER**關鍵字,驅動程式可以從系統資訊中檢索有關資料來源的資訊,如下所示:  
  
1.  如果連接字串包含**DSN**關鍵字,驅動程式將檢索指定數據來源的資訊。  
  
2.  如果連接字串不包含**DSN**關鍵字,則找不到指定的資料來源,或者**DSN**關鍵字設置為"DEFAULT",驅動程式將檢索預設數據源的資訊。  
  
 驅動程式使用從系統資訊檢索到的任何資訊來增強在連接字串中傳遞給它的資訊。 如果系統資訊中的資訊複製連接字串中的資訊,則驅動程式將使用連接字串中的資訊。  
  
 根據*Driver 完成*的值,驅動程式會提示使用者取得連接資訊(如使用者 ID 和密碼)並連接到資料來源:  
  
-   SQL_DRIVER_PROMPT:驅動程式顯示一個對話框,使用連接字串中的值和系統資訊(如果有)作為初始值。 當使用者退出對話框時,驅動程式將連接到數據源。 它還從\**InConnectionString*中的**DSN**或**DRIVER**關鍵字的值以及從對話框返回的資訊構造連接字串。 它將此連接字串放在 +*外連接字串*緩衝區中。  
  
-   SQL_DRIVER_COMPLETE\*或SQL_DRIVER_COMPLETE_REQUIRED:如果連接字串包含足夠的資訊,並且該資訊是正確的,則驅動程式連接到資料源,並將*InConnectionString*複製\*到*OutConnectionString*。 如果缺少或不正確任何資訊,驅動程式將執行與*SQL_DRIVER_PROMPT Driver 完成*時相同的操作,但如果未SQL_DRIVER_COMPLETE_REQUIRED*驅動程式完成*,則驅動程式將禁用連接到數據源所需的任何資訊的控制項。  
  
-   SQL_DRIVER_NOPROMPT:如果\*連接字串包含足夠的資訊,驅動程式將連接到資料來源並將*InConnectString*複製\*到*OutConnectString*。 否則,驅動程式將返回**SQLDriverConnect**SQL_ERROR。  
  
 成功連接到資料源時,驅動程式還將\**StringLength2Ptr*設置到輸出連接字串的長度,該字串可在 +*OutConnectString*中返回。  
  
 如果使用者取消驅動程式管理器或驅動程式提供的對話框 **,SQLDriverConnect**將返回SQL_NO_DATA。  
  
 有關驅動程式管理員和驅動程式在連接過程中如何互動的資訊,請參閱[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
 如果驅動程式支援**SQLDriverConnect,** 則驅動程式的系統資訊的驅動程式關鍵字部分必須包含**ConnectFunctions**關鍵字,第二個字元設置為「Y」。。  
  
## <a name="connecting-when-connection-pooling-is-enabled"></a>開啟連線池時連接  
 連接池允許應用程式重用已創建的連接。 調用**SQLDriverConnect**時,驅動程式管理器嘗試使用已指定用於連接池的環境中的連接池中的連接。 有關連接池的詳細資訊,請參閱[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
 應用程式可以在啟用池的連接上調用 SQLDisconnect 之前設置SQL_ATTR_RESET_CONNECTION。 有關詳細資訊,請參閱[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 當應用程式呼叫**SQLDriverConnect**連線到池連線時,將應用以下限制:  
  
-   在連接字串中指定**SAVEFILE**關鍵字時,不執行連接池處理。  
  
-   如果啟用了連接池,則只能使用*驅動程式完成*參數SQL_DRIVER_NOPROMPT才能調用**SQLDriverConnect;** 如果**SQLDriverConnect**與任何其他*驅動程式完成*調用,則 SQLSTATE HY110(無效驅動程式完成)將返回。  
  
## <a name="connection-attributes"></a>連接屬性  
 使用**SQLSetConnectAttr**設定SQL_ATTR_LOGIN_TIMEOUT連接屬性定義等待登錄請求在返回應用程式之前由驅動程式成功完成連接的秒數。 如果提示使用者完成連接字串,則當驅動程式啟動連接過程時,每個登錄請求的等待期將開始。  
  
 默認情況下,驅動程式以SQL_MODE_READ_WRITE訪問模式打開連接。 要將存取模式設定為SQL_MODE_READ_ONLY,應用程式必須在調用**SQLDriverConnect**之前使用SQL_ATTR_ACCESS_MODE屬性調用**SQLSetConnectAttr。**  
  
 如果在數據源的系統資訊中指定了默認翻譯庫,驅動程式將載入它。 可以使用SQL_ATTR_TRANSLATE_LIB屬性調用**SQLSetConnectAttr**來載入不同的翻譯庫。 可以通過使用SQL_ATTR_TRANSLATE_OPTION選項調用**SQLSetConnectAttr**來指定轉換選項。  
  
 有關詳細資訊,請參閱使用[SQLDriverConnect 連線](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)。  
  
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
  
 另請參閱[ODBC 範例計畫](../../../odbc/reference/sample-odbc-program.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|配置控點|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|找到與枚舉連線到資料來源所需的值|[SQLBrowseConnect 函式](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|連接到資料來源|[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|與資料源斷線連線|[SQLDisconnect 函式](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|傳回驅動程式描述與屬性|[SQLDrivers 函式](../../../odbc/reference/syntax/sqldrivers-function.md)|  
|釋放手柄|[SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|設定連線屬性|[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
