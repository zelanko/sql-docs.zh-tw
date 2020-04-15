---
title: SQLGetDescfield 函數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescField
helpviewer_keywords:
- SQLGetDescField function [ODBC]
ms.assetid: f09ff660-1e4a-4370-be85-90d4da0487d3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89972d7f36b436868cc8e243b03827f095b90492
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285472"
---
# <a name="sqlgetdescfield-function"></a>SQLGetDescField 函數
**一致性**  
 推出版本: ODBC 3.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLGetDescField**傳回描述符記錄的單個字段的當前設置或值。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLGetDescField(  
     SQLHDESC        DescriptorHandle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     FieldIdentifier,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>引數  
 *DescriptorHandle*  
 [輸入]描述符句柄。  
  
 *RecNumber*  
 [輸入]指示應用程式從中查找資訊的描述符記錄。 描述符記錄從 0 編號,記錄編號 0 是書籤記錄。 如果*欄位識別子*參數指示標題欄位,則*忽略 RecNumber。* 如果*RecNumber*小於或等於SQL_DESC_COUNT但該行不包含列或參數的數據,則對**SQLGetDescField**的調用將返回欄位的預設值。 (有關詳細資訊,請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的"描述欄位的初始化"。  
  
 *FieldIdentifier*  
 [輸入]指示要返回其值的描述符的欄位。 有關詳細資訊,請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的「*欄位識別元*參數」部分。  
  
 *ValuePtr*  
 【輸出]指向要返回描述符資訊的緩衝區的指標。 資料類型取決於*字段標識碼*的值。  
  
 如果*ValuePtr*是整數類型,則應用程式應使用 SQLULEN 的緩衝區,並在調用此函數之前將值初始化為 0,因為某些驅動程式可能只寫入緩衝區的較低 32 位元或 16 位元,並且保持高階位不變。  
  
 如果*ValuePtr*為 NULL,*則 StringLengthPtr*仍將返回可用返回*ValuePtr*指向的緩衝區中的位元組總數(不包括字元資料的空終止字元)。  
  
 *緩衝區長度*  
 [輸入]如果*Field 識別碼*是 ODBC 定義的欄位 *,ValuePtr*指向字串或二進位緩衝區,則\*此參數應為*ValuePtr*的長度。 如果*欄位識別碼*是 ODBC\*定義的欄位 *,ValuePtr*是整數,則忽略*緩衝區長度*。 如果*\*ValuePtr*中的值是 Unicode 資料類型(在呼叫**SQLGetDescFieldW**時),*緩衝區長度*參數必須是偶數。  
  
 如果*Field 識別碼*是驅動程式定義的欄位,則應用程式透過設定*BufferLength*參數向驅動程式管理員指示該欄位的性質。 *緩衝區長度*可以具有以下值:  
  
-   如果*\*ValuePtr*是指向字串的指標,則*緩衝區長度*是字串的長度或SQL_NTS。  
  
-   如果*\*ValuePtr*是指向二進位緩衝區的指標,則應用程式將SQL_LEN_BINARY_ATTR(*長度*)宏的結果放在*緩衝區長度*中。 這將在*緩衝區長度*中放置負值。  
  
-   如果*\*ValuePtr*是指向字串或二進位元字串以外的值的指標,則*BufferLength*應具有該值SQL_IS_POINTER。  
  
-   如果*\*ValuePtr*包含固定長度的數據類型,則*緩衝區長度*是SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT或SQL_IS_USMALLINT(視適用)。  
  
 *字串長度 Ptr*  
 【輸出]指向要返回在 #*ValuePtr*中傳回的位元組總數(不包括空終止字元所需的位元)的緩衝區的指標。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_NO_DATA或SQL_INVALID_HANDLE。  
  
 如果*RecNumber*大於當前描述符記錄數,則返回SQL_NO_DATA。  
  
 如果*描述符句柄*是 IRD 句柄,並且語句處於準備或執行狀態,但沒有與其關聯的打開游標,則返回SQL_NO_DATA。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetDescField**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*語句句柄*的*句柄*。 下表列出了**SQLGetDescField**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|緩衝區\* *ValuePtr*不夠大,無法返回整個描述符欄位,因此該欄位被截斷。 未壓縮的描述符位的長度在 #*StringLengthPtr*中傳回。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|07009|不合法的描述符索引|(DM) *RecNumber*參數等於 0,SQL_ATTR_USE_BOOKMARK語句屬性SQL_UB_OFF,*描述符句柄*參數是 IRD 句柄。 (僅當描述符與語句句柄關聯時,才能為顯式分配的描述符返回此錯誤。<br /><br /> *欄位識別符*參數是記錄欄位 *,RecNumber*參數為 0,*描述符句柄*參數是 IPD 句柄。<br /><br /> *RecNumber*參數小於 0。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY007|未準備關聯語句|*描述符句柄*作為 IRD 與*語句句柄*相關聯,並且關聯的語句句柄尚未準備或執行。|  
