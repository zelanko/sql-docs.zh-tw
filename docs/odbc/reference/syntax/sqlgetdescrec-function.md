---
title: SQLGetDescRec 函數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescRec
helpviewer_keywords:
- SQLGetDescRec function [ODBC]
ms.assetid: 325e0907-8e87-44e8-a111-f39e636a9cbc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 87d7b971b379f19f8451e924932a5e699e9b9983
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285483"
---
# <a name="sqlgetdescrec-function"></a>SQLGetDescRec 函式
**一致性**  
 推出版本: ODBC 3.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLGetDescRec**傳回描述符記錄的多個字段的當前設置或值。 傳回的欄位描述列或參數資料的名稱、資料類型和存儲。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLGetDescRec(  
      SQLHDESC        DescriptorHandle,  
      SQLSMALLINT     RecNumber,  
      SQLCHAR *       Name,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLSMALLINT *   TypePtr,  
      SQLSMALLINT *   SubTypePtr,  
      SQLLEN *        LengthPtr,  
      SQLSMALLINT *   PrecisionPtr,  
      SQLSMALLINT *   ScalePtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="arguments"></a>引數  
 *DescriptorHandle*  
 [輸入]描述符句柄。  
  
 *RecNumber*  
 [輸入]指示應用程式從中查找資訊的描述符記錄。 描述符記錄從 1 編號,記錄編號 0 是書籤記錄。 *RecNumber*參數必須小於或等於SQL_DESC_COUNT的值。 如果*RecNumber*小於或等於SQL_DESC_COUNT但該行不包含列或參數的數據,則對**SQLGetDescRec**的調用將返回欄位的預設值。 (有關詳細資訊,請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的"描述欄位的初始化"。  
  
 *名稱*  
 【輸出]指向要返回描述符記錄SQL_DESC_NAME欄位的緩衝區的指標。  
  
 如果*名稱*為 NULL,*則 StringLengthPtr*仍將傳回字元總數(不包括字元資料的空終止字元),這些字元可用於*返回名稱*指向的緩衝區中。  
  
 *緩衝區長度*  
 [輸入]**名稱*緩衝區的長度(以字元表示)。  
  
 *字串長度 Ptr*  
 【輸出]指向緩衝區的指標,用於返回\**名稱*緩衝區中可返回的數據字元數,不包括空終止字元。 如果字元數大於或等於*BufferLength,* 則\**名稱*中的數據將被截斷為*BufferLength*減去空終止字元的長度,並且被驅動程式終止為 null。  
  
 *類型 Ptr*  
 【輸出]指向緩衝區的指標,用於在其中返回描述符記錄的SQL_DESC_TYPE欄位的值。  
  
 *子型別的 Ptr*  
 【輸出]對於類型為SQL_DATETIME或SQL_INTERVAL的記錄,這是指向緩衝區的指標,用於返回SQL_DESC_DATETIME_INTERVAL_CODE字段的值。  
  
 *長度Ptr*  
 【輸出]指向緩衝區的指標,用於在其中返回描述符記錄的SQL_DESC_OCTET_LENGTH欄位的值。  
  
 *精密Ptr*  
 【輸出]指向緩衝區的指標,用於在其中返回描述符記錄的SQL_DESC_PRECISION欄位的值。  
  
 *縮放器*  
 【輸出]指向緩衝區的指標,用於在其中返回描述符記錄的SQL_DESC_SCALE欄位的值。  
  
 *空可點*  
 【輸出]指向緩衝區的指標,用於在其中返回描述符記錄的SQL_DESC_NULLABLE欄位的值。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_NO_DATA或SQL_INVALID_HANDLE。  
  
 如果*RecNumber*大於當前描述符記錄數,則返回SQL_NO_DATA。  
  
 如果*描述符句柄*是 IRD 句柄,並且語句處於準備或執行狀態,但沒有與其關聯的打開游標,則返回SQL_NO_DATA。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetDescRec**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有*Handle*SQL_HANDLE_DESC的*句柄類型*和*描述符句柄*。 下表列出了**SQLGetDescRec**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|緩衝區\**名稱*不夠大,無法返回整個描述符欄位。 因此,該欄位被截斷。 未壓縮的描述符位的長度在 #*StringLengthPtr*中傳回。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|07009|不合法的描述符索引|*欄位識別符*參數是記錄欄位 *,RecNumber*參數設定為 0,*描述符句柄*參數是 IPD 句柄。<br /><br /> (DM) *RecNumber*參數設定為 0,SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_OFF,*描述符句柄*參數是 IRD 句柄。<br /><br /> *RecNumber*參數小於 0。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY007|未準備關聯語句|*描述符句柄*與 IRD 相關聯,關聯的語句句柄未處於準備或執行狀態。|  
|HY010|函式序列錯誤|(DM)*描述符處理*與*語句句柄*相關聯,在調用此函數時,調用了非同步執行函數(不是此函數),並且仍在執行。<br /><br /> (DM)*描述符句柄*與*語句句柄*相關聯,SQL_NEED_DATA調用並返回 SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLExecute****SQLExecDirect****SQLSetPos。** 在發送所有執行時數據參數或列的數據之前,調用了此功能。<br /><br /> (DM) 對於與*描述符句柄*關聯的連接句柄,調用了非同步執行函數。 調用**SQLGetDescRec**時,此異步函數仍在執行。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*描述符處理*關聯的驅動程式不支援該函數。|  
  
## <a name="comments"></a>註解  
 應用程式可以呼叫**SQLGetDescRec**來檢索單列或參數的以下描述符位的值:  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE(對於其類型為SQL_DATETIME或SQL_INTERVAL的記錄)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec**不檢索標頭欄位的值。  
  
 應用程式可以通過設置與字段對應的空指標的參數來阻止欄位設置的返回。  
  
 當應用程式呼叫**SQLGetDescRec**檢索特定描述符類型未定義的欄位的值時,該函數將返回SQL_SUCCESS但返回該欄位的值未定義。 例如,為 APD 或 ARD 的SQL_DESC_NAME或SQL_DESC_NULLABLE欄位調用**SQLGetDescRec**將返回SQL_SUCCESS但字段的未定義值。  
  
 當應用程式呼叫**SQLGetDescRec**檢索為特定描述符類型定義但尚未設置預設值但尚未設置的欄位的值時,該函數將返回SQL_SUCCESS但返回該字段的值未定義。 有關詳細資訊,請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的「描述欄位的初始化」。。  
  
 還可以通過調用**SQLGetDescField**單獨檢索欄位的值。 有關描述符標題或記錄中的欄位的說明,請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 有關描述符的詳細資訊,請參閱[描述子](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|繫結欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|繫結參數|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取得描述字列|[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|設定多個描述符位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
