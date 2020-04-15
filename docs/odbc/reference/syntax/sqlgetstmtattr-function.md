---
title: SQLGetStmtAttr 函數 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303302"
---
# <a name="sqlgetstmtattr-function"></a>SQLGetStmtAttr 函數
**一致性**  
 推出版本: ODBC 3.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLGetStmtAttr**傳回敘述屬性的當前設置。  
  
> [!NOTE]  
>  有關驅動程式管理員將此功能映射到 ODBC 3 時的詳細資訊。*x*應用程式使用 ODBC 2。*x*驅動程式,請參閱[映射應用程式向後相容性的替代函數](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
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
 *語句句柄*  
 [輸入]語句句柄。  
  
 *屬性*  
 [輸入]要檢索的屬性。  
  
 *ValuePtr*  
 【輸出]指向要返回*屬性*中指定的屬性值的緩衝區的指標。  
  
 如果*ValuePtr*為 NULL,*則 StringLengthPtr*仍將返回可用返回*ValuePtr*指向的緩衝區中的位元組總數(不包括字元資料的空終止字元)。  
  
 *緩衝區長度*  
 [輸入]如果*屬性*是 ODBC 定義的屬性 *,ValuePtr*指向字串或二進位緩衝區,\*則此參數應為*ValuePtr*的長度。 如果*屬性*是 ODBC\*定義的屬性 *,ValuePtr*是整數,則忽略*緩衝區長度*。 如果*\*ValuePtr*中傳回的值是 Unicode 字串(在呼叫**SQLGetStmtAttrW**時),*緩衝區長度*參數必須是偶數。  
  
 如果*屬性*是驅動程式定義的屬性,則應用程式通過設置*BufferLength*參數指示該屬性對驅動程式管理員的性質。 *緩衝區長度*可以具有以下值:  
  
-   如果*\*ValuePtr*是指向字串的指標,則*緩衝區長度*是字串的長度或SQL_NTS。  
  
-   如果*\*ValuePtr*是指向二進位緩衝區的指標,則應用程式將SQL_LEN_BINARY_ATTR(*長度*)宏的結果放在*緩衝區長度*中。 這將在*緩衝區長度*中放置負值。  
  
-   如果*\*ValuePtr*是指向字串或二進位元字串以外的值的指標,則*BufferLength*應具有該值SQL_IS_POINTER。  
  
-   如果*\*ValuePtr*包含固定長度的數據類型,則*緩衝區長度*SQL_IS_INTEGER或SQL_IS_UINTEGER(視適用而定)。  
  
 *字串長度 Ptr*  
 【輸出]指向緩衝區的指標,用於返回可在*\*ValuePtr*中返回的位元組總數(不包括空終止字元)。 如果*ValuePtr*是空指標,則不返回任何長度。 如果屬性值是字串,並且可供返回的位元組數大於或等於*BufferLength,* 則*\*ValuePtr*中的數據將被截斷為*BufferLength*減去空終止字元的長度,並且被驅動程式終止。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetStmtAttr**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*語句句柄*的*句柄*。 下表列出了**SQLGetStmtAttr**通常返回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|ValuePtr 中返回的數據被截斷為*緩衝區長度*減去空終止字元的長度。 * \** 未壓縮字串值的長度在 #*StringLengthPtr*中返回。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|24000|指標狀態無效|參數*屬性*處於SQL_ATTR_ROW_NUMBER並且游標未打開,或者游標位於結果集開始之前或結果集結束之後。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在參數*MessageText*中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQLGetStmtAttr**函數時,此異步函數仍在執行。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數,並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|*(DM) \*ValuePtr*是一個字串,緩衝區長度小於零,但不等於SQL_NTS。|  
|HY092|不合法屬性/選項識別碼|為參數*屬性*指定的值對於驅動程式支援的 ODBC 版本無效。|  
|HY109|游標位置無效|*屬性*參數已SQL_ATTR_ROW_NUMBER,並且該行已被刪除或無法提取。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|為參數*屬性*指定的值是驅動程式支援的 ODBC 版本的有效 ODBC 語句屬性,但驅動程式不支援該屬性。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*對應的驅動程式不支援該函數。|  
  
## <a name="comments"></a>註解  
 有關敘述屬性的一般資訊,請參閱[敘述屬性](../../../odbc/reference/develop-app/statement-attributes.md)。  
  
 對**SQLGetStmtAttr 的**呼叫在*\*ValuePtr*中傳回*屬性*中指定的語句屬性的值。 該值可以是 SQLULEN 值,也可以是 null 端接字串。 如果值是 SQLULEN 值,則某些驅動程式可能只寫入緩衝區的較低 32 位元或 16 位元,並且保持高階位不變。 因此,應用程式應在調用此函數之前使用 SQLULEN 的緩衝區並將該值初始化為 0。 此外,不使用*緩衝區長度*和*字串長度 Ptr*參數。 如果該值是 null 端接字串,則應用程式在*BufferLength 參數*中指定該字串的最大長度,並且驅動程式將在*\*StringLengthPtr*緩衝區中傳回該字串的長度。  
  
 允許調用**SQLGetStmtAttr**的應用程式使用 ODBC 2。*x*驅動程式,對**SQLGetStmtAttr**的呼叫在驅動程式管理器映射到**SQLGetStmtOption**。  
  
 以下語句屬性是唯讀的,因此可以透過**SQLGetStmtAttr**檢索,但不能由**SQLSetStmtAttr**設定:  
  
-   SQL_ATTR_IMP_PARAM_DESC  
  
-   SQL_ATTR_IMP_ROW_DESC  
  
-   SQL_ATTR_ROW_NUMBER  
  
 有關可以設定和檢索的屬性清單,請參閱[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|傳回連線屬性的設定|[SQLGetConnectAttr 函數](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|設定連線屬性|[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定敘述屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
