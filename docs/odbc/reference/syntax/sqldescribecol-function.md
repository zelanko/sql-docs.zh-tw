---
title: SQLDescribeCol 功能 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c727f6b36930b0d2ad0d5a61592b83bcd4995426
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301168"
---
# <a name="sqldescribecol-function"></a>SQLDescribeCol 函數
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLDescribeCol**傳回結果集中一列的結果描述符 - 列名、類型、列大小、十進位數位和空度。 此資訊也可在稅務局的欄位中查閱。  
  
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
 *語句句柄*  
 [輸入]語句句柄。  
  
 *ColumnNumber*  
 [輸入]按增加列順序按順序排序的結果數據的列編號,從 1 開始。 列*數*參數也可以設置為 0 來描述書籤列。  
  
 *ColumnName*  
 【輸出]指向用於返回列名稱的 null 端結束的緩衝區的指標。 此值從 IRD 的SQL_DESC_NAME欄位中讀取。 如果列未命名或無法確定列名稱,則驅動程式將返回一個空字串。  
  
 如果*列名*為*NULL,NameLengthPtr*仍將傳回字元總數(不包括字元資料的空終止字元),這些字元可在*列名*指向的緩衝區中返回。  
  
 *緩衝區長度*  
 [輸入]**列名*緩衝區的長度(以字元表示)。  
  
 *名稱長度 Ptr*  
 【輸出]指向要返回\**列名*中返回的字元總數(不包括空終止)的緩衝區的指標。 如果可返回的字元數大於或等於*BufferLength,* 則\**列名中的列*名稱將截斷為 *「緩衝區長度*」減去空終止字元的長度。  
  
 *資料類型Ptr*  
 【輸出]指向要返回列的 SQL 資料類型的緩衝區的指標。 此值從 IRD 的SQL_DESC_CONCISE_TYPE欄位中讀取。 這將是[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)或特定於驅動程式的 SQL 資料類型中的值之一。 如果無法確定數據類型,驅動程式將返回SQL_UNKNOWN_TYPE。  
  
 在 ODBC 3 中。* *x、SQL_TYPE_DATE、SQL_TYPE_TIME或SQL_TYPE_TIMESTAMP分別在*\*DataTypePtr*中返回日期、時間或時間戳數據;在 ODBC 2 中。*x*返回 SQL_DATE、SQL_TIME 或SQL_TIMESTAMP。 當 ODBC 2 時,驅動程式管理員執行所需的映射。*x*應用程式使用 ODBC 3。*x*驅動程式或當 ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式。  
  
 當*列數*等於 0(對於書籤列),SQL_BINARY在*\*DataTypePtr*中返回,用於可變長度書籤。 (如果 ODBC 3 使用書籤,則返回SQL_INTEGER。*x*應用程式使用 ODBC 2。*x*驅動程式或 ODBC 2。*x*使用 ODBC 3 的應用程式。*x*驅動程式。  
  
 有關這些資料類型的詳細資訊,請參閱附錄 D 中的[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md):數據類型。 有關特定於驅動程式的 SQL 資料類型的資訊,請參閱驅動程式的文檔。  
  
 *欄大小器*  
 【輸出]指向要在數據源上返回列大小(以字元)的緩衝區的指標。 如果無法確定列大小,驅動程式返回 0。 關於欄位的詳細資訊,請參考附入的 D:資料型態中的[欄位、十進位數字、傳輸八字長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *十進位數字Ptr*  
 【輸出]指向要返回數據源上列的小數位數的緩衝區的指標。 如果無法確定或不適用小數位數,則驅動程式返回 0。 有關十進位數字的詳細資訊,請參閱附錄 D 中的[列大小、十進位數字、傳輸八字長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md):數據類型。  
  
 *空可點*  
 【輸出]指向要返回指示列是否允許 NULL 值的值的緩衝區的指標。 此值從 IRD 的SQL_DESC_NULLABLE欄位中讀取。 這是下列值之一：  
  
 SQL_NO_NULLS:該列不允許 NULL 值。  
  
 SQL_NULLABLE:該列允許 NULL 值。  
  
 SQL_NULLABLE_UNKNOWN:驅動程式無法確定列是否允許 NULL 值。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDescribeCol**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT*Handle*的*句柄類型*和*敘述句柄*。 下表列出了**SQLDescribeCol**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|緩衝區\**列名*不夠大,無法返回整個列名稱,因此列名稱被截斷。 未壓縮的欄名稱的長度在 #*NameLengthPtr*中傳回。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|07005|已準備好的語句不是*游標規範*|與*語句句柄*關聯的語句未返回結果集。 沒有要描述的列。|  
|07009|不合法的描述符索引|(DM) 為參數*列編號*指定的值等於 0,SQL_ATTR_USE_BOOKMARKS 語句選項SQL_UB_OFF。<br /><br /> 為參數*ColumnNumber*指定的值大於結果集中的列數。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置失敗|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**呼叫到*敘述 。* 然後在*語句處理*上再次調用該函數。<br /><br /> 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**是從多線程式中的不同線程呼叫*的敘述的句柄*。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQLDescribeCol**時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) 在調用**SQLPrepare、SQLExecute****SQLExecute**或語句句柄上的目錄函數之前調用函數。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) 為參數*BufferLength*指定的值小於 0。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
 **SQLDescribeCol**可以返回**SQLPrepare**或**SQLExecute**可在**SQLPrepare**之後和**SQLExecute**之前調用時返回的任何 SQLSTATE,具體取決於資料源何時計算與語句句柄關聯的 SQL 語句。  
  
 出於性能原因,應用程式在執行語句之前不應調用**SQLDescribeCol。**  
  
## <a name="comments"></a>註解  
 應用程式通常在調用**SQLPrepare**後以及關聯調用 SQLExecute 之前或之後調用**SQLDescribeCol。** **SQLExecute** 應用程式也可以調用**SQLExecDirect**後調用**SQLDescribeCol。** 有關詳細資訊,請參閱[結果集中資料](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 **SQLDescribeCol**檢索**SELECT**語句生成的列名稱、類型和長度。 如果列是表示式,則 **列名*是空字串或驅動程式定義的名稱。  
  
> [!NOTE]  
>  ODBC 支援SQL_NULLABLE_UNKNOWN作為擴展,即使開放組和 SQL 訪問組調用級別介面規範未指定**SQLDescribeCol**的選項。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區繫結到結果集中的欄|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|解除敘述處理|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回有關結果集中的資訊|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|取得多行資料|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|傳回結果集欄數|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|準備執行敘述|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
