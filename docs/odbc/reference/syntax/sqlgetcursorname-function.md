---
title: SQLGetCursorName 函數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 262eee1b795907c7c429443ae85a25485f257ed5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetcursorname-function"></a>SQLGetCursorName 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ISO 92  
  
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
 [輸出]這是要傳回資料指標名稱的緩衝區指標。  
  
 如果*Current*是 NULL， *NameLengthPtr*仍會傳回的總字元數 （不含字元資料 null 結束字元） 可用來傳回中所指向的緩衝區*Current*。  
  
 *BufferLength*  
 [輸入]長度\* *Current*，以字元為單位。 如果中的值 *\*Current*是 Unicode 字串 (當呼叫**SQLGetCursorNameW**)、 *Columnsize*引數必須是偶數。  
  
 *NameLengthPtr*  
 [輸出]這是要傳回的總字元數 （不包括 null 結束字元） 中的記憶體指標可用來傳回中\* *Current*。 可傳回的字元數目是否大於或等於*Columnsize*中的資料指標名稱\* *Current*會被截斷成*Columnsize*減去 null 結束字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetCursorName**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以藉由呼叫取得相關聯的 SQLSTATE 值**SQLGetDiagRec**與*HandleType*利用 SQL_HANDLE_STMT 的和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLGetCursorName** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|緩衝區\* *Current*仍不夠大，無法傳回整個資料指標名稱，所以已截斷的資料指標名稱。 中會傳回未截斷的資料指標名稱的長度 **NameLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY010|函數順序錯誤|(DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 此非同步函式還在執行時**SQLGetCursorName**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可以使用。 此函式呼叫之前的所有資料流處理的參數擷取資料。<br /><br /> 以非同步方式執行的函式的呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY015|沒有可用的資料指標名稱|(DM) 驅動程式為 ODBC 2 *.x*驅動程式陳述式上沒有任何開啟的資料指標及使用已設定任何資料指標名稱**SQLSetCursorName**。|  
|HY090|字串或緩衝區長度無效|(DM) 引數中指定的值*Columnsize*小於 0。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 資料指標名稱只用於定位的 update 和 delete 陳述式 (例如，**更新***資料表名稱*...**WHERE CURRENT OF** *資料指標名稱*)。 如需詳細資訊，請參閱[定位的更新和刪除陳述式](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)。 如果應用程式不會呼叫**SQLSetCursorName**若要定義資料指標名稱，此驅動程式產生的名稱。 這個名稱開頭為字母 SQL_CUR。  
  
> [!NOTE]  
>  ODBC 2 *.x*，當沒有任何開啟的資料指標並沒有名稱已由呼叫設定**SQLSetCursorName**，呼叫**SQLGetCursorName**傳回 SQLSTATE HY015 （沒有資料指標名稱有的話）。 在 ODBC 3 *.x*，這不會再為 true，不論何時**SQLGetCursorName**是呼叫，驅動程式會傳回資料指標名稱。  
  
 **SQLGetCursorName**傳回的名稱是否建立明確或隱含資料指標的名稱。 如果資料指標名稱就會隱含地產生**SQLSetCursorName**則不會呼叫。 **SQLSetCursorName**可以呼叫以重新命名的資料指標陳述式，只要游標位於未配置或已備妥狀態。  
  
 明確或隱含地設定資料指標名稱會保持原位直到*StatementHandle*與它相關聯卸除，則使用**SQLFreeHandle**與*HandleType*利用 SQL_HANDLE_STMT。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|執行 SQL 陳述式|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|準備執行陳述式|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|設定資料指標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
