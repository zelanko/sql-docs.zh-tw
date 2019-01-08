---
title: SQLGetCursorName 函式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: faa88d18a5b682b98a56b6426ba6a94ee4687cab
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591812"
---
# <a name="sqlgetcursorname-function"></a>SQLGetCursorName 函數
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ISO 92  
  
 **摘要**  
 **SQLGetCursorName**傳回與指定的陳述式相關聯的資料指標名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLGetCursorName(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CursorName,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   NameLengthPtr);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *Current*  
 [輸出]在其中傳回資料指標名稱之緩衝區的指標。  
  
 如果*Current*為 NULL，就*NameLengthPtr*仍會傳回 （不含字元資料的 null 終止字元） 的字元總數可用來傳回中所指向的緩衝區*Current*。  
  
 *BufferLength*  
 [輸入]長度\* *Current*，以字元為單位。 如果中的值 *\*Current*是 Unicode 字串 (呼叫時**SQLGetCursorNameW**)，則*Columnsize*引數必須是偶數。  
  
 *NameLengthPtr*  
 [輸出]要在其中傳回 （不包括 null 結束字元） 的字元總數的記憶體指標來傳回在可用\* *Current*。 可用來傳回字元的數目是否大於或等於*Columnsize*中的資料指標名稱\* *Current*會被截斷成*Columnsize*減去 null 結束字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetCursorName**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可取得相關聯的 SQLSTATE 值，請呼叫**SQLGetDiagRec**使用*HandleType*利用 SQL_HANDLE_STMT 的和 a*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLGetCursorName** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|緩衝區\* *Current*仍不夠大，無法傳回整個資料指標名稱，所以已截斷的資料指標名稱。 未截斷的資料指標名稱的長度會傳入 **NameLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLGetCursorName**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> (DM) 的呼叫以非同步方式執行的函式*StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY015|沒有可用的資料指標名稱|(DM) 驅動程式的 ODBC 2 *.x*驅動程式陳述式中沒有任何開啟的資料指標，並使用已設定任何資料指標名稱**SQLSetCursorName**。|  
|HY090|字串或緩衝區長度無效|(DM) 引數中指定的值*Columnsize*為小於 0。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 資料指標名稱僅用於定位的 update 和 delete 陳述式 (例如**更新**_資料表名稱_...**WHERE CURRENT OF** _資料指標名稱_)。 如需詳細資訊，請參閱 <<c0> [ 定位更新和刪除陳述式](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)。 如果應用程式不會呼叫**SQLSetCursorName**來定義資料指標名稱，此驅動程式產生的名稱。 這個名稱開頭為字母 SQL_CUR。  
  
> [!NOTE]
>  ODBC 2 *.x*，在沒有任何開啟的資料指標和已設定沒有名稱的呼叫所**SQLSetCursorName**，來呼叫**SQLGetCursorName**傳回 SQLSTATE HY015 （沒有資料指標名稱有的話）。 在 ODBC 3 *.x*，這不會再為 true，不論何時**SQLGetCursorName**是呼叫，驅動程式會傳回資料指標名稱。  
  
 **SQLGetCursorName**傳回名稱是否建立明確或隱含資料指標的名稱。 如果資料指標名稱就會以隱含方式產生**SQLSetCursorName**就不會呼叫。 **SQLSetCursorName**可以呼叫來重新命名的資料指標陳述式，只要游標處於已配置或已備妥狀態。  
  
 設定之前明確或隱含地設定資料指標名稱會維持*StatementHandle*與它相關聯卸除，則使用**SQLFreeHandle**使用*HandleType*利用 SQL_HANDLE_STMT。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|執行 SQL 陳述式|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|準備執行陳述式|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|設定資料指標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
