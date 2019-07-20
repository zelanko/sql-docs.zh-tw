---
title: SQLGetEnvAttr 函式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0940a5a2c70a7b670ca6a81521759fd08e60461e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345623"
---
# <a name="sqlgetenvattr-function"></a>SQLGetEnvAttr 函式
**標準**  
 引進的版本:ODBC 3.0 標準合規性:ISO 92  
  
 **摘要**  
 **SQLGetEnvAttr**會傳回環境屬性的目前設定。  
  
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
 *EnvironmentHandle*  
 源環境控制碼。  
  
 *Attribute*  
 源要取出的屬性。  
  
 *ValuePtr*  
 輸出緩衝區的指標, 要在其中傳回*屬性*所指定之屬性的目前值。  
  
 如果*valueptr 是*為 Null, *StringLengthPtr*仍會傳回*valueptr 是*所指向的緩衝區中可傳回的位元組總數 (不包括字元資料的 Null 終止字元)。  
  
 *BufferLength*  
 源如果*valueptr 是*指向字元字串, 這個引數應該是\* *valueptr 是*的長度。 如果\* *valueptr 是*是整數, 則會忽略*BufferLength* 。 *如果\*valueptr 是*是 Unicode 字串 (在呼叫**SQLGetEnvAttrW**時), 則*BufferLength*引數必須是偶數。 如果屬性值不是字元字串, 則不會使用*BufferLength* 。  
  
 *StringLengthPtr*  
 輸出緩衝區的指標, 要在其中傳回 *\*valueptr 是*中可傳回的位元組總數 (不包括 null 終止字元)。 如果*valueptr 是*為 null 指標, 則不會傳回長度。 如果屬性值是字元字串, 而且可用來傳回的位元組數目大於或等於*BufferLength*, 則\* *valueptr 是*中的資料會截斷為*BufferLength*減去 null 終止的長度字元, 並由驅動程式終止。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetEnvAttr**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時, 可以藉由呼叫 SQLGetDiagRec HandleType SQL_HANDLE_ENV 和  *EnvironmentHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。  下表列出**SQLGetEnvAttr**常傳回的 SQLSTATE 值, 並在此函式的內容中說明每一個值;「(DM)」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明, 否則, 與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|Error|說明|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|01004|字串資料, 右邊已截斷|\* *Valueptr 是*中傳回的資料被截斷為*BufferLength*減去 null 終止字元。 Untruncated 字串值的長度會在 **StringLengthPtr*中傳回。 (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|HY000|一般錯誤|發生錯誤, 但沒有任何特定 SQLSTATE, 且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中**的 SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 *\**|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY010|函數順序錯誤|(DM) **SQL_ATTR_ODBC_VERSION**尚未透過**SQLSetEnvAttr**設定。 如果您使用**SQLAllocHandleStd**, 則不需要明確設定**SQL_ATTR_ODBC_VERSION** 。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫, 因為無法存取基礎記憶體物件, 可能是因為記憶體不足的狀況。|  
|HY092|不正確屬性/選項識別碼|為引數*屬性*指定的值對驅動程式支援的 ODBC 版本無效。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|(DM) 如需暫停狀態的詳細資訊, 請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|為引數*屬性*指定的值是驅動程式所支援之 odbc 版本的有效 odbc 環境屬性, 但驅動程式並不支援。|  
|IM001|驅動程式不支援此功能|(DM) 對應至*EnvironmentHandle*的驅動程式不支援函數。|  
  
## <a name="comments"></a>註解  
 如需屬性的清單, 請參閱[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。 沒有驅動程式特定的環境屬性。 如果*屬性*指定了傳回字串的屬性, *valueptr 是*就必須是要傳回字串之緩衝區的指標。 字串的最大長度 (包含 null 終止位元組) 將會是*BufferLength*個位元組。  
  
 **SQLGetEnvAttr**可以在配置和釋放環境控制碼之間的任何時間呼叫。 環境的應用程式成功設定的所有環境屬性都會持續, 直到在*EnvironmentHandle*上呼叫**SQLFreeHandle** , 且*HandleType*為 SQL_HANDLE_ENV 為止。 ODBC 3.x 中可以同時配置一個以上的環境控制碼  。 當另一個環境已配置時, 不會影響一個環境上的環境屬性。  
  
> [!NOTE]
>  符合標準的應用程式支援 SQL_ATTR_OUTPUT_NTS 環境屬性。 呼叫**SQLGetEnvAttr**時, ODBC 3.X 驅動程式  管理員一律會傳回此屬性的 SQL_TRUE。 只有對**SQLSetEnvAttr**的呼叫, 才能將 SQL_ATTR_OUTPUT_NTS 設定為 SQL_TRUE。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|傳回連接屬性的設定|[SQLGetConnectAttr 函式](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|傳回語句屬性的設定|[SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函式](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定環境屬性|[SQLSetEnvAttr 函式](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|設定語句屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
