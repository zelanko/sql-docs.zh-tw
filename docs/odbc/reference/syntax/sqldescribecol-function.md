---
title: SQLDescribeCol 函數 |Microsoft 文件
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
- SQLDescribeCol
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeCol
helpviewer_keywords:
- SQLDescribeCol function [ODBC]
ms.assetid: eddef353-83f3-4a3c-8f24-f9ed888890a4
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e35649b865a41481de3bfe3356d8738888be39c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqldescribecol-function"></a>SQLDescribeCol 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ISO 92  
  
 **摘要**  
 **SQLDescribeCol**傳回的結果描述項 — 資料行名稱、 類型、 資料行大小、 十進位數字和 null 屬性，在結果中的單一資料行的設定。 這項資訊也可以使用在 IRD 欄位中。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLDescribeCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLCHAR *      ColumnName,  
      SQLSMALLINT    BufferLength,  
      SQLSMALLINT *  NameLengthPtr,  
      SQLSMALLINT *  DataTypePtr,  
      SQLULEN *      ColumnSizePtr,  
      SQLSMALLINT *  DecimalDigitsPtr,  
      SQLSMALLINT *  NullablePtr);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *ColumnNumber*  
 [輸入]結果資料的資料行數目循序排序依遞增的資料行順序，從 1 開始。 *ColumnNumber*引數也可以設定為 0 來描述書籤資料行。  
  
 *ColumnName*  
 [輸出]這是要傳回的資料行名稱中的 null 結束緩衝區的指標。 這個值會從 IRD 的 SQL_DESC_NAME 欄位讀取。 如果資料行未命名或無法判別資料行名稱，此驅動程式會傳回空字串。  
  
 如果*ColumnName*是 NULL， *NameLengthPtr*仍會傳回的總字元數 （不含字元資料 null 結束字元） 可用來傳回中所指向的緩衝區*ColumnName*。  
  
 *BufferLength*  
 [輸入]長度 **ColumnName*緩衝區，以字元為單位。  
  
 *NameLengthPtr*  
 [輸出]這是要傳回的總字元數 （不含 null 終止） 中的緩衝區指標可用來傳回中\* *ColumnName*。 可傳回的字元數目是否大於或等於*Columnsize*中的資料行名稱\* *ColumnName*會被截斷成*Columnsize*減去 null 結束字元的長度。  
  
 *DataTypePtr*  
 [輸出]這是要傳回的資料行的 SQL 資料類型的緩衝區指標。 這個值會從 IRD 的 SQL_DESC_CONCISE_TYPE 欄位讀取。 這會是中值的其中一個[SQL 資料型別](../../../odbc/reference/appendixes/sql-data-types.md)，或驅動程式專屬 SQL 資料類型。 如果無法判別資料型別，則驅動程式會傳回 SQL_UNKNOWN_TYPE。  
  
 在 ODBC 3。*x*中, 傳回 SQL_TYPE_DATE、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP  *\*DataTypePtr*的日期、 時間或時間戳記資料分別; 在 ODBC 2。*x*、 SQL_DATE、 SQL_TIME、 或 SQL_TIMESTAMP 會傳回。 驅動程式管理員會執行必要的對應時 ODBC 2。*x*應用程式使用 ODBC 3。*x*驅動程式或 ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式。  
  
 當*ColumnNumber*等於中為 0 （適用於的書籤資料行），傳回 SQL_BINARY  *\*DataTypePtr*可變長度的書籤。 （如果書籤由 ODBC 3，會傳回 SQL_INTEGER。*x*應用程式使用 ODBC 2。*x*驅動程式或 ODBC 2。*x*應用程式使用 ODBC 3。*x*驅動程式。)  
  
 如需有關這些資料類型的詳細資訊，請參閱[SQL 資料型別](../../../odbc/reference/appendixes/sql-data-types.md)附錄 d： 資料型別中。 如需驅動程式特有的 SQL 資料類型資訊，請參閱驅動程式的文件。  
  
 *ColumnSizePtr*  
 [輸出]這是要傳回的資料行的大小 （以字元為單位），資料來源上的緩衝區指標。 如果無法判別資料行大小，則驅動程式會傳回 0。 如需有關資料行大小的詳細資訊，請參閱[資料行大小、 十進位數字、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d： 資料型別中。  
  
 *DecimalDigitsPtr*  
 [輸出]這是要傳回的資料行的小數位數數目的資料來源上的緩衝區指標。 如果無法判別小數位數數目，或不適用，驅動程式會傳回 0。 多個十進位數字的詳細資訊，請參閱[資料行大小、 十進位數字、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d： 資料型別中。  
  
 *NullablePtr*  
 [輸出]傳回值，指出資料行是否允許 NULL 值的緩衝區指標。 這個值會從 IRD 的 SQL_DESC_NULLABLE 欄位讀取。 這是下列值之一：  
  
 SQL_NO_NULLS： 資料行不允許 NULL 值。  
  
 SQL_NULLABLE： 資料行允許 NULL 值。  
  
 SQL_NULLABLE_UNKNOWN： 驅動程式無法判斷資料行是否允許 NULL 值。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDescribeCol**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以藉由呼叫取得相關聯的 SQLSTATE 值**SQLGetDiagRec**與*HandleType*利用 SQL_HANDLE_STMT 的和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLDescribeCol** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|緩衝區\* *ColumnName*仍不夠大，無法傳回整個資料行名稱，所以已截斷的資料行名稱。 中會傳回未截斷的資料行名稱的長度 **NameLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07005|無法準備陳述式*資料指標規格*|與相關聯的陳述式*StatementHandle*未傳回結果集。 沒有資料行來描述。|  
|07009|無效的描述元索引|(DM) 指定的引數的值*ColumnNumber*即等於 0，而且 SQL_ATTR_USE_BOOKMARKS 陳述式選項 SQL_UB_OFF。<br /><br /> 指定的引數的值*ColumnNumber*大於結果集中的資料行數目。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置失敗|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY008|已取消操作|非同步處理已啟用*StatementHandle*。 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*。 上一次呼叫函式則*StatementHandle*。<br /><br /> 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 此非同步函式還在執行時**SQLDescribeCol**呼叫。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可以使用。 此函式呼叫之前的所有資料流處理的參數擷取資料。<br /><br /> 以非同步方式執行的函式 （不是這一個） 已呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> (DM) 函式呼叫之前呼叫**SQLPrepare**， **SQLExecute**，或目錄上的函式的陳述式控制代碼。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY090|字串或緩衝區長度無效|(DM) 引數指定的值*Columnsize*小於 0。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|中的非同步通知模式已停用輪詢|每當通知模型使用時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，且如果已啟用通知模式， **SQLCompleteAsync**必須在後續處理作業，並完成此作業的控制代碼上呼叫。|  
  
 **SQLDescribeCol**可以傳回任何可傳回的 SQLSTATE **SQLPrepare**或**SQLExecute**之後呼叫**SQLPrepare**之前**SQLExecute**，端視資料來源時評估陳述式控制代碼相關聯的 SQL 陳述式。  
  
 基於效能考量，應用程式不應該呼叫**SQLDescribeCol**之前執行的陳述式。  
  
## <a name="comments"></a>註解  
 應用程式通常會呼叫**SQLDescribeCol**呼叫之後**SQLPrepare**和呼叫之前或之後關聯至**SQLExecute**。 應用程式也可以呼叫**SQLDescribeCol**呼叫之後**SQLExecDirect**。 如需詳細資訊，請參閱[結果集的中繼資料](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 **SQLDescribeCol**擷取資料行名稱、 類型和所產生的長度**選取**陳述式。 如果資料行是運算式，**ColumnName*是空字串或驅動程式定義的名稱。  
  
> [!NOTE]  
>  ODBC 會支援做為擴充，SQL_NULLABLE_UNKNOWN 即使 Open Group 和 SQL 存取群組呼叫層級介面規格中未指定的選項**SQLDescribeCol**。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集內的資料行的緩衝區|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消陳述式處理|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回結果集內的資料行的相關資訊|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|擷取多個資料列|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|傳回結果集資料行|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|準備執行陳述式|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
