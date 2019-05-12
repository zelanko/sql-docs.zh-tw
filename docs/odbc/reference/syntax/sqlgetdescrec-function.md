---
title: SQLGetDescRec Function | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescRec
helpviewer_keywords:
- SQLGetDescRec function [ODBC]
ms.assetid: 325e0907-8e87-44e8-a111-f39e636a9cbc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c737a9dfd6e7a33b5e160b3d952fac0b354148b4
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/11/2019
ms.locfileid: "65538195"
---
# <a name="sqlgetdescrec-function"></a>SQLGetDescRec 函式
**合規性**  
 導入的版本：ODBC 3.0 版的標準合規性：ISO 92  
  
 **摘要**  
 **SQLGetDescRec**傳回目前的設定或多個欄位的描述項記錄的值。 傳回的欄位描述的名稱、 資料類型和資料行或參數資料的儲存體。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLGetDescRec(  
      SQLHDESC        DescriptorHandle,  
      SQLSMALLINT     RecNumber,  
      SQLCHAR *       Name,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLSMALLINT *   TypePtr,  
      SQLSMALLINT *   SubTypePtr,  
      SQLLEN *        LengthPtr,  
      SQLSMALLINT *   PrecisionPtr,  
      SQLSMALLINT *   ScalePtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="arguments"></a>引數  
 *DescriptorHandle*  
 [輸入]描述項控制代碼。  
  
 *RecNumber*  
 [輸入]指出從中應用程式搜尋資訊的描述項記錄。 描述項記錄與記錄編號 0 表示書籤記錄編號從 1。 *RecNumber*引數必須小於或等於 SQL_DESC_COUNT 的值。 如果*RecNumber*小於或等於 SQL_DESC_COUNT，但資料列不包含資料的資料行或參數，呼叫**SQLGetDescRec**會傳回欄位的預設值。 (如需詳細資訊，請參閱 [初始設定的描述元的欄位] 中[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。)  
  
 *名稱*  
 [輸出]在其中傳回與 SQL_DESC_NAME 欄位的描述項記錄緩衝區的指標。  
  
 如果*名稱*為 NULL，就*StringLengthPtr*仍會傳回 （不含字元資料的 null 終止字元） 的字元總數可用來傳回中指向緩衝區*名稱*。  
  
 *BufferLength*  
 [輸入]長度 **名稱*緩衝區，以字元為單位。  
  
 *StringLengthPtr*  
 [輸出]在其中傳回的資料可用來傳回中的字元數的緩衝區的指標\**名稱*緩衝區，但不包括 null 結束字元。 字元數目是否大於或等於*Columnsize*中的資料\**名稱*會被截斷成*Columnsize*減去的長度null 結束字元，以及是以 null 終止的驅動程式。  
  
 *TypePtr*  
 [輸出]在其中傳回描述項記錄的 SQL_DESC_TYPE 欄位值的緩衝區指標。  
  
 *SubTypePtr*  
 [輸出]型別是 SQL_DATETIME 或 SQL_INTERVAL 的記錄，這是在其中傳回 SQL_DESC_DATETIME_INTERVAL_CODE 欄位的值之緩衝區的指標。  
  
 *LengthPtr*  
 [輸出]在其中傳回描述項記錄的 SQL_DESC_OCTET_LENGTH 欄位值的緩衝區指標。  
  
 *PrecisionPtr*  
 [輸出]在其中傳回描述項記錄的 SQL_DESC_PRECISION 欄位值的緩衝區指標。  
  
 *ScalePtr*  
 [輸出]在其中傳回描述項記錄的 SQL_DESC_SCALE 欄位值的緩衝區指標。  
  
 *NullablePtr*  
 [輸出]在其中傳回描述項記錄的 SQL_DESC_NULLABLE 欄位值的緩衝區指標。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 sql_no_data 之後或 SQL_INVALID_HANDLE。  
  
 如果，則會傳回 SQL_NO_DATA *RecNumber*大於目前的描述項記錄的數目。  
  
 如果，則會傳回 SQL_NO_DATA *DescriptorHandle* IRD 的控制代碼和陳述式是在已備妥或已執行的狀態，但沒有任何與其相關聯的開啟資料指標。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetDescRec**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_DESC 並*處理*的*DescriptorHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLGetDescRec** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|緩衝區\**名稱*仍不夠大，無法傳回完整的描述項欄位。 因此，已截斷的欄位。 中會傳回未截斷的描述項欄位的長度 **StringLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07009|描述項索引無效|*FieldIdentifier*引數就是 [記錄] 欄位中， *RecNumber*引數設定為 0，而*DescriptorHandle*引數為 IPD 控點。<br /><br /> (DM) *RecNumber*引數設定為 0，且 SQL_ATTR_USE_BOOKMARKS 陳述式屬性已設定為 SQL_UB_OFF，而*DescriptorHandle*引數為 IRD 控制代碼。<br /><br /> *RecNumber*引數為小於 0。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY007|尚未備妥相關聯的陳述式|*DescriptorHandle*聯 IRD 和相關聯的陳述式控制代碼不是處於已備妥或已執行的狀態。|  
|HY010|函數順序錯誤|(DM) *DescriptorHandle*與建立關聯*StatementHandle*以非同步方式執行的函式 （不這一個） 的呼叫和仍在呼叫此函式時所執行。<br /><br /> (DM) *DescriptorHandle*與建立關聯*StatementHandle*讓**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**已呼叫且傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*DescriptorHandle*。 此非同步函式仍在執行時**SQLGetDescRec**呼叫。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*DescriptorHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 應用程式可以呼叫**SQLGetDescRec**來擷取單一資料行或參數的下列描述項欄位的值：  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE （適用於記錄型別是 SQL_DATETIME 或 SQL_INTERVAL）  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec**不會擷取標頭欄位的值。  
  
 應用程式可以將對應的引數設定為 null 指標的欄位，以避免傳回欄位的設定。  
  
 當應用程式呼叫**SQLGetDescRec**擷取未定義特定的描述元類型欄位的值，此函式都會傳回 SQL_SUCCESS，但是傳回欄位的值會是未定義。 例如，呼叫**SQLGetDescRec** APD 或 ARD 與 SQL_DESC_NAME 或 SQL_DESC_NULLABLE 欄位將會傳回 SQL_SUCCESS，但未定義欄位的值。  
  
 當應用程式呼叫**SQLGetDescRec**若要擷取特定的描述元類型定義但沒有預設值而且尚未設定欄位的值，此函式都會傳回 SQL_SUCCESS，但是傳回值未定義的欄位。 如需詳細資訊，請參閱 [初始設定的描述元的欄位] 中[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 欄位的值也可以擷取個別的呼叫所**SQLGetDescField**。 如需描述項標頭或記錄中欄位的說明，請參閱 < [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 如需描述項的詳細資訊，請參閱[描述元](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|資料行繫結|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|將參數繫結|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取得描述項欄位|[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|設定多個描述項欄位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
