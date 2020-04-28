---
title: SQLGetStmtAttr 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetStmtAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetStmtAttr
helpviewer_keywords:
- SQLGetStmtAttr function [ODBC]
ms.assetid: e321d460-e997-4527-aee6-207cf5a498e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89e7c75b412a6358806017102915989a8370dd43
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303302"
---
# <a name="sqlgetstmtattr-function"></a>SQLGetStmtAttr 函數
**標準**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **摘要**  
 **SQLGetStmtAttr**會傳回語句屬性的目前設定。  
  
> [!NOTE]  
>  如需在 ODBC 3 時，驅動程式管理員將此函式對應至哪個功能的詳細資訊。*x*應用程式正在使用 ODBC 2。*x*驅動程式，請參閱[對應取代函式以取得應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLGetStmtAttr(  
     SQLHSTMT        StatementHandle,  
     SQLINTEGER      Attribute,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
 *特性*  
 源要取出的屬性。  
  
 *ValuePtr*  
 輸出緩衝區的指標，要在其中傳回*屬性*中指定之屬性的值。  
  
 如果*valueptr 是*為 Null， *StringLengthPtr*仍會傳回*valueptr 是*所指向的緩衝區中可傳回的位元組總數（不包括字元資料的 Null 終止字元）。  
  
 *BufferLength*  
 源如果*attribute*是 ODBC 定義的屬性，而且*valueptr 是*指向字元字串或二進位緩衝區，則這個引數應該是\* *valueptr 是*的長度。 如果*attribute*是 ODBC 定義的屬性，而\* *valueptr 是*是整數，則會忽略*BufferLength* 。 如果* \*valueptr 是*中傳回的值是 Unicode 字串（在呼叫**SQLGetStmtAttrW**時），則*BufferLength*引數必須是偶數。  
  
 如果*屬性*是驅動程式定義的屬性，則應用程式會藉由設定*BufferLength*引數，來指出該屬性對驅動程式管理員的本質。 *BufferLength*可以有下列值：  
  
-   如果* \*valueptr 是*是字元字串的指標，則*BufferLength*是字串或 SQL_NTS 的長度。  
  
-   如果* \*valueptr 是*是二進位緩衝區的指標，則應用程式會將 SQL_LEN_BINARY_ATTR （*長度*）宏的結果放在*BufferLength*中。 這會將負數值放在*BufferLength*中。  
  
-   如果* \*valueptr 是*是字元字串或二進位字串以外的值指標，則*BufferLength*應具有 SQL_IS_POINTER 的值。  
  
-   如果* \*valueptr 是*包含固定長度的資料類型，則*BufferLength*會適當地 SQL_IS_INTEGER 或 SQL_IS_UINTEGER。  
  
 *StringLengthPtr*  
 輸出緩衝區的指標，要在其中傳回* \*valueptr 是*中可傳回的位元組總數（不包括 null 終止字元）。 如果*valueptr 是*為 null 指標，則不會傳回長度。 如果屬性值是字元字串，而且可用來傳回的位元組數目大於或等於*BufferLength*，則* \*valueptr 是*中的資料會截斷為*BufferLength*減去 null 終止字元的長度，並由驅動程式以 null 終止。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetStmtAttr**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_STMT *HandleType*和*StatementHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出**SQLGetStmtAttr**常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|* \*Valueptr 是*中傳回的資料被截斷為*BufferLength*減去 null 終止字元的長度。 Untruncated 字串值的長度會在 **StringLengthPtr*中傳回。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|24000|指標狀態無效|引數*屬性*已 SQL_ATTR_ROW_NUMBER，且資料指標未開啟，或資料指標位於結果集開頭之前或結果集的結尾之後。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在引數*MessageText*中傳回的錯誤訊息描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY010|函數順序錯誤|（DM）已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLGetStmtAttr**函數時，這個非同步函式仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫非同步執行的函式，且在呼叫此函式時仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|*（DM） \*valueptr 是*是字元字串，而 BufferLength 小於零，但不等於 SQL_NTS。|  
|HY092|不正確屬性/選項識別碼|為引數*屬性*指定的值對驅動程式支援的 ODBC 版本無效。|  
|HY109|不正確資料指標位置|*屬性*引數已 SQL_ATTR_ROW_NUMBER，且資料列已被刪除或無法提取。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|為引數*屬性*指定的值，對於驅動程式所支援的 odbc 版本而言是有效的 odbc 語句屬性，但驅動程式並不支援。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）對應至*StatementHandle*的驅動程式不支援函數。|  
  
## <a name="comments"></a>評價  
 如需語句屬性的一般資訊，請參閱[語句屬性](../../../odbc/reference/develop-app/statement-attributes.md)。  
  
 呼叫**SQLGetStmtAttr**時，會在* \*valueptr 是*中傳回*屬性*中指定之語句屬性的值。 該值可以是 SQLULEN 值或以 null 結束的字元字串。 如果值是 SQLULEN 值，某些驅動程式可能只會寫入較低的32位或16位的緩衝區，並不會變更較高的順序位。 因此，應用程式應該使用 SQLULEN 的緩衝區，並在呼叫此函式之前，將值初始化為0。 此外，不會使用*BufferLength*和*StringLengthPtr*引數。 如果值是以 null 結束的字串，應用程式會在*BufferLength*引數中指定該字串的最大長度，而驅動程式會傳回* \*StringLengthPtr*緩衝區中該字串的長度。  
  
 允許呼叫**SQLGetStmtAttr**的應用程式與 ODBC 2 搭配使用。*x*驅動程式， **SQLGetStmtAttr**的呼叫會在驅動程式管理員中對應至**SQLGetStmtOption**。  
  
 下列語句屬性是唯讀的，因此可由**SQLGetStmtAttr**抓取，但不能由**SQLSetStmtAttr**所設定：  
  
-   SQL_ATTR_IMP_PARAM_DESC  
  
-   SQL_ATTR_IMP_ROW_DESC  
  
-   SQL_ATTR_ROW_NUMBER  
  
 如需可設定和抓取的屬性清單，請參閱[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|傳回連接屬性的設定|[SQLGetConnectAttr 函數](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定語句屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