|HY010|函式序列錯誤|(DM)*描述符處理*與*語句句柄*相關聯,在調用此函數時,調用了非同步執行函數(不是此函數),並且仍在執行。<br /><br /> (DM)*描述符句柄*與*語句句柄*相關聯,SQL_NEED_DATA調用並返回 SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLExecute****SQLExecDirect****SQLSetPos。** 在發送所有執行時數據參數或列的數據之前,調用了此功能。<br /><br /> (DM) 對於與*描述符句柄*關聯的連接句柄,調用了非同步執行函數。 呼叫**SQLGetDescField**函數時,此異步函數仍在執行。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY021|描述符資訊不一致|SQL_DESC_TYPE欄位和SQL_DESC_DATETIME_INTERVAL_CODE欄位不形成有效的 ODBC SQL 類型、有效的特定於驅動程式的 SQL 類型(對於 IPD)或有效的 ODBC C 類型(對於 AD 或 AD)。|  
|HY090|不合法的字串或緩衝區長度|(DM) * \*ValuePtr*是一個字串,*緩衝區長度*小於零。|  
|HY091|不合法的字段識別碼|*欄位識別碼*不是 ODBC 定義的欄位,不是實現定義的值。<br /><br /> 對*描述子處理*, 未定義*欄位識別碼*。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*描述符處理*關聯的驅動程式不支援該函數。|  
  
## <a name="comments"></a>註解  
 應用程式可以調用**SQLGetDescField**來傳回描述符記錄的單個字段的值。 對**SQLGetDescField**的呼叫可以傳回任何描述符類型中的任何欄位的設置,包括標頭欄位、記錄欄位和書籤欄位。 應用程式可以通過對**SQLGetDescField**進行重複調用,以任意順序獲取相同或不同描述符中的多個字段的設置。 也可以調用**SQLGetDescField**來返回驅動程式定義的描述符欄位。  
  
 出於性能原因,應用程式在執行語句之前不應調用**SQLGetDescField**進行 IRD。  
  
 在**SQLGetDescRec**的單個調用中,還可以檢索描述列或參數數據的名稱、數據類型和存儲的多個字段的設置。 可以調用**SQLGetStmtAttr**來傳回描述符標頭中單個字段的設置,該欄位也是語句屬性。 **SQLCol屬性****、SQL描述科爾**和**SQL 描述Param**返回記錄或書籤欄位。  
  
 當應用程式呼叫**SQLGetDescField**檢索特定描述符類型未定義的欄位的值時,該函數返回SQL_SUCCESS但返回該欄位的值未定義。 例如,為 APD 或 ARD 的SQL_DESC_NAME或SQL_DESC_NULLABLE欄位調用**SQLGetDescField**將返回SQL_SUCCESS但字段的未定義值。  
  
 當應用程式調用**SQLGetDescField**檢索為特定描述符類型定義但尚未設置預設值但尚未設置的欄位的值時,該函數返回SQL_SUCCESS但返回該字段的值未定義。 有關描述符欄位的初始化和欄位描述的詳細資訊,請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的「描述字欄位的初始化」。 有關描述符的詳細資訊,請參閱[描述子](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取得多個描述符位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定單一描述符欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定多個描述符位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
