---
title: SQLGetEnvAttr 函數 |微軟文件
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetEnvAttr
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLGetEnvAttr
helpviewer_keywords:
- SQLGetEnvAttr function [ODBC]
ms.assetid: 01f4590f-427a-4280-a1c3-18de9f7d86c1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 77cd24386a8eea6769aee59f3674b681c516d9ed
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285308"
---
# <a name="sqlgetenvattr-function"></a>SQLGetEnvAttr 函式
**一致性**  
 推出版本: ODBC 3.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLGetEnvAttr**傳回環境屬性的當前設置。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLGetEnvAttr(  
     SQLHENV        EnvironmentHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>引數  
 *環境處理*  
 [輸入]環境句柄。  
  
 *屬性*  
 [輸入]要檢索的屬性。  
  
 *ValuePtr*  
 【輸出]指向要返回*屬性*指定的屬性的當前值的緩衝區的指標。  
  
 如果*ValuePtr*為 NULL,*則 StringLengthPtr*仍將返回可用返回*ValuePtr*指向的緩衝區中的位元組總數(不包括字元資料的空終止字元)。  
  
 *緩衝區長度*  
 [輸入]如果*ValuePtr*指向字串,則此參數應\*為*ValuePtr*的長度。 如果\* *ValuePtr*是整數,則忽略*緩衝區長度*。 如果*\*ValuePtr*是 Unicode 字串(在呼叫**SQLGetEnvAttrW**時),*緩衝區長度*參數必須是偶數。 如果屬性值不是字串,則*緩衝區長度*未使用。  
  
 *字串長度 Ptr*  
 【輸出]指向緩衝區的指標,用於返回可在*\*ValuePtr*中返回的位元組總數(不包括空終止字元)。 如果*ValuePtr*是空指標,則不返回任何長度。 如果屬性值是字串,並且可供返回的位元組數大於或等於*BufferLength,* 則\**ValuePtr*中的數據將被截斷為*BufferLength*減去空終止字元的長度,並且由驅動程式終止。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetEnvAttr**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_ENV的*句柄類型*和環境*句柄**句柄。* 下表列出了**SQLGetEnvAttr**通常返回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|\* *ValuePtr*中傳回的資料被截斷為*緩衝區長度*減去 null 終止字元。 未壓縮字串值的長度在 #*StringLengthPtr*中返回。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY010|函式序列錯誤|(DM) **SQL_ATTR_ODBC_VERSION**尚未通過**SQLSetEnvAttr**設置。 如果使用**SQLAllocHandleStd,** 則無需顯式設置**SQL_ATTR_ODBC_VERSION。**|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY092|不合法屬性/選項識別碼|為參數*屬性*指定的值對於驅動程式支援的 ODBC 版本無效。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|為參數*屬性*指定的值是驅動程式支援的 ODBC 版本的有效 ODBC 環境屬性,但驅動程式不支援該屬性。|  
|IM001|驅動程式不支援此功能|(DM) 與*環境處理*對應的驅動程式不支援該函數。|  
  
## <a name="comments"></a>註解  
 有關屬性清單,請參閱[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。 沒有特定於驅動程式的環境屬性。 如果*屬性*指定返回字串的屬性 *,ValuePtr*必須是指向要返回字串的緩衝區的指標。 字串的最大長度(包括 null 端接位元組)將為*BufferLength*位元組。  
  
 **SQLGetEnvAttr**可以在環境句柄的分配和自由之間隨時調用。 應用程式為環境成功設置的所有環境屬性將一直持續到在具有SQL_HANDLE_ENV*的處理類型的**環境處理*上調用**SQLFreeHandle**為止。 可以在 ODBC 3 *.x*中同時分配多個環境句柄。 分配另一個環境後,一個環境中的環境屬性不受影響。  
  
> [!NOTE]
>  SQL_ATTR_OUTPUT_NTS環境屬性由符合標準的應用程式支援。 調用**SQLGetEnvAttr**時,ODBC 3 *.x*驅動程式管理器始終返回此屬性的SQL_TRUE。 SQL_ATTR_OUTPUT_NTS只能通過調用**SQLSetEnvAttr**設置為SQL_TRUE。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|傳回連線屬性的設定|[SQLGetConnectAttr 函數](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|傳回敘述屬性的設定|[SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|設定連線屬性|[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定環境屬性|[SQLSetEnvAttr 函式](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|設定敘述屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
