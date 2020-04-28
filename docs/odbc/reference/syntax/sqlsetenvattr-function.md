---
title: SQLSetEnvAttr 函式 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetEnvAttr
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetEnvAttr
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC]
ms.assetid: 0343241c-4b15-4d4b-aa2b-2e8ab5215cd2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 640b1e6947d67b92e2b7f8e623597e1d99d4a877
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299538"
---
# <a name="sqlsetenvattr-function"></a>SQLSetEnvAttr 函數
**標準**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **摘要**  
 **SQLSetEnvAttr**會設定可管理環境層面的屬性。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLSetEnvAttr(  
     SQLHENV      EnvironmentHandle,  
     SQLINTEGER   Attribute,  
     SQLPOINTER   ValuePtr,  
     SQLINTEGER   StringLength);  
```  
  
## <a name="arguments"></a>引數  
 *EnvironmentHandle*  
 源環境控制碼。  
  
 *特性*  
 源要設定的屬性，列在 [批註] 中。  
  
 *ValuePtr*  
 源要與*屬性*相關聯之值的指標。 視*屬性*的值而定， *valueptr 是*會是32位的整數值，或指向以 null 結束的字元字串。  
  
 *StringLength*  
 源如果*valueptr 是*指向字元字串或二進位緩衝區，這個引數應該是 **valueptr 是*的長度。 如果是字元字串資料，這個引數應該包含字串中的位元組數目。  
  
 如果*valueptr 是*是整數，則會忽略*StringLength* 。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetEnvAttr**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_ENV *HandleType*和*EnvironmentHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出通常由**SQLSetEnvAttr**所傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。 如果驅動程式不支援環境屬性，則只有在連線時間才會傳回此錯誤。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S02|選項值已變更|驅動程式不支援在*valueptr 是*中指定的值，並會取代類似的值。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY009|Null 指標的使用不正確|屬性引數已識別出需要字串值的環境屬性，而*valueptr 是*引數為 null 指標。|  
|HY010|函數順序錯誤|（DM）已在*EnvironmentHandle*上配置連接控制碼。<br /><br /> （DM）尚未使用**SQLSetEnvAttr**設定**SQL_ATTR_ODBC_VERSION** ，且*屬性*不等於**SQL_ATTR_ODBC_VERSION**。 如果您使用**SQLAllocHandleStd**，則不需要明確地設定**SQL_ATTR_ODBC_VERSION** 。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY024|不正確屬性值|給定指定的*屬性*值，在*valueptr 是*中指定了不正確值。|  
|HY090|不正確字串或緩衝區長度|*StringLength*引數小於0，但不 SQL_NTS。|  
|HY092|不正確屬性/選項識別碼|（DM）為引數*屬性*指定的值，對於驅動程式所支援的 ODBC 版本而言是不正確。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|為引數*屬性*指定的值是驅動程式所支援之 odbc 版本的有效 odbc 環境屬性，但驅動程式不支援。<br /><br /> （DM）已 SQL_ATTR_OUTPUT_NTS*屬性*引數，而且已 SQL_FALSE *valueptr 是*。|  
  
## <a name="comments"></a>評價  
 只有在環境上沒有配置連接控制碼時，應用程式才能呼叫**SQLSetEnvAttr** 。 環境中應用程式成功設定的所有環境屬性都會持續，直到在環境上呼叫**SQLFreeHandle**為止。 ODBC 3.x 中可以同時配置一個*以上的環境*控制碼。  
  
 透過*valueptr 是*設定的資訊格式取決於指定的*屬性*。 **SQLSetEnvAttr**會以兩種不同格式的其中一種來接受屬性資訊：以 null 結束的字元字串或32位的整數值。 屬性的描述中會注明每個的格式。  
  
 沒有驅動程式特定的環境屬性。  
  
 呼叫**SQLSetEnvAttr**時，無法設定連接屬性。 嘗試這麼做會傳回 SQLSTATE HY092 （不正確屬性/選項識別碼）。  
  
|*特性*|*Valueptr 是*內容|  
|-----------------|-------------------------|  
|SQL_ATTR_CONNECTION_POOLING （ODBC 3.8）|32位的 SQLUINTEGER 值，可啟用或停用環境層級的連接共用。 會使用下列值：<br /><br /> SQL_CP_OFF = 連接共用已關閉。 這是預設值。<br /><br /> SQL_CP_ONE_PER_DRIVER = 每個驅動程式都支援單一連接集區。 集區中的每個連接都會與一個驅動程式相關聯。<br /><br /> SQL_CP_ONE_PER_HENV = 每個環境都支援單一連接集區。 集區中的每個連線都會與一個環境建立關聯。<br /><br /> SQL_CP_DRIVER_AWARE = 使用驅動程式的連接集區感知功能（如果有的話）。 如果驅動程式不支援連接集區感知，則會忽略 SQL_CP_DRIVER_AWARE 並使用 SQL_CP_ONE_PER_HENV。 如需詳細資訊，請參閱可[感知驅動程式的連接](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)共用。 在某些驅動程式支援的環境中，有些驅動程式不支援連線集區感知，SQL_CP_DRIVER_AWARE 可以在支援的驅動程式上啟用連線集區感知功能，但這相當於在不支援連線集區感知功能的那些驅動程式上設定 SQL_CP_ONE_PER_HENV。<br /><br /> 藉由呼叫**SQLSetEnvAttr** ，將 SQL_ATTR_CONNECTION_POOLING 屬性設定為 SQL_CP_ONE_PER_DRIVER 或 SQL_CP_ONE_PER_HENV，即可啟用連接共用。 必須先進行此呼叫，應用程式才會配置要啟用連接共用的共用環境。 **SQLSetEnvAttr**呼叫中的環境控制碼設定為 null，這會使 SQL_ATTR_CONNECTION_POOLING 進程層級的屬性。 啟用連接共用之後，應用程式會藉由呼叫**SQLAllocHandle**並將*InputHandle*引數設定為 SQL_HANDLE_ENV，來配置隱含的共用環境。<br /><br /> 啟用連線共用並選取應用程式的共用環境之後，就無法重設該環境的 SQL_ATTR_CONNECTION_POOLING，因為在設定這個屬性時，會以 null 環境控制碼呼叫**SQLSetEnvAttr** 。 如果在共用環境上已啟用連線集區時設定此屬性，此屬性只會影響後續配置的共用環境。<br /><br /> 您也可以在環境上啟用連接共用。 請注意下列關於環境連接共用的資訊：<br /><br /> -在 Null 控制碼上啟用連接共用是進程層級的屬性。 後續配置的環境將會是共用環境，並會繼承進程層級的連線集區設定。<br />-配置環境之後，應用程式仍然可以變更其連接集區設定。<br />-如果已啟用環境連接共用，且連接的驅動程式使用驅動程式共用，則環境共用會優先採用。<br /><br /> SQL_ATTR_CONNECTION_POOLING 會在驅動程式管理員內執行。 驅動程式不需要執行 SQL_ATTR_CONNECTION_POOLING。 ODBC 2.0 和3.0 應用程式可以設定此環境屬性。<br /><br /> 如需詳細資訊，請參閱 [ODBC 連接共用](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。|  
|SQL_ATTR_CP_MATCH （ODBC 3.0）|32位的 SQLUINTEGER 值，決定如何從連接集區中選擇連接。 呼叫**SQLConnect**或**SQLDriverConnect**時，驅動程式管理員會決定要從集區重複使用的連接。 驅動程式管理員會嘗試將呼叫中的連接選項和應用程式所設定的連接屬性，與集區中連接的關鍵字和連接屬性進行比對。 這個屬性的值會決定符合準則的有效位數層級。<br /><br /> 下列值是用來設定這個屬性的值：<br /><br /> SQL_CP_STRICT_MATCH = 只有完全符合呼叫中連接選項的連接，以及應用程式所設定的連接屬性，才會重複使用。 這是預設值。<br /><br /> SQL_CP_RELAXED_MATCH = 可以使用符合的連接字串關鍵字的連接。 關鍵字必須相符，但並非所有連接屬性都必須相符。<br /><br /> 如需驅動程式管理員如何在連接到共用連接時執行相符的詳細資訊，請參閱[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)。 如需連接共用的詳細資訊，請參閱[ODBC 連接](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)共用。|  
|SQL_ATTR_ODBC_VERSION （ODBC 3.0）|32位整數，判斷特定功能是否展現 ODBC 2.x*行為或 odbc* *3.x 行為。* 下列值是用來設定這個屬性的值：<br /><br /> SQL_OV_ODBC3_80 = 驅動程式管理員和驅動程式會展示下列 ODBC 3.8 行為：<br /><br /> -驅動程式會傳回，而且預期會*有 ODBC 3.x*程式碼的日期、時間和時間戳記。<br />-呼叫**SQLError**、 **SQLGetDiagField**或**SQLGetDiagRec**時，驅動程式會傳回 ODBC *3. x* SQLSTATE 程式碼。<br />- **SQLTables**呼叫中的*CatalogName*引數會接受搜尋模式。<br />-驅動程式管理員支援 C 資料類型擴充性。 如需 C 資料類型擴充性的詳細資訊，請參閱[ODBC 中的 c 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。<br /><br /> 如需詳細資訊，請參閱[ODBC 3.8 的新功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。<br /><br /> SQL_OV_ODBC3 = 驅動程式管理員和驅動程式會展示下列*ODBC 3.x*行為：<br /><br /> -驅動程式會傳回，而且預期會*有 ODBC 3.x*程式碼的日期、時間和時間戳記。<br />-呼叫**SQLError**、 **SQLGetDiagField**或**SQLGetDiagRec**時，驅動程式會傳回 ODBC *3. x* SQLSTATE 程式碼。<br />- **SQLTables**呼叫中的*CatalogName*引數會接受搜尋模式。<br />-驅動程式管理員不支援 C 資料類型擴充性。<br /><br /> SQL_OV_ODBC2 = 驅動程式管理員和驅動程式會展示下列*ODBC 2.x 行為。* 這對於*使用 odbc 3.x* *驅動程式的 odbc 2.x 應用程式*特別有用。<br /><br /> -驅動程式會傳回，而且預期會*有 ODBC 2.x*程式碼的日期、時間和時間戳記。<br />-呼叫**SQLError**、 **SQLGetDiagField**或**SQLGetDiagRec**時，驅動程式會傳回 ODBC *2. x* SQLSTATE 程式碼。<br />- **SQLTables**呼叫中的*CatalogName*引數不接受搜尋模式。<br />-驅動程式管理員不支援 C 資料類型擴充性。<br /><br /> 應用程式必須在呼叫具有 SQLHENV 引數的任何函式之前設定此環境屬性，否則呼叫將會傳回 SQLSTATE HY010 （函數順序錯誤）。 無論這些環境旗標是否有額外的行為，都是驅動程式特有的。<br /><br /> -如需詳細資訊，請參閱宣告[應用程式的 ODBC 版本](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)和[行為變更](../../../odbc/reference/develop-app/behavioral-changes.md)。|  
|SQL_ATTR_OUTPUT_NTS （ODBC 3.0）|32位整數，決定驅動程式傳回字串資料的方式。 如果 SQL_TRUE，驅動程式會傳回以 null 結束的字串資料。 如果 SQL_FALSE，驅動程式不會傳回以 null 結束的字串資料。<br /><br /> 此屬性預設為 SQL_TRUE。 呼叫**SQLSetEnvAttr**將其設定為 SQL_TRUE 會傳回 SQL_SUCCESS。 呼叫**SQLSetEnvAttr**將其設定為 SQL_FALSE 會傳回 SQL_ERROR 和 SQLSTATE HYC00 （未實作為選擇性功能）。|  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|配置控制碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|傳回環境屬性的設定|[SQLGetEnvAttr 函式](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 3.8 的新功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
