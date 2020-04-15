---
title: SQLGetCursor 名稱函數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetCursorName
helpviewer_keywords:
- SQLGetCursorName function [ODBC]
ms.assetid: e6e92199-7bb6-447c-8987-049a4c6ce05d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3ac65dc07897ddc789ee03b06b1bc1f71d37c3c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285546"
---
# <a name="sqlgetcursorname-function"></a>SQLGetCursorName 函數
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLGetCursorName**傳回與指定文句關聯的游標名稱。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLGetCursorName(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CursorName,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   NameLengthPtr);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
 *游標名稱*  
 【輸出]指向要返回游標名稱的緩衝區的指標。  
  
 如果*CursorName 名稱*為 NULL,NameLengthPtr 仍將傳回字元總數(不包括字元資料的空終止字元),這些字元可在*NameLengthPtr**CursorName*指向的緩衝區中傳回。  
  
 *緩衝區長度*  
 [輸入]\**游標名稱*的長度 ,以字元表示。 如果*\*CursorName*中的值是 Unicode 字串(在呼叫**SQLGetCursorNameW**時),*則緩衝區長度*參數必須是偶數。  
  
 *名稱長度 Ptr*  
 【輸出]傳回在\**CursorName*中傳回的字元總數(不包括空終止字元)的記憶體的指標。 如果可供返回的字元數大於或等於*BufferLength,* 則\**CursorName*中的遊標名稱將截斷為 *「緩衝區長度*」減去空終止字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetCursorName**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*敘述的句**柄*。 下表列出了**SQLGetCursorName**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|緩衝區\* *CursorName*不夠大,無法傳回整個游標名稱,因此游標名稱被截斷。 未壓縮的游標名稱的長度在 #*NameLengthPtr*中返回。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 呼叫**SQLGetCursorName**函數時,此非同步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數,並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY015|沒有可用的游標名稱|(DM) 驅動程式是 ODBC 2 *.x*驅動程式,語句上沒有打開的游標,並且沒有使用**SQLSetCursorName**設定游標名稱。|  
|HY090|不合法的字串或緩衝區長度|(DM) 參數*緩衝區長度*中指定的值小於 0。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
  
## <a name="comments"></a>註解  
 游標名稱只有定位的更新與移除語句(例如,**更新**_表名_...**其中游**_標名稱_的目前 。 有關詳細資訊,請參閱[位置更新與刪除語句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)。 如果應用程式不呼叫**SQLSetCursorName**來定義游標名稱,則驅動程式將生成一個名稱。 此名稱以字母SQL_CUR開頭。  
  
> [!NOTE]
>  在 ODBC 2 *.x*中,當沒有打開的游標,並且沒有透過呼叫**SQLSetCursorName**設定名稱時,對**SQLGetCursorName 的**呼叫傳回 SQLSTATE HY015(沒有可用的游標名稱)。 在 ODBC 3 .x 中,這不再正確;在 ODBC 3 *.x*中,這不再正確。無論何時呼叫**SQLGetCursorName,** 驅動程式都會傳回游標名稱。  
  
 **SQLGetCursorName**傳回游標的名稱,無論該名稱是顯式還是隱式創建。 如果未呼叫**SQLSetCursorName,** 則隱式產生游標名稱。 只要游標處於已分配或準備狀態,就可以調用**SQLSetCursorName**在語句上重新命名游標。  
  
 明確設定或隱式設定的游標名稱會保持設定,直到刪除與其關聯的*語句方向*,使用**有** *SQL_HANDLE_STMT的句柄類型*。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行準備好的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|準備執行敘述|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|設定游標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
