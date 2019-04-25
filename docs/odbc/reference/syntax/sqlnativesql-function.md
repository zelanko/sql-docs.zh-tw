---
title: SQLNativeSql 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab39d1fca288196dcf42da70083dad323c406ba0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62465954"
---
# <a name="sqlnativesql-function"></a>SQLNativeSql 函數
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ODBC  
  
 **摘要**  
 **SQLNativeSql**為已修改驅動程式所傳回的 SQL 字串。 **SQLNativeSql**不會執行 SQL 陳述式。  
  
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
 [輸出]在其中傳回的已翻譯的 SQL 字串緩衝區的指標。  
  
 如果*OutStatementText*為 NULL，就*TextLength2Ptr*仍會傳回 （不含字元資料的 null 終止字元） 的字元總數可傳回緩衝區中指向*OutStatementText*。  
  
 *BufferLength*  
 [輸入]中的字元數\* *OutStatementText*緩衝區。 如果在傳回的值 *\*InStatementText*是 Unicode 字串 (呼叫時**SQLNativeSqlW**)，則*Columnsize*引數必須是偶數。  
  
 *TextLength2Ptr*  
 [輸出]在其中傳回的字元 （不含 null 終止） 可用來傳回中總數緩衝區的指標\* *OutStatementText*。 可用來傳回字元的數目是否大於或等於*Columnsize*，則轉譯中的 SQL 字串\* *OutStatementText*會被截斷成*BufferLength*減去 null 結束字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLNativeSql**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可取得相關聯的 SQLSTATE 值，請呼叫**SQLGetDiagRec**具有*HandleType*利用 SQL_HANDLE_DBC 的並*處理*的*ConnectionHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLNativeSql** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|緩衝區\* *OutStatementText*仍不夠大，無法傳回完整的 SQL 字串，所以 SQL 字串遭截斷。 未截斷的 SQL 字串的長度會傳入 **TextLength2Ptr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08003|未開啟連接|*ConnectionHandle*無法處於連線狀態。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|22007|無效的日期時間格式|**InStatementText*包含無效的日期、 時間戳記值使用 escape 子句。|  
|24000|指標狀態無效|陳述式中參考的指標置於結果集或結果集的結尾之後開始之前。 具有原生的 DBMS 資料指標實作的驅動程式可能不會傳回此錯誤。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY009|使用無效的 null 指標|(DM) **InStatementText*是 null 指標。|  
|HY010|函數順序錯誤|(DM) 的呼叫以非同步方式執行的函式*ConnectionHandle*和仍在呼叫此函式時所執行。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|(DM) 引數*TextLength1*小於 0，但不是等於 SQL_NTS。|  
|||(DM) 引數*Columnsize*是 0，將引數大於或等於*OutStatementText*不是 null 指標。|  
|HY109|無效的資料指標位置|資料指標的目前資料列已刪除，或尚未擷取。 具有原生的 DBMS 資料指標實作的驅動程式可能不會傳回此錯誤。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*ConnectionHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 以下是範例，示範哪些**SQLNativeSql**可能會傳回下列輸入包含純量函式轉換的 SQL 字串。 假設資料來源中的整數類型的資料行 empid:  
  
```  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Microsoft SQL Server 的驅動程式可能會傳回下列已翻譯的 SQL 字串：  
  
```  
SELECT convert (smallint, empid) FROM employee  
```  
  
 ORACLE 伺服器的驅動程式可能會傳回下列已翻譯的 SQL 字串：  
  
```  
SELECT to_number (empid) FROM employee  
```  
  
 Ingres 的驅動程式可能會傳回下列已翻譯的 SQL 字串：  
  
```  
SELECT int2 (empid) FROM employee  
```  
  
 如需詳細資訊，請參閱 <<c0> [ 直接執行](../../../odbc/reference/develop-app/direct-execution-odbc.md)並[已備妥執行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)。  
  
## <a name="related-functions"></a>相關函數  
 無。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
