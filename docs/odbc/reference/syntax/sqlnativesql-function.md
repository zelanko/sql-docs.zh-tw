---
title: "SQLNativeSql 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLNativeSql
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLNativeSql
helpviewer_keywords:
- SQLNativeSql function [ODBC]
ms.assetid: b8efc247-27ab-4a00-92b6-1400785783fe
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1672e4c1f21d223ed326c0e0649fc7cbb2376f74
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlnativesql-function"></a>SQLNativeSql 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ODBC  
  
 **摘要**  
 **SQLNativeSql**已修改過此驅動程式會傳回 SQL 字串。 **SQLNativeSql**不會執行 SQL 陳述式。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLNativeSql(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      InStatementText,  
     SQLINTEGER     TextLength1,  
     SQLCHAR *      OutStatementText,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   TextLength2Ptr);  
```  
  
## <a name="arguments"></a>引數  
 *ConnectionHandle*  
 [輸入]連接控制代碼。  
  
 *InStatementText*  
 [輸入]要轉譯的 SQL 文字字串。  
  
 *TextLength1*  
 [輸入]中的字元長度 **InStatementText*文字字串。  
  
 *OutStatementText*  
 [輸出]用來傳回翻譯的 SQL 字串緩衝區的指標。  
  
 如果*OutStatementText*是 NULL， *TextLength2Ptr*仍會傳回的總字元數 （不含字元資料 null 結束字元） 可用來傳回緩衝區中所指*OutStatementText*。  
  
 *Columnsize*  
 [輸入]中的字元數\* *OutStatementText*緩衝區。 如果中傳回的值 *\*InStatementText*是 Unicode 字串 (當呼叫**SQLNativeSqlW**)、 *Columnsize*引數必須是偶數。  
  
 *TextLength2Ptr*  
 [輸出]這是要傳回的總字元數 （不含 null 終止） 來傳回中可用的緩衝區指標\* *OutStatementText*。 可傳回的字元數目是否大於或等於*Columnsize*、 轉譯中的 SQL 字串\* *OutStatementText*會被截斷成*Columnsize*減去 null 結束字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLNativeSql**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以藉由呼叫取得相關聯的 SQLSTATE 值**SQLGetDiagRec**與*HandleType*利用 SQL_HANDLE_DBC 的和*處理*的*ConnectionHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLNativeSql** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|緩衝區\* *OutStatementText*仍不夠大，無法傳回整個 SQL 字串，所以已截斷 SQL 字串。 中會傳回未截斷的 SQL 字串的長度 **TextLength2Ptr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08003|未開啟連線。|*ConnectionHandle*不是處於連線狀態。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|22007|無效的 datetime 格式|**InStatementText*包含逸出子句，無效的日期、 時間戳記值。|  
|24000|指標狀態無效|陳述式中參考的指標置於結果集或結果集的結尾之後開始之前。 由具有原生的 DBMS 資料指標實作的驅動程式不會傳回此錯誤。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY009|無效的 null 指標使用|(DM) **InStatementText*為 null 指標。|  
|HY010|函數順序錯誤|以非同步方式執行的函式的呼叫 (DM) *ConnectionHandle*和還在執行時呼叫此函式。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY090|字串或緩衝區長度無效|(DM) 引數*TextLength1*小於 0，但不是等於 SQL_NTS。|  
|||(DM) 引數*Columnsize*是 0 和引數大於或等於*OutStatementText*不是 null 指標。|  
|HY109|無效的資料指標位置|資料指標的目前資料列都已刪除，或未擷取。 由具有原生的 DBMS 資料指標實作的驅動程式不會傳回此錯誤。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*ConnectionHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 以下是範例，示範哪些**SQLNativeSql**可能會傳回下列輸入包含純量函數轉換的 SQL 字串。 假設資料來源中的整數類型的資料行 empid:  
  
```  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Microsoft SQL Server 的驅動程式可能會傳回下列翻譯的 SQL 字串：  
  
```  
SELECT convert (smallint, empid) FROM employee  
```  
  
 ORACLE 伺服器的驅動程式可能會傳回下列翻譯的 SQL 字串：  
  
```  
SELECT to_number (empid) FROM employee  
```  
  
 Ingres 的驅動程式可能會傳回下列翻譯的 SQL 字串：  
  
```  
SELECT int2 (empid) FROM employee  
```  
  
 如需詳細資訊，請參閱[直接執行](../../../odbc/reference/develop-app/direct-execution-odbc.md)和[已備妥執行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)。  
  
## <a name="related-functions"></a>相關函數  
 無。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)

