---
title: SQLGetDescField 函數 |Microsoft 文件
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
- SQLGetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescField
helpviewer_keywords:
- SQLGetDescField function [ODBC]
ms.assetid: f09ff660-1e4a-4370-be85-90d4da0487d3
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 900d85e7aa8e2ff100df7ba223929671903b3d90
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetdescfield-function"></a>SQLGetDescField 函數
**一致性**  
 版本引進了： ODBC 3.0 版的標準相容性： ISO 92  
  
 **摘要**  
 **SQLGetDescField**傳回目前的設定或值的單一欄位的描述項記錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLGetDescField(  
     SQLHDESC        DescriptorHandle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     FieldIdentifier,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>引數  
 *DescriptorHandle*  
 [輸入]描述項控制代碼。  
  
 *RecNumber*  
 [輸入]指出從中應用程式搜尋資訊的描述項記錄。 描述項記錄與記錄編號 0 的書籤記錄編號從 0。 如果*FieldIdentifier*引數表示的標頭欄位， *RecNumber*會被忽略。 如果*RecNumber*小於或等於 SQL_DESC_COUNT 但資料列不包含資料的資料行或參數，呼叫**SQLGetDescField**會傳回欄位的預設值。 (如需詳細資訊，請參閱 「 初始設定的描述元的欄位 」 中[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。)  
  
 *FieldIdentifier*  
 [輸入]表示描述元，其值是要傳回的欄位。 如需詳細資訊，請參閱 「*FieldIdentifier*引數 」 一節中[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 *ValuePtr*  
 [輸出]傳回描述元資訊的緩衝區指標。 資料型別取決於值*FieldIdentifier*。  
  
 如果*ValuePtr*是整數類型、 應用程式應使用的緩衝區 SQLULEN 和初始化為 0 的值，才能呼叫這個函式，有些驅動程式可能只寫入的低 32 位元或 16 位元的緩衝區和保留的高序位位元保持不變。  
  
 如果*ValuePtr*是 NULL， *StringLengthPtr*仍會傳回的總位元組數 （不含字元資料 null 結束字元） 可用來傳回所指向之緩衝區中*ValuePtr*。  
  
 *BufferLength*  
 [輸入]如果*FieldIdentifier*是 ODBC 定義的欄位和*ValuePtr*指向字元字串或二進位的緩衝區，這個引數應該是長度\* *ValuePtr*. 如果*FieldIdentifier*是 ODBC 定義的欄位和\* *ValuePtr*是整數， *Columnsize*會被忽略。 如果中的值 *\*ValuePtr*是 Unicode 資料類型 (呼叫時**SQLGetDescFieldW**)、 *Columnsize*引數必須是偶數。  
  
 如果*FieldIdentifier*是驅動程式定義的欄位，應用程式設定指出欄位驅動程式管理員性質*Columnsize*引數。 *Columnsize*可以是下列值：  
  
-   如果 *\*ValuePtr*是字元字串的指標，則*Columnsize*是 SQL_NTS 之字串的長度。  
  
-   如果 *\*ValuePtr*是二進位緩衝區的指標，則應用程式會將 SQL_LEN_BINARY_ATTR 結果 (*長度*) 中的巨集*Columnsize*。 這樣做會放在負值*Columnsize*。  
  
-   如果 *\*ValuePtr*是字元字串或二進位字串以外的值的指標，則*Columnsize*應該有 SQL_IS_POINTER 的值。  
  
-   如果 *\*ValuePtr*是包含固定長度資料類型，則*Columnsize*是 SQL_IS_INTEGER、 SQL_IS_UINTEGER、 SQL_IS_SMALLINT 或 SQL_IS_USMALLINT，視需要。  
  
 *StringLengthPtr*  
 [輸出]要傳回的總位元組數 （不包括 null 結束字元所需的位元組數） 緩衝區指標可用來傳回中 **ValuePtr*。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 sql_no_data 為止或 SQL_INVALID_HANDLE。  
  
 如果，則會傳回 SQL_NO_DATA *RecNumber*大於目前的描述項記錄數目。  
  
 如果，則會傳回 SQL_NO_DATA *DescriptorHandle* IRD 的控制代碼和陳述式是在已備妥或已執行狀態但沒有任何與其相關聯的開啟資料指標。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetDescField**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType*的利用 SQL_HANDLE_STMT 和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLGetDescField** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|緩衝區\* *ValuePtr*仍不夠大，無法傳回整個描述項欄位，所以已截斷欄位。 中會傳回未截斷的描述項欄位的長度 **StringLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07009|無效的描述元索引|(DM) *RecNumber*引數的等於 0、 SQL_ATTR_USE_BOOKMARK 陳述式屬性 SQL_UB_OFF，而*DescriptorHandle*引數以前是 IRD 控制代碼。 （可以會傳回此錯誤的明確配置描述項只有描述元是陳述式控制代碼相關聯。）<br /><br /> *FieldIdentifier*引數就是記錄 欄位中， *RecNumber*引數為 0，而*DescriptorHandle*引數以前是 IPD 控制代碼。<br /><br /> *RecNumber*引數為小於 0。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY007|相關的陳述式未準備好|*DescriptorHandle*與*StatementHandle* IRD，以及相關聯的陳述式控制代碼必須尚未準備或執行。|  
|HY010|函數順序錯誤|(DM) *DescriptorHandle*與*StatementHandle*以非同步方式執行的函式 （不這一個） 的呼叫和還在執行時呼叫此函式。<br /><br /> (DM) *DescriptorHandle*與*StatementHandle*其**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**已呼叫而傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*DescriptorHandle*。 此非同步函式還在執行時**SQLGetDescField**呼叫函式。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY021|不一致的描述項資訊|SQL_DESC_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 欄位並非來自有效的 ODBC SQL 類型、 有效的特定驅動程式 SQL 類型 （適用於 Ipd) 或有效的 ODBC C 類型 （適用於 Apd 或 ARDs）。|  
|HY090|字串或緩衝區長度無效|(DM)  *\*ValuePtr*是字元字串，並*Columnsize*小於零。|  
|HY091|無效的描述項欄位識別碼|*FieldIdentifier*不是 ODBC 定義的欄位，且不實作定義的值。<br /><br /> *FieldIdentifier*未定義的*DescriptorHandle*。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*DescriptorHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 應用程式可以呼叫**SQLGetDescField**来傳回的單一欄位的描述項記錄的值。 呼叫**SQLGetDescField**可以傳回任何描述項類型，包括標頭欄位、 記錄的欄位，以及書籤欄位中的任何欄位的設定。 應用程式可以取得相同或不同的描述元，以任何順序，在多個欄位的設定，藉由重複的呼叫**SQLGetDescField**。 **SQLGetDescField**也可以呼叫以傳回驅動程式定義的描述項欄位。  
  
 基於效能考量，應用程式不應該呼叫**SQLGetDescField**的 IRD 之前執行的陳述式。  
  
 描述的名稱、 資料類型和資料行或參數資料的儲存體的多個欄位的設定也可以擷取的單一呼叫中**SQLGetDescRec**。 **SQLGetStmtAttr**可以呼叫以傳回也是陳述式屬性描述項標頭中的單一欄位的設定。 **SQLColAttribute**， **SQLDescribeCol**，和**SQLDescribeParam**傳回記錄或書籤的欄位。  
  
 當應用程式呼叫**SQLGetDescField**若要擷取特定的描述元類型未定義欄位的值，此函數會傳回 SQL_SUCCESS，但是傳回欄位的值為未定義。 例如，呼叫**SQLGetDescField** APD 或 ARD SQL_DESC_NAME 或 SQL_DESC_NULLABLE 欄位將會傳回 SQL_SUCCESS，但未定義欄位的值。  
  
 當應用程式呼叫**SQLGetDescField**若要擷取的欄位，為特定的描述元類型定義，但沒有預設值，而且尚未設定值，此函數會傳回 SQL_SUCCESS 不過傳回的值欄位會定義。 描述項欄位的欄位描述的初始化資訊，請參閱"的初始化的描述項欄位 」，在[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 如需有關描述元的詳細資訊，請參閱[描述元](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|取得多個描述項欄位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定單一描述項欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定多個描述項欄位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
