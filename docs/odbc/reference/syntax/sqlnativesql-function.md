---
title: SQLNativeSql 函數 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304719"
---
# <a name="sqlnativesql-function"></a>SQLNativeSql 函數
**一致性**  
 版本介紹: ODBC 1.0 標準合規性: ODBC  
  
 **摘要**  
 **SQLNativeSql**傳回由驅動程式修改的 SQL 字串。 **SQLNativeSql**不執行 SQL 語句。  
  
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
 *連接句柄*  
 [輸入] 連線控制代碼。  
  
 *宣告文字*  
 [輸入]要翻譯的 SQL 文字字串。  
  
 *文字長度1*  
 [輸入]**語句文字*文字字串的字元的長度。  
  
 *外文文字*  
 【輸出]指向要返回翻譯的 SQL 字串的緩衝區的指標。  
  
 如果*Out語句文字*為*NULL,TextLength2Ptr*仍將傳回可用於在*Out語句文本*指向的緩衝區中返回的字元總數(不包括字元資料的空終止字元)。  
  
 *緩衝區長度*  
 [輸入]\* *Out聲明文字*緩衝區中的字元數。 如果在*\*In語句文字*中傳回的值是 Unicode 字串(在呼叫**SQLNativeSqlW**時),*緩衝區長度*參數必須是偶數。  
  
 *文字長度2Ptr*  
 【輸出]指向緩衝區的指標,其中返回可在\**Out語句文本*中返回的字元總數(不包括空終止)。 如果可返回的字元數大於或等於*BufferLength,* 則\**Out語句文本*中翻譯的 SQL 字串將截斷為*BufferLength*減去空終止字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLNativeSql**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_DBC的*句柄類型*和*連接句柄*的*句柄*。 下表列出了**SQLNativeSql**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|緩衝區\* *Out語句文本*不夠大,無法返回整個 SQL 字串,因此 SQL 字串被截斷。 未壓縮的 SQL 字串的長度在 [*文字長度2Ptr*中傳回】 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08003|連線未開啟|*連接句柄*未處於連接狀態。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|22007|不合法日期時間格式|**In語句文字*包含具有無效日期、時間或時間戳值的轉義子句。|  
|24000|指標狀態無效|語句中引用的游標位於結果集開始之前或結果集結束之後。 具有本機 DBMS 游標實現的驅動程式可能無法返回此錯誤。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY009|不合法的空白指標|(DM) =*顯示文字*是一個空指標。|  
|HY010|函式序列錯誤|(DM) 為*ConnectHandle*調用了非同步執行函數,並且在調用此函數時仍在執行。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) 參數*TextLength1*小於 0,但不等於SQL_NTS。|  
|||(DM) 參數*BufferLength*小於 0,參數*Out語句文本*不是空指標。|  
|HY109|游標位置無效|游標的當前行已被刪除或未提取。 具有本機 DBMS 游標實現的驅動程式可能無法返回此錯誤。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*連接句柄*關聯的驅動程式不支援該功能。|  
  
## <a name="comments"></a>註解  
 以下是**SQLNativeSql**可能為包含標量函數 CONVERT 的以下輸入 SQL 字串返回的內容的範例。 假設列 empid 在資料來源中為 INTEGER 類型:  
  
```sql  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Microsoft SQL Server 的驅動程式可能會傳回以下翻譯的 SQL 字串:  
  
```sql  
SELECT convert (smallint, empid) FROM employee  
```  
  
 ORACLE 伺服器的驅動程式可能會傳回以下翻譯的 SQL 字串:  
  
```sql  
SELECT to_number (empid) FROM employee  
```  
  
 Ingres 的驅動程式可能會傳回以下翻譯的 SQL 字串:  
  
```sql  
SELECT int2 (empid) FROM employee  
```  
  
 有關詳細資訊,請參閱[直接執行](../../../odbc/reference/develop-app/direct-execution-odbc.md)和[準備執行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)。  
  
## <a name="related-functions"></a>相關函數  
 無。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
