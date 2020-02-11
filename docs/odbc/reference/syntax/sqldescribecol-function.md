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
ms.openlocfilehash: 63982d87f0dbbe0c8ab1a540185e298d9943f630
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104788"
---
# <a name="sqldescribecol-function"></a>SQLDescribeCol 函數
**標準**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **摘要**  
 **SQLDescribeCol**會針對結果集中的一個資料行，傳回結果描述中繼資料行名稱、類型、資料行大小、十進位數和 null 屬性。 您也可以在 IRD 的欄位中取得這項資訊。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
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
 源語句控制碼。  
  
 *ColumnNumber*  
 源結果資料的資料行數目，順序是以遞增的資料行順序排序，從1開始。 *ColumnNumber*引數也可以設定為0，以描述書簽資料行。  
  
 *ColumnName*  
 輸出要傳回資料行名稱之以 null 終止的緩衝區指標。 此值會從 IRD 的 [SQL_DESC_NAME] 欄位讀取。 如果資料行未命名或無法判斷資料行名稱，則驅動程式會傳回空字串。  
  
 如果*columnname*是 Null，則*NameLengthPtr*仍然會傳回可在*ColumnName*所指向的緩衝區中傳回的字元總數（不包括字元資料的 Null 終止字元）。  
  
 *BufferLength*  
 源**ColumnName*緩衝區的長度（以字元為單位）。  
  
 *NameLengthPtr*  
 輸出緩衝區的指標，其中會傳回可在\* *ColumnName*中傳回的字元總數（不包括 null 終止）。 如果可傳回的字元數大於或等於*BufferLength*，則\* *ColumnName*中的資料行名稱會截斷為*BufferLength*減去 null 終止字元的長度。  
  
 *DataTypePtr*  
 輸出要傳回資料行之 SQL 資料類型的緩衝區指標。 此值會從 IRD 的 [SQL_DESC_CONCISE_TYPE] 欄位讀取。 這會是[Sql 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)中的其中一個值，或驅動程式特定的 sql 資料類型。 如果無法判斷資料類型，驅動程式會傳回 SQL_UNKNOWN_TYPE。  
  
 在 ODBC 3 中。*x*、SQL_TYPE_DATE、SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP 會分別在* \*DataTypePtr*中傳回日期、時間或時間戳記資料。在 ODBC 2 中。會傳回*x*、SQL_DATE、SQL_TIME 或 SQL_TIMESTAMP。 當 ODBC 2 時，驅動程式管理員會執行必要的對應。*x*應用程式正在使用 ODBC 3。*x*驅動程式或 ODBC 3。*x*應用程式正在使用 ODBC 2。*x*驅動程式。  
  
 當*ColumnNumber*等於0（針對書簽資料行）時，會在* \*DataTypePtr*中傳回可變長度書簽的 SQL_BINARY。 （如果 ODBC 3 使用書簽，則會傳回 SQL_INTEGER。使用 ODBC 2 的*x*應用程式。*x*驅動程式或 ODBC 2。使用 ODBC 3 的*x*應用程式。*x*驅動程式）。  
  
 如需這些資料類型的詳細資訊，請參閱附錄 D：資料類型中的[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)。 如需有關驅動程式特定 SQL 資料類型的詳細資訊，請參閱驅動程式的檔。  
  
 *ColumnSizePtr*  
 輸出緩衝區的指標，要在其中傳回資料來源上資料行的大小（以字元為單位）。 如果無法判斷資料行大小，驅動程式會傳回0。 如需資料行大小的詳細資訊，請參閱附錄 D：資料類型中的資料[行大小、小數位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *DecimalDigitsPtr*  
 輸出緩衝區的指標，傳回資料來源上資料行的小數位數。 如果無法判斷十進位數的數目或不適用，則驅動程式會傳回0。 如需十進位數的詳細資訊，請參閱附錄 D：資料類型中的資料[行大小、小數位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *NullablePtr*  
 輸出緩衝區的指標，會在其中傳回值，指出資料行是否允許 Null 值。 此值會從 IRD 的 [SQL_DESC_NullABLE] 欄位讀取。 這是下列值之一：  
  
 SQL_NO_NullS：資料行不允許 Null 值。  
  
 SQL_NullABLE：資料行允許 Null 值。  
  
 SQL_NullABLE_UNKNOWN：驅動程式無法判斷資料行是否允許 Null 值。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDescribeCol**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_STMT *HandleType*和*StatementHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出**SQLDescribeCol**常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|緩衝區\* *ColumnName*的大小不足以傳回整個資料行名稱，因此資料行名稱已截斷。 Untruncated 資料行名稱的長度會在 **NameLengthPtr*中傳回。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07005|備妥的語句不是資料*指標規格*|與*StatementHandle*相關聯的語句未傳回結果集。 沒有要描述的資料行。|  
|07009|不正確描述項索引|（DM）為引數*ColumnNumber*指定的值等於0，而且已 SQL_UB_OFF SQL_ATTR_USE_BOOKMARKS 語句選項。<br /><br /> 為引數*ColumnNumber*指定的值大於結果集中的資料行數目。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置失敗|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|已啟用*StatementHandle*的非同步處理。 已呼叫函式，在完成執行之前，會在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後在*StatementHandle*上再次呼叫函式。<br /><br /> 已呼叫函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY010|函數順序錯誤|（DM）已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLDescribeCol**時，這個非同步函數仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並 SQL_PARAM_DATA_AVAILABLE 傳回。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。<br /><br /> （DM）已針對*StatementHandle*呼叫非同步執行的函式（而非這個函式），而且在呼叫這個函數時仍在執行中。<br /><br /> （DM）在呼叫**SQLPrepare**、 **SQLExecute**或語句控制碼上的目錄函數之前，已呼叫過函數。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|（DM）為引數*BufferLength*指定的值小於0。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*StatementHandle*相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 而且如果啟用通知模式，則必須在控制碼上呼叫**SQLCompleteAsync** ，才能執行後置處理並完成作業。|  
  
 視資料來源評估與語句控制碼相關聯的 SQL 語句的時間而定， **SQLDescribeCol**可以傳回**SQLPrepare**或**SQLExecute**在**SQLPrepare**和**SQLExecute**之前所能傳回的任何 SQLSTATE。  
  
 基於效能的考慮，應用程式不應該在執行語句之前呼叫**SQLDescribeCol** 。  
  
## <a name="comments"></a>註解  
 應用程式通常會在呼叫**SQLPrepare**之後，以及在**SQLExecute**的相關呼叫之前或之後呼叫**SQLDescribeCol** 。 應用程式也可以在呼叫**SQLExecDirect**之後呼叫**SQLDescribeCol** 。 如需詳細資訊，請參閱[結果集中繼資料](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 **SQLDescribeCol**會抓取**SELECT**語句所產生的資料行名稱、類型和長度。 如果資料行是運算式，則 **ColumnName*可以是空字串或驅動程式定義的名稱。  
  
> [!NOTE]  
>  ODBC 支援 SQL_NullABLE_UNKNOWN 做為延伸模組，即使開啟群組和 SQL 存取群組呼叫層級介面規格並未指定**SQLDescribeCol**的選項也是一樣。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回結果集中資料行的相關資訊|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|提取多個資料列|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|傳回結果集資料行的數目|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|準備語句以執行|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
