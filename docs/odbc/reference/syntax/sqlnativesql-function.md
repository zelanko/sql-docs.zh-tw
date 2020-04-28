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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9666bc767affb3b6bb624c416614079193d4b921
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304719"
---
# <a name="sqlnativesql-function"></a>SQLNativeSql 函數
**標準**  
 引進的版本： ODBC 1.0 標準合規性： ODBC  
  
 **摘要**  
 **SQLNativeSql**會傳回驅動程式修改的 SQL 字串。 **SQLNativeSql**不會執行 SQL 語句。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
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
 [輸入] 連線控制代碼。  
  
 *InStatementText*  
 源要轉譯的 SQL 文字字串。  
  
 *TextLength1*  
 源**InStatementText*文字字串的長度（以字元為單位）。  
  
 *OutStatementText*  
 輸出要在其中傳回已轉譯 SQL 字串之緩衝區的指標。  
  
 如果*OutStatementText*為 Null， *TextLength2Ptr*仍會傳回*OutStatementText*所指向的緩衝區中可傳回的字元總數（不包括字元資料的 Null 終止字元）。  
  
 *BufferLength*  
 源\* *OutStatementText*緩衝區中的字元數。 如果* \*InStatementText*中傳回的值是 Unicode 字串（在呼叫**SQLNativeSqlW**時），則*BufferLength*引數必須是偶數。  
  
 *TextLength2Ptr*  
 輸出緩衝區的指標，要在其中傳回\* *OutStatementText*中可傳回的字元總數（不包括 null 終止）。 如果可傳回的字元數大於或等於*BufferLength*， \* *OutStatementText*中轉譯的 SQL 字串會截斷為*BufferLength*減去 null 終止字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLNativeSql**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_DBC *HandleType*和*ConnectionHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出**SQLNativeSql**常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|緩衝區\* *OutStatementText*不夠大，無法傳回整個 sql 字串，因此 SQL 字串已截斷。 Untruncated SQL 字串的長度會在 **TextLength2Ptr*中傳回。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08003|連接未開啟|*ConnectionHandle*不是處於已線上狀態。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|22007|不正確日期時間格式|**InStatementText*包含含有無效日期、時間或時間戳記值的 escape 子句。|  
|24000|指標狀態無效|語句中所參考的資料指標，位於結果集開頭之前或結果集結尾的後面。 具有原生 DBMS 資料指標執行的驅動程式可能不會傳回此錯誤。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY009|Null 指標的使用不正確|（DM） **InStatementText*是 null 指標。|  
|HY010|函數順序錯誤|（DM）已針對*ConnectionHandle*呼叫非同步執行的函式，且在呼叫此函式時仍在執行中。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|（DM）引數*TextLength1*小於0，但不等於 SQL_NTS。|  
|||（DM）引數*BufferLength*小於0，而引數*OutStatementText*不是 null 指標。|  
|HY109|不正確資料指標位置|資料指標的目前資料列已被刪除或尚未提取。 具有原生 DBMS 資料指標執行的驅動程式可能不會傳回此錯誤。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*ConnectionHandle*相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>評價  
 以下是**SQLNativeSql**可能會針對包含純量函數轉換的下列輸入 SQL 字串傳回的範例。 假設資料行 empid 在資料來源中是整數類型：  
  
```sql  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Microsoft SQL Server 的驅動程式可能會傳回下列已轉譯的 SQL 字串：  
  
```sql  
SELECT convert (smallint, empid) FROM employee  
```  
  
 ORACLE 伺服器的驅動程式可能會傳回下列已轉譯的 SQL 字串：  
  
```sql  
SELECT to_number (empid) FROM employee  
```  
  
 Ingres 的驅動程式可能會傳回下列已轉譯的 SQL 字串：  
  
```sql  
SELECT int2 (empid) FROM employee  
```  
  
 如需詳細資訊，請參閱[直接執行](../../../odbc/reference/develop-app/direct-execution-odbc.md)和已備妥的[執行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)。  
  
## <a name="related-functions"></a>相關函數  
 無。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
