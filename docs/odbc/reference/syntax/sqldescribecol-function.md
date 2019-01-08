---
title: SQLDescribeCol 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b8453d76dc2af0499dc8d8af2ca1ec3024aee83
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52523814"
---
# <a name="sqldescribecol-function"></a>SQLDescribeCol 函數
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ISO 92  
  
 **摘要**  
 **SQLDescribeCol**傳回的結果描述項-資料行名稱、 類型、 資料行大小、 小數位數和可 null 性-針對結果集中的一個資料行。 這項資訊也可在 IRD 欄位中。  
  
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
 [輸出]在其中傳回的資料行名稱以 null 結尾的緩衝區指標。 這個值會從 IRD 的與 SQL_DESC_NAME 欄位讀取。 如果資料行未命名或無法判別資料行名稱，此驅動程式會傳回空字串。  
  
 如果*ColumnName*為 NULL，就*NameLengthPtr*仍會傳回 （不含字元資料的 null 終止字元） 的字元總數可用來傳回中所指向的緩衝區*ColumnName*。  
  
 *BufferLength*  
 [輸入]長度 **ColumnName*緩衝區，以字元為單位。  
  
 *NameLengthPtr*  
 [輸出]在其中傳回 （不含 null 終止） 的字元總數緩衝區的指標來傳回在可用\* *ColumnName*。 可用來傳回字元的數目是否大於或等於*Columnsize*中的資料行名稱\* *ColumnName*會被截斷成*Columnsize*減去 null 結束字元的長度。  
  
 *DataTypePtr*  
 [輸出]在其中傳回的資料行的 SQL 資料類型的緩衝區指標。 這個值會從 IRD 的 SQL_DESC_CONCISE_TYPE 欄位讀取。 這會在值的其中一個[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)，或驅動程式專屬的 SQL 資料型別。 如果無法判別資料型別，則驅動程式會傳回 SQL_UNKNOWN_TYPE。  
  
 在 ODBC 3。*x*中, 傳回 SQL_TYPE_DATE、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP  *\*DataTypePtr*日期、 時間或時間戳記資料的 ODBC 2 中分別;。*x*、 SQL_DATE、 SQL_TIME、 或 SQL_TIMESTAMP 會傳回。 驅動程式管理員會執行必要的對應時的 ODBC 2。*x*應用程式使用 ODBC 3。*x*驅動程式或 ODBC 3。*x*應用程式正在使用的 ODBC 2。*x*驅動程式。  
  
 當*ColumnNumber*等於為 0 （表示書籤資料行中），傳回 SQL_BINARY  *\*DataTypePtr*可變長度的書籤。 （如果書籤由 ODBC 3，則傳回 SQL_INTEGER。*x*應用程式使用 ODBC 2。*x*驅動程式或 ODBC 2。*x*應用程式使用 ODBC 3。*x*驅動程式。)  
  
 如需有關這些資料類型的詳細資訊，請參閱 < [SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)附錄 d:資料類型。 如需驅動程式專用的 SQL 資料類型資訊，請參閱驅動程式的文件。  
  
 *ColumnSizePtr*  
 [輸出]在其中傳回資料來源上的資料行的大小 （以字元為單位） 的緩衝區指標。 如果無法判別資料行大小，則驅動程式會傳回 0。 如需有關資料行大小的詳細資訊，請參閱 <<c0> [ 資料行大小、 小數位數、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d:資料類型。  
  
 *DecimalDigitsPtr*  
 [輸出]在其中傳回的資料行的小數位數的資料來源上之緩衝區的指標。 如果無法判斷的小數位數，或不適用，則驅動程式會傳回 0。 如需有關十進位數字的詳細資訊，請參閱[資料行大小、 小數位數、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d:資料類型。  
  
 *NullablePtr*  
 [輸出]若要在其中傳回值，指出資料行是否允許 NULL 值的緩衝區的指標。 這個值會從 IRD 的 SQL_DESC_NULLABLE 欄位讀取。 這是下列值之一：  
  
 SQL_NO_NULLS:資料行不允許 NULL 值。  
  
 SQL_NULLABLE:資料行允許 NULL 值。  
  
 SQL_NULLABLE_UNKNOWN:無法判斷驅動程式，是否資料行允許 NULL 值。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDescribeCol**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可取得相關聯的 SQLSTATE 值，請呼叫**SQLGetDiagRec**使用*HandleType*利用 SQL_HANDLE_STMT 的和 a*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLDescribeCol** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|緩衝區\* *ColumnName*仍不夠大，無法傳回整個資料行名稱，所以已截斷的資料行名稱。 未截斷的資料行名稱的長度會傳入 **NameLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07005|無法準備陳述式*資料指標規格*|與相關聯的陳述式*StatementHandle*未傳回結果集。 沒有資料行來描述。|  
|07009|描述項索引無效|(DM) 引數指定的值*ColumnNumber*等於 0，因而 SQL_ATTR_USE_BOOKMARKS 陳述式選項 SQL_UB_OFF。<br /><br /> 指定的引數的值*ColumnNumber*大於結果集中的資料行數目。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置失敗|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 呼叫函式，和之前執行，完成**SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*。 然後在上一次呼叫函式*StatementHandle*。<br /><br /> 呼叫函式，和之前已完成執行時， **SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLDescribeCol**呼叫。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) 在呼叫之前呼叫的函式**SQLPrepare**， **SQLExecute**，或目錄上的函式的陳述式控制代碼。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|(DM) 引數指定的值*Columnsize*為小於 0。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
 **SQLDescribeCol**可以傳回任何可傳回的 SQLSTATE **SQLPrepare**或是**SQLExecute**之後呼叫**SQLPrepare**之前**SQLExecute**，取決於資料來源時評估陳述式控制代碼相關聯的 SQL 陳述式。  
  
 基於效能考量，應用程式不應該呼叫**SQLDescribeCol**之前執行的陳述式。  
  
## <a name="comments"></a>註解  
 應用程式通常會呼叫**SQLDescribeCol**呼叫後**SQLPrepare**並呼叫之前或之後關聯至**SQLExecute**。 應用程式也可以呼叫**SQLDescribeCol**呼叫後**SQLExecDirect**。 如需詳細資訊，請參閱 <<c0> [ 結果集的中繼資料](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 **SQLDescribeCol**擷取資料行名稱、 類型和所產生的長度**選取**陳述式。 如果資料行是運算式，**ColumnName*空字串，或驅動程式定義的名稱。  
  
> [!NOTE]  
>  ODBC 支援 SQL_NULLABLE_UNKNOWN 延伸模組，即使 Open Group 和 SQL 存取群組呼叫層級介面規格未指定的選項**SQLDescribeCol**。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集的資料行的緩衝區|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消陳述式處理|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在結果集中傳回資料行的相關資訊|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|正在擷取多個資料列|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|傳回結果集資料行|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|準備執行陳述式|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
