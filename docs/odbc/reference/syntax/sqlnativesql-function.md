---
description: SQLNativeSql 函數
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
ms.openlocfilehash: cbdf43d1120065f981d43e58490e328c6ef7691c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428900"
---
# <a name="sqlnativesql-function"></a>SQLNativeSql 函數
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ODBC  
  
 **總結**  
 **SQLNativeSql** 會傳回驅動程式修改的 SQL 字串。 **SQLNativeSql** 不會執行 SQL 語句。  
  
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
 輸出要轉譯的 SQL 文字字串。  
  
 *TextLength1*  
 輸出**InStatementText* 文字字串的長度（以字元為單位）。  
  
 *OutStatementText*  
 出要傳回已轉譯之 SQL 字串的緩衝區指標。  
  
 如果 *OutStatementText* 是 Null， *TextLength2Ptr* 仍會傳回字元總數 (排除字元資料的 Null 終止字元) 可在 *OutStatementText*所指向的緩衝區中傳回。  
  
 *BufferLength*  
 輸出OutStatementText 緩衝區中的字元數 \* *OutStatementText* 。 如果在* \* InStatementText*中傳回的值是在呼叫**SQLNativeSqlW**) 時 (的 Unicode 字串，則*BufferLength*引數必須是偶數。  
  
 *TextLength2Ptr*  
 出緩衝區的指標，此緩衝區會傳回 (不包括 null 終止) 可在 OutStatementText 中傳回的字元總數 \* * *。 如果可傳回的字元數大於或等於*BufferLength*，OutStatementText 中已轉譯的 SQL 字串 \* *OutStatementText*會截斷為*BufferLength*減去 null 終止字元的長度。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLNativeSql**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_DBC）和*ConnectionHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLNativeSql** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01004|字串資料，右邊已截斷|緩衝區 \* *OutStatementText*不夠大，無法傳回整個 sql 字串，因此 sql 字串已被截斷。 Untruncated SQL 字串的長度會在 **TextLength2Ptr*中傳回。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|08003|連接未開啟|*ConnectionHandle*不是處於線上狀態。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|22007|不正確日期時間格式|**InStatementText* 包含具有無效日期、時間或時間戳記值的 escape 子句。|  
|24000|指標狀態無效|語句中所參考的資料指標位於結果集的開頭之前，或在結果集的結尾之後。 具有原生 DBMS 資料指標執行的驅動程式可能不會傳回這個錯誤。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY009|Null 指標的用法無效| (DM) **InStatementText* 為 null 指標。|  
|HY010|函數順序錯誤| (DM) 針對 *ConnectionHandle* 呼叫非同步執行的函式，但在呼叫此函式時仍在執行。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY090|不正確字串或緩衝區長度| (DM) 引數 *TextLength1* 小於0，但不等於 SQL_NTS。|  
||| (DM) 引數 *BufferLength* 小於0且引數 *OutStatementText* 不是 null 指標。|  
|HY109|不正確資料指標位置|資料指標目前的資料列已刪除或尚未提取。 具有原生 DBMS 資料指標執行的驅動程式可能不會傳回這個錯誤。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *ConnectionHandle* 相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  
 以下是 **SQLNativeSql** 可能會針對下列包含純量函式轉換的輸入 SQL 字串所傳回的範例。 假設資料行 empid 是資料來源中的整數類型：  
  
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
  
 如需詳細資訊，請參閱 [直接執行](../../../odbc/reference/develop-app/direct-execution-odbc.md) 和已備妥的 [執行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)。  
  
## <a name="related-functions"></a>相關函數  
 無。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
